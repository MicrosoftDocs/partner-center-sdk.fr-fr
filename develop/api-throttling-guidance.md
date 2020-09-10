---
title: Aide sur la limitation des API
description: Lorsque la limitation peut se produire
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: b83e3ee7189cd0be9201d05d40d8959fa0644f34
ms.sourcegitcommit: e55d630e82114754c385616be10d179544ad8470
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643996"
---
# <a name="api-throttling-guidance"></a>Aide sur la limitation des API 

**S’applique à**

- Espace partenaires

Microsoft implémente la limitation des API pour offrir des performances plus cohérentes dans un intervalle de temps pour les partenaires qui appellent les API de l’espace partenaires. La limitation limite le nombre de demandes à un service dans un intervalle de temps pour empêcher la surutilisation des ressources. Alors que l’espace partenaires est conçu pour gérer un volume élevé de demandes, si un nombre excessif de demandes se produit par peu de partenaires, la limitation contribue à maintenir une fiabilité et des performances optimales pour tous les partenaires.  

Les limites varient selon les scénarios. Par exemple, si vous réalisez un volume important d’écritures, la possibilité de limitation est plus élevée que si vous effectuez uniquement des lectures.

## <a name="what-happens-when-throttling-occurs"></a>Que se passe-t-il en cas de limitation ? 

Lorsqu’un seuil de limitation est dépassé, l’espace partenaires limite les demandes ultérieures de ce client pendant un certain temps. Le comportement de limitation peut dépendre du type et du nombre de demandes.   

### <a name="common-throttling-scenarios"></a>Scénarios de limitation courants 

Les causes les plus courantes de la limitation des clients sont entre autres : 

- **Un grand nombre de demandes pour une API par ID de locataire de partenaire**: pour certaines API de l’espace partenaires, la limitation est déterminée par l’ID de locataire partenaire. un nombre excessif d’appels à ces API sur le même ID de locataire de partenaire entraînera un dépassement du seuil de limitation.  

- **Un grand nombre de demandes pour une API par ID de locataire de partenaire par ID de locataire client**: pour d’autres API, la limitation est déterminée par la combinaison ID de locataire partenaire/ID de locataire client ; dans ce cas, le fait d’effectuer un trop grand nombre d’appels sur le même ID de locataire client entraîne une limitation, tandis que les appels à d’autres clients peuvent aboutir.

## <a name="best-practices-to-avoid-throttling"></a>Meilleures pratiques pour éviter la limitation 
 
Les pratiques de programmation telles que l’interrogation continue d’une ressource pour rechercher des mises à jour et l’analyse régulière des regroupements de ressources pour rechercher des ressources nouvelles ou supprimées sont plus susceptibles d’entraîner une limitation et dégradent les performances globales. Les appels d’API simultanés peuvent entraîner un nombre élevé de demandes par unité de temps, ce qui entraîne également la limitation des demandes. Au lieu de cela, vous devez utiliser le suivi des modifications et les notifications de modification. En outre, vous devez être en mesure de tirer parti des journaux d’activité pour la détection des modifications. pour plus d’informations, consultez les journaux d’activité de l' [espace partenaires](get-a-record-of-paratner-center-activity-by-user.md) .  Nous recommandons vivement aux partenaires d’utiliser l’API du journal d’activité pour améliorer l’efficacité et éviter la limitation. Consultez également l’exemple d’utilisation des journaux d’activité, ci-dessous.

## <a name="best-practices-to-avoid-throttling"></a>Meilleures pratiques pour éviter la limitation

Voici les meilleures pratiques pour la gestion de la limitation : 

- Réduisez le degré de parallélisme. 
- Réduire la fréquence des appels. 
- Évitez les nouvelles tentatives immédiates, car toutes les requêtes sont exécutées sur vos limites d’utilisation. 

Lorsque vous implémentez la gestion des erreurs, utilisez le code d’erreur HTTP 429 pour détecter la limitation. L’échec de la réponse comprend l’en-tête de réponse Retry-after. La méthode la plus rapide pour effectuer une récupération à partir de la limitation consiste à sauvegarder les demandes à l’aide du délai nouvelle tentative. 

Pour utiliser le délai de nouvelle tentative, procédez comme suit : 

1. Attendez le nombre de secondes spécifié dans l’en-tête Retry-after. 

2. Relancez la requête.  

3. Si la demande échoue à nouveau avec un code d’erreur 429, vous êtes toujours limité. Réessayez avec une interruption exponentielle, utilisez le délai de nouvelle tentative recommandé, puis recommencez la demande jusqu’à ce qu’elle aboutisse.

## <a name="apis-currently-impacted-by-throttling"></a>Les API sont actuellement affectées par la limitation

À long terme, chaque API de l’espace partenaires unique qui appelle le point de terminaison « api.partnercenter.microsoft.com/ » sera limitée. Actuellement, les limites de limitation ne sont appliquées que sur les quelques API répertoriées ci-dessous. L’espace partenaires va collecter les données de télémétrie sur chacune des API et ajustera dynamiquement les limites de limitation. Le tableau suivant répertorie les API pour lesquelles la limitation est actuellement appliquée.  


|**opération**| **Documentation sur Espace partenaires**|       
|------------------------|----------------------------|
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions|obtenir tous les abonnements client-s|    
|https://api.partnercenter.microsoft.com/v1/productUpgrades/eligibility|obtenir-éligibilité-for-Product-mise à niveau|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|obtenir un abonnement par ID|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|récupération de toutes les commandes client|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|recevoir une commande par ID|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|Obtient l’état d’approvisionnement de l’abonnement|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|gérer les commandes et gérer un abonnement|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|obtenir la liste des modules complémentaires pour un abonnement|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|obtenir la liste des droits Azure pour l’abonnement|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|créer une commande|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|afficher l’état d’inscription de l’abonnement|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|transition d’un abonnement|          
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/transfers|récupération de tous les clients|   
|https://api.partnercenter.microsoft.com/v1/productUpgrades/{upgrade-id}/status|récupérer l’état de la mise à niveau du produit| 
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|recevoir une commande par ID|           
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/orders/{order-id}|acheter un module complémentaire à un abonnement|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|créer un panier|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}/checkout|extraire un panier|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|mettre à jour un panier|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|inscrire un abonnement|  
|https://api.partnercenter.microsoft.com/v1/productupgrades|créer une entité de mise à niveau du produit|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
obtenir la liste des offres de conversion d’essai|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
convertir un abonnement d’évaluation en payant|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}|obtenir un client par ID|

### <a name="error-code-response"></a>Réponse du code d’erreur :

HTTP/1.1 429 trop de requêtes 

Content-Length : 84 

Content-Type: application/json 

Nouvelle tentative-après : 57 

Date : Mar, 21 juillet 2020 04:10:58 GMT 

{"statusCode" : 429, "message" : "la limite du débit est dépassée. Réessayez dans 57 secondes.» } 


## <a name="example-of-activity-log"></a>Exemple de journal d’activité

Pour les meilleures pratiques en matière d’analyse des modifications quotidiennes, nous vous recommandons d’interroger l’enregistrement d’audit pour un jour spécifique. 

Dans la réponse, vous obtiendrez un résultat avec les modifications apportées à un type d’opération spécifique.Vous pouvez filtrer en fonction de l’opération qui vous intéresse. Par exemple, si vous êtes intéressé par un client récemment créé, vous pouvez consulter operationType = "add_customer".  

La liste des OperationType/ressources se trouve dans les documents d’API ci-dessous.  

- [Audit des ressources](https://docs.microsoft.com/partner-center/develop/auditing-resources)  

- [Obtenir un enregistrement d’une activité espace partenaires par utilisateur](https://docs.microsoft.com/partner-center/develop/get-a-record-of-partner-center-activity-by-user)  



### <a name="response-example"></a>Exemple de réponse

**Demande**:  

Appel http : https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Autorisation : porteur <token> 

Accept: application/json 

MS-RequestId : 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId : de9c2ccc-40DD-4186-9660-65b9b64c3d14 

X-locale : en-US 

Hôte : api.partnercenter.microsoft.com 

Connexion : Keep-Alive 

**Réponse**:    

{ 

    « totalCount » : 17, 

    « éléments » : [ 

        { 

            « ID » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d_e905b566-4779-4E57-944C-7b1b5312705b_updatecustomeruserlicenses_637346859797753934 », 

            « Partenaire » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d », 

            « participants » : [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            « customerId » : « e905b566-4779-4E57-944C-7b1b5312705b », 

            « userPrincipalName » : « admin@testsw09.onmicrosoft.com », 

            « applicationId » : « FulfillmentService », 

            « resourceType » : « licence », 

            « operationType » : « update_customer_user_licenses », 

            "operationDate" : "2020-09-02T23:26:19.7753934 Z", 

            « operationStatus » : « réussite », 

            "customizedData": [ 

                { 

                    « Key » : « CustomerUserId », 

                    « valeur » : « 933808c7-B165-496c-A24E-1a4b7846fab4 » 

                } 

            ], 

            "attributs" : { 

                « objectType » : « AuditRecord » 

            } 

        }, 

        { 

            « ID » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372 », 

            « Partenaire » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d », 

            « participants » : [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            « customerId » : « 86bddccf-9a53-40c6-907c-08067a3f8da7 », 

            « customerName » : « CustomMetersStagingTest », 

            « userPrincipalName » : « admin@testsw09.onmicrosoft.com », 

            « applicationId » : « 4990cffe-04e8-4e8b-808A-1175604b879f », 

            « resourceType » : « Order », 

            "resourceNewValue" : "{ \" ID \" : \" Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1 \" , \" AlternateId \" : \" 64144d300bde \" , \" ReferenceCustomerId \" : \" 86bddccf-9a53-40c6-907c-08067a3f8da7 \" , \" BillingCycle \" : \" Monthly \" , \" CurrencyCode \" : \" USD \" , \" CurrencySymbol \" : \" $ \" , \" LineItem \" : [{ \" LineItemNumber \" : 0, \" ProvisioningContext \" : null, \" OfferID \" : \" DZH318Z0C964:0001 : DZH318Z0BZDG \" , \" SubscriptionId \" : \" f428d44a-d08b-348b-579e-ce92a6362c7b \" , \" ParentSubscriptionId \" : null, \" TermDuration \" : \" p1m \" , \" transactionType \" : \" New \" , \" FriendlyName : la \" \" valeur de l’offre personnalisée Saas-bronze \" , \" quantité \" : 1, tarification : null, PartnerIdOnRecord : null, \" \" \" \" \" RenewsTo \" : null, \" liens \" : { \" Product \" : { \" URI \" : \" /Products/DZH318Z0C964 ? pays = US \" , \" méthode \" : \" Obtient \" , \" corps \" : null, \" en-têtes \" : []}, \" référence SKU \" : { \" URI \" : \" /Products/DZH318Z0C964/SKUs/0001 ? Country = US \" , \" méthode \" : \" Obtient \" , \" corps \" : null, \" en-têtes \" : []}, \" disponibilité \" : { \" URI \" : \" /Products/DZH318Z0C964/SKUs/0001/availabilities/DZH318Z0BZDG ? Country = US \" , \" méthode \" : \" Obtient \" , \" corps \" : null, \" en-têtes \" : []}, \" ActivationLinks \" : { \" URI \" : \" /Customers/86bddccf-9a53-40c6-907c-08067a3f8da7/Orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/LineItems/0/activationlinks \",\" Méthode \" : \" obtenir \" , \" corps \" : null, \" en-têtes \" : []}}}], \" CreationDate \" : \" 2020-09-02T17:58:01.7755853 z \" , \" état \" : \" en attente \" , \" transactionType \" : \" UserPurchase \" , \" liens \" : { \" Self \" : { \" URI \" : \" /Customers/86bddccf-9a53-40c6-907c-08067a3f8da7/Orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1 \" , \" méthode \" : \" obtenir \" , \" corps \" : null, \" en-têtes \" : []}, \" ProvisioningStatus \" : { \" URI \" : \" /Customers/86bddccf-9a53-40c6-907c-08067a3f8da7/Orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus \" , \" méthode \" : \" Obtient \" , \" corps \" : null, \" en-têtes \" : []}, \" PatchOperation \" : { \" URI \" : \" /Customers/86bddccf-9a53-40c6-907c-08067a3f8da7/Orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1 \" , \" méthode \" : \" correctif \" , \" corps \" : null, \" en-têtes \" : []}}, \" client \" : { \" marketplaceCountry \" : \" US \" , \" deviceFamily \" : \" UniversalStore-PartnerCenter \" , \" nom \" : \" Web espace partenaires \" }, \" attributs \" : { \" ObjectType \" : \" Order \" }} ", 

            « operationType » : « create_order », 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate" : "2020-09-02T17:58:10.9268372 Z", 

            « operationStatus » : « réussite », 

            "customizedData": [ 

                { 

                    « clé » : « OrderId », 

                    « valeur » : « Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1 » 

                }, 

                { 

                    « Key » : « AlternateId », 

                    « valeur » : « 64144d300bde » 

                }, 

                { 

                    « Key » : « BillingCycle », 

                    « valeur » : « mensuelle » 

                }, 

                { 

                    « Key » : « OfferId-0 », 

                    « valeur » : « DZH318Z0C964:0001 : DZH318Z0BZDG » 

                }, 

                { 

                    « Key » : « SubscriptionId-0 », 

                    « valeur » : « f428d44a-d08b-348b-579e-ce92a6362c7b » 

                }, 

                { 

                    « Key » : « SubscriptionName-0 », 

                    « valeur » : « offre de compteur personnalisé SaaS-bronze » 

                }, 

                { 

                   « Key » : « Quantity-0 », 

                    « valeur » : « 1 » 

                }, 

                { 

                    « Key » : « PartnerOnRecord-0 », 

                    « valeur » : null 

                } 

            ], 

            "attributs" : { 

                « objectType » : « AuditRecord » 

            } 

        }, 

                           { 

            « ID » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005 », 

            « Partenaire » : « 9daaeb1c-4195-4DB5-9f1d-509eb70c8c2d », 

            « participants » : [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            « customerId » : « 86bddccf-9a53-40c6-907c-08067a3f8da7 », 

            « customerName » : « CustomMetersStagingTest », 

            « userPrincipalName » : « admin@testsw09.onmicrosoft.com », 

            « applicationId » : « 4990cffe-04e8-4e8b-808A-1175604b879f », 

            « resourceType » : « Customer », 

            « resourceNewValue » : «{ \" ID \" : \" 86bddccf-9a53-40c6-907c-08067a3f8da7 \" , \" CommerceId \" : \" 9dd78b4f-F98A-44b4-a2fa-2b82ac58d24c \" , \" CompanyProfile \" : { \" TenantId \" : \" 86bddccf-9a53-40c6-907c-08067a3f8da7 \" , \" Domain \" : \" CustomMetersStagingTest.onmicrosoft.com \" , \" CompanyName \" : \" CustomMetersStagingTest \" , \" adresse \" : null, \" email \" : null, \" OrganizationRegistrationNumber \" : null, \" Links : \" { \" Self \" : { \" URI \" : \" /Customers/86bddccf-9a53-40c6-907c-08067a3f8da7/Profiles/Company \" , \" Method \" : \" obtenir \" , \" corps \" : null, \" en-têtes \" : []}}, \" attributs \" : { \" ObjectType \" : \" CustomerCompanyProfile \" }}, \" BillingProfile \" : { \" ID \" : \" 4beafd7b-CDAB-5bdc-52ed-02e16edf2e7a \" , \" FirstName \" : \" CustomMetersStagingTest \" , \" LastName \" : \" CustomMetersStagingTest \" , \" email \" : \" CustomMetersStagingTest@CustomMetersStagingTest.com \" , \" culture : en \" \" -US \" , \" Language \" : fr, \" \" \" CompanyName \" : \" CustomMetersStagingTest \" , \" DefaultAddress \" : { \" ID \" : null, \" Country \" : \" US \" , \" Region \" : null, \" City \" : \" Seattle \" , \" State \" : \" wa \" , \" district \" : null, AddressLine1 \" \" : CustomMetersStagingTest, AddressLine2 : \" \" \" \" null, \" AddressLine3 \" : null, \" PostalCode \" : \" 98122 \" , \" FirstName \" : \" CustomMetersStagingTest \" , \" LastName \" : \" CustomMetersStagingTest \" , \" EmailAddress \" : null, \" PhoneNumber \" : null, \" MiddleName \" : null}, \" attributs \" : { \" ETag \" : \" -2279334701316321663 \" , \" typeobjet \" : \" CustomerBillingProfile \" }}, \" RelationshipToPartner \" : \" Reseller \" , \" AllowDelegatedAccess \" : true, \" UserCredentials \" : { \" UserName \" : \" admin \" , \" password \" : \" \" }, \" AssociatedPartnerId \" : null, \" CustomDomains \" : null, \" attributs \" : { \" ObjectType \" : \" Customer \" }} ", 

            « operationType » : « add_customer », 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate" : "2020-09-02T17:34:12.8069005 Z", 

            « operationStatus » : « réussite », 

            "customizedData": [ 

                { 

                    « Key » : « PrimaryDomainName », 

                    « valeur » : « CustomMetersStagingTest.onmicrosoft.com » 

                }, 

                { 

                    « Key » : « relationship », 

                    « valeur » : « revendeur » 

                } 

            ], 

            "attributs" : { 

                « objectType » : « AuditRecord » 

            } 

        }, 

                            

        ... 

    ], 

    « Liens » : { 

        « Self » : { 

            « URI » : « /AuditRecords ? startDate = 2020-09-02&endDate = 2020-09-02&Size = 50 », 

            « méthode » : « obtient », 

            "en-têtes" : [] 

        } 

    }, 

    "attributs" : { 

        « objectType » : « collection » 

    } 

} 

 

  
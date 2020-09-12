---
title: Aide sur la limitation des API
description: Lorsque la limitation peut se produire
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: 2531312e5f34a0c35220f009d7aa156331beee43
ms.sourcegitcommit: aa7b12e0156404f64f576e09971ea3deb3529231
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037504"
---
# <a name="api-throttling-guidance"></a>Aide sur la limitation des API 

**S’applique à**

- Espace partenaires

Microsoft implémente la limitation des API pour offrir des performances plus cohérentes dans un intervalle de temps pour les partenaires qui appellent les API de l’espace partenaires. La limitation limite le nombre de demandes à un service dans un intervalle de temps pour empêcher la surutilisation des ressources. Alors que l’espace partenaires est conçu pour gérer un volume élevé de demandes, si un nombre excessif de demandes se produit par peu de partenaires, la limitation contribue à maintenir une fiabilité et des performances optimales pour tous les partenaires.  

Les limites varient selon les scénarios. Par exemple, si vous réalisez un volume important d’écritures, la possibilité de limitation est plus élevée que si vous effectuez uniquement des lectures.

## <a name="what-happens-when-throttling-occurs"></a>Que se passe-t-il en cas de limitation ? 

Lorsqu’un seuil de limitation est dépassé, l’espace partenaires limite les demandes ultérieures de ce client pendant un certain temps. Le comportement de limitation dépend du type et du nombre de demandes.   

### <a name="common-throttling-scenarios"></a>Scénarios de limitation courants 

Les causes les plus courantes de la limitation des clients sont entre autres : 

- **Un grand nombre de demandes pour une API par ID de locataire de partenaire**: pour certaines API de l’espace partenaires, la limitation est déterminée par l’ID de locataire partenaire. un nombre excessif d’appels à ces API sur le même ID de locataire de partenaire entraînera un dépassement du seuil de limitation.  

- **Un grand nombre de demandes pour une API par ID de locataire de partenaire par ID de locataire client**: pour d’autres API, la limitation est déterminée par la combinaison ID de locataire partenaire/ID de locataire client ; dans ce cas, le fait d’effectuer un trop grand nombre d’appels sur le même ID de locataire client entraîne une limitation, tandis que les appels à d’autres clients peuvent aboutir.

## <a name="best-practices-to-avoid-throttling"></a>Meilleures pratiques pour éviter la limitation 
 
Les pratiques de programmation telles que l’interrogation continue d’une ressource pour rechercher des mises à jour et l’analyse régulière des regroupements de ressources pour rechercher des ressources nouvelles ou supprimées sont plus susceptibles d’entraîner une limitation et dégradent les performances globales. Les appels d’API simultanés peuvent entraîner un nombre élevé de demandes par unité de temps, ce qui entraîne également la limitation des demandes. Au lieu de cela, vous devez utiliser le suivi des modifications et les notifications de modification. En outre, vous devez être en mesure de tirer parti des journaux d’activité pour la détection des modifications. pour plus d’informations, consultez les journaux d’activité de l' [espace partenaires](get-a-record-of-partner-center-activity-by-user.md) .  Nous recommandons vivement aux partenaires d’utiliser l’API du journal d’activité pour améliorer l’efficacité et éviter la limitation. Consultez également l’exemple d’utilisation des journaux d’activité, ci-dessous.

## <a name="best-practices-to-handle-throttling"></a>Bonnes pratiques de gestion de la limitation

Voici les meilleures pratiques pour la gestion de la limitation : 

- Réduisez le degré de parallélisme. 
- Réduire la fréquence des appels. 
- Évitez les nouvelles tentatives immédiates, car toutes les requêtes sont exécutées sur vos limites d’utilisation. 

Lorsque vous implémentez la gestion des erreurs, utilisez le code d’erreur HTTP 429 pour détecter la limitation. L’échec de la réponse comprend l’en-tête de réponse Retry-after. La méthode la plus rapide pour effectuer une récupération à partir de la limitation consiste à sauvegarder les demandes à l’aide du délai nouvelle tentative. 

Pour utiliser le délai de nouvelle tentative, procédez comme suit : 

1. Attendez le nombre de secondes spécifié dans l’en-tête Retry-after. 

2. Relancez la requête.  

3. Si la demande échoue à nouveau avec un code d’erreur 429, vous êtes toujours limité. Réessayez avec une interruption exponentielle, utilisez le délai de nouvelle tentative recommandé, puis recommencez la demande jusqu’à ce qu’elle aboutisse.

## <a name="apis-currently-impacted-by-throttling"></a>API actuellement affectées par la limitation

À long terme, chaque API de l’espace partenaires unique qui appelle le point de terminaison « api.partnercenter.microsoft.com/ » sera limitée. Actuellement, les limites de limitation ne sont appliquées que sur les seules API répertoriées ci-dessous. L’espace partenaires va collecter les données de télémétrie sur chacune des API et ajustera dynamiquement les limites de limitation. Le tableau suivant répertorie les API pour lesquelles la limitation est actuellement appliquée.  


|**opération**| **Documentation sur Espace partenaires**|       
|------------------------|----------------------------|
|{baseURL}/v1/Customers/{customer_id}/Orders|[créer une commande](create-an-order.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-subscription}/Upgrades|[transition d’un abonnement](transition-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID}|[acheter un module complémentaire à un abonnement](purchase-an-add-on-to-a-subscription.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}|[créer un panier](create-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}/Checkout|[extraire un panier](checkout-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/carts/{Cart-ID}|[mettre à jour un panier](update-a-cart.md)|
|{baseURL}/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/Registrations|[inscrire un abonnement](register-a-subscription.md)|
|{baseURL}/v1/productupgrades|[créer une entité de mise à niveau du produit](create-product-upgrade-entity.md)|
|{baseURL}/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/conversions |[convertir un abonnement d’évaluation en payant](convert-a-trial-subscription-to-paid.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}|[obtenir un client par ID](get-a-customer-by-id.md)|
|{baseURL}/v1/productUpgrades/eligibility|[obtenir l’éligibilité pour la mise à niveau du produit](get-eligibility-for-product-upgrade.md)|
|{baseURL}/v1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-subscription} |[gérer l’abonnement](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a>Réponse du code d’erreur :
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a>Exemple de journal d’activité

Pour les meilleures pratiques en matière d’analyse des modifications quotidiennes, nous vous recommandons d’interroger l’enregistrement d’audit pour un jour spécifique. 

Dans la réponse, vous obtiendrez un résultat avec les modifications apportées à un type d’opération spécifique.Vous pouvez filtrer en fonction de l’opération qui vous intéresse. Par exemple, si vous êtes intéressé par un client récemment créé, vous pouvez consulter operationType = "add_customer".  

La liste des OperationType/ressources se trouve dans les documents d’API ci-dessous.  

- [Audit des ressources](https://docs.microsoft.com/partner-center/develop/auditing-resources)  

- [Obtenir un enregistrement d’une activité espace partenaires par utilisateur](https://docs.microsoft.com/partner-center/develop/get-a-record-of-partner-center-activity-by-user)  



### <a name="response-example"></a>Exemple de réponse

**Demande**:  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

**Réponse**:    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

  

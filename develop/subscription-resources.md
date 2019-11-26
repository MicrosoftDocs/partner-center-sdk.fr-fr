---
title: Ressources d’abonnement
description: Les ressources d’abonnement peuvent fournir des informations supplémentaires sur les abonnements tout au long du cycle de vie, telles que la prise en charge, les remboursements, les droits Azure.
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc771fcbc8cb03e95684dd32ff0f1f29076bba49
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486699"
---
# <a name="subscription-resources"></a>Ressources d’abonnement

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un abonnement permet à un client d’utiliser un service pendant un certain laps de temps. Tous les champs ne s’appliquent pas à tous les abonnements. De nombreux champs s’appliquent uniquement à certains points du cycle de vie, par exemple si un abonnement est suspendu ou annulé.

## <a name="subscription"></a>Abonnement

>[!NOTE]
>La ressource d' **abonnement** a une limite de 500 de demandes par minute et par identificateur de locataire.

La ressource d' **abonnement** représente le cycle de vie d’un abonnement et comprend des propriétés qui définissent les États tout au long du cycle de vie de l’abonnement.

| Propriété             | Type                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | chaîne                                                        | Identificateur d’abonnement.                                                                                                                                                  |
| offerId              | chaîne                                                        | Identificateur de l’offre.                                                                                                                                                         |
| entitlementId        | chaîne                                                        | L’identificateur d’habilitation (ID d’abonnement Azure).                                                                                                                        |
| offerName            | chaîne                                                        | Nom de l’offre.                                                                                                                                                               |
| friendlyName         | chaîne                                                        | Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté.                                                                                           |
| quantity             | nombre                                                        | Quantité. Par exemple, dans le cas d’une facturation basée sur une licence, cette propriété est définie sur le nombre de licences.                                                            |
| Unité             | chaîne                                                        | Unités définissant la quantité pour l’abonnement.                                                                                                                             |
| ParentSubscriptionId | chaîne                                                        | Obtient ou définit l’identificateur d’abonnement parent.                                                                                                                              |
| CreationDate         | chaîne                                                        | Obtient ou définit la date de création, au format date-heure.                                                                                                                          |
| effectiveStartDate   | chaîne au format date/heure UTC                                | Obtient ou définit la date de début effective de cet abonnement, au format date-heure. Il est utilisé pour mettre à jour un abonnement migré ou pour l’aligner avec un autre.                |
| commitmentEndDate    | chaîne au format date/heure UTC                                | Date de fin d’engagement de cet abonnement, au format date-heure. Pour les abonnements qui ne sont pas renouvelés automatiquement, il s’agit d’une date éloignée à l’avenir.       |
| status               | chaîne                                                        | État de l’abonnement : « None », « active », « pending », « Suspended » ou « Deleted ».                                                                                                         |
| autoRenewEnabled     | booléen                                                       | Obtient une valeur indiquant si l’abonnement est renouvelé automatiquement.                                                                                                    |
| billingType          | chaîne                                                        | Spécifie la manière dont l’abonnement est facturé : « aucun », « utilisation » ou « licence ».                                                                                                      |
| billingCycle         | chaîne                                                        | Indique la fréquence à laquelle le partenaire est facturé pour cette commande. Les valeurs prises en charge sont les noms des membres trouvés dans [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | booléen                                                       | Obtient ou définit une valeur indiquant si l’abonnement a acheté des modules complémentaires.                                                                                             |
| isTrial              | booléen                                                       | Valeur indiquant s’il s’agit d’un abonnement d’évaluation.                                                                                                                      |
| isMicrosoftProduct   | booléen                                                       | Valeur indiquant s’il s’agit d’un produit Microsoft.                                                                                                                       |
| publisherName        | chaîne                                                        | Nom de l’éditeur.                                                                                                                                                           |
| Interventions              | Tableau de chaînes                                              | Obtient ou définit les actions autorisées. Valeurs possibles : « modifier », « annuler »                                                                                                  |
| Partenaire            | chaîne                                                        | ID MPN du revendeur de l’enregistrement, utilisé dans le modèle de partenaire indirect.                                                                                                     |
| suspensionReasons    | Tableau de chaînes                                              | Lecture seule. Si l’abonnement a été suspendu, indique pourquoi.                                                                                                                  |
| contractType         | chaîne                                                        | Lecture seule. Type de contrat : « Subscription », « productKey » ou « redemptionCode ».                                                                                           |
| refundOptions        | Tableau de ressources [RefundOption](#refundoption)   | Lecture seule. Ensemble d’options de remboursement disponibles pour cet abonnement.                                                                                              |
| liens                | [SubscriptionLinks](#subscriptionlinks)                       | Obtient ou définit les liens d’abonnement.                                                                                                                                          |
| orderId              | chaîne                                                        | ID de la commande qui a été placée pour commencer l’abonnement.                                                                                                                |
| termDuration         | chaîne                                                        | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont **p1m** (1 mois), **P1Y** (1 an) et **P3Y** (3 ans).                                                        |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à l’abonnement.                                                                                                                    |
| renewalTermDuration  | chaîne                                                        | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

La ressource **SubscriptionLinks** décrit la collection de liens attachés à une ressource d’abonnement.

| Propriété           | Type                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| mettent              | [Lien](utility-resources.md#link) | Obtient ou définit l’offre.               |
| parentSubscription | [Lien](utility-resources.md#link) | Obtient ou définit l’abonnement parent. |
| production            | [Lien](utility-resources.md#link) | Obtient le produit associé à l’abonnement. |
| paire                | [Lien](utility-resources.md#link) | Obtient la référence SKU du produit associée à l’abonnement. |
| disponibilité       | [Lien](utility-resources.md#link) | Obtient la disponibilité de la référence SKU du produit associée à l’abonnement. |
| activationLinks    | [Lien](utility-resources.md#link) | Obtient la liste des liens d’activation associés à l’abonnement. |
| rythme               | [Lien](utility-resources.md#link) | URI auto.                         |
| suivant               | [Lien](utility-resources.md#link) | Page suivante des éléments.               |
| Premier           | [Lien](utility-resources.md#link) | Page d’éléments précédente.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

La ressource **SubscriptionProvisioningStatus** fournit des informations sur l’état de provisionnement d’un abonnement.

| Propriété   | Type                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | chaîne                                                         | Chaîne au format GUID qui identifie la référence SKU du produit.             |
| status     | chaîne                                                         | Indique l’état de provisionnement : « réussite », « en attente » ou « échec ». |
| quantity   | nombre                                                         | Fournit la quantité d’abonnement après l’approvisionnement.               |
| endDate    | chaîne au format date/heure UTC                                 | Date de fin de l’abonnement.                                    |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

La ressource **SubscriptionRegistrationStatus** décrit la collection de liens attachés à une ressource d’abonnement.

| Propriété           | Type                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | chaîne                             | Identificateur d’abonnement.                                                          |
| status             | chaîne                             | Indique l’état de l’inscription : « Registered », « Registering » ou « notregistered ».    |

## <a name="supportcontact"></a>SupportContact

La ressource **SupportContact** représente un contact de support pour l’abonnement d’un client.

| Propriété        | Type                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | chaîne                                                         | Chaîne au format GUID qui indique l’identificateur de locataire du contact de support. |
| supportMpnId    | chaîne                                                         | Identificateur Microsoft Partner Network (MPN) du contact.                       |
| name            | chaîne                                                         | Nom du contact du support technique.                                                |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)            | Liens associés au contact du support technique.                                              |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées. Contient « objectType » : « SupportContact ».              |

## <a name="registersubscription"></a>RegisterSubscription

La ressource **RegisterSubscription** retourne un lien qui peut être utilisé pour interroger l’état d’inscription d’un abonnement. L’état de l’inscription est renvoyé dans le corps de la réponse d’une demande acceptée avec succès pour inscrire un abonnement Azure.

| Propriété                | Type                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | objet                             | Retourne le code d’état HTTP 202 « accepté », avec un en-tête d’emplacement contenant un lien pour interroger l’état de l’inscription. Par exemple, `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"`. |

## <a name="refundoption"></a>RefundOption

La ressource **RefundOption** représente une option de remboursement possible pour l’abonnement.

| Propriété          | Type | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| type | chaîne | Type de remboursement. Les valeurs prises en charge sont « partial » et « Full » |
| expiresAfter      | chaîne au format date/heure UTC | Horodateur de l’expiration de cette option. Si la valeur est null, cela signifie qu’elle n’a pas d’expiration. |

## <a name="azureentitlement"></a>AzureEntitlement

La ressource **AzureEntitlement** représente les droits Azure pour l’abonnement.

| Propriété          | Type | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | chaîne | L’identificateur d’habilitation |
| friendlyName      | chaîne | Nom convivial du droit. |
| status | chaîne | État du droit. |
| subscriptionId | chaîne | Identificateur d’abonnement auquel le droit appartient. |

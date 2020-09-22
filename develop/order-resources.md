---
title: Commander des ressources
description: Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925873"
---
# <a name="order-resources"></a>Commander des ressources

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.

>[!NOTE]
>La ressource de commande a une limite de débit de 500 demandes par minute et par identificateur de locataire.

## <a name="order"></a>JSON

Décrit l’ordre d’un partenaire.

| Propriété           | Type                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | string                                             | Identificateur d’ordre qui est fourni lors de la création réussie de la commande.                                   |
| alternateId        | string                                             | Identificateur convivial pour la commande.                                                                          |
|referenceCustomerId | string                                             | Identificateur du client. |
| billingCycle       | string                                             | Indique la fréquence à laquelle le partenaire est facturé pour cette commande. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype). La valeur par défaut est « Monthly » ou « OneTime » lors de la création de la commande. Ce champ est appliqué lors de la création réussie de la commande. |
| transactionType    | string                                             | Lecture seule. Type de transaction de la commande. Les valeurs prises en charge sont « UserPurchase », « SystemPurchase » ou « SystemBilling » |
| lineItems          | Tableau de ressources [OrderLineItem](#orderlineitem) | Liste répertoriant les offres achetées par le client, y compris la quantité.        |
| currencyCode       | string                                             | Lecture seule. Devise utilisée lors de la mise en place de la commande. Appliqué en cas de création réussie de la commande.           |
| currencySymbol     | string                                             | Lecture seule. Symbole monétaire associé au code de la devise. |
| creationDate       | DATETIME                                           | Lecture seule. Date à laquelle la commande a été créée, au format date/heure. Appliqué en cas de création réussie de la commande.                                   |
| status             | string                                             | Lecture seule. État de la commande.  Les valeurs prises en charge sont les noms des membres trouvés dans [**OrderStatus**](#orderstatus).        |
| liens              | [OrderLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant à la commande.            |
| attributs         | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à l’ordre.       |

## <a name="orderlineitem"></a>OrderLineItem

Une commande contient une liste d’offres, et chaque élément est représenté sous la forme d’un OrderLineItem.

| Propriété             | Type                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Chaque élément de ligne dans la collection obtient un numéro de ligne unique, allant de 0 à nombre-1.                                                                                                                                                 |
| offerId              | string                                    | ID de l’offre.                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | ID de l'abonnement.                                                                                                                                                                                                                |
| parentSubscriptionId | string                                    | facultatif. ID de l’abonnement parent dans une offre de module complémentaire. S’applique uniquement à PATCH.                                                                                                                                                     |
| friendlyName         | string                                    | facultatif. Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté.                                                                                                                                              |
| quantité             | int                                       | Nombre de licences ou d’instances.                                                                                                                                                                                |
| termDuration         | string                                    | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont **p1m** (1 mois), **P1Y** (1 an) et **P3Y** (3 ans).                               |
| transactionType      | string                                    | Lecture seule. Type de transaction de l’élément de ligne. Les valeurs prises en charge sont « New », « Renew », « addQuantity », « removeQuantity », « Cancel », « Convert » ou « customerCredit ». |
| partnerIdOnRecord    | string                                    | Lorsqu’un fournisseur indirect passe une commande pour le compte d’un revendeur indirect, renseignez ce champ avec l’ID MPN du **revendeur indirect uniquement** (jamais l’ID du fournisseur indirect). Cela garantit une comptabilité appropriée des incitations. |
| provisioningContext  | Dictionary<String, String>            | Informations requises pour l’approvisionnement de certains éléments du catalogue. La propriété provisioningVariables d’une référence (SKU) indique les propriétés requises pour des éléments spécifiques dans le catalogue.                                                                                                                                               |
| liens                | [OrderLineItemLinks](#orderlineitemlinks) | Lecture seule. Liens de ressource correspondant à l’élément de ligne de commande.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Détails de la durée du terme de renouvellement.                                                                           |

## <a name="renewsto"></a>RenewsTo

Représente les détails de la durée du terme de renouvellement.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

## <a name="orderlinks"></a>OrderLinks

Représente les liens de ressource correspondant à la commande.

| Propriété           | Type                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Lien](utility-resources.md#link)            | Une fois rempli, le lien pour récupérer l’état de provisionnement de la commande.       |
| self               | [Lien](utility-resources.md#link)            | Lien permettant de récupérer la ressource de commande.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Représente l’abonnement complet associé à la commande.

| Propriété           | Type                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Lien](utility-resources.md#link)            | Une fois rempli, le lien pour récupérer l' [État de provisionnement](#orderlineitemprovisioningstatus) de l’élément de ligne.       |
| sku                | [Lien](utility-resources.md#link)            | Lien permettant de récupérer les informations de référence SKU pour l’élément de catalogue acheté.                    |
| subscription       | [Lien](utility-resources.md#link)            | Une fois rempli, le lien vers les informations d’abonnement complètes.                       |
| activationLinks    | [Lien](utility-resources.md#link)            | Une fois rempli, obtient la ressource pour les liens permettant d’activer l’abonnement.             |

## <a name="orderstatus"></a>OrderStatus

[Enum/dotnet/API/System. Enum] avec des valeurs qui indiquent l’état de la commande.

| Valeur              | Position     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | Initialiseur Enum.                               |
| Terminé          | 1            | Indique que la commande est terminée.          |
| en attente            | 2            | Indique que la commande est toujours en attente.      |
| rayé          | 3            | Indique que la commande a été annulée.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Représente l’état d’approvisionnement d’un [OrderLineItem](#orderlineitem).

| Propriété                        | Type                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Numéro de ligne unique de l’élément de ligne de commande. Les valeurs sont comprises entre 0 et Count-1.             |
| status                          | string                              | État de configuration de l’élément de ligne de commande. Ces valeurs comprennent :</br>« Respecté » : l’exécution de la commande est terminée avec succès et l’utilisateur peut utiliser les réservations</br>« Non rempli » : non respecté en raison de l’annulation</br>« PrefulfillmentPending » : votre demande est toujours en cours de traitement, le traitement n’est pas encore terminé |
| quantityProvisioningInformation | Liste<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Liste des informations d’état de la configuration de la quantité pour l’élément de ligne de commande. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Représente l’état d’approvisionnement par quantité.

| Propriété                           | Type                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantité                           | int                                          | Nombre d'éléments.                                 |
| status                             | string                                       | État du nombre d’éléments.                   |

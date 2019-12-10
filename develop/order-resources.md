---
title: Commander des ressources
description: Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.
ms.assetid: 5CFA35FF-1C0D-461D-A942-309AFCD98395
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0d6b42414c12c299d9205e6abfa1aadc98fc530e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488269"
---
# <a name="order-resources"></a>Commander des ressources

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.

>[!NOTE]
>La ressource de commande a une limite de débit de 500 demandes par minute et par identificateur de locataire.

## <a name="order"></a>Ordre

Décrit l’ordre d’un partenaire.

| Propriété           | Type                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | chaîne                                             | Identificateur d’ordre qui est fourni lors de la création réussie de la commande.                                   |
| AlternateId        | chaîne                                             | Identificateur convivial pour la commande.                                                                          |
|ReferenceCustomerId | chaîne                                             | Identificateur du client. |
| billingCycle       | chaîne                                             | Indique la fréquence à laquelle le partenaire est facturé pour cette commande. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype). La valeur par défaut est « Monthly » ou « OneTime » lors de la création de la commande. Ce champ est appliqué lors de la création réussie de la commande. |
| transactionType    | chaîne                                             | Lecture seule. Type de transaction de la commande. Les valeurs prises en charge sont « UserPurchase », « SystemPurchase » ou « SystemBilling » |
| LineItems          | Tableau de ressources [OrderLineItem](#orderlineitem) | Liste répertoriant les offres achetées par le client, y compris la quantité.        |
| currencyCode       | chaîne                                             | Lecture seule. Devise utilisée lors de la mise en place de la commande. Appliqué en cas de création réussie de la commande.           |
| currencySymbol     | chaîne                                             | Lecture seule. Symbole monétaire assciated avec le code de devise. |
| CreationDate       | DateHeure                                           | Lecture seule. Date à laquelle la commande a été créée, au format date/heure. Appliqué en cas de création réussie de la commande.                                   |
| status             | chaîne                                             | Lecture seule. État de la commande.  Les valeurs prises en charge sont les noms des membres trouvés dans [**OrderStatus**](#orderstatus).        |
| liens              | [OrderLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant à la commande.            |
| attributs         | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à l’ordre.       |

## <a name="orderlineitem"></a>OrderLineItem

Une commande contient une liste d’offres, et chaque élément est représenté sous la forme d’un OrderLineItem.

| Propriété             | Type                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LineItemNumber       | entier                                       | Chaque élément de ligne de la collection obtient un numéro de ligne unique, en comptant de 0 à Count-1.                                                                                                                                                 |
| offerId              | chaîne                                    | ID de l’offre.                                                                                                                                                                                                                       |
| subscriptionId       | chaîne                                    | L’ID de l’abonnement.                                                                                                                                                                                                                |
| ParentSubscriptionId | chaîne                                    | Facultatif. ID de l’abonnement parent dans une offre complémentaire. S’applique uniquement au correctif.                                                                                                                                                     |
| friendlyName         | chaîne                                    | Facultatif. Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté.                                                                                                                                              |
| quantity             | entier                                       | Nombre de licences ou d’instances.                                                                                                                                                                                |
| termDuration         | chaîne                                    | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont **p1m** (1 mois), **P1Y** (1 an) et **P3Y** (3 ans).                               |
| transactionType      | chaîne                                    | Lecture seule. Type de transaction de l’élément de ligne. Les valeurs prises en charge sont « New », « Renew », « addQuantity », « removeQuantity », « Cancel », « Convert » ou « customerCredit ». |
| partnerIdOnRecord    | chaîne                                    | Lorsqu’un fournisseur indirect passe une commande pour le compte d’un revendeur indirect, renseignez ce champ avec l’ID MPN du **revendeur indirect uniquement** (jamais l’ID du fournisseur indirect). Cela garantit une gestion correcte des incentives. |
| provisioningContext  | Dictionary < String, String >            | Informations requises pour l’approvisionnement de certains éléments du catalogue. La propriété provisioningVariables d’une référence (SKU) indique les propriétés requises pour des éléments spécifiques dans le catalogue.                                                                                                                                               |
| liens                | [OrderLineItemLinks](#orderlineitemlinks) | Lecture seule. Liens de ressource correspondant à l’élément de ligne de commande.                                                                                                                                                                                |
| RenewsTo             | Tableau d’objets                          | Tableau de ressources [RenewsTo](#renewsto) .                                                                            |

## <a name="renewsto"></a>RenewsTo

Représente un élément contenu dans un élément de ligne de commande.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | chaîne           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

## <a name="orderlinks"></a>OrderLinks

Représente les liens de ressource correspondant à la commande.

| Propriété           | Type                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Lien](utility-resources.md#Link)            | Une fois rempli, le lien pour récupérer l’état de provisionnement de la commande.       |
| rythme               | [Lien](utility-resources.md#Link)            | Lien permettant de récupérer la ressource de commande.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Représente l’abonnement complet associé à la commande.

| Propriété           | Type                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Lien](utility-resources.md#Link)            | Une fois rempli, le lien pour récupérer l' [État de provisionnement](#orderlineitemprovisioningstatus) de l’élément de ligne.       |
| paire                | [Lien](utility-resources.md#Link)            | Lien permettant de récupérer les informations de référence SKU pour l’élément de catalogue acheté.                    |
| abonnement       | [Lien](utility-resources.md#Link)            | Une fois rempli, le lien vers les informations d’abonnement complètes.                       |
| activationLinks    | [Lien](utility-resources.md#Link)            | Une fois rempli, obtient la ressource pour les liens permettant d’activer l’abonnement.             |

## <a name="orderstatus"></a>OrderStatus

[Enum](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent l’état de la commande.

| Valeur              | Position     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | Initialiseur Enum.                               |
| Procédé          | 1            | Indique que la commande est terminée.          |
| instance            | 2            | Indique que la commande est toujours en attente.      |
| Rayé          | 3            | Indique que la commande a été annulée.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Représente l’état d’approvisionnement d’un [OrderLineItem](#orderlineitem).

| Propriété                        | Type                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| LineItemNumber                  | entier                                 | Numéro de ligne unique de l’élément de ligne de commande. Les valeurs sont comprises entre 0 et Count-1.             |
| status                          | chaîne                              | État de configuration de l’élément de ligne de commande. Les valeurs sont les suivantes :</br>« Respecté » : l’exécution de la commande est terminée avec succès et l’utilisateur peut utiliser les réservations</br>« Non rempli » : non respecté en raison de l’annulation</br>« PrefulfillmentPending » : votre demande est toujours en cours de traitement, le traitement n’est pas encore terminé |
| quantityProvisioningInformation | Répertorier <[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Liste des informations d’état de la configuration de la quantité pour l’élément de ligne de commande. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Représente l’état d’approvisionnement par quantité.

| Propriété                           | Type                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | entier                                          | Nombre d’éléments.                                 |
| status                             | chaîne                                       | État du nombre d’éléments.                   |
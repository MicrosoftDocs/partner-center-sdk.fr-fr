---
title: Ressources du panier
description: Un partenaire passe une commande dans un panier lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88937889"
---
# <a name="cart-resources"></a>Ressources du panier

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire passe une commande lorsqu’un client souhaite acheter un abonnement à partir d’une liste d’offres.

## <a name="cart"></a>Panier

Décrit un panier.

| Propriété              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | Identificateur de panier qui est fourni lors de la création réussie du panier.                               |
| creationTimeStamp     | DateTime         | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.      |
| lastModifiedTimeStamp | DateTime         | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier. |
| expirationTimeStamp   | DateTime         | Date d’expiration du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.          |
| lastModifiedUser      | string           | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                          |
| lineItems             | Tableau d’objets | Tableau de ressources [CartLineItem](#cartlineitem) .                                                   |
| status                | string           | État du panier. Les valeurs possibles sont « active » (peut être mise à jour/envoyée) et « ordered » (a déjà été envoyé). |

## <a name="cartlineitem"></a>CartLineItem

Représente un élément contenu dans un panier.

| Propriété             | Type                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                           | Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                                                                   |
| catalogItemId        | string                           | Identificateur de l’élément de catalogue.                                                                                                                          |
| friendlyName         | string                           | facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                                                                 |
| quantité             | int                              | Nombre de licences ou d’instances.                                                                                                                  |
| currencyCode         | string                           | Code de la devise.                                                                                                                                    |
| billingCycle         | Object                           | Type de cycle de facturation défini pour la période actuelle.                                                                                                 |
| termDuration         | string                           | Représentation ISO 8601 de la durée du terme. Les valeurs actuellement prises en charge sont P1M (1 mois), P1Y (1 an) et P3Y (3 ans).                                |
| participants         | Liste de paires de chaînes d’objets      | Collection de partenaire sur l’enregistrement (MPNID) sur l’achat.                                                                                          |
| provisioningContext  | Dictionary<String, String>       | Contexte supplémentaire utilisé lors de la configuration de l’élément acheté. Pour déterminer les valeurs nécessaires pour un élément particulier, reportez-vous à la propriété provisioningVariables de la référence. |
| orderGroup           | string                           | Groupe pour indiquer les éléments qui peuvent être envoyés ensemble dans le même ordre.                                                                          |
| addonItems           | Liste d’objets **CartLineItem** | Collection d’éléments de ligne de panier pour les modules complémentaires. Ces éléments seront achetés pour l’abonnement de base qui résulte de l’achat de l’élément de ligne de panier de la racine. |
| error                | Object                           | Appliqué après la création du panier si une erreur s’est produite.                                                                                                    |
| renewsTo             | Tableau d’objets                 | Tableau de ressources [RenewsTo](#renewsto) .                                                                            |

## <a name="renewsto"></a>RenewsTo

Représente un élément contenu dans un élément de ligne de panier.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

## <a name="carterror"></a>CartError

Représente une erreur qui se produit après la création d’un panier.

| Propriété         | Type                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [Codes d’erreur de l’espace partenaires](error-codes.md) | Type d’erreur de panier.                                                                       |
| errorDescription | string                                 | Description de l’erreur, y compris les remarques sur les valeurs prises en charge, les valeurs par défaut ou les limites. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Représente le résultat d’une extraction de panier.

| Propriété    | Type                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | Liste d’objets de [commande](order-resources.md#order) .         | Collection de commandes.       |
| orderErrors | Liste d’objets [OrderError](#ordererror) . | Collection d’erreurs de commande. |

## <a name="ordererror"></a>OrderError

Représente une erreur qui se produit pendant l’extraction d’un panier lors de la création d’une commande.

| Propriété     | Type   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | string | ID du groupe de commandes avec l’erreur. |
| code         | int    | Code d'erreur.                                 |
| description  | string | Description de l'erreur.                   |

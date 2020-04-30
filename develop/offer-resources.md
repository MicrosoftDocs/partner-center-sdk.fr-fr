---
title: Ressources de l’offre
description: Décrit un produit figurant dans le catalogue des revendeurs qu’il peut offrir à ses clients.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a4bec5d83faa4454857cd093bb109495bce4c17a
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118655"
---
# <a name="offer-resources"></a>Ressources de l’offre

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit un produit figurant dans le catalogue des revendeurs qu’il peut offrir à ses clients.

## <a name="offer"></a>Offre

| Propriété                    | Type                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | string                    | Identificateur de l’offre.                                                                                           |
| name                        | string                    | Nom de l’offre.                                                                                                 |
| description                 | string                    | Description de l’offre.                                                                                     |
| minimumQuantity             | int                       | Quantité minimale disponible.                                                                                 |
| maximumQuantity             | int                       | Quantité maximale disponible.                                                                                 |
| rank                        | int                       | Le classement ou la priorité de l’offre est comparé à d’autres catégories de la même ligne de produits. Cette propriété doit être définie uniquement s’il existe plusieurs offres pour une ligne de produit donnée.  |
| URI                         | string                    | URI de l’offre.                                                                                                  |
| locale                      | string                    | Paramètres régionaux auxquels s’applique l’offre.                                                                          |
| country                     | string                    | Pays/région où l’offre s’applique.                                                                    |
| catégorie                    | [OfferCategory](#offercategory)           | Catégorie de l’offre.                                                                   |
| limitUnitOfMeasure          | string                    | Valeur qui indique le type de limitation d’achat. Les valeurs possibles incluent :<br/> « None » : il n’existe aucune restriction sur le nombre d’abonnements en fonction de l’offre achetée.<br/> « Concurrent » : nombre d’abonnements qui peuvent exister sur le locataire client à un moment donné, y compris les abonnements qui sont actifs ou annulés. Cette valeur s’applique principalement aux petites offres commerciales où le nombre de licences est inférieur à 300. Les abonnements de provisionioned ne sont pas comptés.<br/> « Durée de vie »-nombre d’abonnements pouvant exister pendant la durée de vie du locataire client. Cette valeur est la plus applicable aux versions d’évaluation. Les abonnements de provisionioned ne sont pas comptés.      |
| limit                       | int                       | Nombre d’abonnements qui peuvent être achetés pour cette offre en fonction du limitUnitOfMeasure.                |
| prerequisiteOffers          | string                    | Les offres requises.                                                                                        |
| isAddOn                     | boolean                   | Valeur indiquant si cette instance est un module complémentaire.                                                           |
| hasAddOns                   | boolean                   | Valeur indiquant si cette offre a des modules complémentaires.                                                           |
| isAvailableForPurchase      | boolean                   | Valeur indiquant si cette instance est disponible à l’achat.                                             |
| facturation                     | string                    | Spécifie le type de facturation pour l’achat d’une ligne : « aucun », « utilisation » ou « licence ».                           |
| supportedBillingCycles      | tableau de chaînes          | Indique les cycles de facturation pris en charge pour cette offre. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | Valeur indiquant si l’offre renouvelle automatiquement.                                                      |
| upgradeTargetOffers         | tableau de chaînes          | Liste des offres vers lesquelles cette offre peut être mise à niveau.                                                          |
| conversionTargetOffers      | tableau de chaînes          | Liste des offres vers lesquelles cette offre peut être convertie.                                                         |
| reselleeQualifications      | tableau de chaînes          | Les qualifications requises par le client pour qu’un partenaire achète l’offre pour ce client.     |
| resellerQualifications      | tableau de chaînes          | Les qualifications requises par le partenaire pour acheter l’offre pour un client.                       |
| salesGroupId                | string                    | Chaîne utilisée pour regrouper les offres dans des commandes distinctes.                                                             |
| isTrial                     | boolean                   | Valeur indiquant s’il s’agit d’une offre d’évaluation.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Obtient le produit de l’offre.                                                                           |
| unitType                    | string                    | Type de l’unité.                                                                                      |
| liens                       | [OfferLinks](#offerlinks)               | Lien « en savoir plus » de l’offre.                                                                    |
| attributs                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à l’offre.                         |

## <a name="offercategory"></a>OfferCategory

Décrit la catégorisation d’une offre. Cela comprend le classement ou la priorité de cette catégorie d’offre par rapport aux autres sur la même ligne de produits.

| Propriété   | Type                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | string                                                         | Identificateur de la catégorie.                                                                                                                                                   |
| name       | string                                                         | Nom de la catégorie.                                                                                                                                                         |
| rank       | int                                                            | Le classement ou la priorité de la catégorie par rapport aux autres catégories de la même offre. Cette propriété doit être définie uniquement s’il existe plusieurs catégories d’offres pour une offre donnée. |
| locale     | string                                                         | Paramètres régionaux auxquels s’applique l’offre.                                                                                                                        |
| country    | string                                                         | Pays/région où l’offre s’applique.                                                                                                                   |
| liens      | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant à OfferCategory.                                                                                                                     |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Contient des liens pour en savoir plus sur l’offre.

| Propriété  | Type | Description                 |
|-----------|------|-----------------------------|
| learnMore | Lien | Lien « en savoir plus ».      |
| self      | Lien | URI auto                |
| Suivant      | Lien | Page suivante des éléments.     |
| previous  | Lien | Page d’éléments précédente. |

## <a name="offerproduct"></a>OfferProduct

Produit ou service qui peut avoir plusieurs offres associées, chacune avec des ensembles de fonctionnalités différents et ciblant différents besoins des clients.

| Propriété | Type   | Description              |
|----------|--------|--------------------------|
| Id       | string | Identificateur de la catégorie. |
| Nom     | string | Nom de la catégorie.       |
| Unité     | string | Unité de produit.        |

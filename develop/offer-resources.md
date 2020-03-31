---
title: Ressources de l’offre
description: Décrit un produit figurant dans le catalogue des revendeurs qu’il peut offrir à ses clients.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 338230497fdb780823c30c9542c26aa58e89c07a
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416442"
---
# <a name="offer-resources"></a>Ressources de l’offre

**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit un produit figurant dans le catalogue des revendeurs qu’il peut offrir à ses clients.

## <a name="span-idofferspan-idofferspan-idofferoffer"></a><span id="Offer"/><span id="offer"/><span id="OFFER"/>offre

| Propriété                    | Type                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | chaîne                    | Identificateur de l’offre.                                                                                           |
| nom                        | chaîne                    | Nom de l’offre.                                                                                                 |
| description                 | chaîne                    | Description de l’offre.                                                                                     |
| minimumQuantity             | int                       | Quantité minimale disponible.                                                                                 |
| maximumQuantity             | int                       | Quantité maximale disponible.                                                                                 |
| rank                        | int                       | Le classement ou la priorité de l’offre est comparé à d’autres catégories de la même ligne de produits. Cette propriété doit être définie uniquement s’il existe plusieurs offres pour une ligne de produit donnée.  |
| uri                         | chaîne                    | URI de l’offre.                                                                                                  |
| paramètres régionaux                      | chaîne                    | Paramètres régionaux auxquels s’applique l’offre.                                                                          |
| country                     | chaîne                    | Pays/région où l’offre s’applique.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Catégorie de l’offre.                                                                   |
| limitUnitOfMeasure          | chaîne                    | Valeur qui indique le type de limitation d’achat. Les valeurs possibles incluent notamment :<br/> « None » : il n’existe aucune restriction sur le nombre d’abonnements en fonction de l’offre achetée.<br/> « Concurrent » : nombre d’abonnements qui peuvent exister sur le locataire client à un moment donné, y compris les abonnements qui sont actifs ou annulés. Cette valeur s’applique principalement aux petites offres commerciales où le nombre de licences est inférieur à 300. Les abonnements de provisionioned ne sont pas comptés.<br/> « Durée de vie »-nombre d’abonnements pouvant exister pendant la durée de vie du locataire client. Cette valeur est la plus applicable aux versions d’évaluation. Les abonnements de provisionioned ne sont pas comptés.      |
| sépar                       | int                       | Nombre d’abonnements qui peuvent être achetés pour cette offre en fonction du limitUnitOfMeasure.                |
| prerequisiteOffers          | chaîne                    | Les offres requises.                                                                                        |
| isAddOn                     | booléen                   | Valeur indiquant si cette instance est un module complémentaire.                                                           |
| hasAddOns                   | booléen                   | Valeur indiquant si cette offre a des modules complémentaires.                                                           |
| isAvailableForPurchase      | booléen                   | Valeur indiquant si cette instance est disponible à l’achat.                                             |
| facturation                     | chaîne                    | Spécifie le type de facturation pour l’achat d’une ligne : « aucun », « utilisation » ou « licence ».                           |
| supportedBillingCycles      | tableau de chaînes          | Indique les cycles de facturation pris en charge pour cette offre. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | booléen                   | Valeur indiquant si l’offre renouvelle automatiquement.                                                      |
| upgradeTargetOffers         | tableau de chaînes          | Liste des offres vers lesquelles cette offre peut être mise à niveau.                                                          |
| conversionTargetOffers      | tableau de chaînes          | Liste des offres vers lesquelles cette offre peut être convertie.                                                         |
| reselleeQualifications      | tableau de chaînes          | Les qualifications requises par le client pour qu’un partenaire achète l’offre pour ce client.     |
| resellerQualifications      | tableau de chaînes          | Les qualifications requises par le partenaire pour acheter l’offre pour un client.                       |
| salesGroupId                | chaîne                    | Chaîne utilisée pour regrouper les offres dans des commandes distinctes.                                                             |
| isTrial                     | booléen                   | Valeur indiquant s’il s’agit d’une offre d’évaluation.                                                               |
| produit                     | [OfferProduct](#offerproduct)           | Obtient le produit de l’offre.                                                                           |
| Unité                    | chaîne                    | Type de l’unité.                                                                                      |
| liens                       | [OfferLinks](#offerlinks)               | Lien « en savoir plus » de l’offre.                                                                    |
| attributs                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à l’offre.                         |

## <a name="span-idoffercategoryspan-idoffercategoryspan-idoffercategoryoffercategory"></a><span id="OfferCategory"/><span id="offercategory"/><span id="OFFERCATEGORY"/>OfferCategory

Décrit la catégorisation d’une offre. Cela comprend le classement ou la priorité de cette catégorie d’offre par rapport aux autres sur la même ligne de produits.

| Propriété   | Type                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | chaîne                                                         | Identificateur de la catégorie.                                                                                                                                                   |
| nom       | chaîne                                                         | Nom de la catégorie.                                                                                                                                                         |
| rank       | int                                                            | Le classement ou la priorité de la catégorie par rapport aux autres catégories de la même offre. Cette propriété doit être définie uniquement s’il existe plusieurs catégories d’offres pour une offre donnée. |
| paramètres régionaux     | chaîne                                                         | Paramètres régionaux auxquels s’applique l’offre.                                                                                                                        |
| country    | chaîne                                                         | Pays/région où l’offre s’applique.                                                                                                                   |
| liens      | [ResourceLinks](utility-resources.md#resourcelinks)           | Liens de ressource correspondant à OfferCategory.                                                                                                                     |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à OfferCategory.                                                                                                                |

## <a name="span-idofferlinksspan-idofferlinksspan-idofferlinksofferlinks"></a><span id="OfferLinks"/><span id="offerlinks"/><span id="OFFERLINKS"/>OfferLinks

Contient des liens pour en savoir plus sur l’offre.

| Propriété  | Type | Description                 |
|-----------|------|-----------------------------|
| learnMore | Lien | Lien « en savoir plus ».      |
| self      | Lien | URI auto                |
| next      | Lien | Page suivante des éléments.     |
| previous  | Lien | Page d’éléments précédente. |

## <a name="span-idofferproductspan-idofferproductspan-idofferproductofferproduct"></a><span id="OfferProduct"/><span id="offerproduct"/><span id="OFFERPRODUCT"/>OfferProduct

Produit ou service qui peut avoir plusieurs offres associées, chacune avec des ensembles de fonctionnalités différents et ciblant différents besoins des clients.

| Propriété | Type   | Description              |
|----------|--------|--------------------------|
| ID       | chaîne | Identificateur de la catégorie. |
| Nom     | chaîne | Nom de la catégorie.       |
| Unit     | chaîne | Unité de produit.        |

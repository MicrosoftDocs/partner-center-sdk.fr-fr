---
title: Offer resources
description: Describes a product listed in the reseller catalog that they can offer to their customers.
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 287482a934fecd73bce7d455098b3ab8a39d527c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486889"
---
# <a name="offer-resources"></a>Offer resources

**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Describes a product listed in the reseller catalog that they can offer to their customers.

## <a name="span-idofferspan-idofferspan-idofferoffer"></a><span id="Offer"/><span id="offer"/><span id="OFFER"/>Offer

| Propriété                    | Tapez                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | chaîne                    | The offer identifier.                                                                                           |
| name                        | chaîne                    | The offer name.                                                                                                 |
| description                 | chaîne                    | A description of the offer.                                                                                     |
| minimumQuantity             | entier                       | The minimum quantity available.                                                                                 |
| maximumQuantity             | entier                       | The maximum quantity available.                                                                                 |
| rank                        | entier                       | The offer rank or priority compared to other categories in the same product line. This property should be set only if there is more than one offer for a given product line.  |
| uri                         | chaîne                    | The offer URI.                                                                                                  |
| locale                      | chaîne                    | The locale in which the offer applies.                                                                          |
| country                     | chaîne                    | The country/region  where the offer applies.                                                                    |
| catégorie                    | [OfferCategory](#offercategory)           | The category of the offer.                                                                   |
| limitUnitOfMeasure          | chaîne                    | A value that indicates the type of purchase limitation. Les valeurs possibles sont :<br/> "None" - There are no restrictions on the number of subscriptions based on the offer purchased.<br/> "Concurrent" - The number of subscriptions that can exist on the customer tenant at a given time, this includes subscriptions that are active or canceled. This value applies mostly to small business offers where license counts are less than 300. De-provisionioned subscriptions don't count.<br/> "LifeTime" - The number of subscriptions that can exist for the lifetime of the customer tenant. This value is most applicable to Trials. De-provisionioned subscriptions don't count.      |
| limit                       | entier                       | The amount of subscriptions that can be purchased of this offer based on the limitUnitOfMeasure.                |
| prerequisiteOffers          | chaîne                    | The prerequisite offers.                                                                                        |
| isAddOn                     | booléen                   | A value indicating whether this instance is an addon.                                                           |
| hasAddOns                   | booléen                   | A value indicating whether this offer has any addons.                                                           |
| isAvailableForPurchase      | booléen                   | A value indicating whether this instance is available for purchase.                                             |
| facturation                     | chaîne                    | Specifies the billing type for the line item purchase: "none", "usage", or "license".                           |
| supportedBillingCycles      | array of strings          | Indicates the billing cycles supported for this offer. Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | booléen                   | A value indicating whether the offer renews automatically.                                                      |
| upgradeTargetOffers         | array of strings          | The list of offers that this offer can be upgraded to.                                                          |
| conversionTargetOffers      | array of strings          | The list of offers that this offer can be converted to.                                                         |
| reselleeQualifications      | array of strings          | The qualifications required by the customer in order for a partner to purchase the offer for that customer.     |
| resellerQualifications      | array of strings          | The qualifications required by the partner in order to purchase the offer for a customer.                       |
| salesGroupId                | chaîne                    | A string used to group offers into separate orders.                                                             |
| isTrial                     | booléen                   | A value indicating whether this is a trial offer.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Gets the offer product.                                                                           |
| unitType                    | chaîne                    | The type of the unit.                                                                                      |
| liens                       | [OfferLinks](#offerlinks)               | The offer's "learn more" link.                                                                    |
| attributs                  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the offer.                         |

## <a name="span-idoffercategoryspan-idoffercategoryspan-idoffercategoryoffercategory"></a><span id="OfferCategory"/><span id="offercategory"/><span id="OFFERCATEGORY"/>OfferCategory

Describes the categorization of an offer. This includes the rank or priority of this offer category compared to others in the same product line.

| Propriété   | Tapez                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | chaîne                                                         | The category identifier.                                                                                                                                                   |
| name       | chaîne                                                         | The category name.                                                                                                                                                         |
| rank       | entier                                                            | The category rank or priority compared to other categories in the same offer. This property should be set only if there is more than one offer category for a given offer. |
| locale     | chaîne                                                         | The locale in which the offer applies.                                                                                                                        |
| country    | chaîne                                                         | The country/region where the offer applies.                                                                                                                   |
| liens      | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the OfferCategory.                                                                                                                     |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the OfferCategory.                                                                                                                |

## <a name="span-idofferlinksspan-idofferlinksspan-idofferlinksofferlinks"></a><span id="OfferLinks"/><span id="offerlinks"/><span id="OFFERLINKS"/>OfferLinks

Contains links for learning more information about the offer.

| Propriété  | Tapez | Description                 |
|-----------|------|-----------------------------|
| learnMore | Lier | The "learn more" link.      |
| self      | Lier | The self URI                |
| suivant      | Lier | The next page of items.     |
| previous  | Lier | The previous page of items. |

## <a name="span-idofferproductspan-idofferproductspan-idofferproductofferproduct"></a><span id="OfferProduct"/><span id="offerproduct"/><span id="OFFERPRODUCT"/>OfferProduct

A product or service which may have more than one offer associated with it, each with different sets of features and targeted at different customer needs.

| Propriété | Tapez   | Description              |
|----------|--------|--------------------------|
| Id       | chaîne | The category identifier. |
| Nom     | chaîne | The category name.       |
| Unit     | chaîne | The product unit.        |

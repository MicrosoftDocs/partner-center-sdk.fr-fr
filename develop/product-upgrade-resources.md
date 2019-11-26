---
title: Product upgrade resources
description: You can use multiple resources related to Partner Center product upgrades to an Azure plan. These include ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct and ErrorDetails.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3f891c3e7d25dfc6ec47ef861fa79345c32c1f9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488199"
---
# <a name="product-upgrade-resources"></a>Product upgrade resources

S'applique à :

- Espace partenaires

You can use the following resources for information about Partner Center product upgrades from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

The **ProductUpgradesRequest** resource provides information about the product upgrades request object.

| Propriété | Tapez | Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| customerId           | chaîne                                       | A GUID-formatted string that identifies the customer. |
| productFamily        | chaîne                                       | The product family for which the upgrade is requested for. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

The **ProductUpgradesEligibility** resource provides information about the customer's eligibility for upgrading a product.

| Propriété | Tapez | Description |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| customerId           | chaîne                                       | A GUID-formatted string that identifies the customer. |          | productFamily        | chaîne                                       | The product family for which the upgrade is requested for. |
| isEligible           | bool                                         | The bool value indicates whether the customer is eligible for requested upgrade. |
| upgradeId            | chaîne                                       | The upgrade ID if a product upgrade for given family is already in place. |
| reason               | chaîne                                       | The reason for which customer isn't eligible for product upgrade. |
| productFamily        | chaîne                                       | The product family for which the upgrade is requested for. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

The **ProductUpgradesStatus** resource provides information about the status of a product upgrade.

| Propriété | Tapez | Description |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | chaîne                                                         | A GUID-formatted string that identifies the upgrade. |
| productFamily       | chaîne                                                         | The product family for which the upgrade is requested for.
| status              | chaîne                                                         | The status of the product upgrade.
| lineItems           | array of [UpgradesLineItem](#upgradeslineitem) resources       | An array of objects that provides information of the upgrade details for each line item that was part of the request body.
| errorDetails        | [ErrorDetails](#errordetails) resource                         | The error details for upgrade requested.
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

The **UpgradesLineItem** resource describes the status of product upgrade details for each line item of the request.

| Propriété | Tapez | Description |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | [UpgradeProduct](#upgradeproduct) object            | Information of the source product being upgraded. |
| targetProduct   | [UpgradeProduct](#upgradeproduct) object            | Information of the target product post upgrade. |
| upgradedDate    | string in UTC date-time format                      | The date the subscription was upgraded. |
| status          | chaîne                                              | The status of the product upgrade. |
| errorDetails    | [ErrorDetails](#errordetails) resource              | The error details for upgrade requested. |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="upgradeproduct"></a>UpgradeProduct

The **UpgradeProduct** resource provides information about the product being upgraded.

| Propriété | Tapez |Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | chaîne                                       | A GUID-formatted string that identifies the product. |
| name                 | chaîne                                       | The friendly name of product being upgraded. |  
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |

## <a name="errordetails"></a>ErrorDetails

The **ErrorDetails** resource provides details about errors during the upgrade process.

| Propriété | Tapez | Description |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| code                    | chaîne                                       | A error code when the product upgrade fails. |
| message                 | chaîne                                       | The error message when the product upgrade fails. |
| attributs              | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. |

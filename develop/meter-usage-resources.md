---
title: Meter usage record resource
description: You can use the MeterUsageRecord resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 003db39c92e96b12863edebb46b3e3341ffae10e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488309"
---
# <a name="meter-usage-record-resource"></a>Meter usage record resource

S'applique à :

- Espace partenaires

You can use the **MeterUsageRecord** resource to describe the estimated monetary cost of a subscription's meter level usage in the current billing cycle.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Propriété         | Tapez               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | chaîne             | A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan. For Microsoft Azure (MS-AZR-0145P) subscriptions,, this value is the commerce subscription identifier. For Azure plan subscription resources, this value is the Azure plan identifier.                  |
| MeterId  | chaîne             | Gets or sets the meter identifier.                                                        |
| MeterName          | chaîne             | Gets or sets the meter name.                                       |
| Catégorie               | chaîne             | Gets or sets the Azure resource category.                                                 |
| Sous-catégorie             | chaîne             |  Gets or sets the Azure resource sub-category.                                                     |
| QuantityUsed        | décimal             | Gets or sets the quantity of the Azure resource used.   |
| Unit   | chaîne             | Gets or sets the unit of measure for the Azure resource. |
| TotalCost   | décimal             | Gets or sets the estimated total cost of usage. |
| CurrencyLocale   | chaîne             | The locale in which the subscription was used. This property determines the currency that is used on the invoice. This property is available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | chaîne             | Gets or sets the currency code. This property is available for Azure plans.                                         |
| USDTotalCost   | décimal             | Gets or sets the estimated total cost in USD. This property is available for Azure plans.                                         |
| LastModifiedDate | chaîne             | The day (in date-time format) that this record was last modified.                             |
| Attributs       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |                                           |

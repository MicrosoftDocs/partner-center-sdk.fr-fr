---
title: Azure rate card resources
description: The Azure Rate Card provides real-time prices for Azure offers.
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e81debb15c30ba024d897a00075bffe28be3acaf
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489139"
---
# <a name="azure-rate-card-resources"></a>Azure rate card resources

S'applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The Azure Rate Card provides real-time prices for Azure offers. Azure pricing is quite dynamic and changes frequently. Microsoft publishes updates on Partner Center, but the REST API provides the fastest way for Cloud Solution Provider partners to get current prices.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, it uses your partner profile settings in Partner Center and your browser language, but those are customizable. This is especially relevant if you manage sales in multiple markets from a single, centralized office.

## <a name="azureratecard"></a>AzureRateCard

Describes the properties of an Azure Rate Card resource.

| Propriété      | Tapez                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | chaîne                                    | The currency in which the rates are provided.                     |
| isTaxIncluded | booléen                                   | All rates are pretax, so this will always be returned as "false". |
| locale        | chaîne                                    | The culture in which the resource information is localized.       |
| meters        | array of objects                          | Array of [AzureMeter](#azuremeter) objects.                       |
| offerTerms    | array of objects                          | Array of [AzureOfferTerm](#azureofferterm) objects.               |
| attributs    | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Contains "objectType": "AzureRateCard"   |


### <a name="operations-on-the-azureratecard-resource"></a>Operations on the AzureRateCard resource

- [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Propriété         | Tapez             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | chaîne           | Meter's unique identifier.                                                                    |
| name             | chaîne           | Friendly name of the meter.                                                                   |
| rates            | object           | Meter rates. The key is the meter quantity (string) and the value is the meter rate (number). |
| tags             | array of strings | Optional meter tags. This array can be empty.                                                 |
| catégorie         | chaîne           | Category of the resource.                                                                     |
| subcategory      | chaîne           | Sub-category of the resource.                                                                 |
| region           | chaîne           | Region of the id.                                                                             |
| unités             | chaîne           | The type of quantity (hours, bytes, etc.)                                                     |
| includedQuantity | nombre           | Meter quantity that is included free of charge.                                               |
| effectiveDate    | chaîne           | The date this meter is in effect.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Propriété         | Tapez             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | chaîne           | Friendly name of the offer term.        |
| discount         | nombre           | The discount applied, if any.           |
| excludedMeterIds | array of strings | Meters excluded from the offer, if any. |
| effectiveDate    | chaîne           | The date the offer is in effect.        |
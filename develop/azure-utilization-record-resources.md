---
title: Azure utilization record resources
description: The Azure utilization record contains details about the utilization of an Azure subscription resource.
ms.assetid: 4C1EEEB3-DB25-4D61-BFED-C4AB5D3BB5CF
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8874ce3a9dd3c6f8b0745baafd0f6a09fdbeb842
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489129"
---
# <a name="azure-utilization-record-resources"></a>Azure utilization record resources

S'applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The Azure utilization record contains details about the utilization of an Azure subscription resource. If you are a cloud service provider partner who owns the billing relationship for your customers' Azure subscriptions, you can use this REST API to provide a scalable way to track usage incurred on the subscriptions in order to send an invoice to your customers at the end of every billing cycle.

To track usage and help predict your monthly bill and the bills for individual customers, you can combine a Rate Card query to [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).

Prices differ by market and currency, and this API takes location into consideration. By default, it uses your partner profile settings in Partner Center and your browser language, but those are customizable. This is especially relevant if you manage sales in multiple markets from a single, centralized office.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Describes the properties of an Azure utilization record resource.

| Propriété       | Tapez                                      | Obligatoire | Description                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | chaîne                                    | Oui      | The start of the usage aggregation time range. The response is grouped by the time of consumption (when the resource was actually used vs. when was it reported to the billing system). |
| usageEndTime   | chaîne                                    | Oui      | The end of the usage aggregation time range. The response is grouped by the time of consumption (when the resource was actually used vs. when was it reported to the billing system).   |
| resource       | object                                    | Oui      | Contains an [AzureResource](#azureresource) object.                                                                                                                                     |
| quantity       | nombre                                    | Oui      | The quantity consumed of the [AzureResource.](#azureresource)                                                                                                                           |
| unités           | chaîne                                    | non       | The type of quantity (hours, bytes, etc.) This property is optional                                                                                                                     |
| infoFields     | object                                    | Oui      | Key-value pairs of instance level details. This object may be empty.                                                                                                                    |
| instanceData   | object                                    | non       | Contains an [AzureInstanceData](#azureinstancedata) object that contains key-value pairs of instance level details. This property is optional and may not be included.                  |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Oui      | The metadata attributes. Contains "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Operations on the AzureUtilizationRecord resource

- [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Describes the properties of an Azure Resource.

| Propriété    | Tapez   | Obligatoire | Description                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | chaîne | Oui      | Unique identifier of the Azure resource. Also known as resourceID or resource GUID. |
| name        | chaîne | non       | Friendly name of the resource being consumed. Cette propriété est facultative.            |
| catégorie    | chaîne | non       | The category of the consumed resource. Cette propriété est facultative.                   |
| subcategory | chaîne | non       | The sub-category of the consumed resource. Cette propriété est facultative.               |
| region      | chaîne | non       | The region of the consumed resource. Cette propriété est facultative.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Describes the properties of an Azure Instance Data resource.

| Propriété       | Tapez             | Obligatoire | Description                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | chaîne           | Oui      | The fully qualified Azure resource ID, which includes the resource groups and the instance name.                   |
| location       | chaîne           | Oui      | Region in which the service was run.                                                                               |
| partNumber     | object           | Oui      | Unique namespace used to identify the resource for commercial marketplace 3rd party usage. This may be an empty string. |
| orderNumber    | nombre           | Oui      | Unique namespace used to identify the 3rd party order for commercial marketplace. This may be an empty string.          |
| tags           | array of strings | non       | Resource tags specified by the user. This property is optional and may not be included.                            |
| additionalInfo | array of strings | non       | Additional data for an Azure resource. This property is optional and may not be included.                          |
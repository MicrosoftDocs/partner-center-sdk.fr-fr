---
title: Analytics resources
description: Partner Center resources for data used to report on usage, deployment, and consumption.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8098de53c3fc4632d17ef6cdba7fe983d9fffbbe
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489199"
---
# <a name="analytics-resources"></a>Analytics resources

S'applique à :

- Espace partenaires

The resources defined here contain data used to report on usage, deployment, and consumption.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

The **PartnerLicensesDeploymentInsights** resource contains partner-level insights about license deployment.

| Propriété                  | Tapez                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | nombre                                                         | The percentage of licenses deployed.                                                |
| licensesSold              | nombre                                                         | The number of licenses sold.                                                        |
| processedDateTime         | string in UTC date-time format                                 | The date and time when the data was aggregated.                                     |
| serviceName               | chaîne                                                         | The service name (e.g. o365, crm).                                                  |
| channel                   | chaîne                                                         | The channel name of the service (e.g. reseller).                                    |
| attributs                | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

The **PartnerLicensesUsageInsights** resource contains partner-level insights about license usage.

| Propriété                     | Tapez                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | nombre                                                         | The percentage of licenses deployed.                                           |
| workloadName                 | chaîne                                                         | The workload name (e.g. exchange).                                             |
| processedDateTime            | string in UTC date-time format                                 | The date and time when the data was aggregated.                                |
| serviceName                  | chaîne                                                         | The service name (e.g. o365, crm).                                             |
| channel                      | chaîne                                                         | The channel name of the service (e.g. reseller).                               |
| attributs                   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

The **CustomerLicensesDeploymentInsights** resource contains customer-level insights about license deployment.

| Propriété          | Tapez                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | nombre                                                         | The number of licenses deployed.                                                     |
| licensesSold      | nombre                                                         | The number of licenses sold.                                                         |
| deploymentPercent | nombre                                                         | The adjusted percentage of licenses deployed.                                        |
| customerId        | chaîne                                                         | The customer identifier.                                                             |
| customerName      | chaîne                                                         | The customer name.                                                                   |
| productName       | chaîne                                                         | The product name.                                                                    |
| serviceCode       | chaîne                                                         | The service code of the license.                                                     |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                      |
| serviceName       | chaîne                                                         | The service name (e.g. o365, crm).                                                   |
| channel           | chaîne                                                         | The channel name of the service (e.g. reseller).                                     |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

The **CustomerLicensesUsageInsights** resource contains customer-level insights about license usage.

| Propriété          | Tapez                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | chaîne                                                         | The workload code.                                                              |
| workloadName      | nombre                                                         | The workload name (e.g. Exchange).                                              |
| usagePercent      | nombre                                                         | The adjusted percentage of licenses used.                                       |
| licensesActive    | nombre                                                         | The number of active licenses.                                                  |
| licensesQualified | nombre                                                         | The number of qualified licenses.                                               |
| customerId        | chaîne                                                         | The customer identifier.                                                        |
| customerName      | chaîne                                                         | The customer name.                                                              |
| productName       | chaîne                                                         | The product name.                                                               |
| serviceCode       | chaîne                                                         | The service code of the license.                                                |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                 |
| serviceName       | chaîne                                                         | The service name (e.g. o365, crm).                                              |
| channel           | chaîne                                                         | The channel name of the service (e.g. reseller).                                |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesUsageInsights" |
---
title: Subscription usage resources
description: Subscription usage resources describe subscriptions with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5b6c1a10023b22214bab89473b867a36c5a1eb7f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488019"
---
# <a name="subscription-usage-resources"></a>Subscription usage resources

S'applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

You can use the following subscription usage resources to get usage information for a specific subscription with usage-based billing. These subscriptions have daily and monthly usage records, along with a usage summary for each pay period.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*The **SubscriptionDailyUsageRecord** resource is obsolete and may produce inaccurate results. We recommend that you update your applications to use the APIs described in [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md) and [Get prices for Microsoft Azure](get-prices-for-microsoft-azure.md) instead.*

The **SubscriptionDailyUsageRecord** resource describes how much a subscription is used in a single day.

| Propriété         | Tapez               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | chaîne             | The day, in date-time format, that the subscription was used.                                 |
| ResourceId       | chaîne             | GUID. The unique ID of the resource.                                                          |
| Nom_ressource     | chaîne             | The name of the resource.                                                                     |
| TotalCost        | décimal             | The estimated total cost of using the resources in the subscription on the specified day.     |
| CurrencyLocale   | chaîne             | The locale in which the subscription was used, determines the currency to use on the invoice. |
| LastModifiedDate | chaîne             | The day, in date-time format, that this record was last modified.                             |
| Attributs       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

The **SubscriptionMonthlyUsageRecord** resource describes how much a subscription is used in a single month.

| Propriété         | Tapez               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| le statut           | chaîne             | The status of the subscription: "none", "active", "suspended", or "deleted".                  |
| PartnerOnRecord  | chaîne             | "The MPN ID of the partner on record."                                                        |
| OfferId          | chaîne             | GUID. The id of the offer related to this subscription.                                       |
| Id               | chaîne             | GUID. The id of the subscription or resource.                                                 |
| Nom             | chaîne             | The name of the subscription or resource.                                                     |
| TotalCost        | décimal             | The estimated total cost of using the resources in the subscription in the specified month.   |
| CurrencyLocale   | chaîne             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode     | chaîne             | Gets or sets the currency code. Available for Azure plan subscription resources.                                         |
| USDTotalCost     | décimal             | Gets or sets the estimated total cost in USD. Available for Azure plans.                                         |
| LastModifiedDate | chaîne             | The day, in date-time format, that this record was last modified.                             |
| Attributs       | ResourceAttributes | The metadata attributes corresponding to the resource.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

The **SubscriptionUsageSummary** resource describes how much a specific subscription was used in the current billing period.

| Propriété         | Tapez               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | chaîne             | GUID. The id of the subscription or resource. In the context of CustomerMonthlyUsageRecord this id is the customer id. |
| Nom_ressource     | chaîne             | The name of the subscription or resource. In the context of CustomerMonthlyUsageRecord this name is the customer name. |
| BillingStartDate | date               | The start date of the current billing period, in date-time format.                                                     |
| BillingEndDate   | date               | The end date of the current billing period, in date-time format.                                                       |
| TotalCost        | double             | The estimated total cost of using the resources in the subscription during the specified billing period.               |
| CurrencyLocale   | chaîne             | The locale in which the subscription was used, determines the currency to use on the invoice. Available for Microsoft Azure (MS-AZR-0145P) subscriptions. |
| CurrencyCode   | chaîne             | Gets or sets the currency code. Available for Azure plans.                                         |
| USDTotalCost   | décimal             | Gets or sets the estimated total cost in USD. Available for Azure plan subscription resources.                                         |
| LastModifiedDate | chaîne             | The day, in date-time format, that this record was last modified.                                                      |
| Liens            | ResourceLinks      | The resource links corresponding to the SubscriptionUsageSummary.                                                      |
| Attributs       | ResourceAttributes | The metadata attributes corresponding to the SubscriptionUsageSummary.                                                 |

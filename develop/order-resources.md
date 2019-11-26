---
title: Order resources
description: A partner places an order when a customer wants to buy a subscription from a list of offers.
ms.assetid: 5CFA35FF-1C0D-461D-A942-309AFCD98395
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0d6b42414c12c299d9205e6abfa1aadc98fc530e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488269"
---
# <a name="order-resources"></a>Order resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

A partner places an order when a customer wants to buy a subscription from a list of offers.

>[!NOTE]
>The Order resource has a rate limit of 500 requests per minute per tenant identifier.

## <a name="order"></a>Ordre

Describes a partner's order.

| Propriété           | Tapez                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | chaîne                                             | An order identifier that is supplied upon successful creation of the order.                                   |
| alternateId        | chaîne                                             | A friendly identifier for the order.                                                                          |
|referenceCustomerId | chaîne                                             | The customer identifier. |
| billingCycle       | chaîne                                             | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype). The default is "Monthly" or "OneTime" at order creation. This field is applied upon successful creation of the order. |
| transactionType    | chaîne                                             | Read-only. The transaction type of the order. Supported values are 'UserPurchase', 'SystemPurchase', or 'SystemBilling' |
| lineItems          | array of [OrderLineItem](#orderlineitem) resources | An itemized list of the offers the customer is purchasing including the quantity.        |
| currencyCode       | chaîne                                             | Read-only. The currency used when placing the order. Applied upon successful creation of the order.           |
| currencySymbol     | chaîne                                             | Read-only. The currency symbol assciated with the currency code. |
| creationDate       | DateHeure                                           | Read-only. The date the order was created, in date-time format. Applied upon successful creation of the order.                                   |
| status             | chaîne                                             | Read-only. The status of the order.  Supported values are the member names found in [**OrderStatus**](#orderstatus).        |
| liens              | [OrderLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the Order.            |
| attributs         | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the Order.       |

## <a name="orderlineitem"></a>OrderLineItem

An order contains an itemized list of offers, and each item is represented as an OrderLineItem.

| Propriété             | Tapez                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | entier                                       | Each line item in the collection gets a unique line number, counting up from 0 to count-1.                                                                                                                                                 |
| offerId              | chaîne                                    | The ID of the offer.                                                                                                                                                                                                                       |
| subscriptionId       | chaîne                                    | L’ID de l’abonnement.                                                                                                                                                                                                                |
| parentSubscriptionId | chaîne                                    | Facultatif. The ID of the parent subscription in an add-on offer. Applies to PATCH only.                                                                                                                                                     |
| friendlyName         | chaîne                                    | Facultatif. The friendly name for the subscription defined by the partner to help disambiguate.                                                                                                                                              |
| quantity             | entier                                       | The number of licenses or instances.                                                                                                                                                                                |
| termDuration         | chaîne                                    | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month), **P1Y** (1 year) and **P3Y** (3 years).                               |
| transactionType      | chaîne                                    | Read-only. The transaction type of the line item. Supported Values are 'new', 'renew', 'addQuantity', 'removeQuantity', 'cancel', 'convert', or 'customerCredit'. |
| partnerIdOnRecord    | chaîne                                    | When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider). This ensures proper accounting for incentives. |
| provisioningContext  | Dictionary<string, string>            | Information required for provisioning for some items in the catalog. The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.                                                                                                                                               |
| liens                | [OrderLineItemLinks](#orderlineitemlinks) | Read-only. The resource links corresponding to the order line item.                                                                                                                                                                                |
| renewsTo             | Array of objects                          | An array of [RenewsTo](#renewsto) resources.                                                                            |

## <a name="renewsto"></a>RenewsTo

Represents one item contained in a order line item.

| Propriété              | Tapez             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | chaîne           | non              | An ISO 8601 representation of the renewal term's duration. The current supported values are **P1M** (1 month) and **P1Y** (1 year). |

## <a name="orderlinks"></a>OrderLinks

Represents the resource links corresponding to the order.

| Propriété           | Tapez                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#Link)            | When populated, the link to retrieve provisioning status for the order.       |
| self               | [Link](utility-resources.md#Link)            | The link to retrieve the order resource.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Represents the full subscription associated with the order.

| Propriété           | Tapez                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#Link)            | When populated, the link to retrieve the [provisioning status](#orderlineitemprovisioningstatus) of the line item.       |
| sku                | [Link](utility-resources.md#Link)            | The link to retrieve SKU information for the catalog item bought.                    |
| abonnement       | [Link](utility-resources.md#Link)            | When populated, the link to the full subscription information.                       |
| activationLinks    | [Link](utility-resources.md#Link)            | When populated, the GET resource for links to activate the subscription.             |

## <a name="orderstatus"></a>OrderStatus

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the state of the order.

| Valeur              | Position     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | Enum initializer.                               |
| completed          | 1            | Indicates that the order is completed.          |
| pending            | 2            | Indicates that the order is still pending.      |
| cancelled          | 3            | Indicates that the order has been cancelled.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Represents the provisioning status of an [OrderLineItem](#orderlineitem).

| Propriété                        | Tapez                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | entier                                 | The unique line number of the order line item. Values range from 0 to count-1.             |
| status                          | chaîne                              | The provisioning status of the order line item. Values include:</br>"Fulfilled": Fulfillment of the order is successfully completed and the user will be able to use the reservations</br>"Unfulfilled": Not fulfilled due to cancellation</br>"PrefulfillmentPending": Your request is still processing, fulfillment is not yet complete |
| quantityProvisioningInformation | List<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | A list of quantity provisioning status information for the order line item. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Represents the provisioning status by quantity.

| Propriété                           | Tapez                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | entier                                          | The number of items.                                 |
| status                             | chaîne                                       | The status of the number of items.                   |

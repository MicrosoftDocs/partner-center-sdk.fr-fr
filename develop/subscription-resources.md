---
title: Subscription resources
description: Subscription resources can provide further information about subscriptions throughout the life cycle, such as support, refunds, Azure entitlements.
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc771fcbc8cb03e95684dd32ff0f1f29076bba49
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486699"
---
# <a name="subscription-resources"></a>Subscription resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

A subscription lets a customer use a service for a certain period of time. Not all fields will apply to all subscriptions. Many fields only apply at certain points in the life cycle, such as if a subscription is suspended or cancelled.

## <a name="subscription"></a>Abonnement

>[!NOTE]
>The **Subscription** resource has a rate limit of 500 requests per minute per tenant identifier.

The **Subscription** resource represents the life cycle of a subscription and includes properties that define the states throughout the subscription life cycle.

| Propriété             | Tapez                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | chaîne                                                        | The subscription identifier.                                                                                                                                                  |
| offerId              | chaîne                                                        | The offer identifier.                                                                                                                                                         |
| entitlementId        | chaîne                                                        | The entitlement identifier (an Azure subscription ID).                                                                                                                        |
| offerName            | chaîne                                                        | The offer name.                                                                                                                                                               |
| friendlyName         | chaîne                                                        | The friendly name for the subscription defined by the partner to help disambiguate.                                                                                           |
| quantity             | nombre                                                        | The quantity. For example, in case of license-based billing, this property is set to the license count.                                                            |
| unitType             | chaîne                                                        | The units defining quantity for the subscription.                                                                                                                             |
| parentSubscriptionId | chaîne                                                        | Gets or sets the parent subscription identifier.                                                                                                                              |
| creationDate         | chaîne                                                        | Gets or sets the creation date, in date-time format.                                                                                                                          |
| effectiveStartDate   | string in UTC date time format                                | Gets or sets the effective start date for this subscription, in date-time format. It is used to back date a migrated subscription or to align it with another.                |
| commitmentEndDate    | string in UTC date time format                                | The commitment end date for this subscription, in date-time format. For subscriptions which are not auto-renewable, this represents a date far, far away in the future.       |
| status               | chaîne                                                        | The subscription status: "none", "active", "pending", "suspended", or "deleted".                                                                                                         |
| autoRenewEnabled     | booléen                                                       | Gets a value indicating whether the subscription is renewed automatically.                                                                                                    |
| billingType          | chaîne                                                        | Specifies how the subscription is billed: "none", "usage", or "license".                                                                                                      |
| billingCycle         | chaîne                                                        | Indicates the frequency with which the partner is billed for this order. Supported values are the member names found in [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | booléen                                                       | Gets or sets a value indicating whether the subscription has purchasable add-ons.                                                                                             |
| isTrial              | booléen                                                       | A value indicating whether this is a trial subscription.                                                                                                                      |
| isMicrosoftProduct   | booléen                                                       | A value indicating whether this is a Microsoft product.                                                                                                                       |
| publisherName        | chaîne                                                        | The publisher name.                                                                                                                                                           |
| actions              | array of strings                                              | Gets or sets the actions that are allowed. Possible values: "edit", "cancel"                                                                                                  |
| partnerId            | chaîne                                                        | The MPN ID of the reseller of record, used in the indirect partner model.                                                                                                     |
| suspensionReasons    | array of strings                                              | Read-only. If the subscription was suspended, indicates why.                                                                                                                  |
| contractType         | chaîne                                                        | Read-only. The type of contract: "subscription", "productKey", or "redemptionCode".                                                                                           |
| refundOptions        | array of [RefundOption](#refundoption) resources   | Read-Only. The set of refund options available for this subscription.                                                                                              |
| liens                | [SubscriptionLinks](#subscriptionlinks)                       | Gets or sets the subscription links.                                                                                                                                          |
| orderId              | chaîne                                                        | The ID of the order that was placed to begin the subscription.                                                                                                                |
| termDuration         | chaîne                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month), **P1Y** (1 year) and **P3Y** (3 years).                                                        |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the subscription.                                                                                                                    |
| renewalTermDuration  | chaîne                                                        | An ISO 8601 representation of the term's duration. The current supported values are **P1M** (1 month) and **P1Y** (1 year).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

The **SubscriptionLinks** resource describes the collection of links attached to a subscription resource.

| Propriété           | Tapez                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Link](utility-resources.md#link) | Gets or sets the offer.               |
| parentSubscription | [Link](utility-resources.md#link) | Gets or sets the parent subscription. |
| product            | [Link](utility-resources.md#link) | Gets the product associated with the subscription. |
| sku                | [Link](utility-resources.md#link) | Gets the product sku associated with the subscription. |
| disponibilité       | [Link](utility-resources.md#link) | Gets the product sku availability associated with the subscription. |
| activationLinks    | [Link](utility-resources.md#link) | Gets the list of activation links associated with the subscription. |
| self               | [Link](utility-resources.md#link) | The self URI.                         |
| suivant               | [Link](utility-resources.md#link) | The next page of items.               |
| previous           | [Link](utility-resources.md#link) | The previous page of items.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

The **SubscriptionProvisioningStatus** resource provides information about the provisioning status of a subscription.

| Propriété   | Tapez                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | chaîne                                                         | A GUID formatted string that identifies the product SKU.             |
| status     | chaîne                                                         | Indicates the provisioning status: "success", "pending" or "failed". |
| quantity   | nombre                                                         | Provides the subscription quantity after provisioning.               |
| endDate    | string in UTC date time format                                 | The end date of the subscription.                                    |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

The **SubscriptionRegistrationStatus** resource describes the collection of links attached to a subscription resource.

| Propriété           | Tapez                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | chaîne                             | The subscription identifier.                                                          |
| status             | chaîne                             | Indicates the registration status: "registered", "registering" or "notregistered".    |

## <a name="supportcontact"></a>SupportContact

The **SupportContact** resource represents a support contact for a customer's subscription.

| Propriété        | Tapez                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | chaîne                                                         | A GUID formatted string that indicates the support contact's tenant identifier. |
| supportMpnId    | chaîne                                                         | The contact's Microsoft Partner Network (MPN) identifier.                       |
| name            | chaîne                                                         | The name of the support contact.                                                |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)            | The support contact related links.                                              |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes. Contains "objectType": " SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

The **RegisterSubscription** resource returns a link that can be used to query the registration status of a subscription. The registration status is returned in the response body of a successfully accepted request to register an Azure subscription.

| Propriété                | Tapez                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Returns HTTP Status Code 202 "Accepted", with a Location header containing a link to query the registration status. Par exemple, `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"`. |

## <a name="refundoption"></a>RefundOption

The **RefundOption** resource represents a possible refund option for the subscription.

| Propriété          | Tapez | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| type | chaîne | The type of refund. The supported values are "Partial" and "Full" |
| expiresAfter      | string in UTC date time format | The timestamp when this option expires. If null, this means it has no expiration. |

## <a name="azureentitlement"></a>AzureEntitlement

The **AzureEntitlement** resource represents the Azure entitlements for the subscription.

| Propriété          | Tapez | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | chaîne | The entitlement identifier |
| friendlyName      | chaîne | The friendly name of the entitlement. |
| status | chaîne | The status of entitlement. |
| subscriptionId | chaîne | The subscription identifier the entitlement belongs to. |

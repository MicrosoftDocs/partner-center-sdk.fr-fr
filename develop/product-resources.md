---
title: Products resources
description: Resources that represent purchasable goods or services. Includes resources for describing the product type and shape (SKU), and for checking the availability of the product in an inventory.
ms.assetid: 80C1F9B5-35FB-4DD8-B501-03467E1D75AD
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ef2677994f2a2af2171624d5a7c5f2ad5696fd70
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488249"
---
# <a name="products-resources"></a>Products resources


**Applies To**

- Espace partenaires

Resources that represent purchasable goods or services. Includes resources for describing the product type and shape (SKU), and for checking the availability of the product in an inventory.   


## <a name="product"></a>Produit


Represents a purchasable good or service. A product by itself is not a purchasable item.

| Propriété           | Tapez                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| id                 | chaîne                        | The ID for this product.                                                 |
| title              | chaîne                        | The product title.                                                       |
| description        | chaîne                        | The product description.                                                 |
| productType        | [ItemType](#itemtype)         | An object that describes the type categorization(s) of this product.     |
| isMicrosoftProduct | bool                          | Indicates whether this is a Microswoft product.                          |
| publisherName      | chaîne                        | The name of the product's publisher if available.                          |
| liens              | [ProductLinks](#productlinks) | The resource links contained within the product.                         |



## <a name="itemtype"></a>ItemType


Represents the type of a product.

| Propriété        | Tapez                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| id              | chaîne                        | The type identifier.                                                                 |
| displayName     | chaîne                        | The display name for this type.                                                      |
| subType         | [ItemType](#itemtype)         | Facultatif. An object that describes a sub-type categorization for this item type.     |

 

## <a name="productlinks"></a>ProductLinks


Contains a list of links for a [Product](#product).

| Propriété        | Tapez                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| skus            | [Link](utility-resources.md#link)                             | The link for accessing the underlying SKUs.          |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within this resource.   |



## <a name="sku"></a>Sku


Represents a purchasable Stock Keeping Unit (SKU) under a product. These represent the different shapes of the product. 

| Propriété               | Tapez             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| id                     | chaîne           | The ID for this SKU. This ID is unique only within the context of its parent product. |
| title                  | chaîne           | The title of the SKU.                                                                 |
| description            | chaîne           | The description of the SKU.                                                           |
| productId              | chaîne           | The ID of the parent [Product](#product) that contains this SKU.                      |
| minimumQuantity        | entier              | The minimum quantity allowed for purchase.                                            |
| maximumQuantity        | entier              | The maximum quantity allowed for purchase.                                            |
| isTrial                | bool             | Indicates whether this SKU is a trial item.                                           |
| supportedBillingCycles | array of strings | The list of supported billing cycles for this SKU. Supported values are the member names found in [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | array of strings | The list of prerequisite steps or actions that are needed prior to purchasing this item. The supported values are:<br/>  "InventoryCheck" - Indicates that the item's inventory should be evaluated before attempting to purchase this item.<br/> "AzureSubscriptionRegistration" - Indicates that an Azure subscription is needed and must be registered before attempting to purchase this item.  |
| inventoryVariables     | array of strings | The list of variables needed to execute an inventory check on this item. The supported values are:<br/> "CustomerId" - The ID of the customer that the purchase would be for.<br/> "AzureSubscriptionId" - The ID of the Azure subscription that would be used for an Azure reservation purchase.</br> "ArmRegionName" - The region for which to verify inventory. This value must match the "ArmRegionName" from the SKU's DynamicAttributes. |
| provisioningVariables  | array of strings | The list of variables that must be provided into the provisioning context of a [cart line item](cart-resources.md#cartlineitem) when purchasing this item. The supported values are:<br/> Scope - The scope for an Azure reservation purchase: "Single", "Shared".<br/> "SubscriptionId" - The ID of the Azure subscription that would be used for an Azure reservation purchase.<br/> "Duration" - The duration of the Azure reservation: "1Year", "3Year".  |
| dynamicAttributes      | key/value pairs  | The dictionary of dynamic properties that apply to this item. Please note that the properties in this dictionary are dynamic and can change without notice. You should not create strong dependencies on particular keys existing in the value of this property.    |
| liens                  | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the SKU.                   |



## <a name="availability"></a>Disponibilité

Represents a configuration in which a SKU is available for purchase (such as country, currency, and industry segment). 

| Propriété        | Tapez                                                | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| id              | chaîne                                              | The ID for this availability. This ID is unique only within the context of its parent [product](#product) and [SKU](#sku). **Note** This ID can change over time. You should only rely on this value within a short time span after retrieving it.  |
| productId       | chaîne                                              | The ID of the [product](#product) that contains this availability.           |
| skuId           | chaîne                                              | The ID of the [SKU](#sku) that contains this availability.                   |
| catalogItemId   | chaîne                                              | The unique identifier for this item in the catalog. This is the ID that must be populated into the [OrderLineItem.OfferId](order-resources.md#orderlineitem) or [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) properties when purchasing the parent [SKU](#sku). **Note** This ID can change over time. You should only rely on this value within a short time after retrieving it. It should only be accessed and used at the time of purchase.  |
| defaultCurrency | chaîne                                              | The default currency supported for this availability.                               |
| segment         | chaîne                                              | The industry segment for this availability. Supported values are: Commercial, Education, Government, NonProfit. |
| country         | chaîne                                              | The country or region (in ISO country code format) where this availability applies. |
| isPurchasable   | bool                                                | Indicates whether this availability is purchasable. |
| isRenewable     | bool                                                | Indicates whether this availability is renewable. |
| product         | [Produit](#product)               | The product this availability corresponds to. |
| sku             | [Sku](#sku)                     | The SKU this availability corresponds to. |
| terms           | array of [Term](#term) resources  | The collection of terms that are applicable to this availability. |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the availability. |


## <a name="term"></a>Terme

Represents a term for which the availability can be purchased. 

| Propriété              | Tapez                                                                              | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| duration              | chaîne                                                                            | An ISO 8601 representation of the term's duration. The current supported values are P1M (1 month), P1Y (1 year) and P3Y (3 years). |
| description           | chaîne                                                                            | The description of the term.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Represents a request to check inventory against certain catalog items. 

| Propriété         | Tapez                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | array of [InventoryItem](#inventoryitem)            | The list of catalog items that the inventory check will evaluate.                           |
| inventoryContext | key/value pairs                                     | The dictionary of context values that are needed to carry out the inventory check(s). Each [SKU](#sku) of the products will define which values (if any) are needed to carry out this operation.  |
| liens            | [ResourceLinks](utility-resources.md#resourcelinks) | The resource links contained within the inventory check request.                            |



## <a name="inventoryitem"></a>InventoryItem

Represents a single item in an inventory check operation. This resource is used for specifying the target items in an input request and is also used to represent the output results of the inventory check operation.  

| Propriété         | Tapez                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | chaîne                                                            | (Required) The ID of the [product](#product).                            |
| skuId            | chaîne                                                            | The ID of the [SKU](#sku). When using this resource as input to an inventory request, this value is optional. If this value is not provided, then all SKUs under the product will be considered as target items of the inventory check operation.      |
| isRestricted     | bool                                                              | Indicates whether this item was found to have a restricted inventory.            |
| restrictions     | array of [InventoryRestriction](#inventoryrestriction)            | The details of any restrictions that are found for this item. This property will only be populated if **isRestricted** = "true". |



## <a name="inventoryrestriction"></a>InventoryRestriction

Represents the details of an inventory restriction. This is only applicable for inventory check output results, not for input requests.

| Propriété         | Tapez                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | chaîne                | The code that identifies the reason for the restriction.                                    |
| description      | chaîne                | The description of the inventory restriction.                                               |
| propriétés       | key/value pairs       | The dictionary of properties that may provide further details on the restriction.           |



## <a name="billingcycletype"></a>BillingCycleType

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate a type of billing cycle.

| Valeur              | Position     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Inconnu            | 0            | Enum initializer.                                                                          |
| Une fois par mois            | 1            | Indicates that the partner will be charged monthly.                                        |
| Annual             | 2            | Indicates that the partner will be charged annually.                                       |
| Aucun(e)               | 3            | Indicates that the partner will not be charged. This value may be used for trial items.    |
| OneTime            | 4            | Indicates that the partner will be charged one time.                                       |


---
title: Invoice resources
description: Multiple invoice-related resources are available through the Partner Center APIs. These resources are related to invoice and line item details.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1eb6175538bd4175e4ba1ff8a5641bdce3b0fa36
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486939"
---
# <a name="invoice-resources"></a>Invoice resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The following invoice-related resources are available through the Partner Center APIs.

## <a name="invoice"></a>Invoice

| Propriété | Tapez | Description |
| -------- | ---- | ----------- |
| id | chaîne | The invoice identifier. |
| invoiceDate | string in UTC date-time format | The date the invoice was generated. |
| billingPeriodStartDate | string in UTC date-time format | Billing period start date in UTC. |
| billingPeriodEndDate | string in UTC date-time format   | Billing period end date in UTC. |
| totalCharges | nombre | The total charges. Includes charges for transactions and any adjustments.     |
| paidAmount | nombre  | The amount paid by the partner. Negative if a payment was received.  |
| currencyCode | chaîne  | A code that indicates the currency used for all invoice item amounts and totals. |
| currencySymbol  | chaîne | The currency symbol used for all invoice item amounts and totals. |
| pdfDownloadLink | chaîne  | A link to download the invoice in PDF format. This link is not returned as part of the search results, and is populated only if the invoice is accessed by ID. This link auto-expires in 30 minutes. |
| invoiceDetails  | array of [InvoiceDetail](#invoicedetail) objects  | The invoice details.  |
| amendments      | array of [Invoice](#invoice) objects   | The amendments to this invoice.  |
| documentType    | chaîne | The document type of the invoice: "Credit Note", "Invoice". |
| amendsOf        | chaîne | The reference number of the document of which this document is an amendment.  |
| invoiceType     | chaîne  | The type of invoice: "recurring", "one\_time".   |
| liens           | [ResourceLinks](utility-resources.md#resourcelinks)  | The resource links.  |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="invoicedetail"></a>InvoiceDetail

An invoice contains a collection of billed items, and each item is represented by an InvoiceDetail resource.

| Propriété            | Tapez                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | chaîne                                                         | The type of invoice detail: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | chaîne                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".         |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links.                                                               |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Each individual charge within an invoice is represented as an InvoiceLineItem.

| Propriété            | Tapez                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | chaîne                                                         | The type of invoice line item: "none", "usage\_line\_items", "billing\_line\_items". |
| billingProvider     | chaîne                                                         | The billing provider: "none", "office", "azure" or "azure\_data\_market".            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Describes a summary of the balance and total charges of an invoice.

| Propriété                 | Tapez                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | nombre                                                         | The balance of the invoice. This is the total amount of unpaid bills. |
| currencyCode             | chaîne                                                         | A code that indicates the currency used for the balance amount.       |
| currencySymbol           | chaîne                                                         | The currency symbol used.                                             |
| accountingDate           | string in UTC date-time format                                 | The date the balance amount was last updated.                         |
| firstInvoiceCreationDate | string in UTC date-time format                                 | The date the first invoice for the customer was created.              |
| lastPaymentDate          | string in UTC date-time format                                 | The date of the last payment.                                         |
| lastPaymentAmount        | nombre                                                         | The amount of the last payment.                                       |
| latestInvoiceDate        | string in UTC date-time format                                 | The date the last invoice for the customer was created.               |
| details                  | array of [InvoiceSummaryDetail](#invoicesummarydetail) objects | The invoice summary detail.                                           |
| liens                    | [ResourceLinks](utility-resources.md#resourcelinks)            | The resource links.                                                   |
| attributs               | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Represent a summary of the individual details for an invoice type (for example, recurring, one\_time).

| Propriété            | Tapez                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | chaîne                                                         | The type of invoice: "recurring", "one\_time".                                       |
| summary             | [InvoiceSummary](#invoicesummary) object                       | The summary of the invoice per invoice type.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Represent a collection of type [InvoiceSummary](#invoicesummary) that contain the individual details for an invoice type per currency.  

| Propriété            | Tapez                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | array of [InvoiceSummary](#invoicesummary) objects             | The summary of the invoice per invoice type per currency.                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

Represents an invoice billing line item for licensed based subscriptions.

| Propriété                 | Tapez                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| amount                   | chaîne                                                         | Gets or sets the total amount. Total amount = unit price * quantity.  |
| attributs               | chaîne                                                         | Gets the attributes.                                                  |
| billingCycleType         | chaîne                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | chaîne                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | chaîne                                                         | Gets or sets the type of charge.                                      |
| currency                 | chaîne                                                         | Gets or sets the currency used for this line item.                    |
| customerId               | chaîne                                                         | Gets or sets the customer unique identifier in the Microsoft billing platform.  |
| customerName             | string in UTC date-time format                                 | Gets or sets the customer name.                                       |
| domainName               | chaîne                                                         | Gets or sets domain name.                                             |
| durableOfferId           | chaîne                                                         | Gets or sets the durable offer unique identifier.                     |
| invoiceLineItemType      | chaîne                                                         | Gets the type of invoice line item.                                   |
| mpnId                    | nombre                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN Id of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
| offerId                  | chaîne                                                         | Gets or sets the offer unique identifier.                             |
| offerName                | chaîne                                                         | Gets or sets the offer name.                                          |
| orderId                  | chaîne                                                         | Gets or sets the order unique identifier.                             |
| partnerId                | chaîne                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| quantity                 | nombre                                                         | Gets or sets the number of units associated with this line item.      |
| subscriptionDescription  | chaîne                                                         | Gets or sets the subscription description.                            |
| subscriptionEndDate      | string in UTC date-time format                                 | Gets or sets the date when subscription expires.                      |
| subscriptionId           | chaîne                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | chaîne                                                         | Gets or sets the subscription name.                                   |
| subscriptionStartDate    | string in UTC date-time format                                 | Gets or sets the date when the subscription starts.                   |
| subtotal                 | nombre                                                         | Gets or sets the amount after discount.                               |
| syndicationPartnerSubscriptionNumber | chaîne                                             | Gets or sets the syndication partner subscription number.             |
| tax                      | nombre                                                         | Gets or sets the taxes charged.                                       |
| tier2MpnId               | nombre                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| totalForCustomer         | nombre                                                         | Gets or sets the total amount after discount and tax.                 |
| totalOtherDiscount       | nombre                                                         | Gets or sets the discount associated with this purchase.              |
| unitPrice                | nombre                                                         | Gets or sets the unit price.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Represents an invoice billing line item for usage based subscriptions.

| Propriété                 | Tapez                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| attributs               | chaîne                                                         | Gets the attributes.                                                  |
| billingCycleType         | chaîne                                                         | Gets or sets the billing cycle type.                                  |
| billingProvider          | chaîne                                                         | Gets the billing provider.                                            |
| chargeEndDate            | string in UTC date-time format                                 | Gets or sets the end date for the charge.                             |
| chargeStartDate          | string in UTC date-time format                                 | Gets or sets the start date for the charge.                           |
| chargeType               | chaîne                                                         | Gets or sets the type of charge.                                      |
| consumedQuantity         | nombre                                                         | Gets or sets the total units consumed.                                |
| consumptionDiscount      | chaîne                                                         | Gets or sets the discount on consumption.                             |
| consumptionPrice         | chaîne                                                         | Gets or sets the price of quantity consumed.                          |
| currency                 | chaîne                                                         | Gets or sets the currency associated with the prices.                 |
| customerName             | chaîne                                                         | Gets or sets the customer name.                                       |
| customerId               | chaîne                                                         | Gets or sets the customer unique identifier.                          |
| detailLineItemId         | nombre                                                         | Gets or sets the detail line item ID. Uniquely identifies the line items for cases where calculation is different for units consumed. Example: Total consumed = 1338, 1024 is charged with one rate, 314 is charge with a different rate.        |
| domainName               | chaîne                                                         | Gets or sets domain name.                                             |
| includedQuantity         | nombre                                                         | Gets or sets the units included in the order.                         |
| invoiceLineItemType      | chaîne                                                         | Gets the type of invoice line item.                                   |
| invoiceNumber            | chaîne                                                         | Gets or sets the invoice number.                                      |
| listPrice                | nombre                                                         | Gets or sets the price of each unit.                                  |
| mpnId                    | nombre                                                         | Gets or sets the MPN ID associated to this line item. For direct resellers, this is the MPN ID of the reseller. For indirect resellers, this is the MPN ID of the Value Added Reseller (VAR).                                   |
| orderId                  | chaîne                                                         | Gets or sets the order unique identifier.                             |
| overageQuantity          | nombre                                                         | Gets or sets the quantity consumed above allowed usage.               |
| partnerBillableAccountId | chaîne                                                         | Gets or sets the partner billable account ID.                         |
| partnerId                | chaîne                                                         | Gets or sets the partner Azure active directory tenant ID.            |
| partnerName              | chaîne                                                         | Gets or sets the partner's name.                                      |
| postTaxEffectiveRate     | nombre                                                         | Gets or sets the effective price after taxes.                         |
| postTaxTotal             | nombre                                                         | Gets or sets the total charges after tax. Pretax Charges + Tax Amount |
| preTaxCharges            | nombre                                                         | Gets or sets the price charged before taxes.                          |
| preTaxEffectiveRate      | nombre                                                         | Gets or sets the effective price before taxes.                        |
| region                   | chaîne                                                         | Gets or sets the region associated with the resource instance.        |
| resourceGuid             | chaîne                                                         | Gets or sets the resource identifier.                                 |
| resourceName             | chaîne                                                         | Gets or sets the resource name. Example: Database (GB/month).         |
| serviceName              | chaîne                                                         | Gets or sets the service name. Example: Azure Data Service.           |
| serviceType              | chaîne                                                         | Gets or sets the service type. Example: Azure SQL Azure DB.           |
| sku                      | chaîne                                                         | Gets or sets the service SKU.                                         |
| subscriptionDescription  | chaîne                                                         | Gets or sets the subscription description.                            |
| subscriptionId           | chaîne                                                         | Gets or sets the subscription unique identifier.                      |
| subscriptionName         | chaîne                                                         | Gets or sets the subscription name.                                   |
| taxAmount                | nombre                                                         | Gets or sets the amount of tax charged.                               |
| tier2MpnId               | nombre                                                         | Gets or sets the MPN ID of the Tier 2 partner associated to this line item. |
| unités                     | chaîne                                                         | Gets or sets the unit of measure for Azure usage.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Represents the operations available on an invoice statement in application/pdf.

| Propriété                 | Tapez                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ByteArrayContent with contentType = application/pdf.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Represents an invoice billing line item for licensed-based subscriptions.

| Propriété | Tapez | Description |
| --- | --- | --- |
| PartnerId | chaîne | Gets or sets the partner tenant ID. |
| CustomerId | chaîne | Gets or sets the customer tenant ID. |
| CustomerName | chaîne | Gets or sets the customer name. |
| CustomerDomainName | chaîne | Gets or sets the customer domain name. |
| CustomerCountry | chaîne | Gets or sets the customer country. |
| InvoiceNumber | chaîne | Gets or sets the invoice number. |
| MpnId | chaîne | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | entier | Gets or sets the order unique identifier. |
| OrderDate | DateTime | Gets or sets the date when order created. |
| ProductId | chaîne | Gets or sets the product unique identifier. |
| SkuId | chaîne | Gets or sets the SKU unique identifier. |
| AvailabilityId | chaîne | Gets or sets the availability unique identifier. |
| ProductName | chaîne | Gets or sets the product name. |
| SkuName | chaîne | Gets or sets the SKU name. |
| ChargeType | chaîne | Gets or sets the type of charge. |
| UnitPrice | décimal | Gets or sets the unit price. |
| EffectiveUnitPrice | décimal | Gets or sets the effective unit price. |
| UnitType | chaîne | Gets or sets the unit type. |
| Quantité | entier | Gets or sets the number of units associated with this line item. |
| Sous-total | décimal | Gets or sets the amount after discount. |
| TaxTotal | décimal | Gets or sets the taxes charged. |
| TotalForCustomer | décimal | Gets or sets the total amount after discount and tax. |
| Symbole monétaire | chaîne | Gets or sets the currency used for this line item. |
| PublisherName | chaîne | Gets or sets the publisher name associated with this purchase. |
| PublisherId | chaîne | Gets or sets the publisher ID associated with this purchase. |
| SubscriptionDescription | chaîne | Gets or sets the subscription description associated with this purchase. |
| SubscriptionId | chaîne | Gets or sets the subscription ID associated with this purchase. |
| ChargeStartDate | DateTime | Gets or sets the charge start date associated with this purchase. |
| ChargeEndDate | DateTime | Gets or sets the charge end date associated with this purchase. |
| TermAndBillingCycle | chaîne | Gets or sets the term and billing cycle associated with this purchase. |
| AlternateId | chaîne | Gets or sets the Alternate ID (quote ID). |
| PriceAdjustmentDescription | chaîne | Gets or sets the price adjustment description. |
| DiscountDetails | chaîne |  **Deprecated**. Gets or sets the discount details associated with this purchase. |
| PricingCurrency | chaîne | Gets or sets the pricing currency code. |
| PCToBCExchangeRate | décimal | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the exchange rate date at which the pricing currency to the billing currency exchange rate was determined. |
| BillableQuantity | décimal | Gets or sets the units purchased. For each design column named as **BillableQuantity**. |
| MeterDescription | chaîne | Gets or sets the meter description for consumption line item. |
| BillingFrequency | chaîne | Gets or sets the billing frequency. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Represents unbilled, billed reconciliation line items for daily rated usage.

| Propriété | Tapez | Description |
| --- | --- | --- |
| PartnerId | chaîne | Gets or sets the partner tenant ID. |
| PartnerName | chaîne | Gets or sets the partner name. |
| CustomerId | chaîne | Gets or sets the tenant ID of the customer that usage belongs to. |
| CustomerName | chaîne | Gets or sets the name of the customer company that usage belongs to. |
| CustomerDomainName | chaîne | Gets or sets the domain name of the customer that usage belongs to. |
| InvoiceNumber | chaîne | Gets or sets the ID of the invoice that usage belongs to. |
| ProductId | chaîne | Gets or sets the product unique identifier. |
| SkuId | chaîne | Gets or sets the SKU unique identifier. |
| AvailabilityId | chaîne | Gets or sets the availability unique identifier. |
| SkuName | chaîne | Gets or sets the SKU name for the service. |
| ProductName | chaîne | Gets or sets the name of the product. |
| PublisherName | chaîne | Gets or sets the name of publisher. |
| PublisherId | chaîne | Gets or sets the ID of the publisher. |
| SubscriptionId | chaîne | Gets or sets the subscription ID. |
| SubscriptionDescription | chaîne | Gets or sets the subscription description. |
| ChargeStartDate | DateTime | Gets or sets the charge start date. |
| ChargeEndDate | DateTime | Gets or sets the charge end date. |
| UsageDate | DateTime | Gets or sets the usage date. |
| MeterType | chaîne | Gets or sets the meter type. |
| MeterCategory | chaîne | Gets or sets the meter category. |
| MeterId | chaîne | Gets or sets the  meter ID (GUID). |
| MeterSubCategory | chaîne | Gets or sets the meter sub category. |
| MeterName | chaîne | Gets or sets the meter name. |
| MeterRegion | chaîne | Gets or sets the meter region. |
| UnitOfMeasure | chaîne | Gets or sets the unit of measure. |
| ResourceLocation | chaîne | Gets or sets the location of resource. |
| ConsumedService | chaîne | Gets or sets the consumed service name. |
| ResourceGroup | chaîne | Gets or sets the name of resource group. |
| ResourceUri | chaîne | Gets or sets the uri of the resource instance that the usage is about. |
| Balises | chaîne | Gets or sets the customer added tags. |
| AdditionalInfo | chaîne | Gets or sets the service-specific metadata. For example, an image type for a virtual machine. |
| ServiceInfo1 | chaîne | Gets or sets internal Azure Service Metadata. |
| ServiceInfo2 | chaîne | Gets or sets service information for example, an image type for a virtual machine and ISP name for ExpressRoute. |
| CustomerCountry | chaîne | Gets or sets the country of the customer. |
| MpnId | chaîne | Gets or sets the MPN ID associated to this line item. |
| ResellerMpnId | chaîne | Gets or sets the Reseller MPN ID of the Tier 2 partner associated to this line item. |
| ChargeType | chaîne | Gets or sets the type of charge. |
| UnitPrice | décimal | Gets or sets the price of unit. |
| Quantité | décimal | Gets or sets the quantity of usage. |
| UnitType | chaîne | Gets or sets the unit type (such as 1 hour). |
| BillingPreTaxTotal | décimal | Gets or sets the extended cost or total cost before tax in local currency of the customer or billing currency. |
| BillingCurrency | chaîne | Gets or sets ISO currency in which the meter is charged in local currency of the customer or billing currency. |
| PricingPreTaxTotal | décimal | Gets or sets the extended cost or total cost before tax in USD or catalog currency used for rating. |
| PricingCurrency | chaîne | Gets or sets ISO currency in which the meter is charged in USD or catalog currency used for rating. |
| EntitlementId | chaîne | Gets or sets the entitlement (Azure subscription) ID. |
| EntitlementDescription | chaîne | Gets or sets the entitlement (Azure subscription) description. |
| PCToBCExchangeRate | chaîne | Gets or sets the pricing currency to the billing currency exchange rate. |
| PCToBCExchangeRateDate | DateTime | Gets or sets the pricing currency to the billing currency exchange rate date. |
| EffectiveUnitPrice | décimal | Gets or sets the effective unit price. |
| RateOfPartnerEarnedCredit | décimal | Gets or sets the rate of partner earned credit. |
| hasPartnerEarnedCredit | bool | Gets or sets is partner earned credit applied. |
| InvoiceLineItemType | InvoiceLineItemType | Returns the type of invoice line item. |
| BillingProvider | BillingProvider | Returns the billing provider. |

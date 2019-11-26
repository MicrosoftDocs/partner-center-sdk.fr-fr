---
title: Customer resources
description: Customer resources that represent a customer or reseller.
ms.assetid: C7EC2657-62F2-43B3-B171-2F74498D45E0
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 09dd70431b34ad5c63820931113a71908b24acd0
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489699"
---
# <a name="customer-resources"></a>Customer resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

## <a name="customer"></a>Client

The **Customer** resource represents a customer or reseller. Most broadly, a customer resouce can be any person, employee, or organization that wishes to do business with Microsoft and Microsoft's resellers. Customers also have a company profile and a billing profile.

>[!NOTE]
>The **Customer** resource has a rate limit of 500 requests per minute per tenant identifier.

| Propriété              | Tapez                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| id                    | chaîne                                                           | The customer ID.                                                                                                                             |
| commerceId            | chaîne                                                           | The commerce ID.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Additional information about the company or organization.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Additional information used for billing.                                                                                                     |
| relationshipToPartner | chaîne                                                           | Defines the licensing program that the partner uses for this customer: "none", "reseller", "advisor", "syndication" or "microsoft\_support". |
| allowDelegatedAccess  | booléen                                                          | Whether the partner has been granted delegated admin privileges by this customer.                                                            |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | The user credentials.                                                                                                                        |
| customDomains         | array of strings                                                 | List of custom domains of a customer.                                                                                                        |
| associatedPartnerId   | chaîne                                                           | The indirect reseller associated to this customer account. This value can be set only by indirect CSP partners.                              |
| liens                 | [ResourceLinks](utility-resources.md#resourcelinks)             | The resource links contained within the profile.                                                                                             |
| attributs            | [ResourceAttributes](utility-resources.md#resourceattributes)   | The metadata attributes corresponding to the profile.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

The **CustomerCompanyProfile** resource is additional information about the company or organization.

| Propriété    | Tapez                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | chaîne                                                         | The customer's tenant identifier for Azure AD. This is also called a MicrosoftID. |
| domain      | chaîne                                                         | The customer's name, such as contoso.onmicrosoft.com.                             |
| companyName | chaîne                                                         | The name of the company or organization.                                          |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                  |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                             |

## <a name="customerbillingprofile"></a>CustomerBillingProfile

The **CustomerBillingProfile** resource is additional information used for billing the customer.

| Propriété       | Tapez                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| id             | chaîne                                                         | The profile identifier.                                                                                                                                |
| firstName      | chaîne                                                         | The first name of the billing contact at the customer's company. This is the person that invoices and other billing communication will be directed to. |
| lastName       | chaîne                                                         | The last name of the billing contact.                                                                                                                  |
| Messagerie          | chaîne                                                         | The billing contact's email address                                                                                                                    |
| culture        | chaîne                                                         | Their preferred culture for communication and currency, such as "en-us".                                                                               |
| language       | chaîne                                                         | Their preferred language for communication.                                                                                                            |
| companyName    | chaîne                                                         | The name of the company or organization.                                                                                                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The address that bills are sent to, where the billing contact works.                                                                                   |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links contained within the profile.                                                                                                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

The **CustomerRelationshipRequest** resource contains the URL used by the customer to establish a reseller relationship with a partner.

| Propriété   | Tapez                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | chaîne                                                         | The URL used by the customer to establish a relationship with a partner. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the relationship request.       |
---
title: Profile resources
description: Describes the behavior of a Cloud Solution Provider's profiles.
ms.assetid: 42F2959B-D70D-41A7-9A50-E22A2356A339
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3449aeb3695a9f286f37668d3f0862dc7b5cfa9f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486759"
---
# <a name="profile-resources"></a>Profile resources


**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Describes the behavior of a Cloud Solution Provider's profiles.

## <a name="span-idbillingprofilespan-idbillingprofilespan-idbillingprofilebillingprofile"></a><span id="BillingProfile"/><span id="billingprofile"/><span id="BILLINGPROFILE"/>BillingProfile


Describes a partner's billing profile.

| Propriété            | Tapez                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| companyName         | chaîne                                                         | The billing company name.                                   |
| adresse             | [Address](utility-resources.md#address)                       | The billing address address of the company or organization. |
| primaryContact      | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.        |
| purchaseOrderNumber | chaîne                                                         | The company or organization's purchase order number.        |
| taxId               | chaîne                                                         | The company or organization's tax Id.                       |
| billingCurrency     | chaîne                                                         | The currency used by the company or organization.           |
| profileType         | chaîne                                                         | The partner profile type.                                   |
| liens               | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.            |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.       |

 

## <a name="span-idlegalbusinessprofilespan-idlegalbusinessprofilespan-idlegalbusinessprofilelegalbusinessprofile"></a><span id="LegalBusinessProfile"/><span id="legalbusinessprofile"/><span id="LEGALBUSINESSPROFILE"/>LegalBusinessProfile


Describes a partner's legal business profile.

| Propriété               | Tapez                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| companyName            | chaîne                                                         | The legal company name.                                                                                                                                              |
| adresse                | [Address](utility-resources.md#address)                       | The address of the company or organization.                                                                                                                          |
| primaryContact         | [Contact](utility-resources.md#contact)                       | The primary contact for the company or organization.                                                                                                                 |
| companyApproverAddress | [Address](utility-resources.md#address)                       | The company approver address.                                                                                                                                        |
| companyApproverEmail   | chaîne                                                         | The company approver email.                                                                                                                                          |
| vettingStatus          | chaîne                                                         | The vetting status. This value is the string representation of the one of the member names found in [**VettingStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus).           |
| vettingSubStatus       | chaîne                                                         | The vetting sub-status. This value is the string representation of the one of the member names found in [**VettingSubStatus**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus). |
| profileType            | chaîne                                                         | The partner profile type.                                                                                                                                            |
| liens                  | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                                                                                                                     |
| attributs             | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                                                                                                                |

 

## <a name="span-idmpnprofilespan-idmpnprofilespan-idmpnprofilempnprofile"></a><span id="MpnProfile"/><span id="mpnprofile"/><span id="MPNPROFILE"/>MpnProfile


Describes a partner's Microsoft Partner Network profile.

| Propriété    | Tapez                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | chaîne                                                         | The company or organization name.                     |
| mpnId       | chaîne                                                         | The Microsoft Partner Network Id.                     |
| profileType | chaîne                                                         | The partner profile type.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

## <a name="span-idorganizationprofilespan-idorganizationprofilespan-idorganizationprofileorganizationprofile"></a><span id="OrganizationProfile"/><span id="organizationprofile"/><span id="ORGANIZATIONPROFILE"/>OrganizationProfile


Describes a partner's organization profile.

| Propriété       | Tapez                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| id             | chaîne                                                         | The organization's Id.                                                 |
| companyName    | chaîne                                                         | The name of the company or organization.                               |
| defaultAddress | [Address](utility-resources.md#address)                       | The default address of the company or organization.                    |
| tenantId       | chaîne                                                         | The tenant identifier.                                                 |
| domain         | chaîne                                                         | The company or organization's domain.                                  |
| Messagerie          | chaîne                                                         | Gets or sets the parent subscription.                                  |
| language       | chaîne                                                         | The preferred language for communication.                              |
| culture        | chaîne                                                         | The preferred culture for communication and currency, such as "en-us". |
| profileType    | chaîne                                                         | The partner profile type.                                              |
| liens          | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.                       |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile.                  |

 

## <a name="span-idsupportprofilespan-idsupportprofilespan-idsupportprofilesupportprofile"></a><span id="SupportProfile"/><span id="supportprofile"/><span id="SUPPORTPROFILE"/>SupportProfile


Describes a partner's support profile.

| Propriété    | Tapez                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| Messagerie       | chaîne                                                         | The email address associated with the profile.        |
| téléphone   | chaîne                                                         | The phone number associated with the profile.         |
| site web     | chaîne                                                         | The support website.                                  |
| profileType | chaîne                                                         | The partner profile type.                             |
| liens       | [ResourceLinks](utility-resources.md#resourcelinks)           | The resource links corresponding to the profile.      |
| attributs  | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the profile. |

 

 

 





---
title: License resources
description: Describes resources related to licenses.
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 625209f834a7d89fbf288b7a1430624cb99485b1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486929"
---
# <a name="license-resources"></a>License resources


**Applies To**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Describes resources related to licenses.

## <a name="span-idlicensespan-idlicensespan-idlicenselicense"></a><span id="License"/><span id="license"/><span id="LICENSE"/>License


Describes a user license.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

 

| Propriété     | Tapez                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | array of ServicePlan resources                                 | The collection of service plans that correspond to the license |
| productSKU   | ProductSku                                                     | The sku of the product that corresponds to the license.        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the license.          |

 

## <a name="span-idlicenseupdatespan-idlicenseupdatespan-idlicenseupdatelicenseupdate"></a><span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


Provides information used to assign or remove licenses from a user.

| Propriété         | Tapez                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | array of objects                                               | Array of [LicenseAssignment](#licenseassignment) objects. |
| licensesToRemove | array of strings                                               | The product SKU identifiers of the licenses to remove.    |
| licenseWarnings  | array of objects                                               | Array of [LicenseWarning](#licensewarning) objects.       |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                  |

 

## <a name="span-idlicenseassignmentspan-idlicenseassignmentspan-idlicenseassignmentlicenseassignment"></a><span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


Provides information needed for a license update operation.

| Propriété      | Tapez             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | array of strings | The service plan identifiers to be excluded from availability to the user. |
| skuId         | chaîne           | The product SKU identifier for the license.                                |

 

## <a name="span-idlicensewarningspan-idlicensewarningspan-idlicensewarninglicensewarning"></a><span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


Contains warning information that occurred during a license update operation.

| Propriété     | Tapez             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | chaîne           | The warning code.                                   |
| message      | chaîne           | The warning message.                                |
| servicePlans | array of strings | The service plan names associated with the warning. |

 

## <a name="span-idproductskuspan-idproductskuspan-idproductskuproductsku"></a><span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


Describes product details.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Tapez</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>chaîne</td>
<td>The product identifier.</td>
</tr>
<tr class="even">
<td>name</td>
<td>chaîne</td>
<td>The user principal identifier.</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>chaîne</td>
<td>The SKU part number name for the product. For example, for Office 365 Plan E3 , this value is &quot;EnterprisePack&quot;. This can be used in place of id if the id is not available.</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>chaîne</td>
<td>The target type of the product. This identifies whether the product is applicable to a &quot;User&quot; or a &quot;Tenant&quot;.</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>chaîne</td>
<td>Identifies via a group identifier the authority or service that manages the productSku license. Products are segregated under license groups for better manageability.
<p>&quot;group1&quot; - All products whose licenses can be managed by Azure Active Directory (AAD).</p>
<p>&quot;group2&quot; - Minecraft product licenses.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idserviceplanspan-idserviceplanspan-idserviceplanserviceplan"></a><span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


Identifies a deployable service within a product SKU. A product can have many service plans.

| Propriété         | Tapez   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | chaîne | The service plan identifier.                                                                                      |
| displayName      | chaîne | The localized display name for the service plan.                                                                  |
| serviceName      | chaîne | The service name.                                                                                                 |
| capabilityStatus | chaîne | The service plan status of the service plan.                                                                      |
| targetType       | chaîne | The target type of the service plan. This identifies whether the product is applicable to a "User" or a "Tenant". |

 

## <a name="span-idsubscribedskuspan-idsubscribedskuspan-idsubscribedskusubscribedsku"></a><span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


Describes a subscribed product owned by a tenant.

| Propriété         | Tapez                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | Entier                                                        | The number of units available for assignment. This is calculated as total units - consumed units. |
| activeUnits      | Entier                                                        | The number of units active for assignment.                                                        |
| consumedUnits    | Entier                                                        | The number of units consumed.                                                                     |
| suspendedUnits   | Entier                                                        | The number of units suspended.                                                                    |
| totalUnits       | Entier                                                        | The total number of units. This is calculated as the sum of the active and warning units.         |
| warningUnits     | Entier                                                        | The number of warning units.                                                                      |
| productSku       | ProductSku                                                     | The product sku.                                                                                  |
| servicePlans     | array of ServicePlan resources                                 | The collection of service plans of a product.                                                     |
| capabilityStatus | chaîne                                                         | The sku status of a product.                                                                      |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes corresponding to the resource.                                            |

 

 

 





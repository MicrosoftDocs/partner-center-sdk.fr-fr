---
title: Ressources de licence
description: Décrit les ressources associées aux licences.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1c8cfd1b6edd5b15db72afd7241f2c3d8ad38879
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095105"
---
# <a name="license-resources"></a>Ressources de licence

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit les ressources associées aux licences.

## <a name="license"></a>Licence

Décrit une licence utilisateur.

>[!NOTE]
>Non pris en charge dans l’espace partenaires géré par 21Vianet.

| Propriété     | Type                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | Tableau de ressources ServicePlan                                 | Collection des plans de service qui correspondent à la licence |
| productSKU   | ProductSku                                                     | Référence SKU du produit qui correspond à la licence.        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la licence.          |

## <a name="licenseupdate"></a>LicenseUpdate

Fournit des informations utilisées pour affecter ou supprimer des licences d’un utilisateur.

| Propriété         | Type                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | tableau d’objets                                               | Tableau d’objets [LicenseAssignment](#licenseassignment) . |
| licensesToRemove | tableau de chaînes                                               | Identificateurs SKU du produit des licences à supprimer.    |
| licenseWarnings  | tableau d’objets                                               | Tableau d’objets [LicenseWarning](#licensewarning) .       |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                  |

## <a name="licenseassignment"></a>LicenseAssignment

Fournit les informations nécessaires pour une opération de mise à jour de licence.

| Propriété      | Type             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | tableau de chaînes | Identificateurs de plan de service à exclure de la disponibilité à l’utilisateur. |
| skuId         | string           | Identificateur SKU du produit pour la licence.                                |

## <a name="licensewarning"></a>LicenseWarning

Contient des informations d’avertissement qui se sont produites lors d’une opération de mise à jour de licence.

| Propriété     | Type             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | string           | Code d’avertissement.                                   |
| message      | string           | Message d'avertissement.                                |
| servicePlans | tableau de chaînes | Noms des plans de service associés à l’avertissement. |

## <a name="productsku"></a>ProductSku

Décrit les détails du produit.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propriété</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>id</td>
<td>string</td>
<td>Identificateur du produit.</td>
</tr>
<tr class="even">
<td>name</td>
<td>string</td>
<td>Identificateur du principal de l’utilisateur.</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>string</td>
<td>Nom du numéro de référence SKU du produit. Par exemple, pour Office 365 plan E3, cette valeur est <code>EnterprisePack</code> . Cette propriété peut être utilisée à la place de l’ID si l’ID n’est pas disponible.</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>string</td>
<td>Type de cible du produit. Cette propriété indique si le produit est applicable à un <code>User</code> ou un <code>Tenant</code> .</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>string</td>
<td>Identifie via un identificateur de groupe l’autorité ou le service qui gère la licence productSku. Les produits sont séparés sous des groupes de licences pour une meilleure gestion.
<p><code>group1</code>-Tous les produits dont les licences peuvent être gérées par Azure Active Directory (AAD).</p>
<p><code>group2</code>-Licences de produits Minecraft.</p></td>
</tr>
</tbody>
</table>

## <a name="serviceplan"></a>ServicePlan

Identifie un service déployable au sein d’une référence SKU de produit. Un produit peut avoir de nombreux plans de service.

| Propriété         | Type   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | string | Identificateur du plan de service.                                                                                      |
| displayName      | string | Nom complet localisé pour le plan de service.                                                                  |
| serviceName      | string | Nom du service.                                                                                                 |
| capabilityStatus | string | État du plan de service du plan de service.                                                                      |
| targetType       | string | Type de cible du plan de service. Cette propriété indique si le produit est applicable à un « utilisateur » ou à un « locataire ». |

## <a name="subscribedsku"></a>SubscribedSku

Décrit un produit abonné appartenant à un locataire.

| Propriété         | Type                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | entier                                                        | Nombre d’unités disponibles pour l’assignation. Cette valeur est calculée sous la forme d’unités consommées total unités. |
| activeUnits      | entier                                                        | Nombre d’unités actives pour l’affectation.                                                        |
| consumedUnits    | entier                                                        | Nombre d’unités consommées.                                                                     |
| suspendedUnits   | entier                                                        | Nombre d’unités suspendues.                                                                    |
| totalUnits       | entier                                                        | Nombre total d’unités. Cette valeur est calculée comme la somme des unités actives et d’avertissement.         |
| warningUnits     | entier                                                        | nombre d'unités d'avertissement.                                                                      |
| productSku       | ProductSku                                                     | Référence SKU du produit.                                                                                  |
| servicePlans     | Tableau de ressources ServicePlan                                 | Collection de plans de service d’un produit.                                                     |
| capabilityStatus | string                                                         | État des références (SKU) d’un produit.                                                                      |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la ressource.                                            |

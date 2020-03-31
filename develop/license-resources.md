---
title: Ressources de licence
description: Décrit les ressources associées aux licences.
ms.assetid: 20592E06-8A87-41F4-B8B0-6F9200556FDA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b582f3d0ea32a7d0977cb983798e3ff8debf52e5
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416522"
---
# <a name="license-resources"></a>Ressources de licence


**S’applique à**

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit les ressources associées aux licences.

## <a name="span-idlicensespan-idlicensespan-idlicenselicense"></a><span id="License"/><span id="license"/><span id="LICENSE"/>licence


Décrit une licence utilisateur.

>[!NOTE]
>Non pris en charge dans l’espace partenaires géré par 21Vianet.

 

| Propriété     | Type                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| servicePlans | Tableau de ressources ServicePlan                                 | Collection des plans de service qui correspondent à la licence |
| productSKU   | productSku                                                     | Référence SKU du produit qui correspond à la licence.        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la licence.          |

 

## <a name="span-idlicenseupdatespan-idlicenseupdatespan-idlicenseupdatelicenseupdate"></a><span id="LicenseUpdate"/><span id="licenseupdate"/><span id="LICENSEUPDATE"/>LicenseUpdate


Fournit des informations utilisées pour affecter ou supprimer des licences d’un utilisateur.

| Propriété         | Type                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | Tableau d’objets                                               | Tableau d’objets [LicenseAssignment](#licenseassignment) . |
| licensesToRemove | tableau de chaînes                                               | Identificateurs SKU du produit des licences à supprimer.    |
| licenseWarnings  | Tableau d’objets                                               | Tableau d’objets [LicenseWarning](#licensewarning) .       |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                  |

 

## <a name="span-idlicenseassignmentspan-idlicenseassignmentspan-idlicenseassignmentlicenseassignment"></a><span id="LicenseAssignment"/><span id="licenseassignment"/><span id="LICENSEASSIGNMENT"/>LicenseAssignment


Fournit les informations nécessaires pour une opération de mise à jour de licence.

| Propriété      | Type             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| excludedPlans | tableau de chaînes | Identificateurs de plan de service à exclure de la disponibilité à l’utilisateur. |
| skuId         | chaîne           | Identificateur SKU du produit pour la licence.                                |

 

## <a name="span-idlicensewarningspan-idlicensewarningspan-idlicensewarninglicensewarning"></a><span id="LicenseWarning"/><span id="licensewarning"/><span id="LICENSEWARNING"/>LicenseWarning


Contient des informations d’avertissement qui se sont produites lors d’une opération de mise à jour de licence.

| Propriété     | Type             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| code         | chaîne           | Code d’avertissement.                                   |
| message      | chaîne           | Message d’avertissement.                                |
| servicePlans | tableau de chaînes | Noms des plans de service associés à l’avertissement. |

 

## <a name="span-idproductskuspan-idproductskuspan-idproductskuproductsku"></a><span id="ProductSku"/><span id="productsku"/><span id="PRODUCTSKU"/>ProductSku


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
<td>chaîne</td>
<td>L'identificateur du produit.</td>
</tr>
<tr class="even">
<td>nom</td>
<td>chaîne</td>
<td>Identificateur du principal de l’utilisateur.</td>
</tr>
<tr class="odd">
<td>skuPartNumber</td>
<td>chaîne</td>
<td>Nom du numéro de référence SKU du produit. Par exemple, pour Office 365 plan E3, cette valeur est &quot;&quot;EnterprisePack. Il peut être utilisé à la place de l’ID si l’ID n’est pas disponible.</td>
</tr>
<tr class="even">
<td>targetType</td>
<td>chaîne</td>
<td>Type de cible du produit. Cela indique si le produit est applicable à un &quot;utilisateur&quot; ou à un&quot;client &quot;.</td>
</tr>
<tr class="odd">
<td>licenseGroupId</td>
<td>chaîne</td>
<td>Identifie via un identificateur de groupe l’autorité ou le service qui gère la licence productSku. Les produits sont séparés sous des groupes de licences pour une meilleure gestion.
<p>&quot;Group1&quot;-tous les produits dont les licences peuvent être gérées par Azure Active Directory (AAD).</p>
<p>&quot;les licences Minecraft&quot;-produit.</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idserviceplanspan-idserviceplanspan-idserviceplanserviceplan"></a><span id="ServicePlan"/><span id="serviceplan"/><span id="SERVICEPLAN"/>ServicePlan


Identifie un service déployable au sein d’une référence SKU de produit. Un produit peut avoir de nombreux plans de service.

| Propriété         | Type   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| id               | chaîne | Identificateur du plan de service.                                                                                      |
| displayName      | chaîne | Nom complet localisé pour le plan de service.                                                                  |
| FormName      | chaîne | Nom du service.                                                                                                 |
| capabilityStatus | chaîne | État du plan de service du plan de service.                                                                      |
| targetType       | chaîne | Type de cible du plan de service. Cela indique si le produit est applicable à un « utilisateur » ou à un « locataire ». |

 

## <a name="span-idsubscribedskuspan-idsubscribedskuspan-idsubscribedskusubscribedsku"></a><span id="SubscribedSku"/><span id="subscribedsku"/><span id="SUBSCRIBEDSKU"/>SubscribedSku


Décrit un produit abonné appartenant à un locataire.

| Propriété         | Type                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | integer                                                        | Nombre d’unités disponibles pour l’assignation. Il est calculé comme nombre total d’unités consommées. |
| activeUnits      | integer                                                        | Nombre d’unités actives pour l’affectation.                                                        |
| consumedUnits    | integer                                                        | Nombre d’unités consommées.                                                                     |
| suspendedUnits   | integer                                                        | Nombre d’unités suspendues.                                                                    |
| totalUnits       | integer                                                        | Nombre total d’unités. Il s’agit de la somme des unités actives et d’avertissement.         |
| warningUnits     | integer                                                        | nombre d'unités d'avertissement.                                                                      |
| productSku       | productSku                                                     | Référence SKU du produit.                                                                                  |
| servicePlans     | Tableau de ressources ServicePlan                                 | Collection de plans de service d’un produit.                                                     |
| capabilityStatus | chaîne                                                         | État des références (SKU) d’un produit.                                                                      |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées correspondant à la ressource.                                            |

 

 

 





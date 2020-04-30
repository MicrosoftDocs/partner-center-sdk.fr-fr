---
title: Ressources de mise à niveau du produit
description: Vous pouvez utiliser plusieurs ressources liées aux mises à niveau du produit de l’espace partenaires vers un plan Azure. Cela inclut ProductUpgradeRequest, ProductUpgradesEligibility, ProductUpgradesStatus, UpgradesLineItem, UpgradeProduct et ErrorDetails.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3da809a303580e79e03a7f0e0720901d1bf911d7
ms.sourcegitcommit: 42b4d44796df44c18460145acb5a63566d9153c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82089289"
---
# <a name="product-upgrade-resources"></a>Ressources de mise à niveau du produit

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser les ressources suivantes pour obtenir des informations sur les mises à niveau des produits de l’espace partenaires à partir d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

La ressource **ProductUpgradesRequest** fournit des informations sur l’objet de demande de mise à niveau du produit.

| Propriété | Type | Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| customerId           | string                                       | Chaîne au format GUID qui identifie le client. |
| productFamily        | string                                       | Famille de produits pour laquelle la mise à niveau est demandée. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

La ressource **ProductUpgradesEligibility** fournit des informations sur l’éligibilité du client pour la mise à niveau d’un produit.

| Propriété | Type | Description |
|----------------------|--------------------------------------------- |----------------------------------------------------------------|
| customerId           | string                                       | Chaîne au format GUID qui identifie le client. |          | productFamily        | string                                       | Famille de produits pour laquelle la mise à niveau est demandée. |
| isEligible           | bool                                         | La valeur bool indique si le client est éligible à la mise à niveau demandée. |
| upgradeId            | string                                       | L’ID de mise à niveau si une mise à niveau de produit pour une famille donnée est déjà en place. |
| reason               | string                                       | Raison pour laquelle le client n’est pas éligible à la mise à niveau du produit. |
| productFamily        | string                                       | Famille de produits pour laquelle la mise à niveau est demandée. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

La ressource **ProductUpgradesStatus** fournit des informations sur l’état d’une mise à niveau de produit.

| Propriété | Type | Description |
|---------------------|----------------------------------------------------------------|-----------------------------------------------|
| Id                  | string                                                         | Chaîne au format GUID qui identifie la mise à niveau. |
| productFamily       | string                                                         | Famille de produits pour laquelle la mise à niveau est demandée.
| status              | string                                                         | État de la mise à niveau du produit.
| lineItems           | Tableau de ressources [UpgradesLineItem](#upgradeslineitem)       | Tableau d’objets qui fournit des informations sur les détails de la mise à niveau pour chaque élément de ligne qui faisait partie du corps de la demande.
| errorDetails        | Ressource [ErrorDetails](#errordetails)                         | Détails de l’erreur pour la mise à niveau demandée.
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

La ressource **UpgradesLineItem** décrit l’état des détails de la mise à niveau du produit pour chaque élément de ligne de la demande.

| Propriété | Type | Description |
|-----------------|-----------------------------------------------------|--------------------------------------------------------------|
| sourceProduct   | Objet [UpgradeProduct](#upgradeproduct)            | Informations du produit source en cours de mise à niveau. |
| targetProduct   | Objet [UpgradeProduct](#upgradeproduct)            | Informations du produit cible après la mise à niveau. |
| upgradedDate    | chaîne au format date-heure UTC                      | Date à laquelle l’abonnement a été mis à niveau. |
| status          | string                                              | État de la mise à niveau du produit. |
| errorDetails    | Ressource [ErrorDetails](#errordetails)              | Détails de l’erreur pour la mise à niveau demandée. |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.  |

## <a name="upgradeproduct"></a>UpgradeProduct

La ressource **UpgradeProduct** fournit des informations sur le produit en cours de mise à niveau.

| Propriété | Type |Description |
|----------------------|----------------------------------------------|----------------------------------------------------------------|
| id                   | string                                       | Chaîne au format GUID qui identifie le produit. |
| name                 | string                                       | Nom convivial du produit en cours de mise à niveau. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |

## <a name="errordetails"></a>ErrorDetails

La ressource **ErrorDetails** fournit des détails sur les erreurs pendant le processus de mise à niveau.

| Propriété | Type | Description |
|-------------------------|----------------------------------------------|-------------------------------------------------------------|
| code                    | string                                       | Code d’erreur en cas d’échec de la mise à niveau du produit. |
| message                 | string                                       | Message d’erreur lors de l’échec de la mise à niveau du produit. |
| attributs              | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |

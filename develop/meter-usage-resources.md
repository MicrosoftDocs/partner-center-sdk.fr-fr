---
title: Ressource enregistrement de l’utilisation du compteur
description: Vous pouvez utiliser la ressource MeterUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 48ed74f0440a7743415368fd565e43b6f06b1771
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416459"
---
# <a name="meter-usage-record-resource"></a>Ressource enregistrement de l’utilisation du compteur

S'applique à :

- Centre pour partenaires

Vous pouvez utiliser la ressource **MeterUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | chaîne             | GUID correspondant à l’identificateur d’une [ressource d’abonnement](subscription-resources.md#subscription)de l’espace partenaires, qui représente un abonnement Microsoft Azure (MS-AZR-0145P) ou un plan Azure. Pour les abonnements Microsoft Azure (MS-AZR-0145P),, cette valeur est l’identificateur d’abonnement au commerce. Pour les ressources d’abonnement du plan Azure, cette valeur correspond à l’identificateur du plan Azure.                  |
| MeterId  | chaîne             | Obtient ou définit l’identificateur du compteur.                                                        |
| MeterName          | chaîne             | Obtient ou définit le nom du compteur.                                       |
| Catégorie               | chaîne             | Obtient ou définit la catégorie de ressources Azure.                                                 |
| Subcategory             | chaîne             |  Obtient ou définit la sous-catégorie de ressources Azure.                                                     |
| QuantityUsed        | decimal             | Obtient ou définit la quantité de la ressource Azure utilisée.   |
| Unit   | chaîne             | Obtient ou définit l’unité de mesure de la ressource Azure. |
| TotalCost   | decimal             | Obtient ou définit le coût total d’utilisation estimé. |
| CurrencyLocale   | chaîne             | Paramètres régionaux dans lesquels l’abonnement a été utilisé. Cette propriété détermine la devise utilisée sur la facture. Cette propriété est disponible pour les abonnements Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | chaîne             | Obtient ou définit le code de la devise. Cette propriété est disponible pour les plans Azure.                                         |
| USDTotalCost   | decimal             | Obtient ou définit le coût total estimé en USD. Cette propriété est disponible pour les plans Azure.                                         |
| LastModifiedDate & | chaîne             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

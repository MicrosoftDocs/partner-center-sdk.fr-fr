---
title: Ressource enregistrement de l’utilisation du compteur
description: Vous pouvez utiliser la ressource MeterUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094774"
---
# <a name="meter-usage-record-resource"></a>Ressource enregistrement de l’utilisation du compteur

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser la ressource **MeterUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | GUID correspondant à l’identificateur d’une [ressource d’abonnement](subscription-resources.md#subscription)de l’espace partenaires, qui représente un abonnement Microsoft Azure (MS-AZR-0145P) ou un plan Azure. Pour les abonnements Microsoft Azure (MS-AZR-0145P),, cette valeur est l’identificateur d’abonnement au commerce. Pour les ressources d’abonnement du plan Azure, cette valeur correspond à l’identificateur du plan Azure.                  |
| MeterId  | string             | Obtient ou définit l’identificateur du compteur.                                                        |
| MeterName          | string             | Obtient ou définit le nom du compteur.                                       |
| Category               | string             | Obtient ou définit la catégorie de ressources Azure.                                                 |
| Sous-catégorie             | string             |  Obtient ou définit la sous-catégorie de ressources Azure.                                                     |
| QuantityUsed        | Décimal             | Obtient ou définit la quantité de la ressource Azure utilisée.   |
| Unité   | string             | Obtient ou définit l’unité de mesure de la ressource Azure. |
| TotalCost   | Décimal             | Obtient ou définit le coût total d’utilisation estimé. |
| CurrencyLocale   | string             | Paramètres régionaux dans lesquels l’abonnement a été utilisé. Cette propriété détermine la devise utilisée sur la facture. Cette propriété est disponible pour les abonnements Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | string             | Obtient ou définit le code de la devise. Cette propriété est disponible pour les plans Azure.                                         |
| USDTotalCost   | Décimal             | Obtient ou définit le coût total estimé en USD. Cette propriété est disponible pour les plans Azure.                                         |
| LastModifiedDate & | string             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

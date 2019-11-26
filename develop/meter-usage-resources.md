---
title: Ressource enregistrement de l’utilisation du compteur
description: Vous pouvez utiliser la ressource MeterUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 003db39c92e96b12863edebb46b3e3341ffae10e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488309"
---
# <a name="meter-usage-record-resource"></a>Ressource enregistrement de l’utilisation du compteur

S’applique à :

- Espace partenaires

Vous pouvez utiliser la ressource **MeterUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de mesure d’un abonnement dans le cycle de facturation actuel.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | chaîne             | GUID correspondant à l’identificateur d’une [ressource d’abonnement](subscription-resources.md#subscription)de l’espace partenaires, qui représente un abonnement Microsoft Azure (MS-AZR-0145P) ou un plan Azure. Pour les abonnements Microsoft Azure (MS-AZR-0145P),, cette valeur est l’identificateur d’abonnement au commerce. Pour les ressources d’abonnement du plan Azure, cette valeur correspond à l’identificateur du plan Azure.                  |
| MeterId  | chaîne             | Obtient ou définit l’identificateur du compteur.                                                        |
| MeterName          | chaîne             | Obtient ou définit le nom du compteur.                                       |
| Catégorie               | chaîne             | Obtient ou définit la catégorie de ressources Azure.                                                 |
| Sous-catégorie             | chaîne             |  Obtient ou définit la sous-catégorie de ressources Azure.                                                     |
| QuantityUsed        | décimal             | Obtient ou définit la quantité de la ressource Azure utilisée.   |
| Unit   | chaîne             | Obtient ou définit l’unité de mesure de la ressource Azure. |
| PrixTotal   | décimal             | Obtient ou définit le coût total d’utilisation estimé. |
| CurrencyLocale   | chaîne             | Paramètres régionaux dans lesquels l’abonnement a été utilisé. Cette propriété détermine la devise utilisée sur la facture. Cette propriété est disponible pour les abonnements Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | chaîne             | Obtient ou définit le code de la devise. Cette propriété est disponible pour les plans Azure.                                         |
| USDTotalCost   | décimal             | Obtient ou définit le coût total estimé en USD. Cette propriété est disponible pour les plans Azure.                                         |
| LastModifiedDate & | chaîne             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

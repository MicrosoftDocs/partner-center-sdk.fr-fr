---
title: Ressources de l’enregistrement d’utilisation des ressources
description: Vous pouvez utiliser la ressource ResourceUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5a194a9ee2a7d9f4bffc2daf37a627e6b65a50e8
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415410"
---
# <a name="resource-usage-record-resources"></a>Ressources de l’enregistrement d’utilisation des ressources

S'applique à :

- Centre pour partenaires

Vous pouvez utiliser la ressource **ResourceUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | chaîne             | Obtient ou définit l’identificateur d’abonnement. Pour les abonnements Microsoft Azure (MS-AZR-0145P), cette valeur est l’identificateur d’abonnement au commerce. Pour les plans Azure, cette valeur est l’identificateur du plan Azure.                  |
| URI  | chaîne             | Obtient ou définit l’URI de la ressource.»                                                        |
| ResourceType          | chaîne             | Obtient ou définit le type de ressource.                                       |
| EntitlementId               | chaîne             | Obtient ou définit l’identificateur d’habilitation (identificateur d’abonnement Azure).                                                 |
| EntitlementName             | chaîne             | Obtient ou définit le nom du droit.                                                     |
| ResourceGroupName        | double             | Obtient ou définit le nom du groupe de ressources.   |
| Nom   | chaîne             | Nom de la ressource. |
| Nom_ressource   | chaîne             | Obtient ou définit le nom de la ressource. |
| TotalCost   | decimal             | Obtient ou définit l’estimation de l’utilisation du coût total. |
| CurrencyCode   | chaîne             | Obtient ou définit le code de la devise.                                          |
| USDTotalCost   | decimal             | Obtient ou définit le coût total estimé en USD.                                         |
| LastModifiedDate & | chaîne             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

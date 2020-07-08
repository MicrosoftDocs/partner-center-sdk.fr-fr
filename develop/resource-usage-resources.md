---
title: Ressources de l’enregistrement d’utilisation des ressources
description: Vous pouvez utiliser la ressource ResourceUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a293818cf4a6545dc705bf30fae6753f2e7eaf1
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096687"
---
# <a name="resource-usage-record-resources"></a>Ressources de l’enregistrement d’utilisation des ressources

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser la ressource **ResourceUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Obtient ou définit l’identificateur d’abonnement. Pour les abonnements Microsoft Azure (MS-AZR-0145P), cette valeur est l’identificateur d’abonnement au commerce. Pour les plans Azure, cette valeur est l’identificateur du plan Azure.                  |
| URI  | string             | Obtient ou définit l’URI de la ressource.»                                                        |
| ResourceType          | string             | Obtient ou définit le type de ressource.                                       |
| EntitlementId               | string             | Obtient ou définit l’identificateur d’habilitation (identificateur d’abonnement Azure).                                                 |
| EntitlementName             | string             | Obtient ou définit le nom du droit.                                                     |
| ResourceGroupName        | double             | Obtient ou définit le nom du groupe de ressources.   |
| Nom   | string             | Nom de la ressource. |
| Nom_ressource   | string             | Obtient ou définit le nom de la ressource. |
| TotalCost   | Décimal             | Obtient ou définit l’estimation de l’utilisation du coût total. |
| CurrencyCode   | string             | Obtient ou définit le code de la devise.                                          |
| USDTotalCost   | Décimal             | Obtient ou définit le coût total estimé en USD.                                         |
| LastModifiedDate & | string             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

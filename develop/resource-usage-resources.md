---
title: Ressources de l’enregistrement d’utilisation des ressources
description: Vous pouvez utiliser la ressource ResourceUsageRecord pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2ec59df657a5b49209da9e801dcfcae4a3282d56
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488089"
---
# <a name="resource-usage-record-resources"></a>Ressources de l’enregistrement d’utilisation des ressources

S’applique à :

- Espace partenaires

Vous pouvez utiliser la ressource **ResourceUsageRecord** pour décrire le coût monétaire estimé de l’utilisation du niveau de ressource d’un abonnement dans le cycle de facturation actuel.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | chaîne             | Obtient ou définit l’identificateur d’abonnement. Pour les abonnements Microsoft Azure (MS-AZR-0145P), cette valeur est l’identificateur d’abonnement au commerce. Pour les plans Azure, cette valeur est l’identificateur du plan Azure.                  |
| URI  | chaîne             | Obtient ou définit l’URI de la ressource.»                                                        |
| ResourceType          | chaîne             | Obtient ou définit le type de ressource.                                       |
| entitlementId               | chaîne             | Obtient ou définit l’identificateur d’habilitation (identificateur d’abonnement Azure).                                                 |
| EntitlementName             | chaîne             | Obtient ou définit le nom du droit.                                                     |
| ResourceGroupName        | Double             | Obtient ou définit le nom du groupe de ressources.   |
| Nom   | chaîne             | Nom de la ressource. |
| Nom_ressource   | chaîne             | Obtient ou définit le nom de la ressource. |
| PrixTotal   | décimal             | Obtient ou définit l’estimation de l’utilisation du coût total. |
| CurrencyCode   | chaîne             | Obtient ou définit le code de la devise.                                          |
| USDTotalCost   | décimal             | Obtient ou définit le coût total estimé en USD.                                         |
| LastModifiedDate & | chaîne             | Jour (dans le format date-heure) de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |                                           |

---
title: Dépenses Azure
description: Les partenaires CSP peuvent utiliser les API de l’espace partenaires pour afficher et gérer leurs dépenses Azure. Ils peuvent également consulter par programmation les dépenses Azure de leurs clients par rapport à leur budget.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d4db9a7c8c52b33618652aa5bfaf1fb00d24c49b
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489119"
---
# <a name="azure-spending"></a>Dépenses Azure

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les partenaires fournisseurs de solutions Cloud (CSP) peuvent afficher et gérer leurs dépenses Azure via les API de l’espace partenaires. Ils peuvent également consulter par programmation les dépenses de leurs clients par rapport à un budget de dépenses Azure.

Pour plus d’informations, consultez [scénarios dans lesquels les partenaires CSP peuvent utiliser les API de l’espace partenaires pour gérer les comptes et les commandes des clients et des partenaires](scenarios.md), en particulier la [section d’arrière-plan](scenarios.md#background).

## <a name="partner-usage-management"></a>Gestion de l’utilisation des partenaires

- [Obtenir un résumé de l’utilisation des partenaires](get-a-partner-usage-summary.md) à l’aide de la ressource **PartnerUsageSummary**
- [Obtenir des enregistrements d’utilisation pour tous les clients](get-a-customer-s-usage-records.md) à l’aide de la ressource **CustomerMonthlyUsageRecord**

## <a name="customer-usage-management"></a>Gestion de l’utilisation des clients

- [Obtenir le résumé de l’utilisation d’un client](get-a-customer-usage-summary.md) à l’aide de la ressource **CustomerUsageSummary**
- [Obtenir tous les enregistrements d’utilisation d’abonnement pour un client](get-a-customer-subscription-s-usage-records.md) à l’aide de la ressource **SubscriptionMonthlyUsageRecord**

## <a name="subscription-usage-management"></a>Gestion de l’utilisation des abonnements

- [Obtenir un résumé de l’utilisation de l’abonnement](get-a-customer-subscription-usage-summary.md) à l’aide de la ressource **SubscriptionUsageSummary**
- [Obtenir tous les enregistrements d’utilisation mensuelle pour un abonnement](get-all-monthly-usage-records-for-a-subscription.md) à l’aide de la ressource **AzureResourceMonthlyUsageRecord**
- [Obtenir les données d’utilisation d’un abonnement par ressource](get-a-customer-subscription-resource-usage-records.md) à l’aide de la ressource **ResourceUsageRecord**
- [Obtenir les données d’utilisation d’un abonnement par compteur](get-a-customer-subscription-meter-usage-records.md) à l’aide de la ressource **MeterUsageRecord**

## <a name="azure-spending-budget-management"></a>Gestion du budget pour les dépenses Azure

- [Obtenir le budget d’utilisation d’un client](get-a-customer-s-usage-spending-budget.md) à l’aide de la ressource **CustomerUsageSummary**
- [Mise à jour du budget d’utilisation d’un client](update-a-customer-s-usage-spending-budget.md) à l’aide de la ressource **CustomerUsageSummary**

---
title: Ressources d’utilisation du client
description: Ressources pour les clients ayant des abonnements basés sur l’utilisation et des budgets d’utilisation mensuelle (notamment CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary et SpendingBudget).
ms.assetid: 268C7AF5-3A95-451F-8092-033A3E8126F2
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f94168e7f56e3e6c769c5a563e516046d7cc3509
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489819"
---
# <a name="customer-usage-resources"></a>Ressources d’utilisation du client

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les clients disposant d’abonnements basés sur l’utilisation peuvent avoir un budget d’utilisation mensuelle. Ce budget définit une limite sur l’utilisation maximale du client et permet au partenaire de suivre son utilisation au fil du temps.

> [!NOTE]
> Les numéros d’utilisation des clients sont des estimations (et non des valeurs finales) qui ne doivent pas être utilisées à des fins de facturation.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** représente le coût monétaire estimé de l’utilisation d’un client au cours du mois en cours.

| Propriété         | Type               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Évaluation           | SpendingBudget     | Budget de dépense alloué pour le client.                          |
| PercentUsed      | décimal             | Pourcentage utilisé à partir du budget alloué.                        |
| resourceId       | chaîne             | Identificateur unique de la ressource.                                   |
| Nom_ressource     | chaîne             | Nom de la ressource.                                                |
| PrixTotal        | décimal             | Estimation du coût total d’utilisation pour les ressources de l’abonnement.|
| CurrencyLocale   | chaîne             | Paramètres régionaux de devise du client. Disponible pour les abonnements Microsoft Azure (MS-AZR-0145P).            |
| CurrencyCode     | chaîne             | Obtient ou définit le code de la devise. Disponible pour les plans Azure.           |
| USDTotalCost     | décimal             | Obtient ou définit le coût total estimé en USD. Disponible pour les plans Azure.                                         |
| IsUpgraded       | bool             | Obtient ou définit une valeur indiquant si l’abonnement Azure du client est mis à niveau. La valeur **true** représente les clients qui ont un plan Azure.                         |
| LastModifiedDate & | date               | Date de la dernière modification des données d’utilisation.                               |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à l’enregistrement d’utilisation.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary** représente un résumé de l’utilisation du client pour une période de facturation entière.

| Propriété         | Type               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Évaluation           | SpendingBudget     | Budget de dépense alloué pour le client.                                                                  |
| resourceId       | chaîne             | Identificateur unique de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, cet ID est l’ID du client. |
| Nom_ressource     | chaîne             | Nom de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, il s’agit du nom du client.               |
| BillingStartDate | date               | Date de début de la période de facturation actuelle.                                                                    |
| BillingEndDate   | date               | Date de fin de la période de facturation actuelle.                                                                      |
| PrixTotal        | décimal             | Estimation du coût total d’utilisation pour les ressources de l’abonnement.                                         |
| CurrencyLocale   | chaîne             | Paramètres régionaux de devise du client. Disponible pour les abonnements Microsoft Azure (MS-AZR-0145P).                                         |
| CurrencyCode     | chaîne             | Obtient ou définit le code de la devise. Disponible pour les plans Azure.                                         |
| USDTotalCost     | décimal             | Obtient ou définit le coût total estimé en USD. Disponible pour les ressources d’abonnement du plan Azure.                                         |
| LastModifiedDate & | date               | Date de la dernière modification des données d’utilisation.                                                                       |
| Liens            | ResourceLinks      | Liens de ressource correspondant au résumé d’utilisation.                                                           |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant au résumé d’utilisation.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary** représente un récapitulatif au niveau du partenaire de l’utilisation de la budgétisation pour tous les clients.

| Propriété         | Type               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | Tableau de chaînes   | Liste des adresses de messagerie pour les notifications.                                                                   |
| CustomerOverBudget | Entier          | Nombre de clients qui dépassent le budget.                                                                    |
| CustomersTrendingOver | Entier       | Nombre de clients proches du budget.                                                     |
| CustomersWithUsageBasedSubscriptions  | Entier | Nombre de clients avec un abonnement basé sur l’utilisation.                                               |
| resourceId       | chaîne             | Identificateur unique de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, cet ID est l’ID du client. |
| Nom_ressource     | chaîne             | Nom de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, il s’agit du nom du client.               |
| BillingStartDate | date               | Date de début de la période de facturation actuelle.                                                                    |
| BillingEndDate   | date               | Date de fin de la période de facturation actuelle.                                                                      |
| PrixTotal        | décimal             | Estimation du coût total de l’utilisation du client en fonction de l’utilisation actuelle à partir du début de la période de facturation.      |
| CurrencyLocale   | chaîne             | Paramètres régionaux de devise.                                                                                             |
| LastModifiedDate & | date               | Date de la dernière modification des données d’utilisation.                                                                       |
| Liens            | ResourceLinks      | Liens de ressource correspondant au résumé d’utilisation.                                                           |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant au résumé d’utilisation.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

**SpendingBudget** représente le budget alloué à ce client pour les abonnements basés sur l’utilisation.

| Propriété   | Type               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Montant     | décimal             | Budget alloué. Si la valeur est null, aucune dépense budgétaire n’est allouée à ce client. |
| Attributs | ResourceAttributes | Attributs de métadonnées correspondant au budget.                                                |

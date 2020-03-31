---
title: Ressources d’utilisation de l’abonnement
description: Les ressources d’utilisation d’abonnement décrivent les abonnements avec la facturation basée sur l’utilisation. Ces abonnements ont des enregistrements d’utilisation quotidiens et mensuels, ainsi qu’un résumé de l’utilisation pour chaque période de paiement.
ms.assetid: 61B98AB8-D802-4EC1-91FB-B7A2B95DE20C
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6dbd55edd489cd6672842c81fc392333266b481e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415094"
---
# <a name="subscription-usage-resources"></a>Ressources d’utilisation de l’abonnement

S'applique à :

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser les ressources d’utilisation d’abonnement suivantes pour obtenir des informations sur l’utilisation d’un abonnement spécifique avec une facturation basée sur l’utilisation. Ces abonnements ont des enregistrements d’utilisation quotidiens et mensuels, ainsi qu’un résumé de l’utilisation pour chaque période de paiement.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*La ressource **SubscriptionDailyUsageRecord** est obsolète et peut produire des résultats inexacts. Nous vous recommandons de mettre à jour vos applications pour utiliser les API décrites dans [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md) et [obtenir des prix pour Microsoft Azure à](get-prices-for-microsoft-azure.md) la place.*

La ressource **SubscriptionDailyUsageRecord** décrit l’utilisation d’un abonnement en une seule journée.

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | chaîne             | Jour, dans le format de date et d’heure, utilisé par l’abonnement.                                 |
| resourceId       | chaîne             | GUID. ID unique de la ressource.                                                          |
| Nom_ressource     | chaîne             | Nom de la ressource.                                                                     |
| TotalCost        | decimal             | Estimation du coût total de l’utilisation des ressources de l’abonnement le jour spécifié.     |
| CurrencyLocale   | chaîne             | Les paramètres régionaux dans lesquels l’abonnement a été utilisé déterminent la devise à utiliser sur la facture. |
| LastModifiedDate & | chaîne             | Jour, dans le format date-heure, de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

La ressource **SubscriptionMonthlyUsageRecord** décrit l’utilisation d’un abonnement en un seul mois.

| Propriété         | Type               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Statut           | chaîne             | État de l’abonnement : « None », « active », « Suspended » ou « Deleted ».                  |
| PartnerOnRecord  | chaîne             | « ID MPN du partenaire sur l’enregistrement ».                                                        |
| OfferId          | chaîne             | GUID. ID de l’offre associée à cet abonnement.                                       |
| ID               | chaîne             | GUID. ID de l’abonnement ou de la ressource.                                                 |
| Nom             | chaîne             | Nom de l’abonnement ou de la ressource.                                                     |
| TotalCost        | decimal             | Estimation du coût total de l’utilisation des ressources de l’abonnement dans le mois spécifié.   |
| CurrencyLocale   | chaîne             | Les paramètres régionaux dans lesquels l’abonnement a été utilisé déterminent la devise à utiliser sur la facture. Disponible pour les abonnements Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode     | chaîne             | Obtient ou définit le code de la devise. Disponible pour les ressources d’abonnement du plan Azure.                                         |
| USDTotalCost     | decimal             | Obtient ou définit le coût total estimé en USD. Disponible pour les plans Azure.                                         |
| LastModifiedDate & | chaîne             | Jour, dans le format date-heure, de la dernière modification de cet enregistrement.                             |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à la ressource.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

La ressource **SubscriptionUsageSummary** décrit le degré d’utilisation d’un abonnement spécifique dans la période de facturation actuelle.

| Propriété         | Type               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| resourceId       | chaîne             | GUID. ID de l’abonnement ou de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, cet ID est l’ID du client. |
| Nom_ressource     | chaîne             | Nom de l’abonnement ou de la ressource. Dans le contexte de CustomerMonthlyUsageRecord, ce nom est le nom du client. |
| BillingStartDate | date               | Date de début de la période de facturation actuelle, au format date-heure.                                                     |
| BillingEndDate   | date               | Date de fin de la période de facturation en cours, au format date-heure.                                                       |
| TotalCost        | double             | Estimation du coût total de l’utilisation des ressources dans l’abonnement pendant la période de facturation spécifiée.               |
| CurrencyLocale   | chaîne             | Les paramètres régionaux dans lesquels l’abonnement a été utilisé déterminent la devise à utiliser sur la facture. Disponible pour les abonnements Microsoft Azure (MS-AZR-0145P). |
| CurrencyCode   | chaîne             | Obtient ou définit le code de la devise. Disponible pour les plans Azure.                                         |
| USDTotalCost   | decimal             | Obtient ou définit le coût total estimé en USD. Disponible pour les ressources d’abonnement du plan Azure.                                         |
| LastModifiedDate & | chaîne             | Jour, dans le format date-heure, de la dernière modification de cet enregistrement.                                                      |
| Liens            | ResourceLinks      | Liens de ressource correspondant à SubscriptionUsageSummary.                                                      |
| Attributs       | ResourceAttributes | Attributs de métadonnées correspondant à SubscriptionUsageSummary.                                                 |

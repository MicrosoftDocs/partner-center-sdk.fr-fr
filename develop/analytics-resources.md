---
title: Ressources d’analyse
description: Ressources de l’espace partenaires pour les données utilisées pour signaler l’utilisation, le déploiement et la consommation.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 613f97cf36a3ecb978b7764fbf9fc5065bd74c30
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095410"
---
# <a name="analytics-resources"></a>Ressources d’analyse

**S’applique à :**

- Espace partenaires

Les ressources définies ici contiennent des données utilisées pour signaler l’utilisation, le déploiement et la consommation.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

La ressource **PartnerLicensesDeploymentInsights** contient des Insights au niveau du partenaire sur le déploiement de la licence.

| Propriété                  | Type                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | nombre                                                         | Pourcentage de licences déployées.                                                |
| licensesSold              | nombre                                                         | Nombre de licences vendues.                                                        |
| processedDateTime         | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                     |
| serviceName               | string                                                         | Nom du service (par exemple : o365, CRM).                                                  |
| channel                   | string                                                         | Nom du canal du service (par exemple : Reseller).                                    |
| attributs                | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « PartnerLicensesDeploymentInsights » |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

La ressource **PartnerLicensesUsageInsights** contient des Insights au niveau du partenaire sur l’utilisation des licences.

| Propriété                     | Type                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | nombre                                                         | Pourcentage de licences déployées.                                           |
| workloadName                 | string                                                         | Nom de la charge de travail (par exemple : Exchange).                                             |
| processedDateTime            | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                |
| serviceName                  | string                                                         | Nom du service (par exemple : o365, CRM).                                             |
| channel                      | string                                                         | Nom du canal du service (par exemple : Reseller).                               |
| attributs                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « PartnerLicensesUsageInsights » |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

La ressource **CustomerLicensesDeploymentInsights** contient des Insights au niveau du client sur le déploiement de la licence.

| Propriété          | Type                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | nombre                                                         | Nombre de licences déployées.                                                     |
| licensesSold      | nombre                                                         | Nombre de licences vendues.                                                         |
| deploymentPercent | nombre                                                         | Pourcentage ajusté de licences déployées.                                        |
| customerId        | string                                                         | Identificateur du client.                                                             |
| customerName      | string                                                         | Nom du client.                                                                   |
| ProductName       | string                                                         | Nom du produit.                                                                    |
| serviceCode       | string                                                         | Code de service de la licence.                                                     |
| processedDateTime | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                      |
| serviceName       | string                                                         | Nom du service (par exemple : o365, CRM).                                                   |
| channel           | string                                                         | Nom du canal du service (par exemple : Reseller).                                     |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « CustomerLicensesDeploymentInsights » |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

La ressource **CustomerLicensesUsageInsights** contient des Insights au niveau du client sur l’utilisation des licences.

| Propriété          | Type                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | string                                                         | Code de charge de travail.                                                              |
| workloadName      | nombre                                                         | Nom de la charge de travail (par exemple : Exchange).                                              |
| usagePercent      | nombre                                                         | Pourcentage ajusté de licences utilisées.                                       |
| licensesActive    | nombre                                                         | nombre de licences actives.                                                  |
| licensesQualified | nombre                                                         | Nombre de licences qualifiées.                                               |
| customerId        | string                                                         | Identificateur du client.                                                        |
| customerName      | string                                                         | Nom du client.                                                              |
| ProductName       | string                                                         | Nom du produit.                                                               |
| serviceCode       | string                                                         | Code de service de la licence.                                                |
| processedDateTime | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                 |
| serviceName       | string                                                         | Nom du service (par exemple : o365, CRM).                                              |
| channel           | string                                                         | Nom du canal du service (par exemple : Reseller).                                |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « CustomerLicensesUsageInsights » |
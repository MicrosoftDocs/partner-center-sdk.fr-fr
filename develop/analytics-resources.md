---
title: Ressources d’analyse
description: Ressources de l’espace partenaires pour les données utilisées pour signaler l’utilisation, le déploiement et la consommation.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e7e2faa7e8a72da4a18ca53711942fcc00ba0513
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413241"
---
# <a name="analytics-resources"></a>Ressources d’analyse

S'applique à :

- Centre pour partenaires

Les ressources définies ici contiennent des données utilisées pour signaler l’utilisation, le déploiement et la consommation.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

La ressource **PartnerLicensesDeploymentInsights** contient des Insights au niveau du partenaire sur le déploiement de la licence.

| Propriété                  | Type                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | nombre                                                         | Pourcentage de licences déployées.                                                |
| licensesSold              | nombre                                                         | Nombre de licences vendues.                                                        |
| processedDateTime         | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                     |
| FormName               | chaîne                                                         | Nom du service (par exemple, o365, CRM).                                                  |
| couche                   | chaîne                                                         | Nom du canal du service (par exemple, Reseller).                                    |
| attributs                | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « PartnerLicensesDeploymentInsights » |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

La ressource **PartnerLicensesUsageInsights** contient des Insights au niveau du partenaire sur l’utilisation des licences.

| Propriété                     | Type                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | nombre                                                         | Pourcentage de licences déployées.                                           |
| workloadName                 | chaîne                                                         | Nom de la charge de travail (par exemple, Exchange).                                             |
| processedDateTime            | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                |
| FormName                  | chaîne                                                         | Nom du service (par exemple, o365, CRM).                                             |
| couche                      | chaîne                                                         | Nom du canal du service (par exemple, Reseller).                               |
| attributs                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « PartnerLicensesUsageInsights » |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

La ressource **CustomerLicensesDeploymentInsights** contient des Insights au niveau du client sur le déploiement de la licence.

| Propriété          | Type                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | nombre                                                         | Nombre de licences déployées.                                                     |
| licensesSold      | nombre                                                         | Nombre de licences vendues.                                                         |
| deploymentPercent | nombre                                                         | Pourcentage ajusté de licences déployées.                                        |
| customerId        | chaîne                                                         | Identificateur du client.                                                             |
| customerName      | chaîne                                                         | Nom du client.                                                                   |
| productName       | chaîne                                                         | Nom du produit.                                                                    |
| serviceCode       | chaîne                                                         | Code de service de la licence.                                                     |
| processedDateTime | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                      |
| FormName       | chaîne                                                         | Nom du service (par exemple, o365, CRM).                                                   |
| couche           | chaîne                                                         | Nom du canal du service (par exemple, Reseller).                                     |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « CustomerLicensesDeploymentInsights » |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

La ressource **CustomerLicensesUsageInsights** contient des Insights au niveau du client sur l’utilisation des licences.

| Propriété          | Type                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | chaîne                                                         | Code de charge de travail.                                                              |
| workloadName      | nombre                                                         | Nom de la charge de travail (par exemple, Exchange).                                              |
| usagePercent      | nombre                                                         | Pourcentage ajusté de licences utilisées.                                       |
| licensesActive    | nombre                                                         | nombre de licences actives.                                                  |
| licensesQualified | nombre                                                         | Nombre de licences qualifiées.                                               |
| customerId        | chaîne                                                         | Identificateur du client.                                                        |
| customerName      | chaîne                                                         | Nom du client.                                                              |
| productName       | chaîne                                                         | Nom du produit.                                                               |
| serviceCode       | chaîne                                                         | Code de service de la licence.                                                |
| processedDateTime | chaîne au format date-heure UTC                                 | Date et heure auxquelles les données ont été agrégées.                                 |
| FormName       | chaîne                                                         | Nom du service (par exemple, o365, CRM).                                              |
| couche           | chaîne                                                         | Nom du canal du service (par exemple, Reseller).                                |
| attributs        | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend « objectType » : « CustomerLicensesUsageInsights » |
---
title: Ressources de déploiement de l’appareil
description: Ressources liées au déploiement d’appareils de l’espace partenaires.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5aaf4c9dc80b681c274c68af3439654e27e27be7
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81664615"
---
# <a name="device-deployment-resources"></a>Ressources de déploiement de l’appareil

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Les ressources suivantes sont liées au déploiement d’appareils.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** fournit des informations sur une stratégie de configuration.

| Propriété             | Type                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | Chaîne au format GUID qui identifie la stratégie.                                  |
| name                 | string                                       | Nom convivial de la stratégie.                                                    |
| catégorie             | string                                       | Catégorie.                                                                        |
| description          | string                                       | Description de la stratégie.                                                              |
| devicesAssignedCount | nombre                                       | Nombre d’appareils affectés à cette stratégie.                                       |
| policySettings       | tableau de chaînes                             | Les paramètres de stratégie : « aucun », «\_supprimer\_les préinstallations OEM »,\_«\_l'\_utilisateur\_OOBE n’est pas administrateur\_local\_», « ignorer les\_paramètres\_Express », « ignorer\_l’inscription OEM », « ignorer le CLUF ».    |
| createdDate          | chaîne au format date-heure UTC               | Date et heure de création de la stratégie.                                            |
| LastModifiedDate &     | chaîne au format date-heure UTC               | Date et heure de la dernière modification de la stratégie.                                      |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                            |

## <a name="device"></a>Appareil

L' **appareil** fournit des informations sur un appareil.

| Propriété            | Type                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | Chaîne au format GUID qui identifie l’appareil.                      |
| serialNumber        | string                                                         | Numéro de série associé de manière unique à l’appareil.                   |
| productKey          | string                                                         | Clé de produit associée de manière unique à l’appareil.                     |
| hardwareHash        | string                                                         | Hachage matériel associé de manière unique à l’appareil.                   |
| modelName           | string                                                         | Nom de modèle associé à l’appareil.                               |
| oemManufacturerName | string                                                         | Nom du fabricant OEM associé à l’appareil.             |
| stratégies            | tableau d’objets                                               | Liste des stratégies affectées à l’appareil.                             |
| uploadedDate        | chaîne au format date-heure UTC                                 | Date et heure auxquelles les détails de l’appareil ont été téléchargés.                      |
| allowedOperations   | tableau de chaînes                                               | Liste des méthodes HTTP autorisées sur une synchronisation d’appareil en tant que obtenir, corriger, supprimer. |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** décrit l’état d’un téléchargement par lots d’appareils d’informations sur chaque appareil dans une liste d’appareils.

| Propriété        | Type     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | Chaîne au format GUID qui est associée au lot des appareils téléchargés. |
| status          | string   | État du chargement de lot : « inconnu », « en attente », « en cours de traitement », « terminé »,\_«\_terminé avec des erreurs ». |
| startedTime     | chaîne au format date-heure UTC | Date et heure de début du processus de téléchargement de lot.   |
| completedTime   | chaîne au format date-heure UTC  | Date et heure de fin du processus de téléchargement de lot.   |
| devicesStatus   | Tableau de ressources [DeviceUploadDetails](#deviceuploaddetails) | Tableau d’objets qui spécifient l’état de chaque chargement d’informations sur l’appareil. |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** décrit l’état d’un téléchargement d’informations sur un appareil.

| Propriété         | Type                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | Chaîne au format GUID qui est associée à l’appareil. |
| serialNumber     | string                  | Numéro de série associé de manière unique à l’appareil. |
| productKey       | string                  | Clé de produit associée de manière unique à l’appareil. |
| status           | string                  | État du chargement des informations sur l’appareil : « en cours », « terminé », « terminé\_avec\_des erreurs ». |
| errorCode        | string                  | Code d’erreur d’état HTTP renvoyé en cas d’échec du chargement de l’appareil. |
| errorDescription | string                  | Description de l’erreur HTTP en cas d’échec du chargement de l’appareil. |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** représente une collection d’appareils.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | Chaîne au format GUID associée au lot d’appareils. |
| createdBy    | string                                                         | Nom du locataire qui a créé la collection.                   |
| creationDate | chaîne au format date-heure UTC                                 | Les données et l’heure de création de la collection.                    |
| deviceCount  | nombre                                                         | Nombre d’appareils dans la collection.                              |
| devicesLink  | [Lien](utility-resources.md#link)                              | Un lien vers les appareils contenus dans ce lot.                        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** fournit les informations nécessaires pour créer un lot d’appareils et le remplit avec des appareils.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | Chaîne au format GUID associée au lot d’appareils. |
| périphériques      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les combinaisons de champs suivantes pour identifier un appareil sont acceptées : hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash uniquement, productKey only, serialNumber + oemManufacturerName + modelName. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** fournit les informations nécessaires pour mettre à jour une liste de périphériques avec une stratégie.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| périphériques      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les propriétés suivantes sont requises : ID, stratégies. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

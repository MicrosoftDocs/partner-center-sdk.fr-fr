---
title: Ressources de déploiement de l’appareil
description: Ressources liées au déploiement d’appareils de l’espace partenaires.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094107"
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
| policySettings       | tableau de chaînes                             | Les paramètres de stratégie : « aucun », « supprimer les \_ \_ préinstallations OEM », \_ « \_ l’utilisateur OOBE n’est pas \_ \_ administrateur local », « ignorer les \_ \_ paramètres Express », « ignorer \_ \_ l’inscription OEM », « ignorer le \_ CLUF ».    |
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
| status          | string   | État du chargement de lot : « inconnu », « en attente », « en cours de traitement », « terminé », « terminé \_ avec des \_ Erreurs ». |
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
| status           | string                  | État du chargement des informations sur l’appareil : « en cours », « terminé », « terminé \_ avec des \_ Erreurs ». |
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
| appareils      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les combinaisons de champs suivantes pour identifier un appareil sont acceptées : hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash uniquement, productKey only, serialNumber + oemManufacturerName + modelName. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** fournit les informations nécessaires pour mettre à jour une liste de périphériques avec une stratégie.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| appareils      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les propriétés suivantes sont requises : ID, stratégies. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

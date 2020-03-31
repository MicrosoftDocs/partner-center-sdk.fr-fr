---
title: Ressources de déploiement de l’appareil
description: Ressources liées au déploiement d’appareils de l’espace partenaires.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 910590a9670d7bfc3fe3e0b00d624026b73372e4
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412359"
---
# <a name="device-deployment-resources"></a>Ressources de déploiement de l’appareil

S'applique à :

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany

Les ressources suivantes sont liées au déploiement d’appareils.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** fournit des informations sur une stratégie de configuration.

| Propriété             | Type                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | chaîne                                       | Chaîne au format GUID qui identifie la stratégie.                                  |
| nom                 | chaîne                                       | Nom convivial de la stratégie.                                                    |
| category             | chaîne                                       | Catégorie.                                                                        |
| description          | chaîne                                       | Description de la stratégie.                                                              |
| devicesAssignedCount | nombre                                       | Nombre d’appareils affectés à cette stratégie.                                       |
| policySettings       | tableau de chaînes                             | Les paramètres de stratégie : « aucun », « supprimer\_\_préinstallations OEM », « OOBE\_utilisateur\_pas\_administrateur de\_local », « ignorer les paramètres\_Express\_», « ignorer les\_l’inscription OEM\_», « ignorer\_CLUF ».    |
| createdDate          | chaîne au format date-heure UTC               | Date et heure de création de la stratégie.                                            |
| LastModifiedDate &     | chaîne au format date-heure UTC               | Date et heure de la dernière modification de la stratégie.                                      |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                            |

## <a name="device"></a>Appareil

L' **appareil** fournit des informations sur un appareil.

| Propriété            | Type                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | chaîne                                                         | Chaîne au format GUID qui identifie l’appareil.                      |
| serialNumber        | chaîne                                                         | Numéro de série associé de manière unique à l’appareil.                   |
| productKey          | chaîne                                                         | Clé de produit associée de manière unique à l’appareil.                     |
| hardwareHash        | chaîne                                                         | Hachage matériel associé de manière unique à l’appareil.                   |
| modelName           | chaîne                                                         | Nom de modèle associé à l’appareil.                               |
| oemManufacturerName | chaîne                                                         | Nom du fabricant OEM associé à l’appareil.             |
| stratégies            | Tableau d’objets                                               | Liste des stratégies affectées à l’appareil.                             |
| uploadedDate        | chaîne au format date-heure UTC                                 | Date et heure auxquelles les détails de l’appareil ont été téléchargés.                      |
| allowedOperations   | tableau de chaînes                                               | Liste des méthodes HTTP autorisées sur une synchronisation d’appareil en tant que obtenir, corriger, supprimer. |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** décrit l’état d’un téléchargement par lots d’appareils d’informations sur chaque appareil dans une liste d’appareils.

| Propriété        | Type     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | chaîne   | Chaîne au format GUID qui est associée au lot des appareils téléchargés. |
| statut          | chaîne   | État du chargement de lot : « inconnu », « en attente », « traitement », « terminé », « terminé\_avec des erreurs de\_». |
| startedTime     | chaîne au format date-heure UTC | Date et heure de début du processus de téléchargement de lot.   |
| completedTime   | chaîne au format date-heure UTC  | Date et heure de fin du processus de téléchargement de lot.   |
| devicesStatus   | Tableau de ressources [DeviceUploadDetails](#deviceuploaddetails) | Tableau d’objets qui spécifient l’état de chaque chargement d’informations sur l’appareil. |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** décrit l’état d’un téléchargement d’informations sur un appareil.

| Propriété         | Type                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| DeviceId         | chaîne                  | Chaîne au format GUID qui est associée à l’appareil. |
| serialNumber     | chaîne                  | Numéro de série associé de manière unique à l’appareil. |
| productKey       | chaîne                  | Clé de produit associée de manière unique à l’appareil. |
| statut           | chaîne                  | État du chargement des informations sur l’appareil : « en cours », « terminé », « terminé\_avec des erreurs de\_». |
| errorCode        | chaîne                  | Code d’erreur d’état HTTP renvoyé en cas d’échec du chargement de l’appareil. |
| errorDescription | chaîne                  | Description de l’erreur HTTP en cas d’échec du chargement de l’appareil. |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** représente une collection d’appareils.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | chaîne                                                         | Chaîne au format GUID associée au lot d’appareils. |
| createdBy    | chaîne                                                         | Nom du locataire qui a créé la collection.                   |
| creationDate | chaîne au format date-heure UTC                                 | Les données et l’heure de création de la collection.                    |
| deviceCount  | nombre                                                         | Nombre d’appareils dans la collection.                              |
| devicesLink  | [Lien](utility-resources.md#link)                              | Un lien vers les appareils contenus dans ce lot.                        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** fournit les informations nécessaires pour créer un lot d’appareils et le remplit avec des appareils.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | chaîne                                                         | Chaîne au format GUID associée au lot d’appareils. |
| devices      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les combinaisons de champs suivantes pour identifier un appareil sont acceptées : hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash uniquement, productKey only, serialNumber + oemManufacturerName + modelName. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** fournit les informations nécessaires pour mettre à jour une liste de périphériques avec une stratégie.

| Propriété     | Type                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | Tableau d’objets [Device](#device)                             | Chaque objet spécifie un appareil. Les propriétés suivantes sont requises : ID, stratégies. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Attributs de métadonnées.                                              |

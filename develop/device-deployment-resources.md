---
title: Device deployment resources
description: Resources related to Partner Center device deployment.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1aecf66907d8e39ae3015ba7a7735942555d1d1c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489949"
---
# <a name="device-deployment-resources"></a>Device deployment resources

S'applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

The following resources are related to device deployment.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** provides information about a configuration policy.

| Propriété             | Tapez                                                           | Description                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | chaîne                                       | A GUID-formatted string that identifies the policy.                                  |
| name                 | chaîne                                       | The friendly name for the policy.                                                    |
| catégorie             | chaîne                                       | The category.                                                                        |
| description          | chaîne                                       | The policy description.                                                              |
| devicesAssignedCount | nombre                                       | The number of devices assigned to this policy.                                       |
| policySettings       | array of strings                             | The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip\_oem\_registration", "skip\_eula".    |
| createdDate          | string in UTC date-time format               | The date and time the policy was created.                                            |
| lastModifiedDate     | string in UTC date-time format               | The date and time the policy was last modified.                                      |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                            |

## <a name="device"></a>Appareil

**Device** provides information about a device.

| Propriété            | Tapez                                                           | Description                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | chaîne                                                         | A GUID-formatted string that identifies the device.                      |
| serialNumber        | chaîne                                                         | The serial number uniquely associated with the device.                   |
| productKey          | chaîne                                                         | The product key uniquely associated with the device.                     |
| hardwareHash        | chaîne                                                         | The hardware hash uniquely associated with the device.                   |
| modelName           | chaîne                                                         | The model name associated with the device.                               |
| oemManufacturerName | chaîne                                                         | The name of the OEM manufacturer associated with the device.             |
| politiques            | array of objects                                               | The list of policies assigned to the device.                             |
| uploadedDate        | string in UTC date-time format                                 | The date and time the device details were uploaded.                      |
| allowedOperations   | array of strings                                               | The list of HTTP methods allowed on a device sync as GET, PATCH, DELETE. |
| attributs          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** describes the status of a device batch upload of information about each device in a list of devices.

| Propriété        | Tapez     | Description                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | chaîne   | A GUID-formatted string that is associated with the batch of devices uploaded. |
| status          | chaîne   | The status of the batch upload: "unknown","queued","processing","finished","finished\_with\_errors". |
| startedTime     | string in UTC date-time format | The date and time that the batch upload process started.   |
| completedTime   | string in UTC date-time format  | The date and time that the batch upload process completed.   |
| devicesStatus   | array of [DeviceUploadDetails](#deviceuploaddetails) resources | An array of objects that specify the status of each device information upload. |
| attributs      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** describes the status of an upload of information about a device.

| Propriété         | Tapez                    | Description                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | chaîne                  | A GUID-formatted string that is associated with the device. |
| serialNumber     | chaîne                  | The serial number uniquely associated with the device. |
| productKey       | chaîne                  | The product key uniquely associated with the device. |
| status           | chaîne                  | The status of the device information upload: "in-progress", "finished", "finished\_with\_errors". |
| errorCode        | chaîne                  | The HTTP status error code returned if the device upload fails. |
| errorDescription | chaîne                  | The HTTP error description if the device upload fails. |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** represents a collection of devices.

| Propriété     | Tapez                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | chaîne                                                         | A GUID-formatted string that is associated with the batch of devices. |
| createdBy    | chaîne                                                         | The name of the tenant that created the collection.                   |
| creationDate | string in UTC date-time format                                 | The data and time that the collection was created.                    |
| deviceCount  | nombre                                                         | The number of devices in the collection.                              |
| devicesLink  | [Link](utility-resources.md#link)                              | A link to the devices contained in this batch.                        |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** provides the information required to create a device batch and populates it with devices.

| Propriété     | Tapez                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | chaîne                                                         | A GUID-formatted string that is associated with the batch of devices. |
| appareils      | array of [Device](#device) objects                             | Each object specifies a device. The following combinations of fields for identifying a device are accepted: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** provides the information required to update a list of devices with a policy.

| Propriété     | Tapez                                                           | Description                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| appareils      | array of [Device](#device) objects                             | Each object specifies a device. The following properties are required: Id, Policies. |
| attributs   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

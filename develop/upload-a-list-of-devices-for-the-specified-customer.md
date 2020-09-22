---
title: Charger la liste des appareils dans un lot existant pour le client spécifié
description: Télécharger une liste d’informations sur les appareils dans un lot existant pour le client spécifié. Cela associe les appareils à un lot d’appareils déjà créé.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a3f6522b31d296e10c66cb45b3684eae3e0c25ab
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926435"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a>Charger la liste des appareils dans un lot existant pour le client spécifié

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Télécharger une liste d’informations sur les appareils dans un lot existant pour le client spécifié. Cela associe les appareils à un lot d’appareils déjà créé.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur du lot de l’appareil.

- Liste des ressources d’appareil qui fournissent des informations sur les appareils individuels.

## <a name="c"></a>C\#

Pour télécharger une liste de périphériques sur un lot d’appareils existant, vous devez d’abord instancier un nouveau [list/dotnet/API/System. Collections. Generic. List-1) de type [**Device**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device) et remplir la liste avec les périphériques. Les combinaisons suivantes de propriétés remplies sont requises au minimum pour identifier chaque appareil :

- [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey).

- [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber).

- [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey) + [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber).

- [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) uniquement.

- [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey) uniquement.

- [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber) + [**OemManufacturerName**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.oemmanufacturername) + [**modelname**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ModelName).

Ensuite, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’identificateur du client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, appelez la méthode [**DeviceBatches. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicesbatchcollection.BYID) avec l’identificateur de lot de l’appareil pour obtenir une interface pour les opérations du lot spécifié. Enfin, appelez la méthode [**Devices. Create**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicecollection.Create) ou [**CreateAsync**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicecollection.createasync) avec la liste des appareils pour ajouter les périphériques au lot d’appareils.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateDevices.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le chemin d’accès et les paramètres de requête suivants lors de la création de la demande.

| Nom           | Type   | Obligatoire | Description                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | string | Oui      | Chaîne au format GUID qui identifie le client. |
| ID d’devicebatch | string | Oui      | Identificateur de chaîne qui identifie le lot de l’appareil. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir un tableau d’objets d' [appareil](device-deployment-resources.md#device) . Les combinaisons de champs suivantes permettant d’identifier un appareil sont acceptées :

- hardwareHash + productKey.
- hardwareHash + serialNumber.
- hardwareHash + productKey + serialNumber.
- hardwareHash uniquement.
- productKey uniquement.
- serialNumber + oemManufacturerName + modelName.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient un en-tête d' **emplacement** qui a un URI qui peut être utilisé pour récupérer l’état du chargement de l’appareil. Enregistrez cet URI pour une utilisation avec d’autres API REST associées.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```

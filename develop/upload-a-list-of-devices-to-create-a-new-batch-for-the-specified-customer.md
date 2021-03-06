---
title: Charger la liste des appareils afin de créer un lot pour le client spécifié
description: Télécharger une liste d’informations sur les appareils pour créer un nouveau lot pour le client spécifié. Cela crée un lot d’appareils pour l’inscription dans un déploiement Zero-Touch et associe les appareils et le lot d’appareils au client spécifié.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 68ae21fa790b3c0810e26c54860b83d1ab303b8c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927876"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a>Charger la liste des appareils afin de créer un lot pour le client spécifié

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Télécharger une liste d’informations sur les appareils pour créer un nouveau lot pour le client spécifié. Cela crée un lot d’appareils pour l’inscription dans un déploiement Zero-Touch et associe les appareils et le lot d’appareils au client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur. Suivez le [modèle d’application sécurisée](enable-secure-app-model.md) lors de l’utilisation de l’authentification d’application + utilisateur avec les API de l’espace partenaires.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Liste des ressources d’appareil qui fournissent des informations sur les appareils individuels.

## <a name="c"></a>C\#

Pour télécharger une liste d’appareils afin de créer un nouveau lot d’appareils :

1. Instanciez un nouveau [list/dotnet/API/System. Collections. Generic. List-1) de type [/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device d'**appareil**] et remplissez la liste avec les périphériques. Les combinaisons suivantes de propriétés remplies sont requises au minimum pour identifier chaque appareil :

   - [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey).
   - [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber).
   - [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) + [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey) + [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber).
   - [**HardwareHash**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.hardwarehash) uniquement.
   - [**ProductKey**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ProductKey) uniquement.
   - [**SerialNumber**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.SerialNumber) + [**OemManufacturerName**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.oemmanufacturername) + [**modelname**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device.ModelName).

2. Instanciez un objet [**DeviceBatchCreationRequest**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.devicebatchcreationrequest) et affectez à la propriété [**BatchID**/dotnet/API/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batenfants) un nom unique de votre choix, et la propriété [**Devices**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.devicebatchcreationrequest.Devices) à la liste des appareils à télécharger.

3. Traitez la demande de création de lots d’appareils en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’identificateur de client pour récupérer une interface pour les opérations sur le client spécifié.

4. Appelez la méthode [**DeviceBatches. Create**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicesbatchcollection) ou [**CreateAsync**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicesbatchcollection) avec la demande de création de lot de l’appareil pour créer le lot.

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateDeviceBatch.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir une ressource [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) .

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient un en-tête d' **emplacement** qui a un URI qui peut être utilisé pour récupérer l’état du chargement de l’appareil. Enregistrez cet URI pour une utilisation avec d’autres API REST associées.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```

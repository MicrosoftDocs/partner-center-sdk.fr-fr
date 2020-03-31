---
title: Mettre à jour une liste d’appareils avec une stratégie
description: Comment mettre à jour une liste d’appareils avec une stratégie de configuration pour le client spécifié.
ms.assetid: D68DAE8B-EFBC-4C71-8CB4-3ADA8D45DDBA
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c3c94b53eb30e648862bac4d1ea46bbfdd2cb643
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414818"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>Mettre à jour une liste d’appareils avec une stratégie


**S’applique à**

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment mettre à jour une liste d’appareils avec une stratégie de configuration pour le client spécifié.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client.
- Identificateur de la stratégie.
- Identificateurs des appareils à mettre à jour.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour mettre à jour une liste d’appareils avec la stratégie de configuration spécifiée, commencez par instancier une [liste](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1) de type [KeyValuePair](https://docs.microsoft.com/dotnet/api/system.collections.generic.keyvaluepair-2)[ **(PolicyCategory,** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) et ajoutez la stratégie à appliquer, comme indiqué dans l’exemple de code suivant. Vous aurez besoin de l’identificateur de stratégie de la stratégie.

Ensuite, créez une liste d’objets d' [**appareil**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) à mettre à jour avec la stratégie, en spécifiant l’identificateur de périphérique et la liste qui contient la stratégie à appliquer, pour chaque appareil. Ensuite, instanciez un objet [**DevicePolicyUpdateRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) et définissez la propriété [**Devices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) sur la liste des objets Device.

Pour traiter la demande de mise à jour de la stratégie d’appareil, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, récupérez la propriété [**DevicePolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) pour obtenir une interface pour les opérations de regroupement d’appareils clients. Enfin, appelez la méthode [**Update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) avec l’objet DevicePolicyUpdateRequest pour mettre à jour les appareils avec la stratégie.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId; 
string selectedDeviceId;

// Indicate the policy to apply to the list of devices. 
List<KeyValuePair<PolicyCategory, string>> 
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest 
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices             
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation = 
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : UpdateDevicesPolicy.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode    | URI de demande                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID client | chaîne | Oui      | Chaîne au format GUID qui identifie le client. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Le corps de la demande doit contenir une ressource [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .

**Exemple de requête**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, la réponse contient un en-tête d' **emplacement** qui a un URI qui peut être utilisé pour récupérer l’état de ce processus de traitement par lots. Enregistrez cet URI pour une utilisation avec d’autres API REST associées.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```

 

 





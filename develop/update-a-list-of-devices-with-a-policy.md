---
title: Mettre à jour une liste d’appareils avec une stratégie
description: Comment mettre à jour une liste d’appareils avec une stratégie de configuration pour le client spécifié.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 18ec280995b978a5ac62d3d7288337c1307a6643
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927582"
---
# <a name="update-a-list-of-devices-with-a-policy"></a>Mettre à jour une liste d’appareils avec une stratégie

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment mettre à jour une liste d’appareils avec une stratégie de configuration pour le client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur de la stratégie.

- Identificateurs des appareils à mettre à jour.

## <a name="c"></a>C\#

Pour mettre à jour une liste d’appareils avec la stratégie de configuration spécifiée, commencez par instancier un [list/dotnet/API/System. Collections. Generic. List 1) de type [KeyValuePair/dotnet/API/System. Collections. Generic. KeyValuePair-2) [**(PolicyCategory,**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.PolicyCategory) String) et ajoutez la stratégie à appliquer, comme illustré dans l’exemple de code suivant. Vous aurez besoin de l’identificateur de stratégie de la stratégie.

Ensuite, créez une liste d’objets [/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.Device d'**appareil**) à mettre à jour avec la stratégie, en spécifiant l’identificateur de périphérique et la liste qui contient la stratégie à appliquer pour chaque appareil. Ensuite, instanciez un objet [**DevicePolicyUpdateRequest**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.devicepolicyupdaterequest) et définissez la propriété [**Devices**/dotnet/API/Microsoft.Store.partnercenter.Models.devicesdeployment.devicebatchcreationrequest.Devices) sur la liste des objets d’appareil.

Pour traiter la demande de mise à jour de la stratégie d’appareil, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’identificateur du client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, récupérez la propriété [**DevicePolicy**/dotnet/API/Microsoft.Store.partnercenter.Customers.ICustomer.devicepolicy) pour obtenir une interface pour les opérations de regroupement d’appareils clients. Enfin, appelez la méthode [**Update**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.icustomerdevicecollection.Update) avec l’objet DevicePolicyUpdateRequest pour mettre à jour les appareils avec la stratégie.

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

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de demande                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir une ressource [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) .

### <a name="request-example"></a>Exemple de requête

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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient un en-tête d' **emplacement** qui a un URI qui peut être utilisé pour récupérer l’état de ce processus de traitement par lots. Enregistrez cet URI pour une utilisation avec d’autres API REST associées.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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

---
title: Obtenir la liste des appareils pour le client et le lot spécifiés
description: Comment récupérer une collection de périphériques et les détails de l’appareil dans le lot d’appareils spécifié pour un client.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 125d1b4e239f69ae2dfc9667f5d009bab9f415b2
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927667"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a>Obtenir la liste des appareils pour le client et le lot spécifiés

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Cet article explique comment récupérer un regroupement d’appareils dans un lot spécifié pour un client spécifié. Chaque ressource d’appareil contient des détails sur l’appareil.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur de lot de l’appareil.

## <a name="c"></a>C\#

Pour récupérer un regroupement des appareils dans un lot d’appareils spécifié pour le client spécifié :

1. Appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié.

2. Appelez la méthode [**DeviceBatches. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicesbatchcollection.BYID) pour obtenir une interface pour les opérations de collection de lots de périphériques pour le lot spécifié.

3. Récupérez la propriété [**Devices**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicesbatch.Devices) pour obtenir une interface pour les opérations de collecte d’appareils pour le lot.

4. Appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicecollection.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.idevicecollection.getasync) pour récupérer la collection d’appareils.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **exemples du kit de développement logiciel (SDK) Partner Center**
- Classe : **GetDevices.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices http/1.1 |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom           | Type   | Obligatoire | Description                                           |
|----------------|--------|----------|-------------------------------------------------------|
| customer-id    | string | Oui      | Chaîne au format GUID qui identifie le client. |
| ID d’devicebatch | string | Oui      | Identificateur de chaîne qui identifie le lot de l’appareil. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection paginée des ressources de l' [appareil](device-deployment-resources.md#device) . La collection contient 100 périphériques dans une page. Pour récupérer la page suivante de 100 appareils, continuationToken dans le corps de la réponse doit être inclus dans la requête suivante en tant qu’en-tête MS-ContinuationToken.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

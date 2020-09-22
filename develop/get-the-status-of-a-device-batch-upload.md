---
title: Obtenir l’état d’un chargement de lot d’appareils
description: Comment obtenir l’état d’un téléchargement par lots d’un appareil pour un client spécifié.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07dfe950e92fdd0141518c8cca746c8d958f2843
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927459"
---
# <a name="get-the-status-of-a-device-batch-upload"></a>Obtenir l’état d’un chargement de lot d’appareils

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment obtenir l’état d’un téléchargement par lots d’un appareil pour un client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur de suivi de lot renvoyé dans l’en-tête d’emplacement lors de l’envoi du lot d’appareils. Pour plus d’informations, voir [Télécharger une liste d’appareils pour le client spécifié](upload-a-list-of-devices-for-the-specified-customer.md).

## <a name="c"></a>C\#

Pour obtenir l’état d’un téléchargement par lots d’appareils, appelez d’abord la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, appelez la méthode [**BatchUploadStatus. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.ibatchjobstatuscollection.BYID) avec l’ID de suivi batch pour récupérer une interface pour les opérations d’état de chargement par lots. Enfin, appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.ibatchjobstatus.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) pour récupérer l’État.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetBatchUploadStatus.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/batchJobStatus/{batchtracking-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom             | Type   | Obligatoire | Description                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer-id      | string | Oui      | Chaîne au format GUID qui identifie le client.                                                                                                                          |
| ID d’batchtracking | string | Oui      | Identificateur au format GUID utilisé pour récupérer l’état du chargement par lots d’un appareil. Cet ID est renvoyé dans l’en-tête Location lorsque le lot de l’appareil est envoyé avec succès. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient une ressource [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```

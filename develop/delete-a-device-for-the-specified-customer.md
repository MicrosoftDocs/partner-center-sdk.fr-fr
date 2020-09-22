---
title: Supprimer un appareil pour le client spécifié
description: Comment supprimer un appareil qui appartient à un client spécifié.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927824"
---
# <a name="delete-a-device-for-the-specified-customer"></a>Supprimer un appareil pour le client spécifié

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Cet article explique comment supprimer un appareil qui appartient à un client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur du lot de l’appareil.

- Identificateur de l’appareil.

## <a name="c"></a>C\#

Pour supprimer un appareil pour le client spécifié :

1. Appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client pour récupérer une interface pour les opérations sur le client.

2. Appelez la méthode [**DeviceBatches. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) avec l’identificateur de lot de l’appareil pour obtenir une interface pour les opérations du lot spécifié.

3. Appelez la méthode [**Devices. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) pour faire en sorte qu’une interface fonctionne sur l’appareil spécifié.

4. Appelez la méthode [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) ou [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) pour supprimer l’appareil du lot.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : DeleteDevice.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| Suppression     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/deviceBatches/{devicebatch-ID}/Devices/{Device-ID} http/1.1  |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom           | Type   | Obligatoire | Description                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| customer-id    | string | Oui      | Chaîne au format GUID qui identifie le client.              |
| ID d’devicebatch | string | Oui      | Identificateur du lot de l’appareil qui contient l’appareil. |
| device-id      | string | Oui      | Identificateur de l’appareil.                                             |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse retourne un code d’état **204 aucun contenu** .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```

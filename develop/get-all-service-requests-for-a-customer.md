---
title: Obtenir des demandes de service pour un client
description: Obtient toutes les demandes de service d’un client.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b58f70fa0aae5deb90356707bb601a7a77d33e9d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097777"
---
# <a name="get-all-service-requests-for-a-customer"></a>Obtenir des demandes de service pour un client

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient toutes les demandes de service d’un client.

Dans le tableau de bord espace partenaires, vous pouvez effectuer cette opération en [sélectionnant d’abord un client](get-a-customer-by-name.md). Ensuite, sélectionnez **gestion des services** dans la barre latérale gauche. Les demandes de service du client sont affichées sous **tickets de support**.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour afficher la liste de toutes les demandes de service d’un client, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode [**méthode BYID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Appelez ensuite la propriété [**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) , suivie des méthodes d' [**extraction ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) ou de [**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerCenterSDK. FeaturesSamples, **classe**: CustomerManagedServices.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/servicerequests http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour obtenir toutes les demandes de service pour le client.

| Nom                   | Type     | Obligatoire | Description                            |
|------------------------|----------|----------|----------------------------------------|
| **customer-tenant-id** | **guid** | O        | GUID correspondant au client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources de **demande de service** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```

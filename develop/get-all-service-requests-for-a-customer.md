---
title: Obtenir toutes les demandes de service pour un client
description: Obtient toutes les demandes de service d’un client.
ms.assetid: 21F01038-EE51-4FB3-8BE5-9086DBD0F393
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 32e4f4a45cdfe4726370937cd69858b72f2b95f6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485839"
---
# <a name="get-all-service-requests-for-a-customer"></a>Obtenir toutes les demandes de service pour un client


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient toutes les demandes de service d’un client.

Dans le tableau de bord espace partenaires, vous pouvez effectuer cette opération en [sélectionnant d’abord un client](get-a-customer-by-name.md). Ensuite, sélectionnez **gestion des services** dans la barre latérale gauche. Les demandes de service du client sont affichées sous **tickets de support**.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour afficher la liste de toutes les demandes de service d’un client, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Appelez ensuite la propriété [**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) , suivie des méthodes d' [**extraction ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) ou de [**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerCenterSDK. FeaturesSamples, **classe**: CustomerManagedServices.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/servicerequests http/1.1 |

 

**Paramètre URI**

Utilisez le paramètre de requête suivant pour obtenir toutes les demandes de service pour le client.

| Nom                   | Type     | Obligatoire | Description                            |
|------------------------|----------|----------|----------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | GUID correspondant au client. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, cette méthode retourne une collection de ressources de **demande de service** dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

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

 

 





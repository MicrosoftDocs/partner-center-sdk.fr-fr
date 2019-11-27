---
title: Mettre à jour une demande de service
description: Procédure de mise à jour d’une demande de service client existante qu’un fournisseur de solutions Cloud a déposée auprès de Microsoft au nom du client.
ms.assetid: 09C13775-739B-4CB9-9442-456E17F91452
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7c29f077ce9caf1a44609b599403f254c5ce7c16
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487889"
---
# <a name="update-a-service-request"></a>Mettre à jour une demande de service


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Procédure de mise à jour d’une demande de service client existante qu’un fournisseur de solutions Cloud a déposée auprès de Microsoft au nom du client.

Dans le tableau de bord espace partenaires, vous pouvez effectuer cette opération en [sélectionnant d’abord un client](get-a-customer-by-name.md). Ensuite, sélectionnez **gestion des services** dans la barre latérale gauche. Sous l’en-tête **demandes de support** , sélectionnez la demande de service en question. Pour terminer, apportez les modifications souhaitées à la demande de service, puis sélectionnez **Envoyer.**

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID de demande de service.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour mettre à jour la demande de service d’un client, appelez la méthode [**IServiceRequestCollection. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) avec l’ID de demande de service pour identifier et retourner l’interface de demande de service. Appelez ensuite la méthode [**IServiceRequest. patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) ou [**PatchAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) pour mettre à jour la demande de service. Pour fournir les valeurs mises à jour, créez un nouvel objet [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) vide et définissez uniquement les valeurs de propriété que vous souhaitez modifier. Transmettez ensuite cet objet dans l’appel à la méthode patch ou PatchAsync.

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : UpdatePartnerServiceRequest.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode    | URI de requête                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/servicerequests/{ServiceRequest-ID} http/1.1 |

 

**Paramètre URI**

Utilisez le paramètre URI suivant pour mettre à jour la demande de service.

| Nom                  | Type     | Obligatoire | Description                                 |
|-----------------------|----------|----------|---------------------------------------------|
| **ID d’ServiceRequest** | **uniques** | Y        | GUID qui identifie la demande de service. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Le corps de la demande doit contenir une ressource [ServiceRequest](service-request-resources.md) . Les seules valeurs requises sont celles qui doivent être mises à jour.

**Exemple de requête**

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, cette méthode retourne une ressource de **demande de service** avec des propriétés mises à jour dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```

 

 





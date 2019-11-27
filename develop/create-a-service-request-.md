---
title: Créer une demande de service
description: Comment créer une demande de service de l’espace partenaires.
ms.assetid: 16DA9836-7052-4103-82D4-933E5EEB7E71
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7dcac9a9938f9d197d3ece0d7b777e7efc40274b
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489319"
---
# <a name="create-a-service-request"></a>Créer une demande de service

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment créer une demande de service de l’espace partenaires.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID de rubrique de support. Si vous n’avez pas d’ID de rubrique de support, consultez les [rubriques obtenir un support de demande de service](get-service-request-support-topics--pending-.md).

## <a name="c"></a>\# C

Pour créer une demande de service :

1. Créez et remplissez un objet [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) avec le titre, la description, la gravité et l’ID de la rubrique de support. Pour ajouter des informations supplémentaires, l’objet [**ServiceRequest**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) prend en charge une collection facultative de [**Notes**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.notes), mais ne prend pas en charge les liens vers les fichiers en vue de leur téléchargement.
2. Une fois l’objet créé, appelez la méthode [**collection iaggregatepartner. ServiceRequests. Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.ipartnerservicerequestcollection.create) , en lui transmettant l’objet ServiceRequest nouvellement créé et une chaîne contenant les paramètres régionaux de l’organisation qui crée la demande de service (paramètres régionaux de l’agent).

### <a name="c-example"></a>Exemple de\# C

``` csharp
// IAggregatePartner partnerOperations;
// string supportTopicId;

ServiceRequest serviceRequestToCreate = new ServiceRequest()
{
    Title = "TrialSR",
    Description = "Ignore this SR",
    Severity = ServiceRequestSeverity.Critical,
    SupportTopicId = supportTopicId
};

ServiceRequest serviceRequest = partnerOperations.ServiceRequests.Create(serviceRequestToCreate, "en-US");
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreatePartnerServiceRequest.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Publier** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/servicerequests/{agent-locale} http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre URI suivant pour identifier les paramètres régionaux de l’agent.

| Nom             | Type       | Obligatoire | Description                                                  |
|------------------|------------|----------|--------------------------------------------------------------|
| **paramètres régionaux de l’agent** | **chaîne** | Y        | Paramètres régionaux de l’organisation qui crée la demande de service. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la requête

Ce tableau décrit les propriétés obligatoires et facultatives dans le corps de la demande.

| Nom             | Type                                                                        | Obligatoire | Description                                                                          |
|------------------|-----------------------------------------------------------------------------|----------|--------------------------------------------------------------------------------------|
| Titre            | chaîne                                                                      | Y        | Titre de la demande de service.                                                           |
| Description      | chaîne                                                                      | Y        | Description.                                                                     |
| Sévérité         | chaîne                                                                      | Y        | Gravité : « inconnu », « critique », « modéré » ou « minimal ».                       |
| SupportTopicId   | chaîne                                                                      | Y        | ID de la rubrique de support.                                                         |
| SupportTopicName | chaîne                                                                      | N        | Nom de la rubrique de support.                                                       |
| Id               | chaîne                                                                      | N        | ID de la demande de service.                                                       |
| État           | chaîne                                                                      | N        | État de la demande de service : « None », « Open », « Closed » ou « attention\_needed ». |
| Organisation     | [ServiceRequestOrganization](service-request-resources.md#servicerequestorganization) | N        | Organisation pour laquelle la demande de service est créée.                               |
| PrimaryContact   | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | Contact principal sur la demande de service.                                              |
| LastUpdatedBy    | [ServiceRequestContact](service-request-resources.md#servicerequestcontact)           | N        | « Dernière mise à jour par » permet de contacter les modifications apportées à la demande de service.                        |
| ProductName      | chaîne                                                                      | N        | Nom du produit qui correspond à la demande de service.                     |
| ProductId        | chaîne                                                                      | N        | ID du produit.                                                               |
| CreatedDate      | date                                                                        | N        | Date de création de la demande de service.                                          |
| LastModifiedDate & | date                                                                        | N        | Date à laquelle la demande de service a été modifiée pour la dernière fois.                                 |
| LastClosedDate   | date                                                                        | N        | Date de la dernière fermeture de la demande de service.                                   |
| FileLinks        | Tableau de ressources [FileInfo](utility-resources.md#fileinfo)               | N        | Collection de liens de fichiers qui se rapportent à la demande de service.                    |
| NewNote          | [ServiceRequestNote](service-request-resources.md#servicerequestnote)                 | N        | Une note peut être ajoutée à une demande de service existante.                                  |
| Remarques            | Tableau de [ServiceRequestNotes](service-request-resources.md#servicerequestnote)       | N        | Collection de remarques ajoutées à la demande de service.                                  |
| CountryCode      | chaîne                                                                      | N        | Pays correspondant à la demande de service.                                    |
| Attributs       | objet                                                                      | N        | Contient « ObjectType » : « ServiceRequest ».                                             |

Ce tableau décrit les propriétés requises dans le corps de la demande.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/servicerequests/en-US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 474
Expect: 100-continue

{
    "Id": null,
    "Title": "TrialSR",
    "Description": "Ignore this SR",
    "Severity": "critical",
    "SupportTopicId": "32444671",
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
    "NewNote": null,
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne les propriétés de la ressource de **demande de service** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 721
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae43859b-591d-47ea-9fd1-028b4c799118
MS-RequestId: 55f86bfb-d3bb-4fe4-9f01-2fdaef11a81f
MS-CV: vB9EuWs/ukaxQmuV.0
MS-ServerId: 101112616
Date: Thu, 22 Dec 2016 20:31:14 GMT

 {
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "id": "616122292874576",
    "status": "none",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1",
        "phoneNumber": "2398391056"
    },
    "primaryContact": {
        "organization": {
            "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
            "name": "TEST_TEST_BugBash1",
            "phoneNumber": "2398391056"
        },
        "contactId": "bb4ebcf5-d84c-4b35-8469-f4cfa4ac909e",
        "lastName": "Account",
        "email": "admin@testtestbugbash1.onmicrosoft.com",
        "phoneNumber": "2066017143"
    },
    "createdDate": "0001-01-01T00:00:00",
    "lastModifiedDate": "0001-01-01T00:00:00",
    "lastClosedDate": "0001-01-01T00:00:00",
    "countryCode": "US",
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
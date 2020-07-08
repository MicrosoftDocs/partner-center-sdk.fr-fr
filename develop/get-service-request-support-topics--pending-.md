---
title: Obtenir les rubriques de support des demandes de service
description: Obtient une collection d’éléments représentant des rubriques valides pour les demandes de service.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbc2197f47681b36cd66d0fd5d19732999f86066
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097616"
---
# <a name="get-service-request-support-topics"></a>Obtenir les rubriques de support des demandes de service

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient une collection d’éléments représentant des rubriques valides pour les demandes de service.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

## <a name="c"></a>C\#

Pour obtenir une collection de rubriques de demande de service, utilisez votre collection [**collection ipartneroperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) pour récupérer la propriété [**ServiceRequests**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.servicerequests) de l’objet résultant, suivi de la propriété [**SupportTopics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection) et des méthodes d' [**extraction ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.get) ou de [**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.servicerequests.isupporttopicscollection.getasync) .

``` csharp
// IPartner partnerOperations;

ResourceCollection<SupportTopic> supportTopicsCollection = partnerOperations.ServiceRequests.SupportTopics.Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/supporttopics http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/supporttopics HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
X-Locale: en-US
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection des rubriques valides pour une demande de support.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 4982
Content-Type: application/json
MS-CorrelationId: f447b215-f9bc-48da-a05a-3b5322d86a9c
MS-RequestId: 4c1e8b6c-d136-4931-9df9-d85ec08ccffe
Date: Fri, 29 Jan 2016 22:31:36 GMT

{
    "totalCount":14,
    "items":[{
        "name":"Partner Center Issues",
        "description":"Office 365 questions from the CSP (Cloud Solution Provider) partners using Partner Center",
        "id":32444667,
        "attributes":{
            "objectType":"SupportTopic"
        }
    },
    {
        "name":"Cannot manage my profile",
        "description":"Issues that are related to errors or problems with managing a profile",
        "id":32444671,
        "attributes":{
            "objectType":"SupportTopic"
        }
    }],
    "attributes":{
        "objectType":"Collection"
    }
}
```

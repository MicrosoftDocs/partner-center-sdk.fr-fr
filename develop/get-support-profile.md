---
title: Obtenir le profil de prise en charge
description: Obtient un objet qui représente le profil de support d’un utilisateur.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6107288c0885a6baf6140e66ef1b423ab9b2940d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097490"
---
# <a name="get-support-profile"></a>Obtenir le profil de prise en charge

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient un objet qui représente le profil de support d’un utilisateur.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

## <a name="c"></a>C\#

Pour accéder à votre profil de support, utilisez votre collection **collection iaggregatepartner. Profiles** . Appelez la propriété [**SupportProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , suivie par les méthodes d' [**extraction ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) ou de [**GetAsync ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerCenterSDK. FeaturesSamples, **classe**: GetSupportProfile.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                              |
|---------|--------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/support http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne un objet **SupportProfile** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```

---
title: Accéder au profil de support
description: Obtient un objet qui représente le profil de support d’un utilisateur.
ms.assetid: 7161B81C-09E7-46C8-8EF4-214B3ED76FB7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 400c82a41a12bc02839f4dc835a9ce7631cc1e50
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487099"
---
# <a name="get-support-profile"></a>Accéder au profil de support


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient un objet qui représente le profil de support d’un utilisateur.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

Pour accéder à votre profil de support, utilisez votre collection **collection iaggregatepartner. Profiles** . Appelez la propriété [**SupportProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) , suivie par les méthodes d' [**extraction ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) ou de [**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) .

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerCenterSDK. FeaturesSamples, **classe**: GetSupportProfile.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande

**Syntaxe de la requête**

| Méthode  | URI de requête                                                              |
|---------|--------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Profiles/support http/1.1 |

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse

En cas de réussite, cette méthode retourne un objet **SupportProfile** dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

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
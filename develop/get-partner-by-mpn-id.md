---
title: Vérifier l’ID MPN d’un partenaire
description: Comment vérifier l’identificateur de Microsoft Partner Network d’un partenaire (ID MPN). La technique illustrée ici vérifie l’identificateur de Microsoft Partner Network du partenaire en demandant le profil MPN du partenaire à partir de l’espace partenaires.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2588a75975cce6afe48c252c495291c4ee34eb5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927024"
---
# <a name="verify-a-partner-mpn-id"></a>Vérifier l’ID MPN d’un partenaire

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment vérifier l’identificateur de Microsoft Partner Network d’un partenaire (ID MPN).

La technique illustrée ici vérifie l’identificateur de Microsoft Partner Network du partenaire en demandant le profil MPN du partenaire à partir de l’espace partenaires. L’identificateur est considéré comme valide si la demande est réussie.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID MPN du partenaire à vérifier. Si vous omettez cette valeur, la demande récupère le profil MPN du partenaire connecté.

## <a name="c"></a>C\#

Pour vérifier l’ID MPN d’un partenaire, commencez par récupérer une interface pour les opérations de collection de profils de partenaire à partir de la propriété [**collection iaggregatepartner. Profiles**/dotnet/API/Microsoft.Store.partnercenter.ipartner.Profiles). Ensuite, récupérez une interface pour les opérations de profil MPN à partir de la propriété [**MpnProfile**/dotnet/API/Microsoft.Store.partnercenter.Profiles.ipartnerprofilecollection.mpnprofile). Enfin, appelez les méthodes [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.Profiles.impnprofile.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.PARTNERCENTER.Profiles.IMPNPROFILE.GETASYNC) avec l’ID MPN pour récupérer le profil MPN. Si vous omettez l’ID MPN de l’appel d’extraction ou de GetAsync, la demande tente de récupérer le profil MPN du partenaire connecté.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : VerifyPartnerMpnId.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN ? mpnId = {MPN-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Fournissez le paramètre de requête suivant pour identifier le partenaire. Si vous omettez ce paramètre de requête, la demande retourne le profil MPN du partenaire connecté.

| Nom   | Type | Obligatoire | Description                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | Non       | ID de Microsoft Partner Network qui identifie le partenaire. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient la ressource [MpnProfile](profile-resources.md#mpnprofile) pour le partenaire.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example-success"></a>Exemple de réponse (réussite)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>Exemple de réponse (échec)

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```

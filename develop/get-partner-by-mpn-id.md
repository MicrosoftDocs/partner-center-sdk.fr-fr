---
title: Vérifier un ID MPN de partenaire
description: Comment vérifier l’identificateur de Microsoft Partner Network d’un partenaire (ID MPN). La technique illustrée ici vérifie l’identificateur de Microsoft Partner Network du partenaire en demandant le profil MPN du partenaire à partir de l’espace partenaires.
ms.assetid: 95CBA254-0980-4519-B95D-1F906C321863
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cc18ee559bd3ceafd7239ccb46e7d616d8fc5f13
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415700"
---
# <a name="verify-a-partner-mpn-id"></a>Vérifier un ID MPN de partenaire

**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment vérifier l’identificateur de Microsoft Partner Network d’un partenaire (ID MPN).

La technique illustrée ici vérifie l’identificateur de Microsoft Partner Network du partenaire en demandant le profil MPN du partenaire à partir de l’espace partenaires. L’identificateur est considéré comme valide si la demande est réussie.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- ID MPN du partenaire à vérifier. Si vous omettez cette valeur, la demande récupère le profil MPN du partenaire connecté.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

Pour vérifier l’ID MPN d’un partenaire, commencez par récupérer une interface pour les opérations de collection de profils de partenaire à partir de la propriété [**collection iaggregatepartner. Profiles**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) . Ensuite, récupérez une interface avec les opérations de profil MPN à partir de la propriété [**MpnProfile**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) . Enfin, appelez les méthodes d' [**extraction**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) ou de [**GETASYNC**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) avec l’ID MPN pour récupérer le profil MPN. Si vous omettez l’ID MPN de l’appel d’extraction ou de GetAsync, la demande tente de récupérer le profil MPN du partenaire connecté.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : VerifyPartnerMpnId.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de demande                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Profiles/MPN ? mpnId = {MPN-ID} http/1.1 |

**Paramètre URI**

Fournissez le paramètre de requête suivant pour identifier le partenaire. Si vous omettez ce paramètre de requête, la demande retourne le profil MPN du partenaire connecté.

| Nom   | Type | Obligatoire | Description                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN-ID | int  | Non       | ID de Microsoft Partner Network qui identifie le partenaire. |

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

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

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST

En cas de réussite, le corps de la réponse contient la ressource [MpnProfile](profile-resources.md#mpnprofile) pour le partenaire.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

**Exemple de réponse (réussite)**

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

**Exemple de réponse (échec)**

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
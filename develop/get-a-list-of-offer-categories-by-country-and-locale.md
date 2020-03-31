---
title: Obtenir la liste des catégories d’offres par marché
description: Comment obtenir une collection qui contient toutes les catégories d’offres dans un pays/une région et des paramètres régionaux donnés.
ms.assetid: 69174433-74C6-4294-ACAA-C2CE3D69CFEE
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e04fb68aa3e75ddd0171386b3f9eab7064e7d2ab
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416788"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Obtenir la liste des catégories d’offres par marché

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette rubrique explique comment obtenir une collection qui contient toutes les catégories d’offre dans un pays/une région et des paramètres régionaux donnés.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="c"></a>C\#

Pour obtenir la liste des catégories d’offres dans un pays/une région et des paramètres régionaux donnés :

1. Utilisez votre collection [**collection iaggregatepartner. Operations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) pour appeler la méthode [**with ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) sur un contexte donné.
2. Inspectez la propriété [**OfferCategories**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) de l’objet résultant.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **PartnerSDK. FeatureSample**
- Classe : **PartnerSDK. FeatureSample**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de demande                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/offercategories ? Country = {pays-ID} http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir les catégories d’offre.

| Nom           | Type       | Obligatoire | Description            |
|----------------|------------|----------|------------------------|
| **pays-ID** | **chaîne** | Y        | ID du pays/de la région. |

### <a name="request-headers"></a>En-têtes de requête

Un **ID de paramètres régionaux** mis en forme en tant que chaîne est requis.

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de demande

None.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources **OfferCategory** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```

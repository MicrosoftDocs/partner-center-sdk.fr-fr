---
title: Obtenir toutes les informations analytiques sur la recherche
description: Obtention de toutes les informations d’analyse de recherche.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 10e607a0fd2c973909c4b8aa57d6c7074eab9503
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156561"
---
# <a name="get-all-search-analytics-information"></a>Obtenir toutes les informations analytiques sur la recherche

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir toutes les informations d’analyse de recherche pour vos clients.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête |
|---------|-------------|
| **GET** | baseURL/Partner/v1/Analytics/Search http/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>Paramètres URI

|    Paramètre     |  Type  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      Filter      | string |                                                                     Retourne des données correspondant à la condition de filtre. </br> **Exemple :**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | string |                                         Prend en charge les termes et les dates. La logique de court-circuit pour limiter le nombre de compartiments. </br> **Exemple :**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | string | Le paramètre *aggregationLevel* requiert un *GroupBy*. Le paramètre *aggregationLevel* s’applique à tous les champs de date présents dans le *GroupBy*. </br> **Exemple :**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | string |                                                                     La limite de page est 10000. Prend une valeur inférieure à 10000.  </br> **Exemple :**</br>  `.../search?top=100`                                                                     |
|       skip       | string |                                                                                  Nombre de lignes à ignorer. </br> **Exemple :**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection de ressources de [recherche](partner-center-analytics-resources.md#search-resource) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Voir aussi

- [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)

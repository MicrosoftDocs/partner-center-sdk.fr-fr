---
title: Récupération de toutes les informations analytiques de recherche
description: Obtention de toutes les informations d’analyse de recherche.
ms.assetid: CCF9D929-EE5F-4141-9884-ECA559A5171B
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8237786aceaa19a84abf4277b72ba94debf48e6d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485869"
---
# <a name="get-all-search-analytics-information"></a>Récupération de toutes les informations analytiques de recherche

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


Comment obtenir toutes les informations d’analyse de recherche pour vos clients. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête |
|---------|-------------|
| **Télécharger** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/Search http/1.1 |

 

**Paramètres d’URI**


|    Paramètre     |  Type  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filter      | chaîne |                                                                     Retourne des données correspondant à la condition de filtre. </br> **Exemple :**</br> `.../search?filter=field eq 'value'`                                                                     |
|     groupby      | chaîne |                                         Prend en charge les termes et les dates. La logique de court-circuit pour limiter le nombre de compartiments. </br> **Exemple :**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | chaîne | Le paramètre *aggregationLevel* requiert un *GroupBy*. Le paramètre *aggregationLevel* s’applique à tous les champs de date présents dans le *GroupBy*. </br> **Exemple :**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | chaîne |                                                                     La limite de page est 10000. Prend une valeur inférieure à 10000.  </br> **Exemple :**</br>  `.../search?top=100`                                                                     |
|       skip       | chaîne |                                                                                  Nombre de lignes à ignorer. </br> **Exemple :**</br> `.../search?top=100&skip=100`                                                                                   |
  
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient une collection de ressources de [recherche](partner-center-analytics-resources.md#search_resource) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

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


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>Voir aussi
 - [Analyse de l’espace partenaires-Ressources](partner-center-analytics-resources.md)

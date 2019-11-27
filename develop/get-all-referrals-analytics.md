---
title: Obtient toutes les informations analytiques de références
description: Obtention de toutes les informations analytiques de références.
ms.assetid: C6051714-1D8A-4448-9705-12AEC9A6420E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d5ad0ad0eedcce633940daa6356e2a2e1e9220c5
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485949"
---
# <a name="get-all-referrals-analytics-information"></a>Obtient toutes les informations analytiques de références

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


Obtention de toutes les informations analytiques de référence pour vos clients. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur. 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête |
|---------|-------------|
| **Télécharger** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/Referrals http/1.1 |
 

**Paramètres d’URI**

| Paramètre | Type | Description |
|-----------|------|-------------|
| filter | chaîne | Retourne des données correspondant à la condition de filtre.</br> **Exemple :**</br>  `.../referrals?filter=field eq 'value'` |
| groupby | chaîne |    Prend en charge les termes et les dates. La logique de court-circuit pour limiter le nombre de compartiments.</br> **Exemple :**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | chaîne |   Le paramètre *aggregationLevel* requiert un *GroupBy*. Le paramètre *aggregationLevel* s’applique à tous les champs de date présents dans le *GroupBy*.</br> **Exemple :**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | chaîne | La limite de page est 10000. Prend une valeur inférieure à 10000.</br> **Exemple :**</br> `.../referrals?top=100`</br> |
| skip | chaîne |   Nombre de lignes à ignorer.</br> **Exemple :**</br>  `.../referrals?top=100&skip=100` |

  
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient une collection de ressources de [références](partner-center-analytics-resources.md#referrals) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```


## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>Voir aussi
 - [Analyse de l’espace partenaires-Ressources](partner-center-analytics-resources.md)

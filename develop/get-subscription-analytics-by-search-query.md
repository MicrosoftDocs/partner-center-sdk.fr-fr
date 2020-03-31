---
title: Obtenir une analyse d’abonnement par requête de recherche
description: Comment obtenir des informations d’analyse d’abonnement filtrées par une requête de recherche.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 4cb71638c5ad2c3a708d2eaf874fe904803cd712
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416655"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Obtenir des informations d’analyse d’abonnement filtrées par une requête de recherche

**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


Comment obtenir des informations d’analyse d’abonnement pour vos clients filtrés par une requête de recherche.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.


## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode | URI de demande |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/subscriptions ? Filter = {filter_string} |

 

**Paramètres d’URI**

Utilisez le paramètre de chemin d’accès requis suivant pour identifier votre organisation et filtrer la recherche.

| Nom | Type | Obligatoire | Description |
|------|------|----------|-------------|
| filter_string | chaîne | Oui | Filtre à appliquer à l’analytique d’abonnement. Consultez les sections Syntaxe de filtre et champs de filtre pour connaître la syntaxe, les champs et les opérateurs à utiliser dans ce paramètre. |
 

**Syntaxe de filtre**

Le paramètre de filtre doit être composé d’une série de combinaisons de champs, de valeurs et d’opérateurs. Plusieurs combinaisons peuvent être combinées à l’aide d’opérateurs **and** **ou or.**  

Un exemple non encodé ressemble à ceci :
- Chaîne :? Filter = opérateur de champ’valeur'
- Valeur booléenne :? Filter = champ d’opérateur
- Contains ? Filter = Contains (champ, 'value')


**Filtrer les champs**

Le paramètre de filtre de la requête contient une ou plusieurs instructions qui filtrent les lignes dans la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs **eq** ou **ne**, et certains champs prennent également en charge les opérateurs **contains**, **gt**, **lt**, **ge** et **le**. **Les** instructions peuvent être combinées à l’aide d’opérateurs and **ou or.**

Voici des exemples de chaînes de filtre :  
 
```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```  

Le tableau suivant répertorie les champs pris en charge et les opérateurs de prise en charge pour le paramètre de filtre. Les valeurs de chaîne doivent être entourées de guillemets simples.

| Paramètre | Opérateurs pris en charge | Description |
|-----------|---------------------|-------------|
| CustomerTenantId | EQ, ne | Chaîne au format GUID qui identifie le locataire client. |
| customerName | comprend | Nom du client. |
| customerMarket | EQ, ne | Pays/région dans lequel le client fait des affaires. |
| id | EQ, ne | Chaîne au format GUID qui identifie l’abonnement. |
| statut | EQ, ne | État de l'abonnement. Les valeurs prises en charge sont : « ACTIVE », « SUSPENDed » ou « deprovision ». |
| productName | Contains, EQ, ne | Le nom du produit. |
| subscriptionType | EQ, ne | Type d’abonnement. **Remarque**: ce champ respecte la casse. Les valeurs prises en charge sont : « Office », « Azure », « Microsoft365 », « Dynamics », « EMS ». |
| autoRenewEnabled | EQ, ne | Valeur indiquant si l’abonnement est renouvelé automatiquement. |
| Partenaire | EQ, ne | ID MPN. Pour un revendeur direct, il s’agit de l’ID MPN du partenaire. Pour un revendeur indirect, il s’agit de l’ID MPN du revendeur indirect. |
| friendlyName | comprend | Nom de l'abonnement. |
| partnerName | chaîne | Nom du partenaire pour lequel l’abonnement a été acheté |  
| providerName | chaîne | Lorsque la transaction d’abonnement est destinée au revendeur indirect, le nom du fournisseur est le fournisseur indirect qui a acheté l’abonnement.
| creationDate | eq, ne, gt, lt, ge, le  | Date à laquelle l’abonnement a été créé. |
| effectiveStartDate | eq, ne, gt, lt, ge, le | Date de début de l’abonnement. |
| commitmentEndDate | eq, ne, gt, lt, ge, le  | Date de fin de l’abonnement. |
| currentStateEndDate | eq, ne, gt, lt, ge, le | Date à laquelle l’état actuel de l’abonnement sera modifié. |
| trialToPaidConversionDate | eq, ne, gt, lt, ge, le  | Date à laquelle l’abonnement convertit de l’essai au paiement. La valeur par défaut est null. |
| trialStartDate | eq, ne, gt, lt, ge, le | Date de début de la période d’évaluation de l’abonnement. La valeur par défaut est null. |
| lastUsageDate | eq, ne, gt, lt, ge, le | Date à laquelle l’abonnement a été utilisé pour la dernière fois. La valeur par défaut est null. |
| deprovisionedDate | eq, ne, gt, lt, ge, le | Date à laquelle l’abonnement a été annulé. La valeur par défaut est null. |
| lastRenewalDate | eq, ne, gt, lt, ge, le | Date à laquelle l’abonnement a été renouvelé pour la dernière fois. La valeur par défaut est null. |


**En-têtes de demande** 

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse REST


En cas de réussite, le corps de la réponse contient une collection de ressources d' [abonnement](partner-center-analytics-resources.md#subscription) qui répondent aux critères des filetages.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="span-idsee_alsospan-idsee_alsospan-idsee_alsosee-also"></a><span id="See_Also"/><span id="see_also"/><span id="SEE_ALSO"/>Voir aussi

 - [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)

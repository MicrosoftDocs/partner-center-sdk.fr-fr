---
title: Obtenir une analyse d’abonnement par requête de recherche
description: Comment obtenir des informations d’analyse d’abonnement filtrées par une requête de recherche.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097552"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Obtenir des informations analytiques d’abonnement filtrées par une requête de recherche

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir des informations d’analyse d’abonnement pour vos clients filtrés par une requête de recherche.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête |
|--------|-------------|
| **GET** | [* \{ baseURL \} *](partner-center-rest-urls.md)/Partner/v1/Analytics/subscriptions ? Filter = {filter_string} |

### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez le paramètre de chemin d’accès requis suivant pour identifier votre organisation et filtrer la recherche.

| Nom | Type | Obligatoire | Description |
|------|------|----------|-------------|
| filter_string | string | Oui | Filtre à appliquer à l’analytique d’abonnement. Consultez les sections Syntaxe de filtre et champs de filtre pour connaître la syntaxe, les champs et les opérateurs à utiliser dans ce paramètre. |

### <a name="filter-syntax"></a>Syntaxe des filtres

Le paramètre de filtre doit être composé d’une série de combinaisons de champs, de valeurs et d’opérateurs. Plusieurs combinaisons peuvent être combinées à l’aide d' **`and`** **`or`** opérateurs or.

Voici un exemple d’encodage : 

- Chaîne : `?filter=Field operator 'Value'`
- Booléen : `?filter=Field operator Value`
- Comprend`?filter=contains(field,'value')`

### <a name="filter-fields"></a>Champs de filtrage

Le paramètre filter de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction contient un champ et une valeur associés aux **`eq`** **`ne`** opérateurs ou. Certains champs prennent également en charge les **`contains`** **`gt`** opérateurs,,, **`lt`** **`ge`** et **`le`** . Les instructions peuvent être combinées à l’aide d' **`and`** **`or`** opérateurs or.

Voici des exemples de chaînes de filtre :

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

Le tableau suivant répertorie les champs pris en charge et les opérateurs de prise en charge pour le paramètre de filtre. Les valeurs de chaîne doivent être entourées de guillemets simples.

| Paramètre | Opérateurs pris en charge | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Valeur indiquant si l’abonnement est renouvelé automatiquement. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Date de fin de l’abonnement. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Date à laquelle l’abonnement a été créé. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date à laquelle l’état actuel de l’abonnement sera modifié. |
| customerMarket | `eq`, `ne` | Pays/région dans lequel le client fait des affaires. |
| customerName | `contains` | Nom du client. |
| customerTenantId | `eq`, `ne` | Chaîne au format GUID qui identifie le locataire client. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date à laquelle l’abonnement a été annulé. La valeur par défaut est null. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date de début de l’abonnement. |
| friendlyName | `contains` | Nom de l'abonnement. |
| id | `eq`, `ne` | Chaîne au format GUID qui identifie l’abonnement. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date à laquelle l’abonnement a été renouvelé pour la dernière fois. La valeur par défaut est null. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date à laquelle l’abonnement a été utilisé pour la dernière fois. La valeur par défaut est null. |
| Partenaire | `eq`, `ne` | ID MPN. Pour un revendeur direct, cette valeur sera l’ID MPN du partenaire. Pour un revendeur indirect, cette valeur correspond à l’ID MPN du revendeur indirect. |
| partnerName | string | Nom du partenaire pour lequel l’abonnement a été acheté |
| ProductName | `contains`, `eq`, `ne` | Nom du produit. |
| providerName | string | Lorsque la transaction d’abonnement est destinée au revendeur indirect, le nom du fournisseur est le fournisseur indirect qui a acheté l’abonnement.|
| status | `eq`, `ne` | État de l'abonnement. Les valeurs prises en charge sont : « ACTIVE », « SUSPENDed » ou « deprovision ». |
| subscriptionType | `eq`, `ne` | Type d’abonnement. **Remarque**: ce champ respecte la casse. Les valeurs prises en charge sont : « Office », « Azure », « Microsoft365 », « Dynamics », « EMS ». |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Date de début de la période d’évaluation de l’abonnement. La valeur par défaut est null. |
| trialToPaidConversionDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Date à laquelle l’abonnement convertit de l’essai au paiement. La valeur par défaut est null. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources d' [abonnement](partner-center-analytics-resources.md#subscription-resource) qui répondent aux critères de filtre.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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

## <a name="see-also"></a>Voir aussi

- [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)

---
title: Récupération de l’analyse d’abonnement par dates ou termes
description: Comment faire regrouper les informations d’analyse d’abonnement par dates ou termes.
ms.assetid: 5D0C0649-F64D-40A9-ACCC-2077E2D2BA4E
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 713dceb4c037918f2dfd7793659b70ae8ef3148b
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157221"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Récupération de l’analyse d’abonnement par dates ou termes

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir des informations d’analyse d’abonnement pour vos clients regroupés par dates ou termes.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête |
|--------|-------------|
| **GET** | baseURL/Partner/v1/Analytics/subscriptions ? GroupBy = {groupby_queries} [* \{\}*](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de chemin d’accès requis suivants pour identifier votre organisation et regrouper les résultats.

| Nom | Type | Obligatoire | Description |
|------|------|----------|-------------|
| groupby_queries | paires de chaînes et dateTime | Oui | Termes et dates pour filtrer le résultat. |

### <a name="groupby-syntax"></a>Syntaxe GroupBy

Le paramètre Group by doit être composé d’une série de valeurs de champ séparées par des virgules.

Voici un exemple d’encodage : 

```http
?groupby=termField1,dateField1,termField2
```

Le tableau suivant présente la liste des champs pris en charge pour Group by.

| Champ | Type | Description |
|-------|------|-------------|
| customerTenantId | string | Chaîne au format GUID qui identifie le locataire client. |
| customerName | string | Nom du client. |
| customerMarket | string | Pays/région dans lequel le client fait des affaires. |
| id | string | Chaîne au format GUID qui identifie l’abonnement. |
| status | string | État de l'abonnement. Les valeurs prises en charge sont : « ACTIVE », « SUSPENDed » ou « deprovision ». |
| ProductName | string | Nom du produit. |
| subscriptionType | string | Type d’abonnement. Remarque : ce champ respecte la casse. Les valeurs prises en charge sont : « Office », « Azure », « Microsoft365 », « Dynamics », « EMS ». |
| autoRenewEnabled | Boolean | Valeur indiquant si l’abonnement est renouvelé automatiquement. |
| Partenaire  | string | ID MPN. Pour un revendeur direct, ce paramètre sera l’ID MPN du partenaire. Pour un revendeur indirect, ce paramètre correspond à l’ID MPN du revendeur indirect. |
| friendlyName | string | Nom de l'abonnement. |
| partnerName | string | Nom du partenaire pour lequel l’abonnement a été acheté |
| providerName | string | Lorsque la transaction d’abonnement est destinée au revendeur indirect, le nom du fournisseur est le fournisseur indirect qui a acheté l’abonnement.
| creationDate | Chaîne au format date/heure UTC | Date à laquelle l’abonnement a été créé. |
| effectiveStartDate | Chaîne au format date/heure UTC | Date de début de l’abonnement. |
| commitmentEndDate | Chaîne au format date/heure UTC | Date de fin de l’abonnement. |
| currentStateEndDate | Chaîne au format date/heure UTC | Date à laquelle l’état actuel de l’abonnement sera modifié. |
| trialToPaidConversionDate | Chaîne au format date/heure UTC | Date à laquelle l’abonnement convertit de l’essai au paiement. La valeur par défaut est null. |
| trialStartDate | Chaîne au format date/heure UTC | Date de début de la période d’évaluation de l’abonnement. La valeur par défaut est null. |
| lastUsageDate | Chaîne au format date/heure UTC | Date à laquelle l’abonnement a été utilisé pour la dernière fois. La valeur par défaut est null. |
| deprovisionedDate | Chaîne au format date/heure UTC | Date à laquelle l’abonnement a été annulé. La valeur par défaut est null. |
| lastRenewalDate | Chaîne au format date/heure UTC | Date à laquelle l’abonnement a été renouvelé pour la dernière fois. La valeur par défaut est null. |

### <a name="filter-fields"></a>Champs de filtrage

Le tableau suivant répertorie les champs de filtre facultatifs et leurs descriptions :

| Champ | Type |  Description |
|-------|------|--------------|
| top | int | Le nombre de lignes de données à renvoyer dans la requête. Si la valeur n’est pas spécifiée, la valeur maximale et la valeur par défaut sont 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. |
| skip | int | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, Top = 10000 et Skip = 0 récupère les 10000 premières lignes de données, Top = 10000 et Skip = 10000 récupère les 10000 lignes de données suivantes. |
| Filter | string | Une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction de filtre contient un nom de champ du corps de la réponse et une valeur associée à **`eq`**, **`ne`** ou pour certains champs, l' **`contains`** opérateur. Les instructions peuvent être combinées à l’aide **`and`** de ou de **`or`**. Les valeurs de chaîne doivent être entourées par des guillemets dans le paramètre filter. Consultez la section suivante pour obtenir la liste des champs qui peuvent être filtrés et les opérateurs pris en charge avec ces champs. |
| aggregationLevel | string | Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : **day**, **week** ou **month**. Si la valeur n’est pas spécifiée, la valeur par défaut est **dateRange**. **Remarque**: ce paramètre s’applique uniquement quand un champ de date est passé dans le cadre du paramètre GroupBy. |
| Comportant | string | Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection de ressources d' [abonnement](partner-center-analytics-resources.md#subscription-resource) regroupées selon les conditions et les dates spécifiées.

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
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Voir aussi

[Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)

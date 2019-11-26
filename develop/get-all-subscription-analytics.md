---
title: Get all subscription analytics information
description: How to get all the subscription analytics information.
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a6b3d77dc23a0246d168979f754a3c1be5a2a02d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485849"
---
# <a name="get-all-subscription-analytics-information"></a>Get all subscription analytics information

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

This topic describes how to get all the subscription analytics information for your customers.

## <a name="prerequisites"></a>Conditions préalables

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with User credentials only.

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

The following table lists optional parameters and their descriptions:

| Paramètre | Tapez |  Description |
|-----------|------|--------------|
| top | entier | Le nombre de lignes de données à renvoyer dans la requête. If the value is not specified, the maximum value and the default value are `10000`. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. |
| skip | entier | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data. |
| filter | chaîne | Une ou plusieurs instructions qui filtrent les lignes de la réponse. Each filter statement contains a field name from the response body and a value that are associated with the **eq**, **ne**, or for certain fields, the **contains** operator. Les instructions peuvent être combinées à l’aide des opérateurs **and** ou **or**. Les valeurs de chaîne doivent être entourées par des guillemets dans le paramètre **filter**. See the following section for a list of fields that can be filtered and the operators that are supported with those fields. |
| aggregationLevel | chaîne | Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : **day**, **week** ou **month**. If the value is not specified, the default is **dateRange**. This parameter applies only when a date field is passed as part of the **groupBy** parameter. |
| groupBy | chaîne | Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. |

### <a name="request-headers"></a>En-têtes de requête

See [Headers](headers.md) for more information.

### <a name="request-body"></a>Corps de la requête

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST response

If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription) resources.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Articles associés

- [Partner Center Analytics - Resources](partner-center-analytics-resources.md)

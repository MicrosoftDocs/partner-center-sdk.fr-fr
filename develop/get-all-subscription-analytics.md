---
title: Récupération de toutes les informations d’analyse d’abonnement
description: Obtention de toutes les informations d’analyse d’abonnement.
ms.assetid: 243E54BD-EA34-400E-B9AB-D735EB46B9F6
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 051103450cc0d13dc8a5bc6d77047fc3f6907768
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416058"
---
# <a name="get-all-subscription-analytics-information"></a>Récupération de toutes les informations d’analyse d’abonnement

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette rubrique explique comment obtenir toutes les informations d’analyse d’abonnement pour vos clients.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification avec les informations d’identification de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande |
|--------|-------------|
| **GET** | [ *\{baseURL\}* ](partner-center-rest-urls.md)/Partner/v1/Analytics/subscriptions http/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

Le tableau suivant répertorie les paramètres facultatifs et leurs descriptions :

| Paramètre | Type |  Description |
|-----------|------|--------------|
| top | int | Le nombre de lignes de données à renvoyer dans la requête. Si la valeur n’est pas spécifiée, la valeur maximale et la valeur par défaut sont `10000`. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. |
| skip | int | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, `top=10000` et `skip=0` récupère les 10000 premières lignes de données, `top=10000` et `skip=10000` récupère les 10000 lignes de données suivantes. |
| filtre | chaîne | Une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction de filtre contient un nom de champ du corps de la réponse et une valeur associée à l’opérateur **EQ** **, ne, ou**pour certains champs, l’opérateur **Contains** . Les instructions peuvent être combinées à l’aide des opérateurs **and** ou **or**. Les valeurs de chaîne doivent être entourées par des guillemets dans le paramètre **filter**. Consultez la section suivante pour obtenir la liste des champs qui peuvent être filtrés et les opérateurs pris en charge avec ces champs. |
| aggregationLevel | chaîne | Indique la plage de temps pendant laquelle récupérer les données agrégées. Il peut s’agit des chaînes suivantes : **day**, **week** ou **month**. Si la valeur n’est pas spécifiée, la valeur par défaut est **dateRange**. Ce paramètre s’applique uniquement quand un champ de date est passé dans le cadre du paramètre **GroupBy** . |
| Comportant | chaîne | Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de demande

None.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources d' [**abonnement**](partner-center-analytics-resources.md#subscription) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

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

## <a name="see-also"></a>Voir aussi

- [Analytique de l’Espace partenaires - Ressources](partner-center-analytics-resources.md)

---
title: Obtenir un résumé de l’utilisation d’un partenaire
description: Vous pouvez utiliser la ressource PartnerUsageSummary pour obtenir un résumé de l’utilisation des partenaires pour tous les clients qui ont acheté un service ou une ressource Azure spécifique au cours de la période de facturation en cours.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2e31c21001fc009b1bc4c380514102158f29724d
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155271"
---
# <a name="get-a-usage-summary-for-a-partner"></a>Obtenir un résumé de l’utilisation d’un partenaire

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la ressource **PartnerUsageSummary** pour obtenir un résumé de l’utilisation des partenaires pour tous les clients qui ont acheté un service ou une ressource Azure spécifique au cours de la période de facturation en cours.

*Le total renvoyé par cette API ne retourne pas de consommation pour les clients disposant d’un plan Azure.* Prévue pour la désapprobation à l’avenir.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.

## <a name="c"></a>C\#

Pour obtenir un résumé de l’utilisation de tous les clients qui ont acheté un service ou une ressource Azure spécifique au cours de la période de facturation actuelle :

1. Utilisez votre **collection iaggregatepartner**.

2. Appelez la propriété **UsageSummary** , suivie des méthodes d' **extraction ()** ou de **GetAsync ()** :

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetPartnerUsageSummary.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                         |
|---------|---------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une ressource **PartnerUsageSummary** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```

---
title: Obtenir le résumé de l’utilisation de l’abonnement du client
description: Vous pouvez utiliser la ressource SubscriptionUsageSummary pour obtenir un résumé de l’utilisation des abonnements d’un service ou d’une ressource Azure spécifique pendant la période de facturation en cours.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c2890b1fc57686c08bf7fe0e0dfed0c50dc880b6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487669"
---
# <a name="get-usage-summary-for-customers-subscription"></a>Obtenir le résumé de l’utilisation de l’abonnement du client

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la ressource **SubscriptionUsageSummary** pour obtenir un résumé de l’utilisation des abonnements pour un client. Cette ressource représente le résumé de l’utilisation de l’abonnement d’un service ou d’une ressource Azure spécifique au cours de la période de facturation en cours.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Identificateur du client (**Customer-client-ID**). Si vous n’avez pas d’identificateur de client, vous pouvez rechercher l’identificateur dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant **compte**, puis en enregistrant son **ID Microsoft**.
- Un identificateur d’abonnement

## <a name="c"></a>\# C

Pour obtenir un résumé de l’utilisation des abonnements pour l’abonnement d’un client :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** .
2. Appelez ensuite la propriété Subscriptions, ainsi que la propriété **UsageSummary** . Terminez en appelant les méthodes d’extraction () ou GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetSubscriptionUsageSummary.cs**

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande REST

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{subscription-ID}/usagesummary http/1.1 |

##### <a name="uri-parameters"></a>Paramètres d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir les informations d’utilisation évaluées du client.

| Nom                   | Type     | Obligatoire | Description                               |
|------------------------|----------|----------|-------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | GUID correspondant au client.     |
| **ID d’abonnement**    | **uniques** | Y        | GUID correspondant à l’identificateur d’un abonnement. Pour un plan Azure, il s’agit de l’identificateur de la ressource d' [abonnement](subscription-resources.md#subscription)Partner Center correspondante, qui représente le plan Azure. *Pour les ressources d’abonnement de plan Azure, indiquez l' **ID de plan** en tant qu' **ID d’abonnement** dans cet itinéraire.* |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md).

#### <a name="request-body"></a>Corps de la requête

Aucun.

#### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource **SubscriptionUsageSummary** dans le corps de la réponse.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

#### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Exemple de réponse pour les abonnements Microsoft Azure (MS-AZR-0145P)

Dans cet exemple, le client a acheté une offre **145P Azure PayG** .

*Pour les clients avec des abonnements Microsoft Azure (MS-AZR-0145P), aucune modification n’est apportée à la réponse de l’API.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Exemple de réponse pour le plan Azure

Dans cet exemple, le client a acheté un plan Azure.

*Pour les clients disposant de plans Azure, il existe les modifications de réponse d’API suivantes :*

- **currencyLocale** est remplacé par **currencyCode**
- **usdTotalCost** est un nouveau champ

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
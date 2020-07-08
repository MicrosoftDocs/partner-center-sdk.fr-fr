---
title: Obtenir tous les enregistrements d’utilisation d’abonnement d’un client
description: Vous pouvez utiliser la collection de ressources SubscriptionMonthlyUsageRecord pour obtenir les enregistrements d’utilisation d’abonnement pour un client d’un service ou d’une ressource Azure spécifique pendant la période de facturation en cours.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098259"
---
# <a name="get-subscription-usage-records-for-a-customer"></a>Obtenir les enregistrements d’utilisation d’abonnement pour un client

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la collection de ressources **SubscriptionMonthlyUsageRecord** pour obtenir les enregistrements d’utilisation d’abonnement pour un client d’un service ou d’une ressource Azure spécifique pendant la période de facturation en cours. Cette ressource représente tous les abonnements pour le client. Pour un client disposant d’un plan Azure, cette ressource renvoie une liste de ces plans (pas les abonnements Azure individuels).

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour obtenir les enregistrements d’utilisation d’abonnement pour un client d’un service ou d’une ressource Azure spécifique pendant la période de facturation en cours. :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** .

2. Appelez ensuite la propriété **Subscriptions** , ainsi que la propriété **UsageRecords** . Terminez en appelant les méthodes d’extraction () ou GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetSubscriptionUsageRecords.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/usagerecords http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie le paramètre de requête requis pour obtenir les informations d’utilisation évaluées du client.

| Nom                   | Type     | Obligatoire | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | O        | GUID correspondant au client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource **SubscriptionMonthlyUsageRecord** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Exemple de réponse pour les abonnements Microsoft Azure (MS-AZR-0145P)

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
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Exemple de réponse REST pour le plan Azure

Dans cet exemple, le client a acheté un plan Azure.

*Pour les clients disposant de plans Azure, les modifications suivantes ont été apportées à la réponse de l’API :*

- **currencyLocale** est remplacé par **currencyCode**
- **usdTotalCost** est un nouveau champ

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

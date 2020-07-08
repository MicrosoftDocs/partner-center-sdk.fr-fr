---
title: Obtenir un récapitulatif de l’utilisation de tous les abonnements d’un client
description: Vous pouvez utiliser la ressource CustomerUsageSummary pour obtenir l’utilisation par un client d’un service ou d’une ressource Azure spécifique au cours de la période de facturation en cours.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098235"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>Obtenir un récapitulatif de l’utilisation de tous les abonnements d’un client

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la ressource **CustomerUsageSummary** pour obtenir l’utilisation par un client d’un service ou d’une ressource Azure spécifique au cours de la période de facturation en cours.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour obtenir un résumé de l’utilisation de tous les abonnements d’un client :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** .

2. Appelez la propriété **UsageSummary** , suivie des méthodes d' **extraction ()** ou de **GetAsync ()** :

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetCustomerUsageSummary.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagesummary http/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource **CustomerUsageSummary** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Exemple de réponse pour l’abonnement Microsoft Azure (MS-AZR-0145P)

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
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Exemple de réponse pour le plan Azure

Dans cet exemple, le client a acheté un plan Azure.

*Pour les clients avec des plans Azure, les modifications suivantes ont été apportées à la réponse de l’API :*

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
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```

---
title: Obtenir le budget des dépenses d’utilisation d’un client
description: Vous pouvez utiliser un budget de dépense (l’objet SpendingBudget) pour mettre à jour un résumé de l’utilisation des clients (la ressource CustomerUsageSummary).
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8aaf5d03fd80a7760e3a7648bac0cda723b5d523
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489809"
---
# <a name="get-a-customers-usage-spending-budget"></a>Obtenir le budget des dépenses d’utilisation d’un client

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez mettre à jour le budget des dépenses (objet **SpendingBudget** ) dans le résumé de l' [utilisation du client (la ressource **CustomerUsageSummary** )](customer-usage-resources.md#customerusagesummary).

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client (**Customer-client-ID**). Si vous n’avez pas d’identificateur de client, vous pouvez rechercher l’identificateur dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant **compte**, puis en enregistrant son **ID Microsoft**.

## <a name="c"></a>\# C

Pour mettre à jour le budget des dépenses d’utilisation d’un client :

1. Créez un nouvel objet [**SpendingBudget**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) avec le montant mis à jour.
2. Utilisez la collection [**collection iaggregatepartner. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) pour appeler la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client spécifié.
3. Appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) [**pour connaître le**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) budget d’utilisation du client.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{  
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande REST

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/usagebudget http/1.1 |

##### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour mettre à jour le profil de facturation.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md).

#### <a name="request-body"></a>Corps de la requête

Ressource complète.

#### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne le budget des dépenses d’un utilisateur avec le montant mis à jour.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```

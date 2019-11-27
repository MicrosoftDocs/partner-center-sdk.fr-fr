---
title: Récupération de tous les enregistrements d’utilisation mensuelle pour un abonnement.
description: Vous pouvez utiliser la collection de ressources AzureResourceMonthlyUsageRecord pour obtenir la liste des services inclus dans l’abonnement d’un client et les informations d’utilisation évaluées qui lui sont associées.
ms.assetid: 037D71B9-8E8B-4BC0-8388-9CBC97218CED
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0acd284c1b829330283d2012fcb6a85d3553f763
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485969"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a>Récupération de tous les enregistrements d’utilisation mensuelle pour un abonnement.

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la collection de ressources [**AzureResourceMonthlyUsageRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) pour obtenir la liste des services inclus dans l’abonnement d’un client et les informations d’utilisation évaluées qui lui sont associées.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client (**Customer-client-ID**). Si vous n’avez pas d’identificateur de client, vous pouvez rechercher l’identificateur dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant **compte**, puis en enregistrant son **ID Microsoft**.
- Identificateur d’abonnement.

*Cette API prend en charge uniquement les abonnements Microsoft Azure (MS-AZR-0145P). Si vous utilisez un plan Azure, consultez [obtenir des données d’utilisation pour l’abonnement par compteur à](get-a-customer-subscription-meter-usage-records.md) la place.*

## <a name="c"></a>\# C

Pour obtenir les informations d’utilisation des ressources d’un abonnement :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** . 
2. Appelez la propriété **Subscriptions** , ainsi que **UsageRecords**, puis la propriété **Resources** . 
3. Appelez les méthodes d' **extraction ()** ou de **GetAsync ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **PartnerSDK. FeatureSample**
- Classe : **SubscriptionResourceUsageRecords.cs**

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande REST

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-subscription}/usagerecords/Resources http/1.1 |

##### <a name="uri-parameters"></a>Paramètres d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir les informations d’utilisation évaluées.

| Nom                    | Type     | Obligatoire | Description                               |
|-------------------------|----------|----------|-------------------------------------------|
| **client-locataire-ID**  | **uniques** | Y        | GUID correspondant au client.     |
| **ID d’abonnement** | **uniques** | Y        | GUID correspondant à l’abonnement. |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md).

#### <a name="request-body"></a>Corps de la requête

Aucun.

#### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources **AzureResourceMonthlyUsageRecord** dans le corps de la réponse.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```

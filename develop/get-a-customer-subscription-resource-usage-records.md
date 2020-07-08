---
title: Obtenir les données d’utilisation d’abonnement par ressource
description: Vous pouvez utiliser la ressource ResourceUsageRecord pour obtenir les enregistrements d’utilisation des ressources d’un client pour des services ou des ressources Azure spécifiques pendant la période de facturation en cours.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098267"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>Obtenir les données d’utilisation d’abonnement par ressource

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment récupérer la ressource **ResourceUsageRecord** . Cette ressource représente un total agrégé du mois pour les ressources individuelles approvisionnées dans votre plan Azure. Vous pouvez utiliser cette ressource pour obtenir les enregistrements d’utilisation des ressources d’un client pour des services ou des ressources Azure spécifiques pendant la période de facturation en cours. Cette API retourne des données qui n’étaient pas disponibles précédemment via les API de dépense Azure.

*Cet itinéraire ne prend pas en charge les abonnements Microsoft Azure (MS-AZR-0145P).*

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Un identificateur d’abonnement

## <a name="c"></a>C\#

Pour obtenir les enregistrements d’utilisation des ressources d’un client pour un service ou une ressource Azure spécifique au cours de la période de facturation actuelle :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** .

2. Appelez la propriété Subscriptions, ainsi que **UsageRecords**, puis la propriété **Resources** . Terminez en appelant les méthodes d’extraction () ou GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{subscription-ID}/resourceusagerecords http/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir les informations d’utilisation évaluées du client.

| Nom                   | Type     | Obligatoire | Description                               |
|------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id** | **guid** | O        | GUID correspondant au client.     |
| **ID d’abonnement**    | **guid** | O        | GUID correspondant à l’identificateur d’une [ressource d’abonnement](subscription-resources.md#subscription)de l’espace partenaires, qui représente un abonnement Microsoft Azure (MS-AZR-0145P) ou un plan Azure. *Pour les ressources d’abonnement de plan Azure, indiquez l' **ID de plan** en tant qu' **ID d’abonnement** dans cet itinéraire.* |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource **PagedResourceCollection \<ResourceUsageRecord> ** dans le corps de la réponse.

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
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

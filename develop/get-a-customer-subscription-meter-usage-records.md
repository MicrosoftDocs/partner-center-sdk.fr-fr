---
title: Obtenir les données d’utilisation d’abonnement par compteur
description: Vous pouvez utiliser la collection de ressources MeterUsageRecord pour obtenir les enregistrements d’utilisation de compteur d’un client pour des services ou des ressources Azure spécifiques pendant la période de facturation en cours.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098270"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Obtenir les données d’utilisation d’abonnement par compteur

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser la collection de ressources **MeterUsageRecord** pour obtenir les enregistrements d’utilisation de compteur d’un client pour des services ou des ressources Azure spécifiques pendant la période de facturation en cours. Cette collection de ressources représente un total agrégé pour chaque compteur du cycle de facturation actuel, sur l’ensemble de votre plan Azure.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Un ID d’abonnement

*Ce nouvel itinéraire est équivalent à `subscriptions/{subscription-id}/usagerecords/resources` , qui continuera à fonctionner uniquement pour les abonnements Microsoft Azure (MS-AZR-0145P).* Ce nouvel itinéraire prendra en charge à la fois les abonnements Microsoft Azure (MS-AZR-0145P) et les plans Azure. Pour obtenir ces informations pour votre plan Azure, vous devez passer à ce nouvel itinéraire. À part les propriétés mentionnées dans les sections suivantes, la réponse est la même que l’ancien itinéraire.

## <a name="c"></a>C\#

Pour obtenir les enregistrements d’utilisation de compteur d’un client pour un service ou une ressource Azure spécifique pendant la période de facturation actuelle :

1. Utilisez votre collection **collection iaggregatepartner. Customers** pour appeler la méthode **méthode BYID ()** .

2. Appelez la propriété subscriptions et **UsageRecords**, puis la propriété **mètres** . Terminez en appelant les méthodes d’extraction () ou GetAsync ().

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Pour obtenir un exemple, consultez l’exemple suivant :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{subscription-ID}/meterusagerecords http/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource **PagedResourceCollection \<MeterUsageRecord> ** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Exemple de réponse pour les abonnements Microsoft Azure (MS-AZR-0145P)

Dans cet exemple, le client a acheté **145P Azure PayG**.

*Pour les clients disposant d’un abonnement Microsoft Azure (MS-AZR-0145P), aucune modification n’est apportée à la réponse de l’API.*

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
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
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
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

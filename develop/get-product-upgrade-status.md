---
title: Obtenir l’état de mise à niveau du produit pour un client
description: Vous pouvez utiliser la ressource ProductUpgradeRequest pour déterminer l’état d’une mise à niveau de produit pour un client vers une nouvelle famille de produits, par exemple d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 5ae177c5c57ba12de80884aed3697102a5b1f914
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487289"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Obtenir l’état de mise à niveau du produit pour un client

S’applique à :

- Espace partenaires

Vous pouvez utiliser la ressource [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) pour obtenir l’état d’une mise à niveau vers une nouvelle famille de produits. Cette ressource s’applique lorsque vous mettez à niveau un client à partir d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure. Une demande réussie retourne la ressource [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur. Suivez le [modèle d’application sécurisée](enable-secure-app-model.md) lors de l’utilisation de l’authentification d’application + utilisateur avec les API de l’espace partenaires.
- Identificateur du client.
- Famille de produits.
- L’ID de mise à niveau d’une demande de mise à niveau.

## <a name="c"></a>\# C

Pour vérifier si un client est éligible pour la mise à niveau vers Azure plan :

1. Créez un objet **ProductUpgradesRequest** et spécifiez l’identificateur du client et « Azure » comme famille de produits.
2. Utilisez la collection **collection iaggregatepartner. ProductUpgrades** .
2. Appelez la méthode **méthode BYID** et transmettez l' **ID de mise à niveau**.
3. Appelez la méthode **CheckStatus** et transmettez l’objet **ProductUpgradesRequest** , qui renverra un objet **ProductUpgradeStatus** .

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```
```

## REST

### REST request

#### Request syntax

| Method   | Request URI |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

#### URI parameter

Use the following query parameter to specify the customer for whom you're getting a product upgrade status.

| Name               | Type | Required | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **upgrade-id** | GUID | Yes | The value is a GUID-formatted upgrade identifier. You can use this identifier to specify an upgrade to track. |

#### Request headers

For more information, see [Partner Center REST headers](headers.md).

#### Request body

The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.

#### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) dans le corps.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```

---
title: Vérifier l’éligibilité d’un client pour la mise à niveau vers un plan Azure
description: Vous pouvez utiliser la ressource ProductUpgradeRequest pour retourner une ressource ProductUpgradesEligibility afin de déterminer si un client est éligible pour la mise à niveau d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: b94aa50364ef770a843624d397240e35eaa8cecf
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415940"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Vérifier l’éligibilité d’un client pour la mise à niveau vers un plan Azure

S'applique à :

- Centre pour partenaires

Vous pouvez utiliser la ressource [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) pour vérifier si un client est autorisé à effectuer une mise à niveau vers un plan Azure à partir d’un abonnement Microsoft Azure (MS-AZR-0145P). cette méthode renvoie une ressource [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) avec l’éligibilité à la mise à niveau du produit du client.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur. Suivez le [modèle d’application sécurisée](enable-secure-app-model.md) lors de l’utilisation de l’authentification d’application + utilisateur avec les API de l’espace partenaires.
- Identificateur du client.
- Famille de produits.

## <a name="c"></a>C\#

Pour vérifier si un client est éligible pour la mise à niveau vers Azure plan :

1. Créez un objet **ProductUpgradesRequest** et spécifiez l’identificateur du client et « Azure » comme famille de produits.
2. Utilisez la collection **collection iaggregatepartner. ProductUpgrades** .
3. Appelez la méthode **CheckEligibility** et transmettez l’objet **ProductUpgradesRequest** , qui renverra un objet **ProductUpgradesEligibility** .

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande REST

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de demande                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/productUpgrades/Eligibility http/1.1 |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

#### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir une ressource [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .

#### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```

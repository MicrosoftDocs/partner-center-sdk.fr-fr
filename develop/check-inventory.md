---
title: Vérifier l’inventaire
description: Vérifiez l’inventaire pour un ensemble spécifique d’éléments de catalogue.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5d874b1d69750a08506669061573e511dd6704de
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154621"
---
# <a name="check-inventory"></a>Vérifier l’inventaire

**S’applique à :**

- Espace partenaires

Comment vérifier l’inventaire pour un ensemble spécifique d’éléments de catalogue.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ou plusieurs ID de produit. Vous pouvez également spécifier des ID de référence (SKU).

- Tout contexte supplémentaire nécessaire pour vérifier l’inventaire des références (SKU) référencées par le ou les ID de produit/SKU fournis. Ces exigences peuvent varier selon le type de produit/référence et peuvent être déterminées à partir de la propriété **InventoryVariables** [de la référence SKU](product-resources.md#sku) .

## <a name="c"></a>C\#

Pour vérifier l’inventaire, générez un objet [InventoryCheckRequest](product-resources.md#inventorycheckrequest) à l’aide d’un objet [InventoryItem](product-resources.md#inventoryitem) pour chaque élément à vérifier. Utilisez ensuite un accesseur **collection iaggregatepartner. extensions** , délimitez-le à **Product** , puis sélectionnez le pays à l’aide de la méthode **ByCountry ()** . Enfin, appelez la méthode **CheckInventory ()** avec votre objet **InventoryCheckRequest** .

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/Product/checkInventory ? pays = {country-code} http/1.1                        |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour vérifier l’inventaire.

| Nom                   | Type     | Obligatoire | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| pays-code           | string   | Oui      | ID de pays/région.                                            |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Détails de la demande d’inventaire, comprenant une ressource [InventoryCheckRequest](product-resources.md#inventorycheckrequest) contenant une ou plusieurs ressources [InventoryItem](product-resources.md#inventoryitem) .

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection d’objets [InventoryItem](product-resources.md#inventoryitem) renseignés avec les détails de la restriction, le cas échéant.

>[!NOTE]
>Si un InventoryItem d’entrée représente un élément qui est introuvable dans le catalogue, il n’est pas inclus dans la collection de sortie.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2001         | Le corps de la demande est manquant.                                                                              |
| 400                  | 400026       | Un élément de contexte d’inventaire requis est manquant.                                                             |

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
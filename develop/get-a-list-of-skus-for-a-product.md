---
title: Obtenir la liste des références SKU d’un produit (par pays)
description: Vous pouvez obtenir et filtrer une collection de références SKU par pays pour un produit à l’aide des API de l’espace partenaires.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098058"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Obtenir la liste des références SKU d’un produit (par pays)

**S’applique à :**

- Espace partenaires

Vous pouvez obtenir un ensemble de références SKU disponibles dans un pays pour un produit spécifique à l’aide des API de l’espace partenaires.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Identificateur de produit.

## <a name="c"></a>C\#

Pour obtenir la liste des références SKU pour un produit :

1. Obtenir une interface pour les opérations d’un produit spécifique en suivant les étapes de la section [obtenir un produit par ID](get-a-product-by-id.md).

2. À partir de l’interface, sélectionnez la propriété **SKU** pour obtenir une interface avec les opérations disponibles pour les références (SKU).

3. Appelez la méthode **obtenir ()** ou **GetAsync ()** pour récupérer une collection des références (SKU) disponibles pour le produit.

4. Facultatif Sélectionnez l’étendue de la réservation à l’aide de la méthode **ByReservationScope ()** .

5. Facultatif Utilisez la méthode **ByTargetSegment ()** pour filtrer les références SKU par segment cible avant d’appeler la méthode d' **extraction ()** ou de **GetAsync ()**.

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour obtenir la liste des références SKU pour un produit :

1. Obtenir une interface pour les opérations d’un produit spécifique en suivant les étapes de la section [obtenir un produit par ID](get-a-product-by-id.md).

2. À partir de l’interface, sélectionnez la fonction **getSkus** pour obtenir une interface avec les opérations disponibles pour les références (SKU).

3. Appelez la fonction **obtenir ()** pour récupérer une collection des références (SKU) disponibles pour le produit.

4. Facultatif Utilisez la fonction **byTargetSegment ()** pour filtrer les références SKU par segment cible avant d’appeler la fonction d' **extraction ()** .

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour obtenir la liste des références SKU pour un produit :

1. Exécutez la commande [**PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) .

2. Facultatif Spécifiez le paramètre de **segment** pour filtrer les références SKU par segment cible.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs ? Country = {pays-code} &targetSegment = {Target-segment} http/1.1  |

#### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez le chemin d’accès et les paramètres de requête suivants pour obtenir la liste des références (SKU) d’un produit.

| Nom                   | Type     | Obligatoire | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ID de produit             | string   | Oui      | Chaîne qui identifie le produit.                           |
| pays-code           | string   | Oui      | ID de pays/région.                                            |
| segment cible         | string   | No       | Chaîne qui identifie le segment cible utilisé pour le filtrage. |
| reservationScope | string   | No | Lors de l’interrogation d’une liste de références SKU pour un produit de réservation Azure, spécifiez `reservationScope=AzurePlan` pour obtenir la liste des références (SKU) applicables à AzurePlan. Excluez ce paramètre pour obtenir la liste des références (SKU) pour les produits de réservation Azure applicables aux abonnements Microsoft Azure (MS-AZR-0145P).  |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-examples"></a>Exemples de demande

Obtenir la liste des références (SKU) pour un produit donné :

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Obtenir la liste des références (SKU) pour un produit de réservation Azure. Incluez uniquement les références (SKU) applicables aux abonnements Azure et non Microsoft Azure (MS-AZR-0145P) :

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Obtenir la liste des références (SKU) pour un produit de réservation Azure. Incluez uniquement les références (SKU) applicables aux abonnements Microsoft Azure (MS-AZR-0145P) et non aux plans Azure :

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources [SKU](product-resources.md#sku) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | L’accès au targetSegment demandé n’est pas autorisé.                                                     |
| 404                  | 400013       | Le produit parent est introuvable.                                                                         |

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

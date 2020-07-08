---
title: Obtenir la liste des disponibilités d’une référence SKU (par pays)
description: Comment obtenir une collection de disponibilités pour le produit et la référence SKU spécifiés par le pays du client.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098184"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Obtenir la liste des disponibilités d’une référence SKU (par pays)

**S’applique à :**

- Espace partenaires

Cet article explique comment obtenir une collection de disponibilités dans un pays particulier pour un produit et une référence SKU spécifiés.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Identificateur de produit.

- Identificateur de référence (SKU).

- Un pays.

## <a name="c"></a>C\#

Pour obtenir la liste des [disponibilités](product-resources.md#availability) pour une [référence (SKU](product-resources.md#sku)) :

1. Suivez les étapes de la section [obtenir une référence SKU par ID](get-a-sku-by-id.md) pour obtenir l’interface pour les opérations d’une référence (SKU) spécifique.

2. À partir de l’interface de référence (SKU), sélectionnez la propriété **availabilities** pour obtenir une interface avec les opérations pour Availabilities.

3. Facultatif Utilisez la méthode **ByTargetSegment ()** pour filtrer les disponibilités par segment cible.

4. Appelez **obtenir ()** ou **GetAsync ()** pour récupérer une collection des availabilities pour cette référence (SKU).

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities ? Country = {pays-code} &targetSegment = {Target-segment} http/1.1     |

### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez le chemin d’accès et les paramètres de requête suivants pour obtenir une liste des disponibilités pour une référence (SKU).

| Nom                   | Type     | Obligatoire | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ID de produit             | string   | Oui      | Chaîne qui identifie le produit.                           |
| Réf. SKU                 | string   | Oui      | Chaîne qui identifie la référence (SKU).                               |
| pays-code           | string   | Oui      | ID de pays/région.                                            |
| segment cible         | string   | No       | Chaîne qui identifie le segment cible utilisé pour le filtrage. |
| reservationScope | string   | No | Lors de l’interrogation d’une liste de disponibilités pour une référence (SKU) de réservation Azure, spécifiez `reservationScope=AzurePlan` pour obtenir une liste des disponibilités applicables à AzurePlan. Excluez ce paramètre pour obtenir une liste des disponibilités applicables aux abonnements Microsoft Azure (MS-AZR-0145P).  |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-examples"></a>Exemples de demande

#### <a name="availabilities-for-sku-by-country"></a>Disponibilités pour les références SKU par pays

Suivez cet exemple pour obtenir une liste des disponibilités pour une référence (SKU) donnée par pays :

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>Disponibilités pour les réservations de machines virtuelles (plan Azure)

Suivez cet exemple pour obtenir une liste des disponibilités par pays pour les références SKU de réservation de machines virtuelles Azure. Cet exemple concerne les références (SKU) qui s’appliquent aux plans Azure :

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Disponibilités pour les réservations de machines virtuelles pour les abonnements Microsoft Azure (MS-AZR-0145P)

Suivez cet exemple pour obtenir une liste des disponibilités par pays pour les réservations de machines virtuelles Azure applicables aux abonnements Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources de [**disponibilité**](product-resources.md#availability) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | L’accès au **targetSegment** demandé n’est pas autorisé.                                                     |

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
            "defaultCurrency": {
                "code": "USD",
                "symbol": "$"
            },
            "segment": "commercial",
            "country": "US",
            "isPurchasable": true,
            "isRenewable": false,
            "terms": [{
                "duration": "P1Y",
                "description": "1 Year Prepaid"
            }],
            "product": { ... },
            "sku": { ... },
            "links": {
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

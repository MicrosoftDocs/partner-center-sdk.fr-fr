---
title: Recevoir une disponibilité par ID
description: Obtient une disponibilité pour le produit et la référence SKU spécifiés à l’aide d’un ID de disponibilité.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cff15d30a7fc218a2b6a12e50cc016dec3c8fe98
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416050"
---
# <a name="get-an-availability-by-id"></a>Recevoir une disponibilité par ID 

**S’applique à**

- Centre pour partenaires

Obtient une disponibilité pour le produit et la référence SKU spécifiés à l’aide d’un ID de disponibilité.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID de produit. 
- ID DE RÉFÉRENCE (SKU). 
- Un ID de disponibilité. 

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>exemples

### <a name="c"></a>C# 

Pour obtenir des détails sur une [disponibilité](product-resources.md#availability)spécifique, commencez par suivre les étapes de la section [obtenir une référence SKU par ID](get-a-sku-by-id.md) pour obtenir l’interface pour les opérations [d’une référence (SKU](product-resources.md#sku) ) spécifique. À partir de l’interface obtenue, sélectionnez la propriété **availabilities** pour obtenir une interface avec les opérations disponibles pour Availabilities. Après cela, transmettez l’ID de disponibilité à la méthode **méthode BYID ()** pour obtenir les opérations pour cette disponibilité spécifique, puis appelez la méthode **obtenir ()** ou **GetAsync (** ) pour récupérer les détails de disponibilité.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId; 
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour obtenir des détails sur une [disponibilité](product-resources.md#availability)spécifique, commencez par suivre les étapes de la section [obtenir une référence SKU par ID](get-a-sku-by-id.md) pour obtenir l’interface pour les opérations [d’une référence (SKU](product-resources.md#sku) ) spécifique. À partir de l’interface obtenue, sélectionnez la fonction **getAvailabilities** pour obtenir une interface avec les opérations disponibles pour Availabilities. Après cela, transmettez l’ID de disponibilité à la fonction **méthode BYID ()** pour obtenir les opérations pour cette disponibilité spécifique, puis appelez la fonction **obtenir ()** pour récupérer les détails de disponibilité.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId; 
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour obtenir des détails sur une [disponibilité](product-resources.md#availability)spécifique, exécutez la [**PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) et spécifiez les **paramètres AvailabilityId**, **CountryCode**, **ProductID**et **SkuID** pour récupérer les détails de disponibilité.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST

**Syntaxe de la requête**

| Méthode  | URI de demande |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Products/{Product-ID}/SKUs/{SKU-ID}/availabilities/{Availability-ID} ? pays = {country-code} http/1.1         |

**Paramètre URI**

Utilisez le chemin d’accès et les paramètres de requête suivants pour obtenir une disponibilité spécifique à l’aide d’un ID de disponibilité.

| Nom                   | Type     | Obligatoire | Description                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ID de produit             | chaîne   | Oui      | Chaîne au format GUID qui identifie le produit.            |
| Réf. SKU                 | chaîne   | Oui      | Chaîne au format GUID qui identifie la référence (SKU).                |
| ID de disponibilité        | chaîne   | Oui      | Chaîne au format GUID qui identifie la disponibilité.       |
| pays-code           | chaîne   | Oui      | ID de pays/région.                                            |

 
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse

En cas de réussite, le corps de la réponse contient une ressource de [disponibilité](product-resources.md#availability) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d'état HTTP     | Error code   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Le produit est introuvable.                                                                                    |
| 404                  | 400018       | Référence (SKU) introuvable.                                                                                        |
| 404                  | 400019       | Disponibilité introuvable.                                                                                   |

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
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
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
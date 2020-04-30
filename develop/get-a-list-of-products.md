---
title: Obtenir la liste de produits (par pays)
description: Vous pouvez utiliser la ressource de produit pour obtenir une collection de produits par pays du client.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7427c3b3f28ac3cd6a2694fe90ac9024f913c749
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82156901"
---
# <a name="get-a-list-of-products-by-country"></a>Obtenir la liste de produits (par pays)

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser les méthodes suivantes pour obtenir une collection de produits disponibles dans un pays particulier.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un pays.

## <a name="c"></a>C\#

Pour obtenir la liste des produits :

1. Utilisez votre collection **collection iaggregatepartner. Products** pour sélectionner le pays à l’aide de la méthode **ByCountry ()** .

2. Sélectionnez l’affichage catalogue à l’aide de la méthode **ByTargetView ()** .

3. Facultatif Sélectionnez l’étendue de la réservation à l’aide de la méthode **ByReservationScope ()** .

4. Facultatif Sélectionnez le segment cible à l’aide de la méthode **ByTargetSegment ()** .

5. Appelez la méthode **obten ()** ou **GetAsync ()** pour retourner la collection.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour obtenir la liste des produits :

1. Utilisez la fonction **collection iaggregatepartner. GetProducts** pour sélectionner le pays à l’aide de la fonction **byCountry ()** .

2. Sélectionnez l’affichage catalogue à l’aide de la fonction **byTargetView ()** .
3. Facultatif Sélectionnez le segment cible à l’aide de la fonction **byTargetSegment ()** .

4. Appelez la fonction **obtenir ()** pour retourner la collection.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour obtenir la liste des produits :

1. Exécutez la commande [**PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) .

2. Sélectionnez le catalogue en spécifiant le paramètre **Catalog** .
3. Facultatif Sélectionnez le segment cible en spécifiant le paramètre de **segment** .

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products ? pays = {country} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1 |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez le chemin d’accès et les paramètres de requête suivants pour obtenir une liste de produits.

| Nom                   | Type     | Obligatoire | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| country                | string   | Oui      | ID du pays/de la région.                                                  |
| targetView             | string   | Oui      | Identifie la vue cible du catalogue. Les valeurs prises en charge sont les suivantes : <ul><li>**Azure**, qui comprend tous les éléments Azure</li><li>**AzureReservations**, qui comprend tous les éléments de réservation Azure</li><li>**AzureReservationsVM**, qui comprend tous les éléments de réservation des machines virtuelles</li><li>**AzureReservationsSQL**, qui comprend tous les éléments de réservation SQL</li><li>**AzureReservationsCosmosDb**, qui comprend tous les éléments de réservation de base de données Cosmos</li><li>**MicrosoftAzure**, qui comprend des éléments pour les abonnements Microsoft Azure (**MS-AZR-0145P**) et les plans Azure</li><li>**OnlineServices**, qui inclut tous les éléments de service en ligne (y compris les produits de la place de marché commercial)</li><li>**Logiciel**, qui comprend tous les éléments logiciels</li><li>**SoftwareSUSELinux**, qui comprend tous les éléments logiciels SUSE Linux</li><li>**SoftwarePerpetual**, qui comprend tous les éléments logiciels perpétuels</li><li>**SoftwareSubscriptions**, qui comprend tous les éléments d’abonnement logiciel</li></ul> |
| targetSegment          | string   | Non       | Identifie le segment cible. Affichage pour différents publics cibles. Les valeurs prises en charge sont les suivantes : <ul><li>**but**</li><li>**Département**</li><li>**émis**</li><li>**organismes**</li></ul> |
| reservationScope | string   | Non | Lors de l’interrogation d’une liste de produits pour Azure Reservations `reservationScope=AzurePlan` , spécifiez pour obtenir la liste des produits applicables aux plans Azure. Excluez ce paramètre pour obtenir une liste de produits pour les réservations Azure, applicables aux abonnements Microsoft Azure (**MS-AZR-0145P**).  |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-examples"></a>Exemples de requête

#### <a name="products-by-country"></a>Produits par pays

Suivez cet exemple pour obtenir la liste des produits par pays pour les abonnements Microsoft Azure (MS-AZR-0145P) et les plans Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Réservations de machines virtuelles Azure (plan Azure)

Suivez cet exemple pour obtenir la liste des produits par pays pour les réservations de machines virtuelles Azure applicables aux plans Azure.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Réservations de machines virtuelles Azure pour les abonnements Microsoft Azure (MS-AZR-0145P)

Suivez cet exemple pour obtenir la liste des produits par pays pour les réservations de machines virtuelles Azure applicables aux abonnements Microsoft Azure (MS-AZR-0145P).

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection de ressources de [**produit**](product-resources.md#product) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | L’accès au targetSegment demandé n’est pas autorisé.                                                     |
| 403                  | 400036       | L’accès au targetView demandé n’est pas autorisé.                                                        |

### <a name="response-example"></a>Exemple de réponse

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

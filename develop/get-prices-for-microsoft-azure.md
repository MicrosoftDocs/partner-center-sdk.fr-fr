---
title: Obtenir les prix de Microsoft Azure
description: Comment obtenir une carte de tarifs Azure avec des prix en temps réel pour une offre Azure. La tarification Azure est assez dynamique et elle change fréquemment.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b56e4bbfdf93cf2f4e9c6c07d638f5a24436c3e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097700"
---
# <a name="get-prices-for-microsoft-azure"></a>Obtenir les prix de Microsoft Azure

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir une carte de tarifs [Azure](azure-rate-card-resources.md) avec des prix en temps réel pour une offre Azure. La tarification Azure est assez dynamique et elle change fréquemment.

Pour suivre l’utilisation et aider à prédire votre facture mensuelle et les factures des clients individuels, vous pouvez combiner cette requête de carte de tarifs Azure pour obtenir les prix de Microsoft Azure avec une demande d' [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md).

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, l’API utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, et ces paramètres sont personnalisables. La sensibilisation à l’emplacement est particulièrement pertinente si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé. Pour plus d’informations, consultez [URI, paramètres](#uri-parameters).

## <a name="c"></a>C\#

Pour obtenir la carte de tarifs Azure, appelez la méthode [**IAzureRateCard. obtenir**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) pour retourner une ressource [**AzureRateCard**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) qui contient les prix Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour obtenir la carte de tarifs Azure, appelez la fonction **IAzureRateCard. obten** pour retourner les détails de la carte à taux contenant les prix Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour obtenir la carte Azure, exécutez la commande [**obtenir-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) pour retourner les détails de la carte de taux qui contient les prix Azure.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                        |
|---------|--------------------------------------------------------------------|
| **GET** | *{baseURL}*/v1/ratecards/Azure ? Currency = {currency} &region = {region} |

### <a name="uri-parameters"></a>Paramètres d’URI

| Nom     | Type   | Obligatoire | Description                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | string | No       | Code ISO à trois lettres facultatif pour la devise dans laquelle les taux de ressources seront fournis (par exemple `EUR` ). Par défaut, il s’agit de `USD`. |
| region   | string | No       | Code de pays/région ISO à deux lettres facultatif qui indique le marché où l’offre est achetée (par exemple `FR` ). Par défaut, il s’agit de `US`.        |

Vous pouvez inclure l' [en-tête](headers.md#rest-request-headers) X-locale facultatif dans votre demande. Si vous n’incluez pas l’en-tête X-locale, la valeur par défaut (« en-US ») est utilisée.

- Si vous fournissez des paramètres de devise et de région dans votre demande, la valeur de X-locale est utilisée pour déterminer la langue de la réponse.

- Si vous ne fournissez pas de paramètres de région et de devise dans votre demande, la valeur de X-locale est utilisée pour déterminer la région, la devise et la langue de la réponse.

### <a name="request-header"></a>En-tête de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

Si la demande aboutit, elle retourne une ressource de [carte de tarifs Azure](azure-rate-card-resources.md) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```

---
title: Obtenir les prix des services partagés du partenaire Microsoft Azure
description: Comment obtenir une carte de tarifs Azure avec des prix pour Microsoft Azure les services partagés de partenaires.
ms.assetid: B5B2F63A-D33F-4D76-8917-9952E6355746
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1a11731aedbe3014f6f9b4eb4c26207e3372d070
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489999"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Obtenir les prix des services partagés du partenaire Microsoft Azure

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment obtenir une carte de tarifs [Azure](azure-rate-card-resources.md) avec des prix pour Microsoft Azure les services partagés de partenaires.

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, il utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, mais ceux-ci sont personnalisables. Cela s’avère particulièrement utile si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé.

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>exemples

### <a name="c"></a>C# 

Pour obtenir la carte de tarifs Azure, appelez la méthode [**IAzureRateCard. GetShared**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) pour retourner une ressource [**AzureRateCard**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) qui contient les prix Azure.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

### <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour obtenir la carte de tarifs Azure, appelez la fonction **IAzureRateCard. getShared** pour retourner les détails de la carte de taux qui contient les prix Azure.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour obtenir la carte Azure, exécutez la commande [**PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) et spécifiez le paramètre **SharedServices** pour retrun les détails de la carte de taux qui contiennent les prix Azure.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande

**Syntaxe de la requête**

| Méthode  | URI de requête                                                               |
|---------|---------------------------------------------------------------------------|
| **Télécharger** | *{baseURL}* /v1/ratecards/Azure-Shared ? Currency = {currency} & region = {region} |

**Paramètres d’URI**

| Nom     | Type   | Obligatoire | Description                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| accès | chaîne | Non       | Code ISO à trois lettres facultatif pour la devise dans laquelle les taux de ressources seront fournis (par exemple, « EUR »). La valeur par défaut est la devise associée au marché dans le profil de partenaire. |
| région   | chaîne | Non       | Code de pays/région ISO à deux lettres facultatif qui indique le marché où l’offre est achetée (par exemple, « FR »). La valeur par défaut est le code de pays/région défini dans le profil de partenaire.        |

Si l’en-tête X-locale facultatif est inclus dans la demande, sa valeur détermine la langue utilisée pour les détails dans la réponse.

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse

Si cette opération réussit, elle retourne une ressource de [carte de tarifs Azure](azure-rate-card-resources.md) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

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
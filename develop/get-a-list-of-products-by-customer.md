---
title: Obtenir une liste de produits (par client)
description: Vous pouvez utiliser un identificateur de client pour obtenir une collection de produits par client.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2141de3cd52f4e270b6668321d7736f33b578b3c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412293"
---
# <a name="get-a-list-of-products-by-customer"></a>Obtenir une liste de produits (par client)

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser les méthodes suivantes pour obtenir une collection de produits pour un client existant.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur d’un client (**customer-tenant-id**).

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande Rest

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products ? targetView = {TargetView} http/1.1 |

#### <a name="request-uri-parameters"></a>Paramètres d’URI de demande

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **client-locataire-ID** | GUID | Oui | La valeur est un paramètre **customer-tenant-id** au format GUID, à savoir un identificateur qui vous permet de spécifier un client. |
| **targetView** | chaîne | Oui | Identifie la vue cible du catalogue. Les valeurs prises en charge sont les suivantes : <ul><li>**Azure**, qui comprend tous les éléments Azure</li><li>**AzureReservations**, qui comprend tous les éléments de réservation Azure</li><li>**AzureReservationsVM**, qui comprend tous les éléments de réservation des machines virtuelles</li><li>**AzureReservationsSQL**, qui comprend tous les éléments de réservation SQL</li><li>**AzureReservationsCosmosDb**, qui comprend tous les éléments de réservation de base de données Cosmos</li><li>**MicrosoftAzure**, qui comprend des éléments pour les abonnements Microsoft Azure (**MS-AZR-0145P**) et les plans Azure</li><li>**OnlineServices**, qui inclut tous les éléments de service en ligne, y compris les produits de la place de marché commerciale</li><li>**Logiciel**, qui comprend tous les éléments logiciels</li><li>**SoftwareSUSELinux**, qui comprend tous les éléments logiciels SUSE Linux</li><li>**SoftwarePerpetual**, qui comprend tous les éléments logiciels perpétuels</li><li>**SoftwareSubscriptions**, qui comprend tous les éléments d’abonnement logiciel </ul> |

#### <a name="request-header"></a>En-tête de requête

Pour plus d’informations, consultez [en-têtes](headers.md).

#### <a name="request-body"></a>Corps de demande

None.

#### <a name="request-example"></a>Exemple de requête

Demandez une liste de produits Azure basés sur l’utilisation disponibles pour un client donné. Les produits pour les Microsoft Azure (MS-AZR-0145P) et les plans Azure sont renvoyés pour les clients dans le cloud public :

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

### <a name="rest-response"></a>Réponse Rest

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d'état HTTP | Error code   | Description                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | L’accès au targetView demandé n’est pas autorisé. | 

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
 
{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

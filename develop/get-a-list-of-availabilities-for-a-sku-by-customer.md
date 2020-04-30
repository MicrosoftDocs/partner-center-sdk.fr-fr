---
title: Obtenir la liste des disponibilités d’une référence SKU (par client)
description: Vous pouvez obtenir une collection de disponibilités pour un produit et une référence SKU spécifiés par le client à l’aide des identificateurs du client, du produit et de la référence SKU.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 15d6e0d4454be657a750ba992af294607686e458
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155711"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a>Obtenir la liste des disponibilités d’une référence SKU (par client)

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser les méthodes suivantes pour obtenir une collection de disponibilités pour un produit et une référence SKU spécifiques disponibles pour un client particulier.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- Identificateur de produit (**Product-ID**).

- Identificateur de référence (**SKU-ID**).

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | baseURL/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/SKUs/{SKU-ID} http/1.1 [* \{\}*](partner-center-rest-urls.md) |

### <a name="request-uri-parameters"></a>Paramètres de l’URI de demande

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Oui | La valeur est un paramètre **customer-tenant-id** au format GUID, à savoir un identificateur qui vous permet de spécifier un client. |
| ID de produit | string | Oui | Chaîne qui identifie le produit. |
| Réf. SKU | string | Oui | Chaîne qui identifie la référence (SKU). |

### <a name="request-header"></a>En-tête de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Response REST

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP | Code d'erreur | Description |
|------------------|------------|-------------|
| 404 | 400013 | Le produit parent est introuvable. |

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
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
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
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
```

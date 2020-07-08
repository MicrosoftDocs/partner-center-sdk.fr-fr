---
title: Obtenir la liste des références (SKU) d’un produit (par le client)
description: Obtient une collection de références (SKU) pour le produit spécifié par le client.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6b9c9bcd52798006d7f686405f059192a722c7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098028"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a>Obtenir la liste des références (SKU) d’un produit (par le client)

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient une collection de références (SKU) pour un produit particulier qui est disponible pour un client existant.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- ID de produit (**Product-ID**).

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| POST   | [* \{ BASEURL \} *](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Products/{Product-ID}/SKUs http/1.1 |

### <a name="request-uri-parameter"></a>Paramètre d’URI de demande

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Oui | La valeur est un paramètre **customer-tenant-id** au format GUID, à savoir un identificateur qui vous permet de spécifier un client. |
| ID de produit | string | Yes | Chaîne qui identifie le produit. |

### <a name="request-header"></a>En-tête de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Réponse REST

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
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```

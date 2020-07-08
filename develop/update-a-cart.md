---
title: Mettre à jour un panier
description: Procédure de mise à jour d’une commande pour un client dans un panier.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095712"
---
# <a name="update-a-cart"></a>Mettre à jour un panier

**S’applique à**

- Espace partenaires

Procédure de mise à jour d’une commande pour un client dans un panier.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- ID de panier d’un panier existant.

## <a name="c"></a>C\#

Pour mettre à jour une commande pour un client, récupérez le panier à l’aide de la méthode **obtenir ()** en transmettant l’ID du client et du panier à l’aide de la fonction **méthode BYID ()** . Apportez les modifications nécessaires au panier. À présent, appelez la méthode **put** à l’aide de la méthode **méthode BYID ()** à l’aide de l’ID du client et du panier.

Enfin, appelez la méthode **put ()** ou **PutAsync ()** pour créer la commande.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de demande                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} http/1.1              |

### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et spécifiez le panier à mettre à jour.

| Nom            | Type     | Obligatoire | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID client** | string   | Yes      | ID client au format GUID qui identifie le client.             |
| **Cart-ID**     | string   | Yes      | GUID-ID au format GUID qui identifie le panier.                     |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés du [panier](cart-resources.md) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | No              | Identificateur de panier qui est fourni lors de la création réussie du panier.                                  |
| creationTimeStamp     | DateTime         | No              | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.        |
| lastModifiedTimeStamp | DateTime         | No              | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.    |
| expirationTimeStamp   | DateTime         | No              | Date d’expiration du panier, au format date/heure.  Appliqué en cas de réussite de la création du panier.            |
| lastModifiedUser      | string           | No              | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                             |
| lineItems             | Tableau d’objets | Yes             | Tableau de ressources [CartLineItem](cart-resources.md#cartlineitem) .                                               |

Ce tableau décrit les propriétés [CartLineItem](cart-resources.md#cartlineitem) dans le corps de la demande.

| Propriété             | Type                        | Obligatoire     | Description                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | string                      | No           | Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                |
| catalogId            | string                      | Yes          | Identificateur de l’élément de catalogue.                                                                       |
| friendlyName         | string                      | Non           | facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.              |
| quantité             | int                         | Oui          | Nombre de licences ou d’instances.     |
| currencyCode         | string                      | No           | Code de la devise.                                                                                 |
| billingCycle         | Object                      | Oui          | Type de cycle de facturation défini pour la période actuelle.                                              |
| participants         | Liste de paires de chaînes d’objets | No           | Collection de participants sur l’achat.                                                      |
| provisioningContext  | Dictionary<String, String>  | No           | Contexte utilisé pour l’approvisionnement de l’offre.                                                          |
| orderGroup           | string                      | No           | Groupe pour indiquer les éléments qui peuvent être placés ensemble.                                            |
| erreur                | Object                      | Non            | Appliqué après la création du panier en cas d’erreur.                                                 |

### <a name="request-example"></a>Exemple de requête

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne la ressource [Cart](cart-resources.md) remplie dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```

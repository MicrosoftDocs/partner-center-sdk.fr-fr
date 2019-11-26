---
title: Mettre à jour un panier
description: Procédure de mise à jour d’une commande pour un client dans un panier.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 70e20f1261f29468c5b0b7e017f29f6e64b91cf6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487949"
---
# <a name="update-a-cart"></a>Mettre à jour un panier


**S’applique à**

- Espace partenaires


Procédure de mise à jour d’une commande pour un client dans un panier. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client. Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID de panier d’un panier existant.


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


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

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **POSÉ** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{Cart-ID} http/1.1              |

 

**Paramètres d’URI**

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et spécifiez le panier à mettre à jour.

| Nom            | Type     | Obligatoire | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID client** | chaîne   | Oui      | ID client au format GUID qui identifie le client.             |
| **Cart-ID**     | chaîne   | Oui      | GUID-ID au format GUID qui identifie le panier.                     |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Ce tableau décrit les propriétés du [panier](cart-resources.md) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | chaîne           | Non              | Identificateur de panier qui est fourni lors de la création réussie du panier.                                  |
| creationTimeStamp     | DateTime         | Non              | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.        |
| lastModifiedTimeStamp | DateTime         | Non              | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.    |
| expirationTimeStamp   | DateTime         | Non              | Date d’expiration du panier, au format date/heure.  Appliqué en cas de réussite de la création du panier.            |
| lastModifiedUser      | chaîne           | Non              | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                             |
| LineItems             | Tableau d’objets | Oui             | Tableau de ressources [CartLineItem](cart-resources.md#cartlineitem) .                                               |


Ce tableau décrit les propriétés [CartLineItem](cart-resources.md#cartlineitem) dans le corps de la demande.

| Propriété             | Type                        | Obligatoire     | Description                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | chaîne                      | Non           | Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                |
| catalogId            | chaîne                      | Oui          | Identificateur de l’élément de catalogue.                                                                       |
| friendlyName         | chaîne                      | Non           | Facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.              |
| quantity             | entier                         | Oui          | Nombre de licences ou d’instances.     |
| currencyCode         | chaîne                      | Non           | Code de la devise.                                                                                 |
| billingCycle         | Objet                      | Oui          | Type de cycle de facturation défini pour la période actuelle.                                              |
| participants         | Liste de paires de chaînes d’objets | Non           | Collection de participants sur l’achat.                                                      |
| provisioningContext  | Dictionary < String, String >  | Non           | Contexte utilisé pour l’approvisionnement de l’offre.                                                          |
| orderGroup           | chaîne                      | Non           | Groupe pour indiquer les éléments qui peuvent être placés ensemble.                                            |
| erreur                | Objet                      | Non           | Appliqué après la création du panier en cas d’erreur.                                                 |


**Exemple de requête**

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

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse REST


En cas de réussite, cette méthode retourne la ressource [Cart](cart-resources.md) remplie dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

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

 

 





---
title: Acheter une extension d’abonnement
description: Comment acheter un module complémentaire à un abonnement existant.
ms.assetid: 743520E5-0501-4403-B977-5E6D3E32DEC3
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0ae6aa7a15340eb4173119b1ce3a3bc30ee9f7c2
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157067"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Acheter une extension d’abonnement

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government

Comment acheter un module complémentaire à un abonnement existant.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- ID d’abonnement. Il s’agit de l’abonnement existant pour lequel vous souhaitez acheter une offre complémentaire.

- Un ID d’offre qui identifie l’offre complémentaire à acheter.

## <a name="purchasing-an-add-on-through-code"></a>Achat d’un module complémentaire via du code

Lorsque vous achetez un module complémentaire à un abonnement, vous mettez à jour l’ordre d’abonnement d’origine avec la commande du module complémentaire. Dans l’exemple ci-dessous, customerId est l’ID de client, subscriptionId est l’ID d’abonnement et addOnOfferId est l’ID d’offre du module complémentaire.

Voici la procédure à suivre :

1.  Obtenir une interface pour les opérations de l’abonnement.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Utilisez cette interface pour instancier un objet d’abonnement. Vous pouvez ainsi obtenir les détails de l’abonnement parent, y compris l’ID de commande.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Instanciez un nouvel objet [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) . Cette instance de commande est utilisée pour mettre à jour la commande d’origine utilisée pour acheter l’abonnement. Ajoutez un seul élément de ligne à la commande qui représente le module complémentaire.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Mettez à jour la commande d’origine de l’abonnement avec la nouvelle commande du module complémentaire.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Pour acheter un module complémentaire, commencez par obtenir une interface pour les opérations d’abonnement en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**Subscriptions. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pour identifier l’abonnement qui a l’offre complémentaire. Utilisez cette [**interface**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) pour récupérer les détails de l’abonnement en appelant [**obtenir**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Pourquoi avez-vous besoin des détails de l’abonnement ? Car vous avez besoin de l’ID de commande de la commande d’abonnement. Il s’agit de l’ordre à mettre à jour avec le module complémentaire.

Ensuite, instanciez un nouvel objet [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) et renseignez-le avec une seule instance [**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) contenant les informations permettant d’identifier le module complémentaire, comme illustré dans l’extrait de code suivant. Vous utiliserez ce nouvel objet pour mettre à jour l’ordre d’abonnement avec le module complémentaire. Enfin, appelez la méthode [**patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) pour mettre à jour l’ordre d’abonnement, après avoir d’abord identifié le client avec [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) et la commande Order [**. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : AddSubscriptionAddOn.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres suivants pour identifier le client et la commande.

| Nom                   | Type     | Obligatoire | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un GUID **client-ID-client-ID** qui identifie le client. |
| **ID de commande**           | **guid** | O        | Identificateur de l’ordre.                                                              |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Les tableaux suivants décrivent les propriétés dans le corps de la demande.

## <a name="order"></a>JSON

| Nom                | Type             | Obligatoire | Description                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | ID de la commande.                                        |
| ReferenceCustomerId | string           | O        | ID du client.                                     |
| LineItems           | tableau d’objets | O        | Tableau d’objets [OrderLineItem](#orderlineitem) . |
| CreationDate        | string           | N        | Date à laquelle la commande a été créée, au format date/heure. |
| Attributs          | object           | N        | Contient « ObjectType » : « Order ».                      |

## <a name="orderlineitem"></a>OrderLineItem

| Nom                 | Type   | Obligatoire | Description                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | nombre | O        | Numéro d’élément de ligne, à partir de 0.                       |
| OfferId              | string | O        | ID d’offre du module complémentaire.                                  |
| SubscriptionId       | string | N        | ID de l’abonnement au module complémentaire acheté.                 |
| ParentSubscriptionId | string | O        | ID de l’abonnement parent qui possède l’offre complémentaire. |
| FriendlyName         | string | N        | Nom convivial de cet élément de ligne.                        |
| Quantité             | nombre | O        | Nombre de licences.                                      |
| PartnerIdOnRecord    | string | N        | ID MPN du partenaire de l’enregistrement.                         |
| Attributs           | object | N        | Contient « ObjectType » : « OrderLineItem ».                      |

### <a name="request-example"></a>Exemple de requête

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne l’ordre d’abonnement mis à jour dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```

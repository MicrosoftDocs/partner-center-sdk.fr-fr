---
title: Acheter un module complémentaire à un abonnement
description: Comment acheter un module complémentaire à un abonnement existant.
ms.assetid: 743520E5-0501-4403-B977-5E6D3E32DEC3
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f49685eb142945fc94e551e2113799c4c5b959e5
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416308"
---
# <a name="span-idpc_apiv2purchase_an_add-on_to_a_subscriptionpurchase-an-add-on-to-a-subscription"></a><span id="pc_apiv2.purchase_an_add-on_to_a_subscription"/>acheter un module complémentaire à un abonnement


**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government

Comment acheter un module complémentaire à un abonnement existant.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID d’abonnement. Il s’agit de l’abonnement existant pour lequel vous souhaitez acheter une offre complémentaire.
- Un ID d’offre qui identifie l’offre complémentaire à acheter.

## <a name="span-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codespan-idpurchasing_an_add-on_through_codepurchasing-an-add-on-through-code"></a><span id="Purchasing_an_add-on_through_code"/><span id="purchasing_an_add-on_through_code"/><span id="PURCHASING_AN_ADD-ON_THROUGH_CODE"/>achat d’un module complémentaire par le biais de code


Lorsque vous achetez un module complémentaire à un abonnement, vous mettez à jour l’ordre d’abonnement d’origine avec la commande du module complémentaire. Dans l’exemple ci-dessous, customerId est l’ID de client, subscriptionId est l’ID d’abonnement et addOnOfferId est l’ID d’offre du module complémentaire.

Voici les étapes à suivre :

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

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour acheter un module complémentaire, commencez par obtenir une interface pour les opérations d’abonnement en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**Subscriptions. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pour identifier l’abonnement qui a l’offre complémentaire. Utilisez cette [**interface**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) pour récupérer les détails de l’abonnement en appelant [**obtenir**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get). Pourquoi avez-vous besoin des détails de l’abonnement ? Car vous avez besoin de l’ID de commande de la commande d’abonnement. Il s’agit de l’ordre à mettre à jour avec le module complémentaire.

Ensuite, instanciez un nouvel objet [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) et renseignez-le avec une seule instance [**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) contenant les informations permettant d’identifier le module complémentaire, comme illustré dans l’extrait de code suivant. Vous utiliserez ce nouvel objet pour mettre à jour l’ordre d’abonnement avec le module complémentaire. Enfin, appelez la méthode [**patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) pour mettre à jour l’ordre d’abonnement, après avoir d’abord identifié le client avec [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) et la commande Order [ **. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).

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

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode    | URI de demande                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

 

**Paramètres d’URI**

Utilisez les paramètres suivants pour identifier le client et la commande.

| Nom                   | Type     | Obligatoire | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui identifie le client. |
| **ID de commande**           | **uniques** | Y        | Identificateur de l’ordre.                                                              |

 

**En-têtes de demande**

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Les tableaux suivants décrivent les propriétés dans le corps de la demande.

## <a name="span-idorderspan-idorderspan-idorderorder"></a>Commande de <span id="ORDER"/>de <span id="order"/><span id="Order"/>


| Nom                | Type             | Obligatoire | Description                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| ID                  | chaîne           | N        | ID de la commande.                                        |
| referenceCustomerId | chaîne           | Y        | ID client.                                     |
| lineItems           | Tableau d’objets | Y        | Tableau d’objets [OrderLineItem](#orderlineitem) . |
| CreationDate        | chaîne           | N        | Date à laquelle la commande a été créée, au format date/heure. |
| Attributs          | objet           | N        | Contient « ObjectType » : « Order ».                      |

 

## <a name="span-idorderlineitemspan-idorderlineitemspan-idorderlineitemorderlineitem"></a><span id="orderLineItem"/><span id="orderlineitem"/><span id="ORDERLINEITEM"/>OrderLineItem


| Nom                 | Type   | Obligatoire | Description                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| lineItemNumber       | nombre | Y        | Numéro d’élément de ligne, à partir de 0.                       |
| OfferId              | chaîne | Y        | ID d’offre du module complémentaire.                                  |
| SubscriptionId       | chaîne | N        | ID de l’abonnement au module complémentaire acheté.                 |
| parentSubscriptionId | chaîne | Y        | ID de l’abonnement parent qui possède l’offre complémentaire. |
| FriendlyName         | chaîne | N        | Nom convivial de cet élément de ligne.                        |
| Quantité             | nombre | Y        | Nombre de licences.                                      |
| partnerIdOnRecord    | chaîne | N        | ID MPN du partenaire de l’enregistrement.                         |
| Attributs           | objet | N        | Contient « ObjectType » : « OrderLineItem ».                      |

 

**Exemple de requête**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, cette méthode retourne l’ordre d’abonnement mis à jour dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

**Exemple de réponse**

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

 

 





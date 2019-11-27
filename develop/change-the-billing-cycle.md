---
title: Modifier le cycle de facturation
description: Mettez à jour un abonnement à la facturation mensuelle ou annuelle.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3080ef40f71a043b4f02a7dc37178973d72aa09c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489019"
---
# <a name="change-the-billing-cycle"></a>Modifier le cycle de facturation

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Met à jour une [commande](order-resources.md) d’une facturation mensuelle à une facturation annuelle ou d’une facturation annuelle à une facturation mensuelle.

Dans le tableau de bord de l’espace partenaires, vous pouvez effectuer cette opération en accédant à la page de détails de l’abonnement d’un client. Une fois ici, vous verrez une option qui définit le cycle de facturation actuel de l’abonnement avec la possibilité de le modifier et de l’envoyer.  

**Hors de portée** pour cette rubrique :  

- Modification du cycle de facturation pour les versions d’évaluation
- Modification des cycles de facturation pour les offres non annuelles (mensuelle, 6 ans) & les abonnements Azure
- Modification des cycles de facturation des abonnements inactifs
- Modification des cycles de facturation pour les abonnements basés sur des licences Microsoft services en ligne

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID de commande.

## <a name="c"></a>C#

Pour modifier la fréquence du cycle de facturation, mettez à jour la propriété [**Order. BillingCycle**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle?view=partnercenter-dotnet-latest#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) .

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie le paramètre de requête requis pour modifier la quantité de l’abonnement.

| Nom                   | Type | Obligatoire | Description                                                          |  
|------------------------|------|----------|----------------------------------------------------------------------|  
| **client-locataire-ID** | GUID |    Y     | Un identificateur de **locataire client** au format GUID qui identifie le client |  
| **ID de commande**           | GUID |    Y     | Identificateur de l’ordre                                                 |  

### <a name="request-headers"></a>En-têtes de requête

- Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de la requête

Les tableaux suivants décrivent les propriétés dans le corps de la demande.

## <a name="order"></a>Ordre

| Propriété           | Type             | Obligatoire | Description                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | chaîne           |    N     | Un identificateur de commande qui est fourni lors de la création réussie de la commande |
|ReferenceCustomerId | chaîne           |    Y     | Identificateur du client                                                    |
| BillingCycle       | chaîne           |    Y     | Indique la fréquence à laquelle le partenaire est facturé pour cette commande. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype). |
| LineItems          | Tableau d’objets |    Y     | Tableau de ressources [OrderLineItem](#orderlineitem)                      |
| CreationDate       | DateHeure         |    N     | Date à laquelle la commande a été créée, au format date/heure                        |
| Attributs         | Objet           |    N     | Contient « ObjectType » : « OrderLineItem »                                     |

## <a name="orderlineitem"></a>OrderLineItem

| Propriété             | Type   | Obligatoire | Description                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | nombre |    Y     | Numéro d’élément de ligne, à partir de 0                                              |
| OfferId              | chaîne |    Y     | ID de l’offre                                                                |
| SubscriptionId       | chaîne |    Y     | ID de l’abonnement                                                         |
| FriendlyName         | chaîne |    N     | Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté |
| Quantité             | nombre |    Y     | Nombre de licences ou d’instances                                                |
| PartnerIdOnRecord    | chaîne |    N     | ID MPN du partenaire d’enregistrement                                                |
| Attributs           | Objet |    N     | Contient « ObjectType » : « OrderLineItem »                                             |

### <a name="request-example"></a>Exemple de requête

Mettre à jour la facturation annuelle

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne l’ordre d’abonnement mis à jour dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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
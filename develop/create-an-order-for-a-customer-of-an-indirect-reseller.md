---
title: Créer une commande pour un client d’un revendeur indirect
description: Comment créer une commande pour un client d’un revendeur indirect.
ms.assetid: 3B89F8CE-96A8-443F-927E-6351E24FDBFF
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 126c90e936daa50fcf84b8ec97a8f3e4db0f5321
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413908"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Créer une commande pour un client d’un revendeur indirect

S'applique à :

- Centre pour partenaires

Comment créer une commande pour un client d’un revendeur indirect.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- Identificateur du client.
- Identificateur d’offre de l’article à acheter.
- Identificateur du locataire du revendeur indirect.

## <a name="c"></a>C\#

Pour créer une commande pour un client d’un revendeur indirect :

1. Obtenir une collection des revendeurs indirects qui ont une relation avec le partenaire connecté.
2. Obtenir une variable locale pour l’élément de la collection qui correspond à l’ID du revendeur indirect. Cette étape vous permet d’accéder à la propriété [**MpnId**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) du revendeur lorsque vous créez la commande.
3. Instanciez un objet [**Order**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order) et définissez la propriété [**ReferenceCustomerID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) sur l’identificateur du client afin d’enregistrer le client.
4. Créez une liste d’objets [**OrderLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) et assignez la liste à [**la propriété de l’ordre de tri**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) . Chaque élément de ligne de commande contient les informations d’achat d’une offre. Veillez à renseigner la propriété [**PartnerIdOnRecord**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) dans chaque élément de ligne avec l’ID MPN du revendeur indirect. Vous devez avoir au moins un élément de ligne de commande.
5. Obtenez une interface pour commander des opérations en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client, puis récupérez l’interface à partir de la propriété [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .
6. Appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) pour créer la commande.

### <a name="c-example"></a>Exemple de\# C

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Exemple**:**projet**d' [application de test console](console-test-app.md): **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : PlaceOrderForCustomer.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de demande                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez le paramètre Path suivant pour identifier le client.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID client | chaîne | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de demande

#### <a name="order"></a>Order

Ce tableau décrit les propriétés d' **ordre** dans le corps de la demande.

| Nom | Type | Obligatoire | Description |
| ---- | ---- | -------- | ----------- |
| id | chaîne | Non | Identificateur d’ordre qui est fourni lors de la création réussie de la commande. |
| referenceCustomerId | chaîne | Oui | Identificateur du client. |
| BillingCycle | chaîne | Non | Fréquence à laquelle le partenaire est facturé pour cette commande. La valeur par défaut est &quot;&quot; mensuelle et est appliquée lors de la création réussie de la commande. Les valeurs prises en charge sont les noms des membres trouvés dans [**BillingCycleType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype). Remarque : la fonctionnalité de facturation annuelle n’est pas encore disponible en général. La facturation annuelle sera bientôt prise en charge. |
| lineItems | Tableau d’objets | Oui | Tableau de ressources [**OrderLineItem**](#orderlineitem) . |
| creationDate | chaîne | Non | Date à laquelle la commande a été créée, au format date/heure. Appliqué en cas de création réussie de la commande. |
| attributs | objet | Non | Contient « ObjectType » : « Order ». |

#### <a name="orderlineitem"></a>OrderLineItem

Ce tableau décrit les propriétés **OrderLineItem** dans le corps de la demande.

| Nom | Type | Obligatoire | Description |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Oui | Chaque élément de ligne de la collection obtient un numéro de ligne unique, en comptant de 0 à Count-1. |
| offerId | chaîne | Oui | Identificateur de l’offre. |
| subscriptionId | chaîne | Non | Identificateur d’abonnement. |
| parentSubscriptionId | chaîne | Non | Ce paramètre est facultatif. ID de l’abonnement parent dans une offre complémentaire. S’applique uniquement au correctif. |
| friendlyName | chaîne | Non | Ce paramètre est facultatif. Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté. |
| quantity | int | Oui | Nombre de licences pour un abonnement basé sur une licence. |
| partnerIdOnRecord | chaîne | Non | Lorsqu’un fournisseur indirect passe une commande pour le compte d’un revendeur indirect, renseignez ce champ avec l’ID MPN du **revendeur indirect uniquement** (jamais l’ID du fournisseur indirect). Cela garantit une gestion correcte des incentives. **Si vous ne fournissez pas l’ID MPN du revendeur, cela ne provoque pas l’échec de la commande. Toutefois, le revendeur n’est pas enregistré et, par conséquent, les calculs de l’incentive peuvent ne pas inclure la vente.** |
| attributs | objet | Non | Contient « ObjectType » : « OrderLineItem ». |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

En cas de réussite, le corps de la réponse contient la ressource de [commande](order-resources.md) remplie.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
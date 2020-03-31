---
title: Créer un panier avec des modules complémentaires
description: Comment ajouter une commande avec des modules complémentaires pour un client dans un panier.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 99556ccb26dfe8ce8a43e62bc4a24ea5e7760ef0
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413531"
---
# <a name="create-a-cart-with-add-ons"></a>Créer un panier avec des modules complémentaires

S'applique à :

- Centre pour partenaires

Vous pouvez acheter des modules complémentaires par le biais d’un panier. Pour plus d’informations sur ce qui est actuellement disponible pour la vente, consultez [offres partenaires dans le programme du fournisseur de solutions Cloud](https://docs.microsoft.com/partner-center/csp-offers).

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client. Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="c"></a>C\#

Un panier permet l’achat d’une offre de base et de ses modules complémentaires correspondants. Pour créer un panier, procédez comme suit :

1. Instanciez un objet de [**panier**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart) .
2. Créez une liste d’objets [**CartLineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) qui représentent les offres de base et attribuez la liste à [**la propriété de**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) liste de propriétés du panier.
3. Sous l’élément de ligne de panier de chaque offre de base, renseignez la liste des **AddOnItems** avec d’autres objets **CartLineItem** qui représentent chacun un module complémentaire qui sera acheté dans le cadre de cette offre de base.
4. Obtenez une interface pour les opérations de panier à l’aide de [**collection iaggregatepartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) pour appeler la méthode [**ICustomerCollection. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client, puis récupérer l’interface à partir de la propriété **Cart** .
5. Enfin, appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) pour créer le panier.

### <a name="c-example"></a>Exemple de\# C

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Suivez les étapes ci-dessous pour créer un panier permettant d’acheter des modules complémentaires sur des abonnements de base existants :

1. Créez un **panier** avec une nouvelle **CARTLINEITEM** contenant l’ID d’abonnement dans la propriété **ProvisioningContext** avec la clé « ParentSubscriptionId ».
2. Appelez la méthode **Create** ou **CreateAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de demande                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre Path suivant pour identifier le client.

| Nom            | Type     | Obligatoire | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID client** | chaîne   | Oui      | ID client au format GUID qui identifie le client.             |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés du [panier](cart-resources.md) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | chaîne           | Non              | Identificateur de panier qui est fourni lors de la création réussie du panier.                                  |
| creationTimeStamp     | DateTime         | Non              | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.         |
| lastModifiedTimeStamp | DateTime         | Non              | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.    |
| expirationTimeStamp   | DateTime         | Non              | Date d’expiration du panier, au format date/heure.  Appliqué en cas de réussite de la création du panier.            |
| lastModifiedUser      | chaîne           | Non              | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                             |
| lineItems             | Tableau d’objets | Oui             | Tableau de ressources [CartLineItem](cart-resources.md#cartlineitem) .                                             |

Ce tableau décrit les propriétés [CartLineItem](cart-resources.md#cartlineitem) dans le corps de la demande.

| Propriété             | Type                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | chaîne                           | Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                                                                   |
| catalogId            | chaîne                           | Identificateur de l’élément de catalogue.                                                                                                                          |
| friendlyName         | chaîne                           | Ce paramètre est facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                                                                 |
| quantity             | int                              | Nombre de licences ou d’instances.                                                                                                                  |
| currencyCode         | chaîne                           | Code de la devise.                                                                                                                                    |
| BillingCycle         | Object                           | Type de cycle de facturation défini pour la période actuelle.                                                                                                 |
| participants         | Liste de paires de chaînes d’objets      | Collection de partenaire sur l’enregistrement (MPNID) sur l’achat.                                                                                          |
| provisioningContext  | Dictionary < String, String >       | Contexte utilisé pour l’approvisionnement de l’offre.                                                                                                             |
| orderGroup           | chaîne                           | Groupe pour indiquer les éléments qui peuvent être placés ensemble.                                                                                               |
| addonItems           | Liste d’objets **CartLineItem** | Collection d’éléments de ligne de panier pour les modules complémentaires qui seront achetés vers l’abonnement de base qui résulte de l’achat de l’élément de ligne de panier parent. |
| erreur                | Object                           | Appliqué après la création du panier en cas d’erreur.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>Exemple de requête (nouvel abonnement de base)

L’exemple REST suivant montre comment créer un panier avec des éléments de module complémentaire pour un nouvel abonnement de base.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>Exemple de demande (abonnement de base existant)

L’exemple REST suivant montre comment ajouter des modules complémentaires à un abonnement de base existant.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne la ressource [Cart](cart-resources.md) remplie dans le corps de la réponse.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Exemple de réponse (nouvel abonnement de base)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Exemple de réponse (abonnement de base existant)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
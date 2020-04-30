---
title: Créer un panier
description: Comment ajouter une commande pour un client dans un panier.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8755267c3c7e49064394cd34b2797efdac8455e0
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154931"
---
# <a name="create-a-cart"></a>Créer un panier

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez ajouter une commande pour un client dans un panier. Pour plus d’informations sur ce qui est actuellement disponible pour la vente, consultez [offres partenaires dans le programme du fournisseur de solutions Cloud](https://docs.microsoft.com/partner-center/csp-offers).

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

## <a name="c"></a>C\#

Pour créer une commande pour un client :

1. Instanciez un objet de panier.

2. Créez une liste d’objets **CartLineItem** et affectez la liste à la propriété de liste de propriétés du panier. Chaque élément de ligne de panier contient les informations d’achat d’un produit. Vous devez disposer d’au moins un élément de ligne de panier.

3. Obtenez une interface pour les opérations de panier en appelant la méthode **collection iaggregatepartner. Customers. méthode BYID** avec l’ID client pour identifier le client, puis en récupérant l’interface à partir de la propriété **Cart** .

4. Appelez la méthode **Create** ou **CreateAsync** pour créer le panier.

### <a name="c-example"></a>Exemple\# C

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour créer une commande pour un client :

1. Instanciez un objet de panier.

2. Créez une liste d’objets **CartLineItem** et affectez la liste aux éléments de ligne du panier. Chaque élément de ligne de panier contient les informations d’achat d’un produit. Vous devez disposer d’au moins un élément de ligne de panier.

3. Obtenez une interface pour les opérations de panier en appelant la fonction **collection iaggregatepartner. getCustomers (). méthode BYID** avec l’ID client pour identifier le client, puis en récupérant l’interface à partir de la fonction **getCart** .

4. Appelez la fonction **Create** pour créer le panier.

## <a name="java-example"></a>Exemple Java

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour créer une commande pour un client :

1. Instanciez un objet de panier.

2. Créez une liste d’objets **CartLineItem** et affectez la liste aux éléments de ligne du panier. Chaque élément de ligne de panier contient les informations d’achat d’un produit. Vous devez disposer d’au moins un élément de ligne de panier.

3. Exécutez la commande [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) pour créer le panier.

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts http/1.1                        |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de chemin d’accès suivant pour identifier le client.

| Nom            | Type     | Obligatoire | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID client** | string   | Oui      | ID client au format GUID qui identifie le client.             |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés du [panier](cart-resources.md) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | string           | Non              | Identificateur de panier qui est fourni lors de la création réussie du panier.                                  |
| creationTimeStamp     | DateTime         | Non               | Date à laquelle le panier a été créé, au format date/heure. Appliqué en cas de réussite de la création du panier.         |
| lastModifiedTimeStamp | DateTime         | Non               | Date de la dernière mise à jour du panier, au format date/heure. Appliqué en cas de réussite de la création du panier.    |
| expirationTimeStamp   | DateTime         | Non               | Date d’expiration du panier, au format date/heure.  Appliqué en cas de réussite de la création du panier.            |
| lastModifiedUser      | string           | Non              | Utilisateur qui a mis à jour le panier pour la dernière fois. Appliqué en cas de réussite de la création du panier.                             |
| lineItems             | Tableau d’objets | Oui             | Tableau de ressources [CartLineItem](cart-resources.md#cartlineitem) .                                     |

Ce tableau décrit les propriétés [CartLineItem](cart-resources.md#cartlineitem) dans le corps de la demande.

|      Propriété       |            Type             | Obligatoire |                                                                                         Description                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         id          |           string            |    Non    |                                                     Identificateur unique pour un élément de ligne de panier. Appliqué en cas de réussite de la création du panier.                                                     |
|      catalogId      |           string            |   Oui    |                                                                                Identificateur de l’élément de catalogue.                                                                                 |
|    friendlyName     |           string            |    Non    |                                                    facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                                                    |
|      quantité       |             int             |   Oui    |                                                                            Nombre de licences ou d’instances.                                                                             |
|    currencyCode     |           string            |    Non    |                                                                                     Code de la devise.                                                                                      |
|    billingCycle     |           Object            |   Oui    |                                                                    Type de cycle de facturation défini pour la période actuelle.                                                                    |
|    participants     | Liste de paires de chaînes d’objets |    Non     |                                                                Collection de partenaire sur l’enregistrement (MPNID) sur l’achat.                                                                 |
| provisioningContext | Dictionary<String, String>  |    Non     | Informations requises pour l’approvisionnement de certains éléments du catalogue. La propriété provisioningVariables d’une référence (SKU) indique les propriétés requises pour des éléments spécifiques dans le catalogue. |
|     orderGroup      |           string            |    Non    |                                                                   Groupe pour indiquer les éléments qui peuvent être placés ensemble.                                                                   |
|        error        |           Object            |    Non     |                                                                     Appliqué après la création du panier en cas d’erreur.                                                                      |
|     renewsTo        | Tableau d’objets            |    Non     |                                                    Tableau de ressources [RenewsTo](cart-resources.md#renewsto) .                                                                            |

Ce tableau décrit les propriétés [RenewsTo](cart-resources.md#renewsto) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

### <a name="request-example"></a>Exemple de requête

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
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
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>Response REST

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
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```

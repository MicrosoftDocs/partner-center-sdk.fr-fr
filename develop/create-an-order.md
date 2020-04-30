---
title: Créer une commande
description: Comment créer une commande pour un client.
ms.assetid: FE4949FA-7C4D-462D-8F32-FAADCF166875
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: f1e3182b824d4d8297e7e3c076bc52f3d6865bac
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155201"
---
# <a name="create-an-order"></a>Créer une commande

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government

La création d’une **commande pour les produits d’instance de machine virtuelle réservée Azure** s’applique *uniquement* aux éléments suivants :

- Espace partenaires

Pour plus d’informations sur ce qui est actuellement disponible pour la vente, consultez [offres partenaires dans le programme du fournisseur de solutions Cloud](https://docs.microsoft.com/partner-center/csp-offers).

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- Identificateur d’offre.

## <a name="c"></a>C\#

Pour créer une commande pour un client :

1. Instanciez un objet [**Order**](order-resources.md) et définissez la propriété **REFERENCECUSTOMERID** sur l’ID client pour enregistrer le client.

2. Créez une liste d’objets [**OrderLineItem**](order-resources.md#orderlineitem) et assignez la liste à **la propriété de l’ordre de tri** . Chaque élément de ligne de commande contient les informations d’achat relatives à une offre. Vous devez disposer d’au moins un élément de ligne de commande.

3. Obtenez une interface pour commander des opérations. Tout d’abord, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, récupérez l’interface de la propriété [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) .

4. Appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) et transmettez l’objet [**Order**](order-resources.md) .

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateOrder.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Orders http/1.1 |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez le paramètre de chemin d’accès suivant pour identifier le client.

| Nom        | Type   | Obligatoire | Description                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | string | Oui      | ID client au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

#### <a name="order"></a>JSON

Ce tableau décrit les propriétés d' [ordre](order-resources.md) dans le corps de la demande.

| Propriété             | Type                        | Obligatoire                        | Description                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| id                   | string                      | Non                              | Identificateur d’ordre qui est fourni lors de la création réussie de la commande.   |
| referenceCustomerId  | string                      | Non                              | Identificateur du client. |
| billingCycle         | string                      | Non                              | Indique la fréquence à laquelle le partenaire est facturé pour cette commande. Les valeurs prises en charge sont les noms des membres trouvés dans [BillingCycleType](product-resources.md#billingcycletype). La valeur par défaut est « Monthly » ou « OneTime » lors de la création de la commande. Ce champ est appliqué lors de la création réussie de la commande. |
| lineItems            | Tableau de ressources [OrderLineItem](order-resources.md#orderlineitem) | Oui      | Liste répertoriant les offres achetées par le client, y compris la quantité.        |
| currencyCode         | string                      | Non                              | Lecture seule. Devise utilisée lors de la mise en place de la commande. Appliqué en cas de création réussie de la commande.           |
| creationDate         | DATETIME                    | Non                               | Lecture seule. Date à laquelle la commande a été créée, au format date/heure. Appliqué en cas de création réussie de la commande.                                   |
| status               | string                      | Non                              | Lecture seule. État de la commande.  Les valeurs prises en charge sont les noms des membres trouvés dans [OrderStatus](order-resources.md#orderstatus).        |
| liens                | [OrderLinks](utility-resources.md#resourcelinks)              | Non                               | Liens de ressource correspondant à la commande. |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Non                               | Attributs de métadonnées correspondant à l’ordre. |

#### <a name="orderlineitem"></a>OrderLineItem

Ce tableau décrit les propriétés [OrderLineItem](order-resources.md#orderlineitem) dans le corps de la demande.

>[!NOTE]
>Le partnerIdOnRecord doit être fourni uniquement lorsqu’un fournisseur indirect passe une commande pour le compte d’un revendeur indirect. Il est utilisé pour stocker l’ID de Microsoft Partner Network du revendeur indirect uniquement (jamais l’ID du fournisseur indirect).

| Nom                 | Type   | Obligatoire | Description                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int    | Oui      | Chaque élément de ligne dans la collection obtient un numéro de ligne unique, allant de 0 à nombre-1.                                                                                                                                                 |
| offerId              | string | Oui      | Identificateur de l’offre.                                                                                                                                                                                                                      |
| subscriptionId       | string | Non       | Identificateur de l’abonnement.                                                                                                                                                                                                               |
| parentSubscriptionId | string | Non       | facultatif. ID de l’abonnement parent dans une offre de module complémentaire. S’applique uniquement à PATCH.                                                                                                                                                     |
| friendlyName         | string | Non       | facultatif. Nom convivial de l’abonnement défini par le partenaire pour aider à lever toute ambiguïté.                                                                                                                                              |
| quantité             | int    | Oui      | Nombre de licences pour un abonnement basé sur licence.                                                                                                                                                                                   |
| partnerIdOnRecord    | string | Non       | Lorsqu’un fournisseur indirect passe une commande pour le compte d’un revendeur indirect, renseignez ce champ avec l’ID MPN du **revendeur indirect uniquement** (jamais l’ID du fournisseur indirect). Cela garantit une comptabilité appropriée des incitations. |
| provisioningContext  | Dictionary<String, String>                | Non        |  Informations requises pour l’approvisionnement de certains éléments du catalogue. La propriété provisioningVariables d’une référence (SKU) indique les propriétés requises pour des éléments spécifiques dans le catalogue.                  |
| liens                | [OrderLineItemLinks](order-resources.md#orderlineitemlinks) | Non        |  Lecture seule. Liens de ressource correspondant à l’élément de ligne de commande.  |
| attributs           | [ResourceAttributes](utility-resources.md#resourceattributes) | Non        | Attributs de métadonnées correspondant à OrderLineItem. |
| renewsTo             | Tableau d’objets                          | Non     |Tableau de ressources [RenewsTo](order-resources.md#renewsto) .                                                                            |

##### <a name="renewsto"></a>RenewsTo

Ce tableau décrit les propriétés [RenewsTo](order-resources.md#renewsto) dans le corps de la demande.

| Propriété              | Type             | Obligatoire        | Description |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | Non              | Représentation ISO 8601 de la durée du terme de renouvellement. Les valeurs actuellement prises en charge sont **p1m** (1 mois) et **P1Y** (1 an). |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>Response REST

En cas de réussite, la méthode retourne une ressource [Order](order-resources.md) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 400                  | 2093         | L’inventaire n’est pas disponible pour l’élément de catalogue sélectionné.                                                 |
| 400                  | 2094         | L’abonnement n’est pas un abonnement Azure valide. Applicable uniquement à l’achat d’une instance de machine virtuelle réservée Azure.     |
| 400                  | 2095         | L’abonnement n’est pas activé pour une instance de machine virtuelle réservée Azure. |

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```

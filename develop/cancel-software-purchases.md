---
title: Annuler des achats de logiciel
description: Option libre-service pour annuler les abonnements logiciels et les achats de logiciels perpétuels à l’aide des API de l’espace partenaires.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927406"
---
# <a name="cancel-software-purchases"></a>Annuler des achats de logiciel

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser les API de l’espace partenaires pour annuler les abonnements logiciels et les achats de logiciels perpétuels (à condition que ces achats aient été effectués dans la fenêtre d’annulation de la date d’achat). Vous n’avez pas besoin de créer un ticket de support pour effectuer de telles annulations, et vous pouvez utiliser les méthodes en libre-service suivantes à la place.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="c"></a>C\#

Pour annuler une commande de logiciel,

1. Transmettez les informations d’identification de votre compte à la méthode [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) pour récupérer une interface [**collection ipartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) afin d’accéder aux opérations du partenaire.

2. Sélectionnez une [commande](order-resources.md#order) spécifique que vous souhaitez annuler. Appelez la méthode [**Customers. méthode BYID ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client, suivi de **Orders. méthode BYID ()** avec l’identificateur Order.

3. Appelez la méthode **obtenir** ou **GetAsync** pour récupérer la commande.

4. Affectez à la propriété [**Order. Status**](order-resources.md#order) la valeur `cancelled` .

5. Facultatif Si vous souhaitez spécifier certains éléments de ligne pour l’annulation, définissez [**Order. LineItem**](order-resources.md#order) sur la liste des éléments de ligne que vous souhaitez annuler.

6. Utilisez la méthode **patch ()** pour mettre à jour la commande.

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de requête suivants pour supprimer un client.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un identificateur de locataire client au format GUID qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **ID de commande** | **string** | O        | La valeur est une chaîne qui indique l’identificateur de l’ordre que vous souhaitez annuler. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a>Exemple de requête

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne l’ordre avec les éléments de ligne annulés.

L’état de la commande est marqué comme **annulé** si tous les Articles de la commande sont annulés, ou **terminés** si tous les Articles de la commande ne sont pas annulés.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

Dans l’exemple de réponse suivant, vous pouvez voir que la quantité d’élément de ligne avec l’identificateur d’offre **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** est égale à zéro (0). Cette modification signifie que la ligne marquée pour l’annulation a été annulée avec succès. L’exemple de commande contient d’autres lignes qui n’ont pas été annulées, ce qui signifie que l’état de la commande globale sera marqué comme **terminé**, non **annulé**.

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```

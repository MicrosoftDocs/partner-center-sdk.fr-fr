---
title: Obtenir un lien d’activation par élément de ligne de commande
description: Obtient un lien d’activation d’abonnement par élément de ligne de commande.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 110710650c758c9d38234566cd2c89a4b7f93a3e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097880"
---
# <a name="get-activation-link-by-order-line-item"></a>Obtenir un lien d’activation par élément de ligne de commande

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient un lien d’activation d’abonnement au Marketplace commercial par numéro d’élément de ligne de commande.

Dans le tableau de bord de l’espace partenaires, vous pouvez effectuer cette opération en sélectionnant un **abonnement spécifique** sous **abonnement** dans la page principale, ou en sélectionnant le lien **accéder au site de l’éditeur** à côté de l’abonnement à activer sur la page **abonnements** .

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Commande terminée avec le produit qui nécessite une activation.

## <a name="c"></a>C\#

Pour obtenir le lien d’activation d’un élément de ligne, utilisez votre collection [**collection iaggregatepartner. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) et appelez la méthode [**méthode BYID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID de client sélectionné. Appelez ensuite la propriété [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) et la méthode [**méthode BYID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) avec le [**OrderID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)spécifié. Ensuite, appelez la méthode [**LineItem**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) avec **méthode BYID ()** avec l’identificateur de numéro d’élément de ligne.  Enfin, appelez la méthode **ActivationLinks ()** .

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{CustomerID}/Orders/{OrderID}/LineItems/{lineItemNumber}/activationlinks http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources [client](customer-resources.md#customer) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```

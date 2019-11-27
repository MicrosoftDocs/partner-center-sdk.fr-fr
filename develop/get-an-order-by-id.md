---
title: Recevoir une commande par ID
description: Obtient une ressource de commande qui correspond au client et à l’ID de commande.
ms.assetid: 5E4160AB-6B73-4CA1-903D-7257927CA754
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 875a1f14483b40a1ec2ccb355ae8837d55bddb3c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485719"
---
# <a name="get-an-order-by-id"></a>Recevoir une commande par ID

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient une ressource de [commande](order-resources.md) qui correspond au client et à l’ID de commande.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID de commande.

## <a name="c"></a>\# C

Pour obtenir l’ID de commande d’un client :

1. Utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID ()** .
2. Appelez la propriété [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) , suivie de la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) une fois de plus.
3. Appelez la demande d' [**extraction ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) ou [**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: GetOrder.cs

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour obtenir l’ID de commande d’un client :

1. Utilisez votre fonction **collection iaggregatepartner. getCustomers** et appelez la fonction **méthode BYID ()** .
2. Appelez la fonction **getOrders** , suivie de la fonction **méthode BYID ()** .
3. Appelez la fonction d' **extraction ()** .

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour obtenir l’ID de commande d’un client, exécutez la commande [**PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) et spécifiez **CustomerID** et **OrderID** paramaeters.

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders/{ID-for-order} http/1.1  |

#### <a name="uri-parameters"></a>Paramètres d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir une commande par ID.

| Nom                   | Type     | Obligatoire | Description                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| client-locataire-ID     | chaîne   | Oui      | Chaîne au format GUID correspondant au client. |
| ID-pour-commande           | chaîne   | Oui      | Chaîne correspondant à l’ID de commande.                |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de la requête

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource [Order](order-resources.md) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```

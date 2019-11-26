---
title: Get an order by ID
description: Gets a Order resource that matches the customer and order ID.
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
# <a name="get-an-order-by-id"></a>Get an order by ID

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Gets an [Order](order-resources.md) resource that matches the customer and order ID.

## <a name="prerequisites"></a>Conditions préalables

- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer ID (customer-tenant-id). If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- An order ID.

## <a name="c"></a>C\#

To get a customer's order by ID:

1. Use your **IAggregatePartner.Customers** collection and call the **ById()** method.
2. Call the [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.
3. Call [**Get()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

**Sample**: [Console test app](console-test-app.md). **Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

To get a customer's order by ID:

1. Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.
2. Call the **getOrders** function, followed by the **byID()** function once more.
3. Call the **get()** function.

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** paramaeters.

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a>REST request

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1  |

#### <a name="uri-parameters"></a>Paramètres d’URI

This table lists the required query parameters to get an order by ID.

| Nom                   | Tapez     | Obligatoire | Description                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| customer-tenant-id     | chaîne   | Oui      | A GUID formatted string corresponding to the customer. |
| id-for-order           | chaîne   | Oui      | A string corresponding to the order ID.                |

### <a name="request-headers"></a>En-têtes de requête

See [Headers](headers.md) for more information.

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

## <a name="rest-response"></a>REST response

If successful, this method returns an [Order](order-resources.md) resource in the response body.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

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

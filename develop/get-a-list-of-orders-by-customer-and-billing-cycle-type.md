---
title: Obtenir une liste de commandes par client et type de cycle de facturation
description: Obtient une collection de ressources de commande pour le client et le type de cycle bilingue spécifiés.
ms.assetid: DF1E52F6-1A3D-4B26-8BCC-6E429410C662
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8a23d96a6b0926b0623a7b7360bd296a993e5211
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487339"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a>Obtenir une liste de commandes par client et type de cycle de facturation

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient une collection de ressources de commande qui correspondent à un type de client et de cycle de facturation donné. Notez qu’il y a un délai de 15 minutes au maximum entre le moment où une commande est soumise et le moment où elle apparaîtra dans un regroupement de commandes d’un client.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="c"></a>\# C

Pour obtenir un regroupement des commandes d’un client :

1. Utilisez votre collection [**collection iaggregatepartner. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) et appelez la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID de client sélectionné.
2. Appelez la propriété [**Orders**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) et la méthode **ByBillingCycleType ()** avec le [**BillingCycleType**](product-resources.md#billingcycletype)spécifié.
3. Appelez la méthode [**obten ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) ou [**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Orders ? billingType = {facturation-cycle-type} http/1.1  |

#### <a name="uri-parameters"></a>Paramètres d’URI

Ce tableau répertorie les paramètres de requête requis pour obtenir une collection de commandes par ID de client et type de cycle de facturation.

| Nom                   | Type     | Obligatoire | Description                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| client-locataire-ID     | chaîne   | Oui      | Chaîne au format GUID correspondant au client.    |
| type de cycle de facturation     | chaîne   | Non       | Chaîne correspondant au type de cycle de facturation.         |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de la requête

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources de [commande](order-resources.md) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```

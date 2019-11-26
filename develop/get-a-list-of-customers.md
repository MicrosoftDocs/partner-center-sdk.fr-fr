---
title: Obtenir une liste de clients
description: Comment obtenir une collection de ressources représentant tous les clients d’un partenaire.
ms.assetid: 6D636257-7C23-4DDF-9895-96F208B66232
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 317439b9db7deeb1ffe52848c4d61da82d1583f1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487469"
---
# <a name="get-a-list-of-customers"></a>Obtenir une liste de clients

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette rubrique explique comment obtenir une collection de ressources qui représente tous les clients d’un partenaire.

> [!TIP]
> Vous pouvez également effectuer cette opération dans le tableau de bord de l’espace partenaires. Sur la page principale, sous **gestion des clients**, sélectionnez **afficher les clients**. Ou, dans la barre latérale, sélectionnez **Customers**.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="c"></a>\# C

Pour obtenir la liste de tous les clients :

1. Utilisez la collection [**collection iaggregatepartner. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) pour créer un objet **collection ipartner** .
2. Récupérez la liste des clients à l’aide des méthodes [**query ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) ou [**QueryAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) . (Pour obtenir des instructions sur la création d’une requête, consultez la classe [**QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .)

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

Pour obtenir un exemple, consultez les rubriques suivantes :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **PartnerSDK. FeatureSamples**
- Classe : **CustomerPaging.cs**

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour obtenir la liste de tous les clients :

1. Utilisez la fonction [**collection iaggregatepartner. getCustomers**] pour obtenir une référence aux opérations du client.
2. Récupérez la liste des clients à l’aide de la fonction **query ()** .

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Exécutez la commande [**obtenir-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) sans paramètres pour obtenir une liste complète des clients.

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers ? Size = {Size} http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour obtenir la liste des clients.

| Nom     | Type    | Obligatoire | Description                                        |
|----------|---------|----------|----------------------------------------------------|
| **size** | **tiers** | Y        | Nombre de résultats à afficher en même temps. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de la requête

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources [client](customer-resources.md#customer) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

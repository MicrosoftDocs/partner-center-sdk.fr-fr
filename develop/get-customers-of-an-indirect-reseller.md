---
title: Obtenir les clients d’un revendeur indirect
description: Obtention d’une liste des clients d’un revendeur indirect.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: caf8a4ce707624672215e5b2a0c46659e0f9564b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927082"
---
# <a name="get-customers-of-an-indirect-reseller"></a>Obtenir les clients d’un revendeur indirect

**S’applique à**

- Espace partenaires

Obtention d’une liste des clients d’un revendeur indirect.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- Identificateur du locataire du revendeur indirect.

## <a name="c"></a>C\#

Pour obtenir une collection de clients qui ont une relation avec le revendeur indirect spécifié, commencez par instancier un objet [**SimpleFieldFilter**/dotnet/API/Microsoft.Store.partnercenter.Models.Query.simplefieldfilter) pour créer le filtre. Vous devez passer le membre de l’énumération [**CustomerSearchField. IndirectReseller**/dotnet/API/Microsoft.Store.partnercenter.Models.Customers.customersearchfield) converti en une chaîne, et indiquer [**FieldFilterOperation. StartsWith**/dotnet/API/Microsoft.Store.partnercenter.Models.Query.fieldfilteroperation) comme type d’opération de filtre. Vous devez également fournir l’identificateur de locataire du revendeur indirect sur lequel filtrer.

Ensuite, instanciez un objet [**IQueryable**/dotnet/API/Microsoft.Store.partnercenter.Models.Query.IQuery) à transmettre à la requête en appelant la méthode [**BuildSimpleQuery**/dotnet/API/Microsoft.Store.partnercenter.Models.Query.queryfactory.buildsimplequery) et en lui passant le filtre. BuildSimplyQuery n’est qu’un des types de requêtes pris en charge par la classe [**QueryFactory**/dotnet/API/Microsoft.Store.partnercenter.Models.Query.queryfactory).

Pour exécuter le filtre et obtenir le résultat, utilisez d’abord [**collection iaggregatepartner. Customers**/dotnet/API/Microsoft.Store.partnercenter.ipartner.Customers) pour obtenir une interface pour les opérations du client du partenaire. Appelez ensuite la méthode [**query**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.Query) ou [**QueryAsync**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.QueryAsync).

Pour créer un énumérateur pour parcourir les résultats paginés, récupérez l’interface de fabrique d’énumérateur de la collection Customer de la propriété [**collection iaggregatepartner. enumerates. Customers**/dotnet/API/Microsoft.Store.partnercenter.Enumerators.iresourcecollectionenumeratorcontainer.Customers), puis appelez [**Create**/dotnet/API/Microsoft.Store.partnercenter.Factory.iresourcecollectionenumeratorfactory-1.Create), comme indiqué dans le code ci-dessous, en passant la variable qui contient la collection Customer.

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**Exemple**:**projet**d' [application de test console](console-test-app.md): **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers ? Size = {Size} ? Filter = {Filter} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de requête suivants pour créer la demande.

| Nom   | Type   | Obligatoire | Description                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| taille   | int    | Non       | Nombre de résultats à afficher en même temps. Ce paramètre est optionnel.                                                                                                                                                                                                                |
| Filter | Filter | Oui      | Requête qui filtre la recherche. Pour récupérer les clients d’un revendeur indirect spécifié, vous devez insérer l’identificateur de revendeur indirect et inclure et encoder la chaîne suivante : {"Field" : "IndirectReseller", "value" : "{indirect Reseller identifier}", "Operator" : "commence \_ par"}. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example-encoded"></a>Exemple de requête (encodé)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>Exemple de requête (décodé)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient des informations sur les clients du revendeur.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

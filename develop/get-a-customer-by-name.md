---
title: Obtenir la liste des clients filtrés à l’aide d’un champ de recherche
description: Obtient une collection des ressources client qui correspondent à un filtre. Vous pouvez éventuellement définir une taille de page. Vous pouvez filtrer par nom de société, domaine, revendeur indirect ou fournisseur de solutions Cloud indirect (CSP).
ms.assetid: 7D5D8C83-1DBD-4C54-8CDA-FE0CAC911D14
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: cd050514f49fbb867df117d2220d4f60f94e32b8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490119"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a>Obtenir la liste des clients filtrés à l’aide d’un champ de recherche


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient une collection des ressources [client](customer-resources.md#customer) qui correspondent à un filtre. Vous pouvez éventuellement définir une taille de page. Vous pouvez filtrer par nom de société, domaine, revendeur indirect ou fournisseur de solutions Cloud indirect (CSP).

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Filtre construit par l’utilisateur.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour obtenir une collection de clients qui correspondent à un filtre, commencez par instancier un objet [**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) pour créer le filtre. Vous devez passer une chaîne qui contient le [**CustomerSearchField**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)et indiquer le type d’opération de filtre en tant que [**FieldFilterOperation. StartsWith**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation). Il s’agit de la seule opération de filtre de champ prise en charge par le point de terminaison Customers. Vous devez également fournir la chaîne de filtrage.

Ensuite, instanciez un objet [**IQueryable**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery) à passer à la requête en appelant la méthode [**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) et en lui passant le filtre. BuildSimplyQuery n’est qu’un des types de requêtes pris en charge par la classe [**QueryFactory**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) .

Enfin, pour exécuter le filtre et obtenir le résultat, utilisez d’abord [**collection iaggregatepartner. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.customers) pour obtenir une interface pour les opérations du client du partenaire. Appelez ensuite la méthode [**query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) ou [**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) .

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"  

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : FilterCustomers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers ? Size = {size} & filtre = {filter} http/1.1 |

 

**Paramètres d’URI**

Utilisez les paramètres de requête suivants.

| Nom   | Type   | Obligatoire | Description                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| size   | entier    | Non       | Nombre de résultats à afficher en même temps. Ce paramètre est facultatif. |
| filter | filter | Oui      | Filtre à appliquer aux clients. Il doit s’agir d’une chaîne encodée.              |

 

**Syntaxe de filtre**

Vous devez composer le paramètre de filtre sous la forme d’une série de paires clé-valeur séparées par des virgules. Chaque clé et valeur doit être placée individuellement entre guillemets et séparés par un signe deux-points. Le filtre entier doit être encodé.

Un exemple non encodé ressemble à ceci :

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```  
  
Le tableau suivant décrit les paires clé-valeur requises :

| Clé      | Valeur                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| Champ    | Champ à filtrer. Les valeurs valides se trouvent dans [**CustomerSearchField**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield). |
| Valeur    | Valeur par laquelle filtrer. La casse de la valeur est ignorée.                                                                |
| Opérateur | Opérateur à appliquer. La seule valeur prise en charge pour ce scénario client est « commence\_par ».                            |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST


En cas de réussite, cette méthode retourne une collection de ressources [client](customer-resources.md#customer) correspondantes dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 




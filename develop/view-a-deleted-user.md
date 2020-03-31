---
title: Afficher les utilisateurs supprimés d’un client
description: Obtient une liste de ressources CustomerUser supprimées pour un client par ID de client. Vous pouvez éventuellement définir une taille de page. Vous devez fournir un filtre.
ms.assetid: B2248C7D-0F68-4F52-9249-D3168C2F6E83
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cab6b1cd309757f0754610eca362bcf205d199fb
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414254"
---
# <a name="view-deleted-users-for-a-customer"></a>Afficher les utilisateurs supprimés d’un client


**S’applique à**

- Centre pour partenaires

Obtient une liste de ressources CustomerUser supprimées pour un client par ID de client. Vous pouvez éventuellement définir une taille de page. Vous devez fournir un filtre.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- Identificateur du client.

## <a name="span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_span-idwhat_happens_when_you_delete_a_user_account_what-happens-when-you-delete-a-user-account"></a><span id="What_happens_when_you_delete_a_user_account_"/><span id="what_happens_when_you_delete_a_user_account_"/><span id="WHAT_HAPPENS_WHEN_YOU_DELETE_A_USER_ACCOUNT_"/>que se passe-t-il lorsque vous supprimez un compte d’utilisateur ?


Lorsque vous supprimez un compte d’utilisateur, l’état de l’utilisateur est défini sur « inactif ». Elle reste ainsi pendant trente jours, après quoi le compte d’utilisateur et ses données associées sont purgés et rendus irrécupérables. Si vous souhaitez restaurer un compte d’utilisateur supprimé au cours de la période de 30 jours, consultez [restaurer un utilisateur supprimé pour un client](restore-a-user-for-a-customer.md). Notez qu’une fois supprimée et marquée comme « inactive », le compte d’utilisateur n’est plus renvoyé en tant que membre du regroupement d’utilisateurs (par exemple, en utilisant [obtenir une liste de tous les comptes d’utilisateur d’un client](get-a-list-of-all-user-accounts-for-a-customer.md)). Pour obtenir la liste des utilisateurs supprimés qui n’ont pas encore été purgés, vous devez rechercher les comptes d’utilisateur qui ont été définis comme étant inactifs.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer une liste d’utilisateurs supprimés, construisez une requête qui filtre les utilisateurs dont l’État est défini sur inactif. Tout d’abord, créez le filtre en instanciant un objet [**SimpleFieldFilter**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) avec les paramètres, comme indiqué dans l’extrait de code suivant. Ensuite, créez la requête à l’aide de la méthode [**BuildIndexedQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) . Notez que si vous ne souhaitez pas obtenir de résultats paginés, vous pouvez utiliser la méthode [**BuildSimpleQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) à la place. Ensuite, utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Enfin, appelez la méthode [**query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) pour envoyer la demande.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetCustomerInactiveUsers.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de demande                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users ? Size = {size} & filtre = {filter} http/1.1 |

 

**Paramètre URI**

Utilisez le chemin d’accès et les paramètres de requête suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ID client | GUID   | Oui      | La valeur est un ID client au format GUID qui identifie le client.                                                                                                            |
| size        | int    | Non       | Nombre de résultats à afficher en même temps. Ce paramètre est facultatif.                                                                                                     |
| filtre      | filtre | Oui      | Requête qui filtre la recherche utilisateur. Pour récupérer les utilisateurs supprimés, vous devez inclure et encoder la chaîne suivante : {"Field" : "UserState", "value" : "inactive", "opérateur" : "Equals"}. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST


En cas de réussite, cette méthode retourne une collection de ressources [CustomerUser](user-resources.md#customeruser) dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 





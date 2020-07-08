---
title: Restaurer un utilisateur supprimé pour un client
description: Comment restaurer un utilisateur supprimé à l’aide d’un ID client et d’un ID utilisateur.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c908adaa8ae315003aff2ef3ca1ba1d54484767d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096620"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Restaurer un utilisateur supprimé pour un client

**S’applique à**

- Espace partenaires

Comment restaurer un **utilisateur** supprimé à l’aide d’un ID client et d’un ID utilisateur.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur utilisateur. Si vous ne disposez pas de l’ID utilisateur, consultez [afficher les utilisateurs supprimés pour un client](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>Quand pouvez-vous restaurer un compte d’utilisateur supprimé ?

Lorsque vous supprimez un compte d’utilisateur, l’état de l’utilisateur est défini sur « inactif ». Elle reste ainsi pendant trente jours, après quoi le compte d’utilisateur et ses données associées sont purgés et rendus irrécupérables. Vous pouvez uniquement restaurer un compte d’utilisateur supprimé pendant cette période de 30 jours. Une fois supprimée et marquée comme « inactive », le compte d’utilisateur n’est plus renvoyé en tant que membre du regroupement d’utilisateurs (par exemple, à l’aide de la fonction [obtenir une liste de tous les comptes d’utilisateurs d’un client](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Pour restaurer un utilisateur, créez une nouvelle instance de la classe [**CustomerUser**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) et définissez la valeur de la propriété [**User. State**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state) sur [**userState. active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate).

Vous restaurez un utilisateur supprimé en définissant l’état de l’utilisateur sur actif. Vous n’avez pas besoin de remplir à nouveau les champs restants dans la ressource utilisateur. Ces valeurs seront automatiquement restaurées à partir de la ressource utilisateur inactive supprimée. Ensuite, utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**users. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pour identifier l’utilisateur.

Enfin, appelez la méthode [**patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) et transmettez l’instance **CustomerUser** pour envoyer la demande de restauration de l’utilisateur.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CustomerUserRestore.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de demande                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **PATCH** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de requête suivants pour spécifier l’ID client et l’ID utilisateur.

| Nom                   | Type     | Obligatoire | Description                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un identificateur de **locataire client** au format GUID qui permet au revendeur de filtrer les résultats sur un client donné. |
| **ID utilisateur**            | **guid** | O        | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique.                                         |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom       | Type   | Obligatoire | Description                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| State      | string | O        | L’état de l’utilisateur. Pour restaurer un utilisateur supprimé, cette chaîne doit contenir « active ». |
| Attributs | object | N        | Contient « ObjectType » : « CustomerUser ».                                 |

### <a name="request-example"></a>Exemple de requête

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse retourne les informations utilisateur restaurées dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```

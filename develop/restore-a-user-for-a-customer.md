---
title: Restaurer un utilisateur supprimé pour un client
description: Comment restaurer un utilisateur supprimé à l’aide d’un ID client et d’un ID utilisateur.
ms.assetid: A48A4718-6EAF-4FC8-8B44-F3FDCA2B3298
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cfedefd5b9b8547b79b817c06f44e9b21f12d51c
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415393"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Restaurer un utilisateur supprimé pour un client


**S’applique à**

- Centre pour partenaires

Comment restaurer un **utilisateur** supprimé à l’aide d’un ID client et d’un ID utilisateur.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID de l’utilisateur. Si vous ne disposez pas de l’ID utilisateur, consultez [afficher les utilisateurs supprimés pour un client](view-a-deleted-user.md).

## <a name="span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_span-idwhen_can_you_restore_a_deleted_user_account_when-can-you-restore-a-deleted-user-account"></a><span id="When_can_you_restore_a_deleted_user_account_"/><span id="when_can_you_restore_a_deleted_user_account_"/><span id="WHEN_CAN_YOU_RESTORE_A_DELETED_USER_ACCOUNT_"/>quand pouvez-vous restaurer un compte d’utilisateur supprimé ?


Lorsque vous supprimez un compte d’utilisateur, l’état de l’utilisateur est défini sur « inactif ». Elle reste ainsi pendant trente jours, après quoi le compte d’utilisateur et ses données associées sont purgés et rendus irrécupérables. Vous pouvez uniquement restaurer un compte d’utilisateur supprimé pendant cette période de 30 jours. Notez qu’une fois supprimée et marquée comme « inactive », le compte d’utilisateur n’est plus renvoyé en tant que membre du regroupement d’utilisateurs (par exemple, en utilisant [obtenir une liste de tous les comptes d’utilisateur d’un client](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour restaurer un utilisateur, créez une nouvelle instance de la classe [**CustomerUser**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) et définissez la valeur de la propriété [**User. State**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.user.state) sur [**userState. active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.users.userstate). Vous restaurez un utilisateur supprimé en définissant l’état de l’utilisateur sur actif. Notez que vous n’avez pas besoin de remplir à nouveau les champs restants dans la ressource utilisateur. Ces valeurs seront automatiquement restaurées à partir de la ressource utilisateur inactive supprimée. Ensuite, utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**users. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pour identifier l’utilisateur. Enfin, appelez la méthode [**patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) et transmettez l’instance **CustomerUser** pour envoyer la demande de restauration de l’utilisateur.

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

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode    | URI de demande                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres de requête suivants pour spécifier l’ID client et l’ID utilisateur.

| Nom                   | Type     | Obligatoire | Description                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un identificateur de **locataire client** au format GUID qui permet au revendeur de filtrer les résultats sur un client donné. |
| **ID utilisateur**            | **uniques** | Y        | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique.                                         |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom       | Type   | Obligatoire | Description                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| État      | chaîne | Y        | État de l’utilisateur. Pour restaurer un utilisateur supprimé, il doit contenir « actif ». |
| Attributs | objet | N        | Contient « ObjectType » : « CustomerUser ».                                 |

 

**Exemple de requête**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


En cas de réussite, cette méthode retourne les informations utilisateur restaurées dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

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

---
title: Définir des rôles d’utilisateur pour un client
description: Dans un compte client, il existe un ensemble de rôles d’annuaire. Vous pouvez assigner des comptes d’utilisateurs à ces rôles.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a40b60dddd2a29310c1c4aaefa689f6a8de71327
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927604"
---
# <a name="set-user-roles-for-a-customer"></a>Définir des rôles d’utilisateur pour un client

**S’applique à**

- Espace partenaires

Dans un compte client, il existe un ensemble de rôles d’annuaire. Vous pouvez assigner des comptes d’utilisateurs à ces rôles.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour affecter un rôle d’annuaire à un utilisateur client, créez un nouveau [**UserMember**/dotnet/API/Microsoft.Store.partnercenter.Models.Roles.usermember) avec les détails de l’utilisateur appropriés. Ensuite, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID de client spécifié pour identifier le client. À partir de là, utilisez la méthode [**DirectoryRoles. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.customerdirectoryroles.idirectoryrolecollection.BYID) avec l’ID de rôle d’annuaire pour spécifier le rôle. Ensuite, accédez à la collection **UserMembers** et utilisez la méthode [**Create**/dotnet/API/Microsoft.Store.partnercenter.customerdirectoryroles.iusermembercollection.Create) pour ajouter le nouveau membre utilisateur à la collection de membres d’utilisateur affectés à ce rôle.

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{Role-ID}/usermembers http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Pour identifier le rôle et le client appropriés, utilisez les paramètres d’URI suivants. Pour identifier l’utilisateur auquel attribuer le rôle, fournissez les informations d’identification dans le corps de la demande.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **ID de rôle**            | **guid** | O        | La valeur est un ID de **rôle** au format GUID qui identifie le rôle à attribuer à l’utilisateur.                                                              |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                  | Type       | Obligatoire | Description                            |
|-----------------------|------------|----------|----------------------------------------|
| **Id**                | **string** | O        | ID de l’utilisateur à ajouter au rôle. |
| **DisplayName**       | **string** | O        | Nom complet convivial de l’utilisateur. |
| **UserPrincipalName** | **string** | O        | Nom d’utilisateur principal.        |
| **Attributs**        | **object** | O        | Contient « ObjectType » : « UserMember »     |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a>Réponse REST

Cette méthode retourne le compte d’utilisateur avec l’ID de rôle attaché lorsque le rôle est correctement attribué à l’utilisateur.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```

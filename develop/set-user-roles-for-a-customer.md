---
title: Définir des rôles d’utilisateur pour un client
description: Dans un compte client, il existe un ensemble de rôles d’annuaire. Vous pouvez assigner des comptes d’utilisateurs à ces rôles.
ms.assetid: B7FA3599-9AE9-4494-90B4-F7C9A2EF2338
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6f48403b79b74834723c59f7a2ba4cb39abb993e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488029"
---
# <a name="set-user-roles-for-a-customer"></a>Définir des rôles d’utilisateur pour un client


**S’applique à**

- Espace partenaires

Dans un compte client, il existe un ensemble de rôles d’annuaire. Vous pouvez assigner des comptes d’utilisateurs à ces rôles.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour affecter un rôle d’annuaire à un utilisateur client, créez un nouveau [**UserMember**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) avec les détails de l’utilisateur appropriés. Ensuite, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID de client spécifié pour identifier le client. À partir de là, utilisez la méthode [**DirectoryRoles. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) avec l’ID de rôle d’annuaire pour spécifier le rôle. Ensuite, accédez à la collection **UserMembers** et utilisez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) pour ajouter le nouveau membre utilisateur à la collection de membres d’utilisateur affectés à ce rôle.

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

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode   | URI de requête                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Publier** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{Role-ID}/usermembers http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres URI suivants pour identifier le client et le rôle appropriés. Pour identifier l’utilisateur auquel attribuer le rôle, fournissez les informations d’identification dans le corps de la demande.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **ID de rôle**            | **uniques** | Y        | La valeur est un ID de **rôle** au format GUID qui identifie le rôle à attribuer à l’utilisateur.                                                              |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                  | Type       | Obligatoire | Description                            |
|-----------------------|------------|----------|----------------------------------------|
| **Identifi**                | **chaîne** | Y        | ID de l’utilisateur à ajouter au rôle. |
| **NomComplet**       | **chaîne** | Y        | Nom complet convivial de l’utilisateur. |
| **UserPrincipalName** | **chaîne** | Y        | Nom du principal d’utilisateur.        |
| **Attributs**        | **dessin** | Y        | Contient « ObjectType » : « UserMember »     |

 

**Exemple de requête**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


Cette méthode retourne le compte d’utilisateur avec l’ID de rôle attaché lorsque le rôle est correctement attribué à l’utilisateur.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

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

 

 





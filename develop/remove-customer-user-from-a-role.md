---
title: Supprimer un utilisateur client d’un rôle
description: Comment supprimer un utilisateur d’un rôle d’annuaire dans un compte client.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 42c9894b50a253fe533acbe749527f1d5ff67486
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926452"
---
# <a name="remove-a-customer-user-from-a-role"></a>Supprimer un utilisateur client d’un rôle

**S’applique à**

- Espace partenaires

Comment supprimer un utilisateur d’un rôle d’annuaire dans un compte client.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour supprimer un utilisateur d’un rôle d’annuaire, sélectionnez le client que l’utilisateur doit modifier à l’aide d’un appel à la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID), à partir de là, spécifiez le rôle à l’aide de la méthode [**DirectoryRoles. méthode BYID**/dotnet/API/Microsoft.Store.PARTNERCENTER.CUSTOMERDIRECTORYROLES.IDIRECTORYROLECOLLECTION.BYID) avec l’ID de rôle d’annuaire. Ensuite, accédez à la méthode [**UserMembers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.customerdirectoryroles.iusermembercollection.BYID) pour identifier l’utilisateur à supprimer, et la méthode [**Delete**/dotnet/API/Microsoft.Store.partnercenter.customerdirectoryroles.iusermember.Delete) pour supprimer l’utilisateur du rôle.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : RemoveCustomerUserMemberFromDirectoryRole.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **DELETE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{Role-ID}/usermembers/{user-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres URI suivants pour identifier le client, le rôle et l’utilisateur appropriés.

| Nom                   | Type     | Obligatoire | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un GUID **client-ID-client-ID** qui identifie le client. |
| **ID de rôle**            | **guid** | O        | La valeur est un ID de **rôle** au format GUID qui identifie le rôle.                |
| **ID utilisateur**            | **guid** | O        | La valeur est un ID d' **utilisateur** au format GUID qui identifie un compte d’utilisateur unique.   |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

Si l’utilisateur est correctement supprimé du rôle, le corps de la réponse est vide.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```

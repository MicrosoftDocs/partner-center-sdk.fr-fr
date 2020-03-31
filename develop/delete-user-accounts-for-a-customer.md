---
title: Supprimer un compte d’utilisateur pour un client
description: Comment supprimer un compte d’utilisateur existant pour un client.
ms.assetid: 12097809-A62D-4929-9F1D-08676784BA39
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 728694cc236e0257a24940ad4c3a9284e4e28b21
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415594"
---
# <a name="delete-a-user-account-for-a-customer"></a>Supprimer un compte d’utilisateur pour un client

S'applique à :

- Centre pour partenaires

Cette rubrique explique comment supprimer un compte d’utilisateur existant pour un client.

## <a name="prerequisites"></a>Composants requis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- ID client (**client-locataire-ID**). Si vous n’avez pas d’ID de client, recherchez l’ID dans l’espace partenaires. Sélectionnez le client dans la liste clients, sélectionnez **compte**, puis enregistrez son ID Microsoft.
- Un ID d’utilisateur. Si vous ne disposez pas de l’ID utilisateur, consultez [obtenir la liste de tous les comptes d’utilisateur d’un client](get-a-list-of-all-user-accounts-for-a-customer.md).

## <a name="deleting-a-user-account"></a>Suppression d’un compte d’utilisateur

Lorsque vous supprimez un compte d’utilisateur, l’état de l’utilisateur est défini sur **inactif** pendant trente jours. Après 30 jours, le compte d’utilisateur et ses données associées sont purgés et rendus irrécupérables.

Vous pouvez [restaurer un compte d’utilisateur supprimé pour un client](restore-a-user-for-a-customer.md) si le compte inactif est dans la période de 30 jours. Toutefois, lorsque vous restaurez un compte qui a été supprimé et marqué comme étant inactif, le compte n’est plus renvoyé en tant que membre du regroupement utilisateur (par exemple, lorsque vous [recevez une liste de tous les comptes d’utilisateur d’un client](get-a-list-of-all-user-accounts-for-a-customer.md)).

## <a name="c"></a>C\#

Pour supprimer un compte d’utilisateur client existant :

1. Utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client.
2. Appelez la méthode [**users. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) pour identifier l’utilisateur.
3. Appelez la méthode [**Delete**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) pour supprimer l’utilisateur et définir l’état utilisateur sur inactif.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : DeleteCustomerUser.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| DELETE     | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID} http/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez les paramètres de requête suivants pour identifier le client et l’utilisateur.

| Nom                   | Type     | Obligatoire | Description                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | Y        | La valeur est un **client-client-ID** au format GUID qui permet au revendeur de filtrer les résultats pour un client donné. |
| ID utilisateur                | GUID     | Y        | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique.                                          |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de demande

None.

### <a name="request-example"></a>Exemple de requête

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne un code d’état **204 no content** .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```

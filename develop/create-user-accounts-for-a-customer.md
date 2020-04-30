---
title: Créer des comptes d’utilisateur pour un client
description: Créez un nouveau compte d’utilisateur pour votre client.
ms.assetid: E46AB186-F4E1-4A00-AE62-28A843F9C288
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0c4c6f41dd5bda3965aad4e1b68f339305f18e30
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155391"
---
# <a name="create-user-accounts-for-a-customer"></a>Créer des comptes d’utilisateur pour un client

**S’applique à :**

- Espace partenaires

Créez un nouveau compte d’utilisateur pour votre client.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

## <a name="c"></a>C\#

Pour obtenir un nouveau compte d’utilisateur pour un client :

1. Créez un nouvel objet **CustomerUser** avec les informations utilisateur appropriées.

2. Utilisez votre collection **IAggregatePartner.Customers** et appelez la méthode **ById()**.

3. Appelez la propriété **Utilisateurs**, suivie de la méthode **Créer**.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSamples, **classe**: CustomerUserCreate.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users http/1.1 |

#### <a name="uri-parameters"></a>Paramètres URI

Pour identifier le client approprié, utilisez les paramètres de requête suivants.

| Nom | Type | Obligatoire | Description |
|----- |----- | -------- |------------ |
| **customer-tenant-id** | **guid** | O | La valeur est un GUID **client-ID-client-ID**. Il permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **ID utilisateur** | **guid** | N | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne un compte d’utilisateur, y compris le GUID.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
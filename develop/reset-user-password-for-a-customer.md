---
title: Réinitialiser le mot de passe d’un utilisateur pour un client
description: La réinitialisation d’un mot de passe est très similaire à la mise à jour d’autres détails dans un compte d’utilisateur existant pour votre client.
ms.assetid: DECACEE1-2492-4D2F-B4CF-ED93220B406A
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 05714f983e382753c53e99c5926864ec600546a4
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486579"
---
# <a name="reset-user-password-for-a-customer"></a>Réinitialiser le mot de passe d’un utilisateur pour un client


**S’applique à**

- Espace partenaires

La réinitialisation d’un mot de passe est très similaire à la mise à jour d’autres détails dans un compte d’utilisateur existant pour votre client.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour réinitialiser un mot de passe pour un utilisateur client spécifié, récupérez d’abord l’ID client spécifié et l’utilisateur ciblé. Ensuite, créez un nouvel objet **CustomerUser** qui contient les informations relatives au client existant, mais avec un nouvel objet **PasswordProfile** . Ensuite, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID ()** . Appelez ensuite la propriété **Users** , la méthode **méthode BYID ()** , puis la méthode **patch** .

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSamples, **classe**: CustomerUserUpdate.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode    | URI de requête                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users http/1.1 |



**Paramètre URI**

Utilisez le paramètre de requête suivant pour identifier le client approprié.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **ID utilisateur**            | **uniques** | Y        | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique.                                                                       |



**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

**Exemple de requête**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },


      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


En cas de réussite, cette méthode retourne les informations de l’utilisateur, ainsi que les informations de mot de passe mises à jour.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```








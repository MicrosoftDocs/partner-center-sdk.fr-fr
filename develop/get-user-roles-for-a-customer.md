---
title: Obtenir les rôles d’utilisateur d’un client
description: Obtient la liste de tous les rôles/autorisations attachés à un compte d’utilisateur. Les variantes incluent l’obtention d’une liste de toutes les autorisations sur tous les comptes d’utilisateur pour un client et l’obtention d’une liste d’utilisateurs ayant un rôle donné.
ms.assetid: 304A1C1F-6280-40E9-A96B-F87ECA657FF3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 65492338db16ef83738407510c28f9e1524caed2
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487079"
---
# <a name="get-user-roles-for-a-customer"></a>Obtenir les rôles d’utilisateur d’un client


**S’applique à**

- Espace partenaires

Obtient la liste de tous les rôles/autorisations attachés à un compte d’utilisateur. Les variantes incluent l’obtention d’une liste de toutes les autorisations sur tous les comptes d’utilisateur pour un client et l’obtention d’une liste d’utilisateurs ayant un rôle donné.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer tous les rôles d’annuaire pour un client spécifié, récupérez d’abord l’ID de client spécifié. Ensuite, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID ()** . Appelez ensuite la propriété **DirectoryRoles** , suivie de la méthode d' **extraction ()** ou de la méthode <strong>GetAsync ()</strong>.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetCustomerDirectoryRoles.cs

Pour récupérer une liste d’utilisateurs clients qui ont un rôle donné, récupérez d’abord l’ID de client et l’ID de rôle d’annuaire spécifiés. Ensuite, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID ()** . Appelez ensuite la propriété **DirectoryRoles** , puis la méthode **méthode BYID ()** , puis la propriété **UserMembers** , la suivie par la méthode d' **extraction ()** ou <strong>GetAsync ()</strong>.

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSamples, **classe**: GetCustomerDirectoryRoleUserMembers.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Users/{User-ID}/directoryroles http/1.1 |
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles http/1.1                 |
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directoryroles/{Role-ID}/usermembers    |

 

**Paramètre URI**

Utilisez le paramètre de requête suivant pour identifier le client approprié.

| Nom                   | Type     | Obligatoire | Description                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur.                                                      |
| **ID utilisateur**            | **uniques** | N        | La valeur est un **ID utilisateur** au format GUID qui appartient à un compte d’utilisateur unique.                                                                                                                            |
| **ID de rôle**            | **uniques** | N        | La valeur est un ID de **rôle** au format GUID qui appartient à un type de rôle. Vous pouvez obtenir ces ID en interrogeant tous les rôles d’annuaire pour un client, sur tous les comptes d’utilisateur. (Deuxième scénario, ci-dessus). |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


En cas de réussite, cette méthode retourne une liste des rôles associés au compte d’utilisateur donné.

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
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
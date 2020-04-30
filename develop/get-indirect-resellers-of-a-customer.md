---
title: Obtenir les revendeurs indirects d’un client
description: Obtention d’une liste des revendeurs indirects qui ont une relation avec un client spécifié.
ms.assetid: C3C4BE9A-97E8-41AD-AB28-6F9CB7DCE475
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8ea8422bb31e5614d714323b065fb866d52b4c2a
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157491"
---
# <a name="get-indirect-resellers-of-a-customer"></a>Obtenir les revendeurs indirects d’un client

**S’applique à**

- Espace partenaires

Obtention d’une liste des revendeurs indirects qui ont une relation avec un client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

## <a name="c"></a>C\#

Pour récupérer une liste des revendeurs indirects avec lesquels le client spécifié a une relation, commencez par obtenir une interface pour les opérations de regroupement client pour le client spécifique à partir de la propriété [**partnerOperations. Customers**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) en fournissant l’ID client pour identifier le client. Appelez ensuite la méthode [**relations. obten**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) ou la méthode [**\_Async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) pour récupérer la liste des revendeurs indirects.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

**Exemple**:**projet**d' [application de test console](console-test-app.md): **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetIndirectResellersOfCustomer.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Relationships http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de chemin d’accès suivant pour identifier le client.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Response REST

En cas de réussite, le corps de la réponse contient une collection de ressources [PartnerRelationship](relationships-resources.md) pour identifier les revendeurs.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

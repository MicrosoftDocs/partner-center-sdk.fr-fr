---
title: Récupérer la liste des revendeurs indirects
description: Comment récupérer la liste des revendeurs indirects du partenaire connecté.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d7b8962c24a00ac6892279e7b7c08c4144514f3
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007707"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Récupérer la liste des revendeurs indirects

**S’applique à**

- Espace partenaires

Comment récupérer la liste des revendeurs indirects du partenaire connecté.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

## <a name="c"></a>C\#

Pour récupérer une liste des revendeurs indirects avec lesquels le partenaire connecté a une relation, commencez par obtenir une interface pour les opérations de collection de relations à partir de la propriété [**partnerOperations. Relationships**/dotnet/API/Microsoft.Store.partnercenter.ipartner.Relationships). Appelez ensuite la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.Relationships.irelationshipcollection.Get) ou [**obtenir \_ Async**/dotnet/API/Microsoft.Store.partnercenter.Relationships.irelationshipcollection.getasync), en passant un membre de l’énumération [**PartnerRelationshipType**/dotnet/API/Microsoft.Store.partnercenter.Models.Relationships.partnerrelationshiptype) pour identifier le type de relation. Pour récupérer des revendeurs indirectes, vous devez utiliser IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Exemple**:**projet**d' [application de test console](console-test-app.md): **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetIndirectResellers.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Relationships ? type de relation \_ = IsIndirectCloudSolutionProviderOf http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour identifier le type de relation.

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nom</th>
<th>Type</th>
<th>Obligatoire</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>relationship_type</td>
<td>string</td>
<td>Oui</td>
<td>La valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans <a href="/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>PartnerRelationshipType</strong></a>.
<p>Si le partenaire est connecté en tant que fournisseur et que vous souhaitez obtenir la liste des revendeurs indirects avec lesquels ils ont établi une relation, utilisez IsIndirectCloudSolutionProviderOf.</p>
<p>Si le partenaire est connecté en tant que revendeur et que vous souhaitez obtenir la liste des fournisseurs indirects avec lesquels ils ont établi une relation, utilisez IsIndirectResellerOf.</p></td>
</tr>
</tbody>
</table>

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources [PartnerRelationship](relationships-resources.md) pour identifier les revendeurs.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
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
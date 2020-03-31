---
title: Récupérer une liste de revendeurs indirects
description: Comment récupérer la liste des revendeurs indirects du partenaire connecté.
ms.assetid: 1767BD6C-651A-4C14-930B-35D7EFD46C19
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a1ed1d4d3c0d105a489774d698d832f2e0212934
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415383"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Récupérer une liste de revendeurs indirects


**S’applique à**

- Centre pour partenaires

Comment récupérer la liste des revendeurs indirects du partenaire connecté.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer une liste des revendeurs indirects avec lesquels le partenaire connecté a une relation, commencez par obtenir une interface pour les opérations de collection de relations à partir de la propriété [**partnerOperations. Relationships**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) . Appelez ensuite la méthode Async [**ou obtenir**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) [ **\_Async**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) , en passant un membre de l’énumération [**PartnerRelationshipType**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) pour identifier le type de relation. Pour récupérer des revendeurs indirects, vous devez utiliser IsIndirectCloudSolutionProviderOf.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Exemple**:**projet**d' [application de test console](console-test-app.md): **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetIndirectResellers.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode  | URI de demande                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Relationships ? relation\_type = IsIndirectCloudSolutionProviderOf http/1.1 |

 

**Paramètre URI**

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
<td>chaîne</td>
<td>Oui</td>
<td>La valeur est la représentation sous forme de chaîne de l’un des noms de membres trouvés dans <a href="https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype"><strong>PartnerRelationshipType</strong></a>.
<p>Si le partenaire est connecté en tant que fournisseur et que vous souhaitez obtenir la liste des revendeurs indirects avec lesquels ils ont établi une relation, utilisez IsIndirectCloudSolutionProviderOf.</p>
<p>Si le partenaire est connecté en tant que revendeur et que vous souhaitez obtenir la liste des fournisseurs indirects avec lesquels ils ont établi une relation, utilisez IsIndirectResellerOf.</p></td>
</tr>
</tbody>
</table>

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient une collection de ressources [PartnerRelationship](relationships-resources.md) pour identifier les revendeurs.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

**Exemple de réponse**

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

 

 





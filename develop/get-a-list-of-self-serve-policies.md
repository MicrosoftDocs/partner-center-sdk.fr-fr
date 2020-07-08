---
title: Obtenir la liste des stratégies en libre-service
description: Comment obtenir une collection de ressources représentant les stratégies libre-service d’un client.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 8d2e7e461fee0993176f954aab2d020c2bbc9714
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098073"
---
# <a name="get-a-list-of-self-serve-policies"></a>Obtenir la liste des stratégies en libre-service

**S’applique à :**

- Espace partenaires

Cet article explique comment obtenir une collection de ressources qui représentent des stratégies libre-service pour une entité.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                   |
|---------|-------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy ? entity_id = {ENTITY_ID} http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour obtenir la liste des clients.

| Nom          | Type       | Obligatoire | Description                                        |
|---------------|------------|----------|----------------------------------------------------|
| **entity_id** | **string** | O        | Identificateur d’entité demandant l’accès à. Il s’agit de l’ID de locataire du client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md).

### <a name="request-body"></a>Corps de la demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir une liste complète, consultez [codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
        "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
        "selfServeEntity": {
            "selfServeEntityType": "customer",
            "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
        },
        "grantor": {
            "grantorType": "billToPartner",
            "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
        },
        "permissions": [{
            "resource": "AzureReservedInstances",
            "action": "Purchase"
        }],
        "attributes": {
            "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
            "objectType": "SelfServePolicy"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```

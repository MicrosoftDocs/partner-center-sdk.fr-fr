---
title: Recevoir l’état d’adoption de l’authentification MFA
description: Obtenir la liste de l’état d’adoption de Multi-Factor Authentication pour chaque partenaire à l’aide de l’API REST partenaire.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: f82d163b704323c81e2948b78eb9b9d1a14ddc52
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097009"
---
# <a name="get-mfa-adoption-status"></a>Recevoir l’état d’adoption de l’authentification MFA

S’applique à :

- API d’Espace partenaires

Cet article explique comment obtenir l’état d’adoption de l’authentification multifacteur (MFA) pour chaque partenaire au sein d’un locataire.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                               |
|---------|---------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus> |

### <a name="request-headers"></a>En-têtes de requête

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de [demandes d’API synthétisées par](mfa-resources.md#api-request-summarized-by-application) des ressources d’application dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```

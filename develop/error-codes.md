---
title: Partner Center REST error codes
description: Description of error codes and success responses from the Partner Center APIs.
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7f9cb33c2518cef84d6948783da7d2c4337ecfaa
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489669"
---
# <a name="partner-center-rest-error-codes"></a>Partner Center REST error codes

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The Partner Center REST APIs return a JSON object that contains a status code. This code that indicates whether your request was successful or why it failed.

## <a name="success-responses"></a>Success responses

A **2xx** status code indicates that the client's request was successfully received, understood, and accepted.

## <a name="error-codes"></a>Codes d’erreur

The following **4xx** and **5xx** status codes indicate an error:

- 400: Bad request
- 401: Unauthorized
- 403: Forbidden
- 404: Not found
- 405: Method not allowed
- 406: Not acceptable
- 409: Conflict, error code
- 412: Precondition failed
- 429: Too many requests
- 500: Internal server error
- 501: Not implemented
- 502: Bad gateway
- 503: Service unavailable
- 504: Gateway timeout

## <a name="error-responses"></a>Réponses d’erreur

Any response with a **4xx** or **5xx** status code includes an error message with additional details about the error condition(s) encountered.

The following table and code sample describes the schema of an error response:

| Nom        | Tapez   | Description                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | chaîne | Always returned. Indicates the kind of error that occurred. Non-null.                                                                                  |
| description | chaîne | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| data        | tableau  | Only returned for some error types. A list of error objects.                                                                                           |
| source      | chaîne | Always returned. The source of the error.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

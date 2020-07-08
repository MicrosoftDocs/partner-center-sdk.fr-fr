---
title: Créer une stratégie libre-service
description: Comment créer une nouvelle stratégie libre-service.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7440da859a9086513725c27e1d6945a6941eea28
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096201"
---
# <a name="create-a-selfservepolicy"></a>Créer un SelfServePolicy

**S’applique à :**

- Espace partenaires

Cette rubrique explique comment créer une nouvelle stratégie libre-service.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

- Un ID de demande et un ID de corrélation sont requis.
- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                              | Type   | Description                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | Informations de stratégie libre-service. |

#### <a name="selfservepolicy"></a>SelfServePolicy

Ce tableau décrit les champs obligatoires minimaux de la ressource [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) nécessaire à la création d’une nouvelle stratégie libre-service.

| Propriété              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| SelfServeEntity       | SelfServeEntity  | Entité libre-service à laquelle l’accès est accordé.                                                     |
| Fournisseur d'autorisations               | Fournisseur d'autorisations          | Fournisseur d’autorisations qui accorde l’accès.                                                                    |
| Autorisations           | Tableau d’autorisations| Tableau de ressources d' [autorisation](self-serve-policy-resources.md#permission) .                                                                     |


### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
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
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette API retourne une ressource [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) pour la nouvelle stratégie SELD serv.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

Cette méthode retourne les codes d’erreur suivants :

| Code d’état HTTP     | Code d'erreur   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 409                  | 600041       | La stratégie libre-service existe déjà.                                                     |


### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
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
}
```

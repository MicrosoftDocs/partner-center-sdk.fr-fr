---
title: Obtenir l’état de signature directe du client pour le contrat client Microsoft.
description: Vous pouvez utiliser la ressource DirectSignedCustomerAgreementStatus pour obtenir l’état de la signature directe d’un client (acceptation directe) du contrat de client Microsoft.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0d07630a23ad4d18f992f2fcd9db2d19c637df98
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415954"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Obtenir l’état de la signature directe d’un client (acceptation directe) du contrat de client Microsoft

S'applique à :

- Centre pour partenaires

La ressource **DirectSignedCustomerAgreementStatus** est actuellement prise en charge par l’espace partenaires uniquement dans le cloud public Microsoft.

Cette ressource ne s' *applique pas* aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment vous pouvez récupérer l’état de l’acceptation directe d’un client du contrat de client Microsoft.

## <a name="rest-request"></a>Demande REST

Pour récupérer l’état de l’acceptation directe d’un client du contrat de client Microsoft, créez une demande REST pour récupérer les [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) du client. 

### <a name="request-syntax"></a>Syntaxe de la requête

Utilisez la syntaxe de requête suivante :

| Méthode | URI de demande                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1 |

### <a name="uri-parameters"></a>Paramètres d’URI

Vous pouvez utiliser les paramètres URI suivants avec votre demande :

| Nom             | Type | Obligatoire | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Oui | La valeur est un **CustomerTenantId** au format GUID qui vous permet de spécifier l’ID de locataire d’un client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une [ressource **DirectSignedCustomerAgreementStatus** ](./customer-agreement-direct-sign-status-resource.md) dans le corps de la réponse.

La ressource a une propriété **IsSigned** qui indique l’état de la signature directe du client (acceptation directe). 

- La valeur **true** indique que l’accord a été signé (accepté) directement par le client.
- La valeur **false** indique que l’accord n’a *pas* été signé (accepté) directement par le client.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. 

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
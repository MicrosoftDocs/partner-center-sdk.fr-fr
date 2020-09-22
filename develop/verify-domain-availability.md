---
title: Vérifier la disponibilité du domaine
description: Comment déterminer si un domaine peut être utilisé.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3f2e3d551da30c7b9c25e1fc3f3280a425aff8f8
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925585"
---
# <a name="verify-domain-availability"></a>Vérifier la disponibilité du domaine

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment déterminer si un domaine peut être utilisé.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un domaine (par exemple `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Pour vérifier si un domaine est disponible, commencez par appeler [**collection iaggregatepartner. Domains**/dotnet/API/Microsoft.Store.partnercenter.ipartner.domains) pour obtenir une interface pour les opérations de domaine. Appelez ensuite la méthode [**ByDomain**/dotnet/API/Microsoft.Store.partnercenter.Domains.idomaincollection.bydomain) avec le domaine à vérifier. Cette méthode récupère une interface pour les opérations disponibles pour un domaine spécifique. Enfin, appelez la méthode [**Exists**/dotnet/API/Microsoft.Store.partnercenter.Domains.idomain.Exists) pour voir si le domaine existe déjà.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CheckDomainAvailability.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de demande                                                              |
|----------|--------------------------------------------------------------------------|
| **SIÈGE** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour vérifier la disponibilité du domaine.

| Nom       | Type       | Obligatoire | Description                                   |
|------------|------------|----------|-----------------------------------------------|
| **Domain** | **string** | O        | Chaîne identifiant le domaine à vérifier. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

Si le domaine existe, il n’est pas utilisable et un code d’état de réponse 200 OK est retourné. Si le domaine est introuvable, il est disponible pour utilisation et un code d’état de réponse 404 introuvable est retourné.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Exemple de réponse lorsque le domaine est déjà utilisé

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Exemple de réponse lorsque le domaine est disponible

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```

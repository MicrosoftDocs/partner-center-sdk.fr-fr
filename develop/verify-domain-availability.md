---
title: Vérifier la disponibilité du domaine
description: Comment déterminer si un domaine peut être utilisé.
ms.assetid: 9ECF8241-3672-441D-B34D-83F7C23138B3
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 79f68fe92f22a4e5a6793f97b55da16adee19b5a
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486239"
---
# <a name="verify-domain-availability"></a>Vérifier la disponibilité du domaine


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment déterminer si un domaine peut être utilisé.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Un domaine (par exemple, « contoso.onmicrosoft.com »).

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour vérifier si un domaine est disponible, appelez d’abord [**collection iaggregatepartner. Domains**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.domains) pour obtenir une interface pour les opérations de domaine. Appelez ensuite la méthode [**ByDomain**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) avec le domaine à vérifier. Cela récupère une interface pour les opérations disponibles pour un domaine spécifique. Enfin, appelez la méthode [**Exists**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) pour voir si le domaine existe déjà.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";  

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CheckDomainAvailability.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode   | URI de requête                                                              |
|----------|--------------------------------------------------------------------------|
| **SIÈGE** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/domains/{domain} http/1.1 |

 

**Paramètre URI**

Utilisez le paramètre de requête suivant pour vérifier la disponibilité du domaine.

| Nom       | Type       | Obligatoire | Description                                   |
|------------|------------|----------|-----------------------------------------------|
| **domain** | **chaîne** | Y        | Chaîne qui identifie le domaine à vérifier. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Aucune

**Exemple de requête**

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

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


Si le domaine existe, il n’est pas utilisable et un code d’état de réponse 200 OK est retourné. Si le domaine est introuvable, il est disponible pour utilisation et un code d’état de réponse 404 introuvable est retourné.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse lorsque le domaine est déjà utilisé**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

**Exemple de réponse lorsque le domaine est disponible**

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```

 

 





---
title: Obtenir des informations sur le déploiement des licences partenaire
description: Comment faire en sorte que les informations de déploiement des licences partenaires soient agrégées pour inclure tous les clients.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ac28f10c8d255d0d4fe7f92e9d1977b16d1ae962
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097734"
---
# <a name="get-partner-licenses-deployment-information"></a>Obtenir des informations sur le déploiement des licences partenaire

**S’applique à**

- Espace partenaires

Comment faire en sorte que les informations de déploiement des licences partenaires soient agrégées pour inclure tous les clients.

> [!NOTE]
> Ce scénario est remplacé par les [informations de déploiement de licences d’extraction](get-licenses-deployment-information.md).

## <a name="prerequisites"></a>Prérequis

Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.

## <a name="c"></a>C\#

Pour récupérer des données agrégées sur le déploiement de licences, commencez par obtenir une interface pour les opérations de collection d’analyse de niveau partenaire à partir de la propriété [**collection iaggregatepartner. Analytics**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) . Ensuite, récupérez une interface vers la collection d’analyse des licences de niveau partenaire à partir de la propriété [**licenses**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) . Enfin, appelez la méthode [**Deployment. obten**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) pour récupérer les données agrégées sur le déploiement de licences. Si la méthode est réussie, vous obtenez une collection d’objets [**PartnerLicensesDeploymentInsights**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) .

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                           |
|---------|---------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/licenses/Deployment http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une collection de ressources [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) qui fournissent des informations sur les licences déployées.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

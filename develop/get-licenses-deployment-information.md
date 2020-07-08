---
title: Obtenir des informations sur le déploiement des licences
description: Comment obtenir des informations de déploiement pour les licences Office et Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6f13a90bcae8099d6a1aa6c85f3ce0e9a29f3a90
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096795"
---
# <a name="get-licenses-deployment-information"></a>Obtenir des informations sur le déploiement des licences

**S’applique à**

- Espace partenaires

Comment obtenir des informations de déploiement pour les licences Office et Dynamics.

## <a name="prerequisites"></a>Prérequis

Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/commercial/Deployment/License/http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="uri-parameters"></a>Paramètres d’URI

| Paramètre         | Type     | Description | Obligatoire |
|-------------------|----------|-------------|----------|
| top               | string   | Le nombre de lignes de données à renvoyer dans la requête. La valeur maximale et la valeur par défaut en l’absence de définition est 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. | No |
| skip              | int      | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, indiquez top=10000 et skip=0 pour obtenir les 10000 premières lignes de données, top=10000 et skip=10000 pour obtenir les 10000 lignes suivantes, et ainsi de suite. | No |
| Filter            | string   | <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction contient un champ et une valeur associés aux **`eq`** **`ne`** opérateurs ou, et les instructions peuvent être combinées à l’aide **`and`** de ou de **`or`** . Voici quelques exemples de paramètres <em>filter</em> :</p><ul><li><em>Filter = serviceCode EQ’O365 '</em></li><li><em>Filter = serviceCode EQ’O365 '</em> ou (<em>Channel EQ’Reseller'</em>)</li></ul><p>Vous pouvez spécifier les champs suivants</p><ul><li><strong>serviceCode</strong></li><li><strong>FormName</strong></li><li><strong>couche</strong></li><li><strong>customerTenantId</strong></li><li><strong>Souhaite</strong></li><li><strong>productId</strong></li><li><strong>ProductName</strong></li></ul> | No |
| groupby           | string   | <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p><ul><li><strong>serviceCode</strong></li><li><strong>FormName</strong></li><li><strong>couche</strong></li><li><strong>customerTenantId</strong></li><li><strong>Souhaite</strong></li><li><strong>productId</strong></li><li><strong>ProductName</strong></li></ul><p>Les lignes de données renvoyées comportent les champs spécifiés dans le paramètre <em>groupby</em>, ainsi que dans les paramètres suivants :</p><ul><li><strong>licensesDeployed</strong></li><li><strong>licensesSold</strong></li></ul> | No |
| processedDateTime | DateTime | Vous pouvez spécifier la date à partir de laquelle les données d’utilisation ont été traitées. La valeur par défaut est la dernière date à laquelle les données ont été traitées. | No |

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient les champs suivants contenant les données relatives aux licences déployées.

| Champ             | Type     | Description                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | string   | Code de service                          |
| serviceName       | string   | Nom du service                          |
| channel           | string   | Nom du canal, revendeur                |
| customerTenantId  | string   | Identificateur unique du client    |
| customerName      | string   | Nom de client                         |
| productId         | string   | Identificateur unique du produit     |
| ProductName       | string   | Nom du produit                          |
| licensesDeployed  | long     | Nombre de licences déployées           |
| licensesSold      | long     | Nombre de licences vendues               |
| processedDateTime | DateTime | Date du dernier traitement des données |

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT
{
  "Value": [

{
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```

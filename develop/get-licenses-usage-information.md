---
title: Get licenses usage information
description: How to get licenses usage information at the workload level for Office and Dynamics.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2f3d5a73ef91a8c85515addfa1c6192886a216d8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488579"
---
# <a name="get-licenses-usage-information"></a>Get licenses usage information

**Applies To**

- Espace partenaires

How to get licenses usage information at the workload level for Office and Dynamics.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with App+User credentials.


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>Request

**Request syntax**

| Méthode  | URI de requête                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

 
**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**URI parameters**

| Paramètre         | Tapez     | Description | Obligatoire |  
|-------------------|----------|-------------|----------|  
| top               | chaîne   | Le nombre de lignes de données à renvoyer dans la requête. La valeur maximale et la valeur par défaut en l’absence de définition est 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. | non | 
| skip              | entier      | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, indiquez top=10000 et skip=0 pour obtenir les 10000 premières lignes de données, top=10000 et skip=10000 pour obtenir les 10000 lignes suivantes, et ainsi de suite. | non | 
| filter            | chaîne   | <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs **eq** ou **ne**, et les instructions peuvent être combinées à l’aide des opérateurs **and** ou **or**. Voici quelques exemples de paramètres <em>filter</em> :</p><ul><li><em>filter=workloadCode eq 'SFB'</em></li><li><em>filter=workloadCode eq 'SFB'</em> or (<em>channel eq 'Reseller'</em>)</li></ul><p>You can specify the following fields</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul> | non | 
| groupby           | chaîne   | <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>serviceName</strong></li><li><strong>channel</strong></li><li><strong>customerTenantId</strong></li><li><strong>customerName</strong></li><li><strong>productId</strong></li><li><strong>productName</strong></li></ul><p>Les lignes de données renvoyées comportent les champs spécifiés dans le paramètre <em>groupby</em>, ainsi que dans les paramètres suivants :</p><ul><li><strong>licensesActive</strong></li><li><strong>licensesQualified</strong></li></ul> | non | 
| processedDateTime | DateTime | One can specify the date from which usage data was processed. Defaults to the latest date when the data was processed | non | 


**Request example**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>Response

If successful, the response body contains the following fields containing data about licenses usage.

| Champ             | Tapez     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | chaîne   | Workload code                                 |
| workloadName      | chaîne   | Workload name                                 |
| serviceCode       | chaîne   | Service code                                  |
| serviceName       | chaîne   | Nom du service                                  |
| channel           | chaîne   | Channel name, reseller                        |
| customerTenantId  | chaîne   | Unique identifier for the customer            |
| customerName      | chaîne   | Nom du client                                 |
| productId         | chaîne   | Unique identifier for the product             |
| productName       | chaîne   | Nom du produit                                  |
| licensesActive    | longue     | Number of active licenses per workload        |
| licensesQualified | longue     | Number of qualified licenses for the workload |
| processedDateTime | DateTime | Date when the data was last processed         |


**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

**Response example**

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
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
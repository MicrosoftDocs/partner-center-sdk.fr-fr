---
title: Recevoir des informations sur l’utilisation des licences
description: Comment obtenir des informations sur l’utilisation des licences au niveau de la charge de travail pour Office et Dynamics.
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
# <a name="get-licenses-usage-information"></a>Recevoir des informations sur l’utilisation des licences

**S’applique à**

- Espace partenaires

Comment obtenir des informations sur l’utilisation des licences au niveau de la charge de travail pour Office et Dynamics.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur.


## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande

**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Analytics/commercial/usage/License/http/1.1 |

 
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Paramètres d’URI**

| Paramètre         | Type     | Description | Obligatoire |  
|-------------------|----------|-------------|----------|  
| top               | chaîne   | Le nombre de lignes de données à renvoyer dans la requête. La valeur maximale et la valeur par défaut en l’absence de définition est 10000. Si la requête comporte davantage de lignes, le corps de la réponse inclut un lien sur lequel vous cliquez pour solliciter la page suivante de données. | Non | 
| skip              | entier      | Le nombre de lignes à ignorer dans la requête. Utilisez ce paramètre pour parcourir de grands ensembles de données. Par exemple, indiquez top=10000 et skip=0 pour obtenir les 10000 premières lignes de données, top=10000 et skip=10000 pour obtenir les 10000 lignes suivantes, et ainsi de suite. | Non | 
| filter            | chaîne   | <p>Le paramètre <em>filter</em> de la requête contient une ou plusieurs instructions qui filtrent les lignes de la réponse. Chaque instruction comporte un champ et une valeur qui sont associés aux opérateurs **eq** ou **ne**, et les instructions peuvent être combinées à l’aide des opérateurs **and** ou **or**. Voici quelques exemples de paramètres <em>filter</em> :</p><ul><li><em>Filter = workloadCode EQ’SFB'</em></li><li><em>Filter = workloadCode EQ’SFB'</em> ou (<em>Channel EQ’Reseller</em>)</li></ul><p>Vous pouvez spécifier les champs suivants</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>FormName</strong></li><li><strong>couche</strong></li><li><strong>customerTenantId</strong></li><li><strong>Souhaite</strong></li><li><strong>Réf</strong></li><li><strong>productName</strong></li></ul> | Non | 
| groupby           | chaîne   | <p>Une instruction qui applique l’agrégation des données uniquement sur les champs spécifiés. Vous pouvez spécifier les champs suivants :</p><ul><li><strong>workloadCode</strong></li><li><strong>workloadName</strong></li><li><strong>serviceCode</strong></li><li><strong>FormName</strong></li><li><strong>couche</strong></li><li><strong>customerTenantId</strong></li><li><strong>Souhaite</strong></li><li><strong>Réf</strong></li><li><strong>productName</strong></li></ul><p>Les lignes de données renvoyées comportent les champs spécifiés dans le paramètre <em>groupby</em>, ainsi que dans les paramètres suivants :</p><ul><li><strong>licensesActive</strong></li><li><strong>licensesQualified</strong></li></ul> | Non | 
| processedDateTime | DateTime | Vous pouvez spécifier la date à partir de laquelle les données d’utilisation ont été traitées. La valeur par défaut est la dernière date à laquelle les données ont été traitées. | Non | 


**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse

En cas de réussite, le corps de la réponse contient les champs suivants contenant les données relatives à l’utilisation des licences.

| Champ             | Type     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | chaîne   | Code de charge de travail                                 |
| workloadName      | chaîne   | Nom de la charge de travail                                 |
| serviceCode       | chaîne   | Code de service                                  |
| FormName       | chaîne   | Nom du service                                  |
| couche           | chaîne   | Nom du canal, revendeur                        |
| customerTenantId  | chaîne   | Identificateur unique du client            |
| Souhaite      | chaîne   | Nom du client                                 |
| productId         | chaîne   | Identificateur unique du produit             |
| productName       | chaîne   | Nom du produit                                  |
| licensesActive    | longue     | Nombre de licences actives par charge de travail        |
| licensesQualified | longue     | Nombre de licences qualifiées pour la charge de travail |
| processedDateTime | DateTime | Date du dernier traitement des données         |


**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

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
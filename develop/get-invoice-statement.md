---
title: Instruction d’extraction de facture
description: Récupère une déclaration de facture à l’aide de l’ID de facture.
ms.assetid: 60EAA1F1-AFE2-4FC3-A475-4DBEA58583D1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 754db08297e7a3205441705ff24a23fc0de3e240
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489369"
---
# <a name="get-invoice-statement"></a>Instruction d’extraction de facture

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Récupère une déclaration de facture à l’aide de l’ID de facture.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Un ID de facture valide.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer une instruction de facture par ID, utilisez votre collection **collection ipartner. Invoices** et appelez la méthode **méthode BYID ()** à l’aide de l’ID de facture, puis appelez les méthodes **documents ()** et **Statement ()** pour accéder à l’instruction de facture. Enfin, appelez les méthodes d' **extraction ()** ou de **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: GetInvoiceStatement.cs 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/documents/Statement http/1.1  |


**Paramètre URI**

Utilisez le paramètre de requête suivant pour obtenir l’instruction de facture.

| Nom       | Type       | Obligatoire | Description                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| ID de la facture | chaîne     | Oui      | La valeur est un ID de facture qui permet au revendeur de filtrer les résultats pour une facture donnée. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucune

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse REST


En cas de réussite, cette méthode retourne une ressource [InvoiceStatement](invoice-resources.md#invoicestatement) dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}  System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}  byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
---
title: Instruction de réception de facture
description: Récupère une déclaration de réception de facture à l’aide de l’ID de facture et de l’ID de reçu.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 11549ad4de66d45f8375a6afb9956b2928c8045f
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489519"
---
# <a name="get-invoice-receipt-statement"></a>Instruction de réception de facture

**S’applique à**

- Espace partenaires

Récupère une déclaration de réception de facture à l’aide de l’ID de facture et de l’ID de reçu. 

> [!IMPORTANT]
> Cette fonctionnalité s’applique uniquement aux recettes fiscales de Taïwan.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Un ID de facture valide et un ID de réception correspondant.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

Pour récupérer une déclaration de facture par ID, commencez par le kit de développement logiciel (SDK) du kit de développement logiciel (SDK) v 1.12.0, utilisez votre collection **collection ipartner. factures** , puis appelez la méthode **méthode BYID ()** à l’aide de l’ID de facture, appelez ensuite la collection de **reçus** et appelez **méthode BYID (** ), puis appelez les méthodes **documents ()** et **Statement ()** pour accéder à l' Enfin, appelez les méthodes d' **extraction ()** ou de **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: GetInvoiceReceiptStatement.cs 

## <a name="span-idrequestspan-idrequestspan-idrequestrest-request"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande REST

**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Receipts/{receipt-ID}/documents/Statement http/1.1 |

**Paramètre URI**

Utilisez le paramètre de requête suivant pour obtenir l’instruction de réception de facture.

| Nom       | Type   | Obligatoire | Description                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| ID de la facture | chaîne | Oui      | La valeur est un ID de facture qui permet au revendeur de filtrer les résultats pour une facture donnée. |
| ID de réception | chaîne | Oui      | La valeur est un ID de réception qui permet au revendeur de filtrer les accusés de réception pour une facture donnée. |
 
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucune

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse REST

En cas de réussite, cette méthode retourne un flux PDF dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}  System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}  byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```

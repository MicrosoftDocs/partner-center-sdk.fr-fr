---
title: Obtenir l’instruction de réception de facture
description: Récupère une déclaration de réception de facture à l’aide de l’ID de facture et de l’ID de reçu.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86093550"
---
# <a name="get-invoice-receipt-statement"></a>Obtenir l’instruction de réception de facture

**S’applique à**

- Espace partenaires

Récupère une déclaration de réception de facture à l’aide de l’ID de facture et de l’ID de reçu.

> [!IMPORTANT]
> Cette fonctionnalité s’applique uniquement aux recettes fiscales de Taïwan.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- Un ID de facture valide et un ID de réception correspondant.

## <a name="c"></a>C\#

Pour récupérer une déclaration de facture par ID, commencez par le kit de développement logiciel (SDK) du kit de développement logiciel (SDK) v 1.12.0, utilisez votre collection **collection ipartner. factures** , puis appelez la méthode **méthode BYID ()** à l’aide de l’ID de facture, appelez ensuite la collection de **reçus** et appelez **méthode BYID (** ), puis appelez les méthodes **documents ()** et **Statement ()** pour accéder à l' Enfin, appelez les méthodes d' **extraction ()** ou de **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Receipts/{receipt-ID}/documents/Statement http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour obtenir l’instruction de réception de facture.

| Nom       | Type   | Obligatoire | Description                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| ID de la facture | string | Oui      | La valeur est un ID de facture qui permet au revendeur de filtrer les résultats pour une facture donnée. |
| ID de réception | string | Oui      | La valeur est un ID de réception qui permet au revendeur de filtrer les accusés de réception pour une facture donnée. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne un flux PDF dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```

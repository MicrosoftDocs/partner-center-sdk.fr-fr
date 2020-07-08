---
title: Obtenir l’instruction de facture
description: Récupère une déclaration de facture à l’aide de l’ID de facture.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096913"
---
# <a name="get-invoice-statement"></a>Obtenir l’instruction de facture

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Récupère une déclaration de facture à l’aide de l’ID de facture.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- Un ID de facture valide.

## <a name="c"></a>C\#

Pour récupérer une instruction de facture par ID, utilisez votre collection **collection ipartner. Invoices** et appelez la méthode **méthode BYID ()** à l’aide de l’ID de facture, puis appelez les méthodes **documents ()** et **Statement ()** pour accéder à l’instruction de facture. Enfin, appelez les méthodes d' **extraction ()** ou de **GetAsync ()** .

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: GetInvoiceStatement.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/documents/Statement http/1.1  |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour obtenir l’instruction de facture.

| Nom       | Type       | Obligatoire | Description                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| ID de la facture | string     | Oui      | La valeur est un ID de facture qui permet au revendeur de filtrer les résultats pour une facture donnée. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource [InvoiceStatement](invoice-resources.md#invoicestatement) dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```

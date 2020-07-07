---
title: Obtenir une collection de factures
description: Comment récupérer un regroupement des factures du partenaire.
ms.assetid: B5392987-3D2E-493B-9F97-A20055D5D46A
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f288dd201faa99480fe42bf190611faaa0cf8b0e
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022566"
---
# <a name="get-a-collection-of-invoices"></a>Obtenir une collection de factures

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment récupérer un regroupement des factures du partenaire.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="c"></a>C\#

Pour obtenir une collection de toutes les factures disponibles, utilisez la propriété [**factures**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) pour obtenir une interface pour facturer les opérations, puis [**appelez la méthode**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) pour récupérer la collection.

Pour obtenir une collection paginée de factures, appelez d’abord la méthode [**BuildIndexedQuery**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) et transmettez-lui la taille de page pour créer un objet [**IQueryable**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.query.iquery) . Ensuite, utilisez la propriété des [**factures**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) pour obtenir une interface pour facturer les opérations, puis transmettez l’objet IQueryable à la méthode [**query**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) ou [**QueryAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) pour envoyer la demande et obtenir la première page.

Ensuite, utilisez la propriété d' [**énumérateurs**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) pour obtenir une interface pour la collection d’énumérateurs de collections de ressources prises en charge, puis appelez [**factures. Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) pour créer un énumérateur qui parcourt la collection de factures. Enfin, utilisez l’énumérateur pour récupérer et utiliser chaque page de factures comme indiqué dans l’exemple de code suivant. Chaque appel à la méthode [**suivante**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) envoie une demande pour la page de factures suivante en fonction de la taille de la page.

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

Pour obtenir un exemple légèrement différent, consultez **exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetPagedInvoices.cs

> [!NOTE] 
> La même API est utilisée pour tous les achats commerciaux modernes, ainsi que pour les licences 145p et Office. La taille et le décalage sont uniquement pris en compte pour les factures héritées. Pour tous les achats commerciaux modernes, le décalage de & de page est ignoré.

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices ? Size = {size} &offset = {offset} http/1.1  |

### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez les paramètres de requête suivants lors de la création de la demande.

| Nom   | Type | Obligatoire | Description                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| taille   | int  | Non       | Nombre de ressources de facture à retourner dans la réponse. Ce paramètre est facultatif. |
| offset | int  | Non       | Index de base zéro de la première facture à retourner.                                   |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

None

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient la collection de ressources de [facture](invoice-resources.md#invoice) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

---
title: Récupérer les éléments de ligne de rapprochement non facturés de la facture
description: Vous pouvez obtenir une collection de détails non facturés pour la période spécifiée à l’aide des API de l’espace partenaires.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3f7bc17100c521aeaf7e0be371591942aab6aa21
ms.sourcegitcommit: 534656a8e1f5f31773721892c4735f14379b1019
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76923085"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a>Récupérer les éléments de ligne de rapprochement non facturés de la facture

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez utiliser les méthodes suivantes pour obtenir une collection de détails pour les Articles de facturation non facturés (également appelés éléments de ligne de facturation ouverts).

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur de la facture. Cela permet d’identifier la facture pour laquelle récupérer les éléments de ligne.

## <a name="c"></a>C\#

Pour obtenir les éléments de ligne de la facture spécifiée, récupérez l’objet de facture :

1. Appelez la méthode [**méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) pour obtenir une interface permettant de facturer les opérations pour la facture spécifiée.
2. Appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pour récupérer l’objet [**de la facture**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) .

L’objet Invoice contient toutes les informations relatives à la facture spécifiée :

- Le **fournisseur** identifie la source des informations de détail non facturées (par exemple, **OneTime**).
- **InvoiceLineItemType** spécifie le type (par exemple, **BillingLineItem**).

Pour obtenir une collection d’éléments de ligne qui correspondent à une instance **InvoiceDetail** :

1. Transmettez le BillingProvider et le InvoiceLineItemType de l’instance à la méthode [**par**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) .
2. Appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) pour [**récupérer les éléments**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) de ligne associés.
3. Créez un énumérateur pour parcourir la collection. Pour obtenir un exemple, consultez l’exemple de code suivant.

L’exemple de code suivant utilise une boucle **foreach** pour traiter la collection **InvoiceLineItems** . Une collection distincte d’éléments de ligne est récupérée pour chaque **InvoiceLineItemType**.

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Pour obtenir un exemple similaire, consultez :

- Exemple : [application de test](console-test-app.md) de la console
- Projet : **exemples du kit de développement logiciel (SDK) Partner Center**
- Classe : **GetUnBilledReconLineItemsPaging.cs**

## <a name="rest"></a>REST

### <a name="rest-request"></a>Demande REST

#### <a name="request-syntax"></a>Syntaxe de la requête

Vous pouvez utiliser les syntaxes suivantes pour votre demande REST, en fonction de votre cas d’utilisation. Pour plus d’informations, consultez les descriptions de chaque syntaxe.

 | Méthode  | URI de requête            | Description du cas d’usage de syntaxe                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems ? Provider = OneTime & invoicelineitemtype = billinglineitems & CurrencyCode = {currencycode} & période = {period} http/1.1                              | Utilisez cette syntaxe pour retourner une liste complète de chaque élément de ligne pour la facture donnée. |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems ? Provider = OneTime & invoicelineitemtype = billinglineitems & CurrencyCode = {currencycode} & période = {period} & Size = {Size} http/1.1  | Pour les factures volumineuses, utilisez cette syntaxe avec une taille spécifiée et un décalage de base 0 pour retourner une liste paginée d’éléments de ligne. |
| **GET** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/LineItems ? Provider = OneTime & invoicelineitemtype = billinglineitems & CurrencyCode = {currencycode} & période = {period} & Size = {size} & SeekOperation = Next                               | Utilisez cette syntaxe pour accéder à la page suivante des éléments de ligne de rapprochement à l’aide de `seekOperation = "Next"`. |

##### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez l’URI et les paramètres de requête suivants lors de la création de la demande.

| Nom                   | Tapez   | Requis | Description                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| ID de la facture             | chaîne | Oui      | Chaîne qui identifie la facture. Utilisez « non facturé » pour recevoir des estimations non facturées. |
| fournisseur               | chaîne | Oui      | Le fournisseur : « OneTime ».                                                |
| facture-ligne-élément-type | chaîne | Oui      | Type de détail de la facture : « BillingLineItems ».               |
| hasPartnerEarnedCredit | bool   | non       | Valeur indiquant s’il faut retourner les lignes pour lesquelles un crédit gagné est appliqué. Remarque : ce paramètre est appliqué uniquement lorsque le type de fournisseur est OneTime et InvoiceLineItemType est UsageLineItems.
| currencyCode           | chaîne | Oui      | Code de la devise pour les éléments de ligne non facturés.                                  |
| heures                 | chaîne | Oui      | Période pour la conciliation non facturée. exemple : actuel, précédent.                      |
| size                   | nombre | non       | Nombre maximal d’éléments à retourner. La taille par défaut est 2000                     |
| seekOperation          | chaîne | non       | Définissez seekOperation = Next pour afficher la page suivante des éléments de ligne de rapprochement.                |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md).

#### <a name="request-body"></a>Corps de demande

Aucune.

### <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient la collection des détails de l’élément de ligne.

*Pour l’élément de ligne **ChargeType**, la valeur **Purchase** est mappée sur **New** et le **remboursement** de valeur est mappé sur **Cancel**.*

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="request-response-examples"></a>Exemples de requêtes-réponses

#### <a name="request-response-example-1"></a>Exemple de requête-réponse 1

Les détails suivants s’appliquent à cet exemple :

- Fournisseur : **OneTime**
- InvoiceLineItemType : **BillingLineItems**
- Période : **précédente**

#### <a name="request-example-1"></a>Exemple de requête 1

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a>Exemple de réponse 1

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>Exemple de requête-réponse 2

Les détails suivants s’appliquent à cet exemple :

- Fournisseur : **OneTime**
- InvoiceLineItemType : **BillingLineItems**
- Période : **précédente**
- SeekOperation : **suivant**

#### <a name="request-example-2"></a>Exemple de requête 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a>Exemple de réponse 2

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a>Exemple de requête 3

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a>Exemple de réponse 3

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

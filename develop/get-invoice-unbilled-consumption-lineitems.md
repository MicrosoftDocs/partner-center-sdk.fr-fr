---
title: Obtient les éléments de ligne de facturation commerciale non facturés
description: Vous pouvez obtenir une collection de détails sur la facturation commerciale non facturée pour une facture spécifiée à l’aide des API de l’espace partenaires.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a10ae8fb580b89c6e8bb95035620457f88046d6a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927070"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a>Obtient les éléments de ligne de facturation commerciale non facturés

**S’applique à :**

- Espace partenaires

Procédure d’obtention d’un regroupement de détails sur les lignes de consommation commerciale non facturées.

Vous pouvez utiliser les méthodes suivantes pour obtenir une collection de détails lignes de consommation commerciale non facturées (également appelées « éléments de ligne d’utilisation ouverts ») par programmation.

>[!NOTE]
>L’utilisation à l’aide d’une évaluation quotidienne prend normalement 24 heures pour s’afficher dans l’espace partenaires ou pour être accessible via l’API.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Identificateur de la facture. Cela permet d’identifier la facture pour laquelle récupérer les éléments de ligne.

## <a name="c"></a>C\#

Pour obtenir les lignes de la facture spécifiée :

1. Appelez la méthode [**méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoicecollection.BYID) pour obtenir une interface permettant de facturer les opérations pour la facture spécifiée.

2. Appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoice.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoice.getasync) pour récupérer l’objet de la facture.

L' **objet Invoice** contient toutes les informations relatives à la facture spécifiée. Le **fournisseur** identifie la source des informations de détail non facturées (par exemple, **OneTime**). **InvoiceLineItemType** spécifie le type (par exemple, **UsageLineItem**).

L’exemple de code suivant utilise une boucle **foreach** pour traiter la collection **InvoiceLineItems** . Une collection distincte d’éléments de ligne est récupérée pour chaque **InvoiceLineItemType**.

Pour obtenir une collection d’éléments de ligne qui correspondent à une instance **InvoiceDetail** :

1. Transmettez les **BillingProvider** et **InvoiceLineItemType** de l’instance à la méthode [**by**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoice.by).

2. Appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoice.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.Invoices.iinvoice.getasync) pour récupérer les éléments de ligne associés.
3. Créez un énumérateur pour parcourir la collection comme indiqué dans l’exemple suivant.

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Pour obtenir un exemple similaire, consultez :

- Exemple : [Application de test de console](console-test-app.md)
- Projet : **exemples du kit de développement logiciel (SDK) Partner Center**
- Classe : **GetUnBilledConsumptionReconLineItemsPaging.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

Vous pouvez utiliser les syntaxes suivantes pour votre demande REST, en fonction de votre cas d’utilisation. Pour plus d’informations, consultez les descriptions de chaque syntaxe.

 | Méthode  | URI de demande         | Description du cas d’usage de syntaxe |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems ? Provider = OneTime&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &période = {period} http/1.1                              | Utilisez cette syntaxe pour retourner une liste complète de chaque élément de ligne pour la facture donnée. |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems ? Provider = OneTime&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &période = {period} &Size = {Size} http/1.1  | Utilisez cette syntaxe pour les factures volumineuses. Utilisez cette syntaxe avec une taille spécifiée et un décalage de base 0 pour retourner une liste paginée d’éléments de ligne. |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/unbilled/LineItems ? Provider = OneTime&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &période = {period} &Size = {size} &SeekOperation = Next                               | Utilisez cette syntaxe pour accéder à la page suivante des éléments de ligne de rapprochement à l’aide de `seekOperation = "Next"` . |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez l’URI et les paramètres de requête suivants lors de la création de la demande.

| Nom                   | Type   | Obligatoire | Description                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| provider               | string | Oui      | Le fournisseur : «**OneTime**».                                                |
| invoice-line-item-type | string | Oui      | Type de détail de la facture : «**UsageLineItems**», «**UsageLineItems**».               |
| currencyCode           | string | Oui      | Code de la devise pour les éléments de ligne non facturés.                                  |
| heures                 | string | Oui      | Période pour le rapprochement non facturé (par exemple : **actuel**, **précédent**).<br/><br/>**Précédent** : si le cycle de facturation est de 01/01/2020 – 01/31/2020, il est probable que votre facture soit générée entre 02/06/2020 et 02/08/2020 heure UTC. Si vous avez besoin d’interroger vos données d’utilisation non facturées du cycle de facturation (01/01/2020 – 01/31/2020) à tout moment entre 02/01/2020 et la date générée par la facture (qui est comprise entre 02/06/2020 et 02/08/2020 heure UTC), vous devez choisir période comme « précédent ».<br/><br/>**Actuel** : si le cycle de facturation est de 01/01/2020 – 01/31/2020, il est probable que votre facture soit générée entre 02/06/2020 et 02/08/2020 heure UTC. Si vous avez besoin d’interroger vos données d’utilisation non facturées du cycle de facturation (01/01/2020 – 01/31/2020) à tout moment entre 01/01/2020 et 01/31/2020 qui se trouve dans votre cycle de facturation, vous devez choisir période comme « en cours ». |
| taille                   | nombre | Non       | Nombre maximal d’éléments à retourner. La taille par défaut est 2000.                    |
| seekOperation          | string | Non       | Défini `seekOperation=Next` pour afficher la page suivante des éléments de ligne de rapprochement.                |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient la collection des détails de l’élément de ligne.

*Pour l’élément de ligne **ChargeType**, la valeur **Purchase** est mappée sur **New** et le **remboursement** de valeur est mappé sur **Cancel**.*

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

## <a name="request-response-examples"></a>Exemples de requêtes-réponses

### <a name="request-response-example-1"></a>Exemple de requête-réponse 1

Les détails suivants s’appliquent à cet exemple :

- **Fournisseur**: **OneTime**
- **InvoiceLineItemType**: **UsageLineItems**
- **Période**: **précédente**

#### <a name="request-example-1"></a>Exemple de requête 1

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a>Exemple de réponse 1

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

- **Fournisseur**: **OneTime**
- **InvoiceLineItemType**: **UsageLineItems**
- **Période**: **précédente**
- **SeekOperation**: **suivant**

#### <a name="request-example-2"></a>Exemple de requête 2

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

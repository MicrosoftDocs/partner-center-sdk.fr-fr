---
title: Obtenir la liste des offres de conversion d’essai
description: Comment récupérer la liste des offres de conversion d’évaluation.
ms.assetid: 7B97505F-10B9-4ACD-9307-111FC1E7D042
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 73e8a8752c0e4a754992ce8ccbbeffc9f9df7bca
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490069"
---
# <a name="get-a-list-of-trial-conversion-offers"></a>Obtenir la liste des offres de conversion d’essai


**S’applique à**

- Espace partenaires

Comment récupérer la liste des offres de conversion d’évaluation.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Identificateur du client.
- ID d’abonnement pour un abonnement d’évaluation actif.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour obtenir la liste des conversions d’évaluation disponibles, commencez par utiliser la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**Subscriptions. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) avec l’ID d’abonnement d’évaluation. Ensuite, utilisez la propriété [**conversions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) pour obtenir une interface pour les opérations disponibles sur les conversions, puis [**appelez la méthode**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pour récupérer une collection d’offres de [**conversion**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) disponibles.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId; 

// Get the available conversions.
var conversions = 
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/conversions http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement d’évaluation.

| Nom            | Type   | Obligatoire | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ID client     | chaîne | Oui      | Chaîne au format GUID qui identifie le client.           |
| ID d’abonnement | chaîne | Oui      | Chaîne au format GUID qui identifie l’abonnement d’évaluation. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST


En cas de réussite, le corps de la réponse contient une collection de ressources de [conversion](conversions-resources.md#conversionresult) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

{
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

 

 





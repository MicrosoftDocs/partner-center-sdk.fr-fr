---
title: Convertir un abonnement d’évaluation en payant
description: Conversion d’un abonnement d’évaluation en un abonnement payant.
ms.assetid: 06EB96D7-6260-47E0-ACAE-07D4213BEBB7
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 593b995c8d17ff5bc2425cb9b2672ad1fc125944
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488889"
---
# <a name="convert-a-trial-subscription-to-paid"></a>Convertir un abonnement d’évaluation en payant

S’applique à :

- Espace partenaires

Vous pouvez convertir un abonnement d’évaluation en payant.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Identificateur du client.
- ID d’abonnement pour un abonnement d’évaluation actif.
- Offre de conversion disponible.

## <a name="convert-a-trial-subscription-to-paid-through-code"></a>Conversion d’un abonnement d’évaluation en paiement par code

Pour convertir un abonnement d’évaluation en un abonnement payant, vous devez d’abord obtenir un regroupement des conversions d’essai disponibles. Ensuite, vous devez choisir l’offre de conversion que vous souhaitez acheter.

Les offres de conversion spécifient une quantité qui utilise par défaut le même nombre de licences que l’abonnement d’évaluation. Vous pouvez modifier cette quantité en affectant à la propriété [**Quantity**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) le nombre de licences que vous souhaitez acheter.

> [!NOTE]
> Quel que soit le nombre de licences achetées, l’ID d’abonnement de l’essai est réutilisé pour les licences achetées. En conséquence, l’essai en vigueur disparaît et est remplacé par l’achat.

Procédez comme suit pour convertir un abonnement d’évaluation par le biais du code :

1. Procurez-vous une interface pour les opérations d’abonnement disponibles. Vous devez identifier le client et spécifier l’identificateur d’abonnement de l’abonnement d’évaluation.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Obtenir une collection des offres de conversion disponibles. Pour plus d’informations et des détails sur la requête/réponse pour cette méthode, consultez [obtenir une liste des offres de conversion d’évaluation](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Choisissez une offre de conversion. Le code suivant choisit la première offre de conversion dans la collection.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. Si vous le souhaitez, spécifiez le nombre de licences à acheter. La valeur par défaut est le nombre de licences dans l’abonnement d’évaluation.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) pour convertir l’abonnement d’évaluation en payant.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>\# C

Pour convertir un abonnement d’évaluation en un abonnement payant :

1. Utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client.
2. Procurez-vous une interface pour les opérations d’abonnement en appelant la méthode [**Subscriptions. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) avec l’ID d’abonnement d’évaluation. Enregistrer une référence à l’interface des opérations d’abonnement dans une variable locale.
3. Utilisez la propriété [**conversions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) pour obtenir une interface pour les opérations disponibles sur les conversions, puis [**appelez la méthode**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) pour récupérer une collection d’offres de [**conversion**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) disponibles. Vous devez en choisir un. L’exemple suivant est la première conversion disponible par défaut.
4. Utilisez la référence à l’interface d’opérations d’abonnement que vous avez enregistrée dans une variable locale et la propriété [**conversions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) pour obtenir une interface pour les opérations disponibles sur les conversions.
5. Transmettez l’objet de l’offre de conversion sélectionné à la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) pour tenter la conversion de l’essai.

### <a name="c-example"></a>C#Tels

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Publier** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/conversions http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement d’évaluation.

| Nom            | Type   | Obligatoire | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ID client     | chaîne | Oui      | Chaîne au format GUID qui identifie le client.           |
| ID d’abonnement | chaîne | Oui      | Chaîne au format GUID qui identifie l’abonnement d’évaluation. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la requête

Une ressource de [conversion](conversions-resources.md#conversion) remplie doit être incluse dans le corps de la demande.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une ressource [ConversionResult](conversions-resources.md#conversionresult) .

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
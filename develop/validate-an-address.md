---
title: Valider une adresse
description: Comment valider une adresse à l’aide de l’API de validation d’adresse.
ms.assetid: 38A136CD-5E42-46D2-85A4-ED08E30444B8
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 79a4abf7c9aaf791421f008221d32a89c18f5867
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995204"
---
# <a name="validate-an-address"></a>Valider une adresse

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment valider une adresse à l’aide de l’API de validation d’adresse.

L’API de validation d’adresse doit être utilisée uniquement pour la pré-validation des mises à jour de profil client. Utilisez-le pour comprendre que si le pays est le États-Unis, le Canada, la Chine ou le Mexique, le champ État est validé par rapport à une liste d’États valides pour le pays respectif. Dans tous les autres pays, ce test n’a pas lieu, et l’API vérifie uniquement que l’État est une chaîne valide.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>exemples

### <a name="c"></a>C#

Pour valider une adresse, commencez par instancier un nouvel objet d' **adresse** et remplissez-le avec l’adresse à valider. Ensuite, récupérez une interface pour les opérations de **validations** à partir de la propriété **collection iaggregatepartner. validations** et appelez la méthode **IsAddressValid** avec l’objet Address.

```csharp
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",    
    Country = "US"
};

// Validate the address.
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";
             
    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);
    
    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

### <a name="java"></a>Java

Pour valider une adresse, commencez par instancier un nouvel objet d' **adresse** et remplissez-le avec l’adresse à valider. Ensuite, récupérez une interface pour les opérations de **validations** à partir de la fonction **collection iaggregatepartner. getValidations** , puis appelez la méthode **isAddressValid** avec l’objet Address.

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");
    
    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour valider une adresse, exécutez [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) avec les paramètres d’adresse remplis.

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST

**Syntaxe de la demande**

| Méthode   | URI de requête                                                                 |
|----------|-----------------------------------------------------------------------------|
| **POST** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/validations/Address http/1.1 |

**En-têtes de requête**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom         | Tapez   | Obligatoire | Description                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | chaîne | Y        | Première ligne de l’adresse.                             |
| addressline2 | chaîne | N        | Deuxième ligne de l’adresse. Cette propriété est facultative. |
| city         | chaîne | Y        | Ville.                                                  |
| État        | chaîne | Y        | État.                                                 |
| postalcode   | chaîne | Y        | Le code postal.                                           |
| country      | chaîne | Y        | Le code pays alpha-2 ISO à deux caractères.                |

**Exemple de demande**

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse

En cas de réussite, la méthode retourne un code d’état 200, comme illustré dans l’exemple de validation de réponse qui a réussi, comme indiqué ci-dessous.

Si la requête échoue, la méthode retourne le code d’état 400, comme illustré dans l’exemple d’échec de validation de réponse illustré ci-dessous. Le corps de la réponse contient une charge utile JSON avec des informations supplémentaires sur l’erreur.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Réponse-exemple de validation réussie**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

**Réponse-exemple d’échec de validation**

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```

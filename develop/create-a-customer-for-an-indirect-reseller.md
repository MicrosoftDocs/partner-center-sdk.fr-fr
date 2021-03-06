---
title: Créer un client pour un revendeur indirect
description: Un fournisseur indirect peut créer un client pour un revendeur indirect.
ms.date: 06/03/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e3366f60aea9262b3d6532aded5c595b91eb9cb5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927857"
---
# <a name="create-a-customer-for-an-indirect-reseller"></a>Créer un client pour un revendeur indirect

**S’applique à :**

- Espace partenaires

Un fournisseur indirect peut créer un client pour un revendeur indirect.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- Identificateur du locataire du revendeur indirect.

- Le revendeur indirect doit avoir un partenariat avec le fournisseur indirect.

## <a name="c"></a>C\#

Pour ajouter un nouveau client pour un revendeur indirect :

1. Instanciez un nouvel objet [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) , puis instanciez et remplissez [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) et [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile). Veillez à attribuer l’ID de revendeur indirect à la propriété [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) .

2. Utilisez la propriété [**collection iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) pour accéder à une interface pour les opérations de collection client.

3. Appelez la méthode [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) ou [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) pour créer le client.

### <a name="c-example"></a>\#Exemple C

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                                          | Type   | Obligatoire | Description                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Oui      | Les informations du profil de facturation du client.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Oui      | Les informations du profil de l’entreprise du client.                                                                                                                                                                                                                                                                                                           |
| [AssociatedPartnerId](customer-resources.md#customer) | string | Oui      | ID du revendeur indirect. Le revendeur indirect comme indiqué par l’ID fourni ici doit avoir un partenariat avec le fournisseur indirect, sinon la demande échoue. Notez également que si la valeur AssociatedPartnerId n’est pas fournie, le client est créé en tant que client direct du fournisseur indirect plutôt qu’en tant que revendeur indirect. |

#### <a name="billing-profile"></a>Profil de facturation

Ce tableau décrit les champs obligatoires minimaux de la ressource [CustomerBillingProfile](customer-resources.md#customerbillingprofile) nécessaire à la création d’un nouveau client.

| Nom             | Type                                     | Obligatoire | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| email            | string                                   | Oui      | Adresse e-mail du client.                                                                                                                                                                                   |
| culture          | string                                   | Oui      | La culture par défaut pour la communication et la monnaie, par exemple « en-US ». Consultez [prise en charge des langues et paramètres régionaux pris en charge par l’espace partenaires](partner-center-supported-languages-and-locales.md) pour les cultures prises en charge. |
| langage         | string                                   | Oui      | Langue par défaut. Deux codes de langue de caractères (par exemple `en` ou `fr` ) sont pris en charge.                                                                                                                                |
| nom de la société \_    | string                                   | Oui      | Nom de la société ou de l’Organisation inscrite.                                                                                                                                                                       |
| adresse par défaut \_ | [Adresse](utility-resources.md#address) | Oui      | Adresse inscrite de l’entreprise ou de l’entreprise du client. Pour plus d’informations sur les limitations de longueur, consultez la ressource [Address](utility-resources.md#address) .                                             |

#### <a name="company-profile"></a>Profil de l’entreprise

Ce tableau décrit les champs obligatoires minimaux de la ressource [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) nécessaire à la création d’un nouveau client.

| Nom   | Type   | Obligatoire | Description                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| domaine | string | . Oui     | Le nom de domaine du client, tel que contoso.onmicrosoft.com. |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient une ressource [client](customer-resources.md#customer) pour le nouveau client.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```
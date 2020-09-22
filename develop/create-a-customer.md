---
title: Créer un client
description: Comment créer un nouveau client.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: b82d703b721519ce139fbf1dfcc764796e1c9b9a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926514"
---
# <a name="create-a-customer"></a>Créer un client

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment créer un nouveau client.

> [!IMPORTANT]
> Si vous êtes un fournisseur indirect et que vous souhaitez créer un client pour un revendeur indirect, voir [créer un client pour un revendeur indirect](create-a-customer-for-an-indirect-reseller.md).

En tant que partenaire fournisseur de solutions Cloud (CSP), lorsque vous créez un client, vous pouvez passer des commandes pour le compte du client. Lorsque vous créez un client, vous créez également :

- Objet locataire Azure Active Directory (AD) pour le client.

- Relation entre le revendeur et le client, utilisée pour les privilèges d’administrateur délégué.

- Un nom d’utilisateur et un mot de passe pour se connecter en tant qu’administrateur du client.

Une fois le client créé, veillez à enregistrer l’ID client et Azure AD détails pour une utilisation ultérieure avec le kit de développement logiciel (SDK) de l’espace partenaires (par exemple, la gestion des comptes).

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

> [!IMPORTANT]
> Pour créer un locataire client, vous devez fournir une adresse physique valide pendant le processus de création. Une adresse peut être validée en suivant les étapes décrites dans le scénario [valider une adresse](validate-an-address.md) . Si vous créez un client à l’aide d’une adresse non valide dans l’environnement du bac à sable (sandbox), vous ne pourrez pas supprimer ce locataire client.

## <a name="c"></a>C\#

Pour ajouter un client :

1. Instanciez un nouvel objet [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) . Veillez à renseigner les [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) et [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).

2. Ajoutez le nouveau client à votre collection [**collection iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) en appelant [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) ou [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).

### <a name="c-example"></a>\#Exemple C

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour créer un nouveau client :

1. Créez une nouvelle instance de **CustomerBillingProfile** et des objets **CustomerCompanyProfile** . Veillez à renseigner les champs obligatoires.

2. Créez le client en appelant la fonction **collection iaggregatepartner. getCustomers (). Create** .

### <a name="java-example"></a>Exemple Java

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour créer un client, exécutez la commande [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) .

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                       |
|----------|-------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

- Cette API est idempotent (elle ne produit pas un résultat différent si vous l’appelez plusieurs fois).

- Un ID de demande et un ID de corrélation sont requis.

- Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom                              | Type   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Les informations du profil de facturation du client. |
| [CompanyProfile](#company-profile) | object | Les informations du profil de l’entreprise du client. |

#### <a name="billing-profile"></a>Profil de facturation

Ce tableau décrit les champs obligatoires minimaux de la ressource [CustomerBillingProfile](customer-resources.md#customerbillingprofile) nécessaire à la création d’un nouveau client.

| Nom             | Type                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| email            | string                                   | Adresse e-mail du client.                                                                                                                                                                                   |
| culture          | string                                   | La culture par défaut pour la communication et la monnaie, par exemple « en-US ». Consultez [prise en charge des langues et paramètres régionaux pris en charge par l’espace partenaires](partner-center-supported-languages-and-locales.md) pour les cultures prises en charge. |
| langage         | string                                   | Langue par défaut. Deux codes de langue de caractères (par exemple `en` ou `fr` ) sont pris en charge.                                                                                                                                |
| nom de la société \_    | string                                   | Nom de la société ou de l’Organisation inscrite.                                                                                                                                                                       |
| adresse par défaut \_ | [Adresse](utility-resources.md#address) | Adresse inscrite de l’entreprise ou de l’entreprise du client. Pour plus d’informations sur les limitations de longueur, consultez la ressource [Address](utility-resources.md#address) .                                             |

#### <a name="company-profile"></a>Profil de l’entreprise

Ce tableau décrit les champs obligatoires minimaux de la ressource [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) nécessaire à la création d’un nouveau client.

| Nom   | Type   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| domaine | string | Le nom de domaine du client, tel que contoso.onmicrosoft.com. |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette API retourne une ressource [client](customer-resources.md#customer) pour le nouveau client. Enregistrez l’ID client et les détails de Azure AD pour une utilisation ultérieure avec le kit de développement logiciel (SDK) de l’espace partenaires. Vous en aurez besoin pour une utilisation avec la gestion des comptes, par exemple.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```

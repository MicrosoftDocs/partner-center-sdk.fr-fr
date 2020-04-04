---
title: Confirmer que le client a accepté le Contrat client Microsoft
description: Vérifiez l’acceptation du Contrat client Microsoft par les clients.
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8215fa2a39e269195d2b13d88561b6fbf61875e2
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412868"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>Confirmer que le client a accepté le Contrat client Microsoft

S'applique à :

- Espace partenaires

L’Espace partenaires prend actuellement en charge la confirmation de l’acceptation du Contrat client Microsoft par les clients uniquement dans le *cloud public Microsoft*. Cette fonctionnalité ne s’applique actuellement pas à :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment confirmer ou reconfirmer l’acceptation du Contrat client Microsoft par les clients.

## <a name="prerequisites"></a>Prérequis

- Si vous utilisez le SDK .NET de l’Espace partenaires, la version 1.14 ou une version ultérieure est nécessaire.
- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](./partner-center-authentication.md). *Ce scénario ne prend en charge que l’authentification de l’application et de l’utilisateur.*
- Identificateur d’un client (**customer-tenant-id**).
- Date (**dateAgreed**) à laquelle le client a accepté le Contrat client Microsoft.
- Informations sur l’utilisateur issues de l’organisation du client qui a accepté le Contrat client Microsoft. Cela comprend les éléments suivants :
  - Prénom
  - Nom
  - Adresse de messagerie
  - Numéro de téléphone (facultatif)

## <a name="net"></a>.NET

Pour confirmer ou reconfirmer l’acceptation du Contrat client Microsoft par les clients :

1. Récupérez les métadonnées du Contrat client Microsoft. Vous devez obtenir la valeur **templateId** du Contrat client Microsoft. Pour plus d’informations, consultez [Obtenir les métadonnées du Contrat client Microsoft](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Créez un objet **Agreement** contenant les détails de la confirmation.
3. Utilisez la collection **IAgreggatePartner.Customers** et appelez la méthode **ById** avec la valeur **customer-tenant-id** spécifiée.
4. Utilisez la propriété **Agreements**, puis appelez **Create** ou **CreateAsync**.

```csharp
// string selectedCustomerId;

var agreementToCreate = new Agreement
{
    DateAgreed = DateTime.UtcNow,
    TemplateId = microsoftCustomerAgreementDetails.TemplateId,
    PrimaryContact = new Contact
    {
        FirstName = "Tania",
        LastName = "Carr",
        Email = "someone@example.com",
        PhoneNumber = "1234567890"
    }
};

Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
```

Vous trouverez un exemple complet dans la classe [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) à partir du projet d’[application de test de console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples).


## <a name="rest-request"></a>Demande REST

Pour confirmer ou reconfirmer l’acceptation du Contrat client Microsoft par les clients :

1. Récupérez les métadonnées du Contrat client Microsoft. Vous devez obtenir la valeur **templateId** du Contrat client Microsoft. Pour plus d’informations, consultez [Obtenir les métadonnées du Contrat client Microsoft](get-customer-agreement-metadata.md).
2. Créez une [ressource **Agreement**](agreement-resources.md) pour confirmer qu’un client a accepté le Contrat client Microsoft. Utilisez la [syntaxe de requête REST](#request-syntax) suivante.

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client que vous confirmez.

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Oui | La valeur est un paramètre **customer-tenant-id** au format GUID, à savoir un identificateur qui vous permet de spécifier un client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés nécessaires dans le corps de la requête REST.

| Nom      | Type   | Description                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| Contrat | objet | Détails fournis par le partenaire pour confirmer l’acceptation du Contrat client Microsoft par les clients. |  

#### <a name="agreement"></a>Contrat

Ce tableau décrit les champs obligatoires pour créer une [ressource **Agreement**](agreement-resources.md).

| Propriété       | Type   | Description                              |
|----------------|--------|------------------------------------------|
| primaryContact | [Contact](./utility-resources.md#contact) | Informations sur l’utilisateur issues de l’organisation du client qui a accepté le Contrat client Microsoft, notamment : **firstName**, **lastName**, **email** et **phoneNumber** (facultatif). |
| dateAgreed     | Chaîne au format date/heure UTC |Date à laquelle le client a accepté le contrat. |
| templateId     | string | Identificateur unique du type de contrat accepté par le client. Vous pouvez obtenir la valeur de **templateId** du Contrat client Microsoft en récupérant les métadonnées du Contrat client Microsoft. Consultez [Obtenir les métadonnées du Contrat client Microsoft](./get-customer-agreement-metadata.md) pour plus d’informations. |
| type           | string | Type de contrat accepté par le client. Utilisez « MicrosoftCustomerAgreement » si le client a accepté le Contrat client Microsoft. |
  
#### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une [ressource **Agreement**](./agreement-resources.md).

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. 

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

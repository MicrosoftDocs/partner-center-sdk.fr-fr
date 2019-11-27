---
title: Confirmer l’acceptation du client du contrat client Microsoft
description: Confirmez l’acceptation du client du contrat du client Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c3acea0f2e45b53fde7372bbb1f33fcb9de13
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488949"
---
# <a name="confirm-customer-acceptance-of-microsoft-customer-agreement"></a>Confirmer l’acceptation du client du contrat client Microsoft

S’applique à :

- Espace partenaires

L’espace partenaires prend actuellement en charge la confirmation de l’acceptation par le client du contrat de licence Microsoft uniquement dans le *cloud public Microsoft*. Cette fonctionnalité ne s’applique pas actuellement à :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment confirmer ou reconfirmer l’acceptation du client par le contrat de client Microsoft.

## <a name="prerequisites"></a>Conditions préalables

- Si vous utilisez le kit de développement logiciel (SDK) .NET de l’espace partenaires, la version 1,14 ou une version ultérieure est requise.
- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](./partner-center-authentication.md). *Ce scénario ne prend en charge que l’authentification d’application + utilisateur.*
- Identificateur du client (**Customer-client-ID**).
- Date (**dateAgreed**) à laquelle le client a accepté le contrat du client Microsoft.
- Informations sur l’utilisateur de l’organisation client qui a accepté le contrat du client Microsoft. Cela comprend les éléments suivants :
  - Prénom
  - Nom
  - Adresse électronique
  - Numéro de téléphone (facultatif)

## <a name="net"></a>.NET

Pour confirmer ou reconfirmer l’acceptation du client du contrat du client Microsoft :

1. Récupérez les métadonnées de l’accord pour le contrat client Microsoft. Vous devez obtenir l' **TemplateID** du contrat du client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Créez un nouvel objet de **contrat** contenant les détails de la confirmation.
3. Utilisez la collection **IAgreggatePartner. Customers** et appelez la méthode **méthode BYID** avec l' **ID de locataire client**spécifié.
4. Utilisez la propriété **Agreements** , suivie de l’appel de **Create** ou de **CreateAsync**.

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

Un exemple complet est disponible dans la classe [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .


## <a name="rest-request"></a>Demande REST

Pour confirmer ou reconfirmer l’acceptation du client du contrat du client Microsoft :

1. Récupérez les métadonnées de l’accord pour le contrat client Microsoft. Vous devez obtenir l' **TemplateID** du contrat du client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour le contrat client Microsoft](get-customer-agreement-metadata.md).
2. Créez une nouvelle [ressource de **contrat** ](agreement-resources.md) pour confirmer qu’un client a accepté le contrat du client Microsoft. Utilisez la [syntaxe de requête Rest](#request-syntax)suivante.

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client que vous confirmez.

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| client-locataire-ID | GUID | Oui | La valeur est un **client-client-ID**au format GUID, qui est un identificateur qui vous permet de spécifier un client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md).

### <a name="request-body"></a>Corps de la requête

Ce tableau décrit les propriétés requises dans le corps de la demande REST.

| Nom      | Type   | Description                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| Contrat | objet | Détails fournis par le partenaire pour confirmer l’acceptation du client du contrat du client Microsoft. |  

#### <a name="agreement"></a>Contrat

Ce tableau décrit les champs obligatoires minimum pour créer une [ressource de **contrat** ](agreement-resources.md).

| Propriété       | Type   | Description                              |
|----------------|--------|------------------------------------------|
| PrimaryContact | [Communiquer](./utility-resources.md#contact) | Informations sur l’utilisateur de l’organisation client qui a accepté le contrat de Microsoft Cloud, notamment les suivants : **FirstName**, **LastName**, **email** et **phoneNumber** (facultatif) |
| dateAgreed     | chaîne au format date/heure UTC |Date à laquelle le client a accepté le contrat. |
| templateId     | chaîne | Identificateur unique du type de contrat accepté par le client. Vous pouvez obtenir l' **TemplateID** pour le contrat de client Microsoft en extrayant les métadonnées de l’accord pour le contrat de client Microsoft. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](./get-customer-agreement-metadata.md) . |
| type           | chaîne | Type de contrat accepté par le client. Utilisez « MicrosoftCustomerAgreement » si le client a accepté le contrat du client Microsoft. |
  
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

En cas de réussite, cette méthode retourne une ressource d' [ **accord** ](./agreement-resources.md).

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. 

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

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

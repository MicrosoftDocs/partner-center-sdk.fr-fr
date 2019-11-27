---
title: Confirmer l’acceptation du client du contrat de Microsoft Cloud
description: Comment confirmer l’acceptation du client du contrat de Microsoft Cloud.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1a0cf111f19d5dc16b000642bcd0b060822369e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488939"
---
# <a name="confirm-customer-acceptance-of-microsoft-cloud-agreement"></a>Confirmer l’acceptation du client du contrat de Microsoft Cloud

S’applique à :

- Espace partenaires

> [!NOTE]  
> La ressource d' **accord** est actuellement prise en charge par l’espace partenaires dans le cloud public Microsoft uniquement. Elle ne s’applique pas aux éléments suivants :
> - Espace partenaires géré par 21Vianet
> - Espace partenaires de Microsoft Cloud Germany
> - Espace partenaires de Microsoft Cloud for US Government

Comment confirmer l’acceptation du client du contrat de Microsoft Cloud.

## <a name="prerequisites"></a>Conditions préalables

- Si vous utilisez le kit de développement logiciel (SDK) .NET de l’espace partenaires, la version 1,9 ou une version ultérieure est requise.
- Si vous utilisez le kit de développement logiciel (SDK) Java de l’espace partenaires, la version 1,8 ou une version ultérieure est requise.
- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](./partner-center-authentication.md). Ce scénario ne prend en charge que l’authentification d’application + utilisateur.
- ID client (client-locataire-ID).
- Date à laquelle le client a accepté le contrat de Microsoft Cloud.
- Informations sur l’utilisateur de l’organisation qui a accepté le contrat de Microsoft Cloud, y compris :
  - Prénom
  - Nom
  - Adresse électronique
  - Numéro de téléphone (facultatif)


## <a name="net-version-114-or-newer"></a>.NET (version 1,14 ou ultérieure)

Pour confirmer ou reconfirmer l’acceptation du client du contrat du client Microsoft :

1. Récupérez les métadonnées d’accord pour l’accord de Microsoft Cloud. Vous devez obtenir l' **TemplateID** du contrat de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Créez un nouvel objet de **contrat** contenant les détails de la confirmation.
3. Utilisez la collection **IAgreggatePartner. Customers** et appelez la méthode **méthode BYID** avec l' **ID de locataire client**spécifié.
4. Utilisez la propriété **Agreements** , suivie de l’appel de **Create** ou de **CreateAsync**.

```csharp
// string selectedCustomerId;

var agreementToCreate = new Agreement
{
    DateAgreed = DateTime.UtcNow,
    TemplateId = microsoftCloudAgreementDetails.TemplateId,
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

## <a name="net-version-19---113"></a>.NET (version 1,9-1,13)

Pour confirmer ou reconfirmer qu’un client a accepté le contrat de Microsoft Cloud :

1. Récupérez les métadonnées d’accord pour l’accord de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) . Cette étape est nécessaire pour obtenir l' **TemplateID** du contrat de Microsoft Cloud.

    ```csharp
    /// IAggregatePartner partnerOperations;
    var agreements = partnerOperations.AgreementDetails.Get();

    AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
    ```

2. Créez un nouvel objet de **contrat** contenant les détails de la confirmation. Utilisez ensuite la collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID** avec l’ID du client spécifié. Ensuite, appelez la propriété **Agreements** , suivie de l’appel de **Create** ou de **CreateAsync**.

    ``` csharp
    // string selectedCustomerId;

    var agreementToCreate = new Agreement
    {
        PrimaryContact = new Contact
        {
            FirstName = "Tania",
            LastName = "Carr",
            Email = "someone@example.com",
            PhoneNumber = "1234567890"
        },
        TemplateId = microsoftCloudAgreement.TemplateId,
        DateAgreed = DateTime.UtcNow,
        Type = AgreementType.MicrosoftCloudAgreement
    };

    Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
    ```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour confirmer ou reconfirmer qu’un client a accepté le contrat de Microsoft Cloud :

1. Récupérez les métadonnées d’accord pour l’accord de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) . Cette étape est nécessaire pour obtenir l' **TemplateID** du contrat de Microsoft Cloud.

    ```java
    /// IAggregatePartner partnerOperations;

    ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();
    AgreementMetaData microsoftCloudAgreement;

    for (AgreementMetaData metadata : agreements)
    {
        if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
        {
            microsoftCloudAgreement = metadata;
        }
    }
    ```

2. Créez un nouvel objet de **contrat** contenant les détails de la confirmation. Utilisez ensuite la fonction **collection iaggregatepartner. getCustomers** et appelez la fonction **méthode BYID** avec l’identificateur du client spécifié. Ensuite, appelez la propriété **getAgreements** , suivie de l’appel de la fonction **Create** .

    ```java
    // String selectedCustomerId;

    Contact primaryContact = new Contact();

    primaryContact.setEmail("someone@example.com");
    primaryContact.setFirstName("Tania");
    primaryContact.setLastName("Carr");
    primaryContact.setPhoneNumber("1234567890");

    Agreement agreementToCreate = new Agreement();

    agreementToCreate.setContact(primaryContact);
    agreementToCreate.setDateAgreed(new DateTime());
    agreementToCreate.setTemplateId(microsoftCloudAgreement.getTemplateId());
    agreementToCreate.setType(AgreementType.MicrosoftCloudAgreement);

    Agreement agreement = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().create(agreementToCreate);
    ```

Un exemple complet est disponible dans la classe [CreateCustomerAgreement](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/CreateCustomerAgreement.java) à partir du projet d' [application de test console](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour confirmer ou reconfirmer qu’un client a accepté le contrat de Microsoft Cloud :

1. Récupérez les métadonnées d’accord pour l’accord de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) . Cette étape est nécessaire pour obtenir l' **TemplateID** du contrat de Microsoft Cloud.  

    ```powershell  
    $agreement = Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
    ```  

2. Exécuter la commande [**New-PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/new-partnercustomeragreement)  

    ```powershell  
    New-PartnerCustomerAgreement -TemplateId $agreement.TemplateId -AgreementType MicrosoftCloudAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec' -ContactEmail 'someone@example.com' -ContactFirstName 'Tania' -ContactLastName 'Carr'
    ```  

## <a name="rest"></a>REST

Pour confirmer ou reconfirmer qu’un client a accepté le contrat de Microsoft Cloud, consultez les instructions suivantes.

### <a name="rest-request"></a>Demande REST

1. Récupérez les métadonnées d’accord pour l’accord de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) . Cette étape est nécessaire pour obtenir l' **TemplateID** du contrat de Microsoft Cloud.
2. Créez une ressource pour confirmer qu’un client a accepté le contrat de Microsoft Cloud. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) .

Pour créer une nouvelle ressource de **contrat** pour confirmer qu’un client a accepté le contrat de Microsoft Cloud :

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client que vous confirmez.

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| client-locataire-ID | GUID | Y        | La valeur est un GUID **client-ID-client-ID** qui vous permet de spécifier un client. |

#### <a name="request-headers"></a>En-têtes de requête

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

#### <a name="request-body"></a>Corps de la requête

Ce tableau décrit les propriétés requises dans le corps de la demande.

| Nom      | Type   | Description                                                                                  |  
|-----------|--------|----------------------------------------------------------------------------------------------|  
| Contrat | objet | Détails fournis par le partenaire pour confirmer l’acceptation du client du contrat de Microsoft Cloud. |  

#### <a name="agreement"></a>Contrat

Ce tableau décrit les champs obligatoires minimum pour créer une ressource de **contrat** .

| Propriété       | Type   | Description                              |
|----------------|--------|------------------------------------------|
| PrimaryContact | [Communiquer](./utility-resources.md#contact) | Informations sur l’utilisateur de l’organisation client qui a accepté le contrat de Microsoft Cloud, notamment les suivants : **FirstName**, **LastName**, **email** et **phoneNumber** (facultatif) |
| dateAgreed     | chaîne au format date/heure UTC |Date à laquelle le client a accepté le contrat. |
| templateId     |chaîne | Identificateur unique du type de contrat accepté par le client. Vous pouvez obtenir l' **TemplateID** pour Microsoft Cloud accord en extrayant les métadonnées de l’accord pour Microsoft Cloud accord. Pour plus d’informations, consultez [obtenir les métadonnées de l’accord pour Microsoft Cloud accord](get-agreement-metadata.md) . |
| type           |Énumération AgreementType | Type de contrat accepté par le client. Actuellement, la seule valeur prise en charge est « MicrosoftCloudAgreement ». |
  
#### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCloudAgreement"
}
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource d' **accord** .

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

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
    "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCloudAgreement"
}
```

---

---
title: Recevoir la confirmation de l’acceptation du client du contrat de Microsoft Cloud
description: Cette rubrique explique comment demander la confirmation de l’acceptation du client du contrat de Microsoft Cloud.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ae40cd3c9805ee8ddaae6d98fd0d6b61ede8d40
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74485659"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a>Obtenir une confirmation de l'acceptation du contrat Microsoft Cloud par le client

**S’applique à**

- Espace partenaires

> [!NOTE]  
> La ressource d' **accord** est actuellement prise en charge par l’espace partenaires dans le cloud public Microsoft uniquement. Elle ne s’applique pas aux éléments suivants :
> - Espace partenaires géré par 21Vianet
> - Espace partenaires de Microsoft Cloud Germany
> - Espace partenaires de Microsoft Cloud for US Government

## <a name="prerequisites"></a>Conditions préalables

- Si vous utilisez le kit de développement logiciel (SDK) .NET de l’espace partenaires, la version 1,9 ou une version ultérieure est requise.
- Si vous utilisez le kit de développement logiciel (SDK) Java de l’espace partenaires, la version 1,8 ou une version ultérieure est requise.
- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](./partner-center-authentication.md). Ce scénario prend en charge uniquement l’authentification d’application + utilisateur.
- ID client (client-locataire-ID).

## <a name="net-version-14-or-newer"></a>.NET (version 1,4 ou ultérieure)

Pour récupérer la ou les confirmations de l’acceptation du client qui ont été fournies précédemment :

- Utilisez la collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID** avec l’identificateur de client spécifié.
- Extrayez la propriété **Agreements** et filtrez les résultats pour Microsoft Cloud accord en appelant la méthode **ByAgreementType** .
- Appelez **la** méthode **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Un exemple complet est disponible dans la classe [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="net-version-19---113"></a>.NET (version 1,9-1,13) 

Pour récupérer la confirmation de l’acceptation du client fournie précédemment :

Utilisez la collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID** avec l’identificateur du client spécifié. Ensuite, récupérez la propriété **Agreements** , puis appelez les méthodes d' **extraction** ou de **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

Pour récupérer la confirmation de l’acceptation du client fournie précédemment :

Utilisez la fonction **collection iaggregatepartner. getCustomers** et appelez la fonction **méthode BYID** avec l’identificateur du client spécifié. Ensuite, accédez à la fonction **getAgreements** , suivie de l’appel de la fonction d' **extraction** .

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

Un exemple complet est disponible dans la classe [GetCustomerAgreements](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) à partir du projet d' [application de test console](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

Pour récupérer la confirmation de l’acceptation du client fournie précédemment :

Utilisez la commande [**PartnerCustomerAgreement**](https://docs.microsoft.com/powershell/module/partnercenter/partner-center/get-partnercustomeragreement) .

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest"></a>REST

Pour récupérer la confirmation de l’acceptation du client fournie précédemment, consultez les instructions suivantes.

### <a name="rest-request"></a>Demande REST

Créez une nouvelle ressource de **contrat** avec les informations de certification pertinentes.  

#### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/Agreements http/1.1 |

##### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client que vous confirmez.

| Nom             | Type | Obligatoire | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customerTenantId | GUID | Y        | La valeur est un GUID mis en forme **CustomerTenantId** qui vous permet de spécifier un client. |

#### <a name="request-headers"></a>En-têtes de requête

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

#### <a name="request-body"></a>Corps de la requête

Aucun.

#### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

### <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources de **contrat** dans le corps de la réponse.

#### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

#### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [ 
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```

---
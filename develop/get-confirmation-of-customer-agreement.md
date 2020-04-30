---
title: Obtenir la confirmation de l’acceptation du Contrat client Microsoft par le client
description: Cet article explique comment demander la confirmation de l’acceptation du client par le contrat de client Microsoft.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9daa54968128cdc0b7c6e44fb2a2f0392055b42b
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157711"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Obtenir la confirmation de l’acceptation du Contrat client Microsoft par le client

**S’applique à :**

- Espace partenaires

La ressource d' **accord** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas à :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment vous pouvez récupérer la ou les confirmations de l’acceptation par un client du contrat de client Microsoft.

## <a name="prerequisites"></a>Prérequis

- Si vous utilisez le SDK .NET de l’Espace partenaires, la version 1.14 ou une version ultérieure est nécessaire.

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](./partner-center-authentication.md). Ce scénario ne prend en charge que l’authentification de l’application et de l’utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

## <a name="net"></a>.NET

Pour récupérer la ou les confirmations de l’acceptation du client qui ont été fournies précédemment :

- Utilisez la collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID** avec l’identificateur de client spécifié.

- Extrayez la propriété **Agreements** et filtrez les résultats en accord avec le client Microsoft en appelant la méthode **ByAgreementType** .

- Appelez **la** méthode **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Un exemple complet est disponible dans la classe [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Demande REST

Pour récupérer la confirmation de l’acceptation du client fournie précédemment :

1. Créez une demande REST pour récupérer le regroupement de [contrats](./agreement-resources.md) pour le client.

2. Utilisez le paramètre de requête **agreementType** pour limiter les résultats au contrat de client Microsoft.

### <a name="request-syntax"></a>Syntaxe de la requête

Utilisez la syntaxe de requête suivante :

| Méthode | URI de demande                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | baseURL/v1/Customers/{Customer-tenant-ID}/Agreements ? agreementType = {accord-type} http/1.1 [* \{\}*](partner-center-rest-urls.md) |

#### <a name="uri-parameters"></a>Paramètres URI

Vous pouvez utiliser les paramètres URI suivants avec votre demande :

| Nom             | Type | Obligatoire | Description                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Oui | La valeur est un GUID mis en forme **CustomerTenantId** qui vous permet de spécifier un client. |
| type d’accord | string | Non | Ce paramètre retourne toutes les métadonnées de l’accord. Utilisez ce paramètre pour étendre la réponse de la requête à un type de contrat spécifique. Les valeurs prises en charge sont les suivantes : <ul><li>**MicrosoftCloudAgreement** qui comprend uniquement les métadonnées d’accord de type *MicrosoftCloudAgreement*.</li><li>**MicrosoftCustomerAgreement** qui comprend uniquement les métadonnées d’accord de type *MicrosoftCustomerAgreement*.</li><li>**\*** qui retourne toutes les métadonnées d’accord. (N’utilisez **\*** pas à moins que votre code n’ait la logique nécessaire pour gérer les types d’accord inattendus.)</li></ul> Si le paramètre URI n’est pas spécifié, la requête est définie par défaut sur **MicrosoftCloudAgreement** pour des raisons de compatibilité descendante. Microsoft peut introduire des métadonnées de l’accord avec de nouveaux types de contrat à tout moment.  |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une collection de ressources de **contrat** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires.

Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```

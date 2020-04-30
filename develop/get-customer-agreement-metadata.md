---
title: Obtenir les métadonnées du Contrat client Microsoft
description: Cet article explique comment obtenir les métadonnées d’un accord pour le client Microsoft.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 419be44e0dc82f931826dbf849c7122a98bc8646
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157701"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Obtenir les métadonnées du Contrat client Microsoft

**S’applique à :**

- Espace partenaires

Les métadonnées de l’accord pour le contrat client Microsoft sont actuellement prises en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Elle ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Vous devez récupérer les métadonnées du contrat du client Microsoft avant de pouvoir :

- [Confirmer l’acceptation par un client du contrat de client Microsoft](./confirm-customer-consent-customer-agreement.md)
- [Récupérer un lien de téléchargement pour le modèle de contrat client Microsoft](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Prérequis

- Si vous utilisez le SDK .NET de l’Espace partenaires, la version 1.14 ou une version ultérieure est nécessaire.

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](./partner-center-authentication.md). Ce scénario ne prend en charge que l’authentification d’application + utilisateur.

## <a name="net-version-114-or-newer"></a>.NET (version 1,14 ou ultérieure)

Pour récupérer les métadonnées de l’accord pour le contrat client Microsoft :

1. Tout d’abord, récupérez la collection **collection iaggregatepartner. AgreementDetails** .

2. Appelez la méthode **ByAgreementType** pour filtrer le regroupement en accord avec le client Microsoft.

3. Enfin **, appelez la** méthode **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Un exemple complet est disponible dans la classe [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="rest-request"></a>Demande REST

Pour récupérer les métadonnées de l’accord pour le contrat client Microsoft :

1. Créez une demande REST pour récupérer la collection [AgreementMetaData](./agreement-metadata-resources.md) .

2. Utilisez le paramètre de requête **agreementType** pour limiter le résultat au contrat du client Microsoft.

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                         |
|--------|---------------------------------------------------------------------|
| GET    | baseURL/v1/Agreements ? agreementType = {accord-type} http/1.1 [* \{\}*](partner-center-rest-urls.md) |

#### <a name="uri-parameters"></a>Paramètres URI

| Nom                   | Type     | Obligatoire | Description                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| type d’accord | string | Non | Utilisez ce paramètre pour étendre la réponse de la requête à un type de contrat spécifique. Les valeurs prises en charge sont les suivantes : <ul><li>**MicrosoftCloudAgreement** qui contient les métadonnées d’accord uniquement du type *MicrosoftCloudAgreement*</li><li>**MicrosoftCustomerAgreement** qui contient les métadonnées d’accord uniquement du type *MicrosoftCustomerAgreement*.</li><li>**\*** qui retourne toutes les métadonnées d’accord. (N’utilisez **\*** pas à moins que votre code n’ait la logique d’exécution nécessaire pour gérer des types d’accord non familiers, car Microsoft peut introduire des métadonnées d’accord avec de nouveaux types de contrat à tout moment.)</li></ul> Si le paramètre URI n’est pas spécifié, la requête est définie par défaut sur **MicrosoftCloudAgreement** pour des raisons de compatibilité descendante.  |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une collection de [ressources **AgreementMetaData** ](./agreement-metadata-resources.md) dans le corps de la réponse.

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
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

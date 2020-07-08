---
title: Obtenir les métadonnées de contrat pour le contrat Microsoft Cloud
description: Cet article explique comment obtenir les métadonnées d’un accord pour Microsoft Cloud accord.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 909dec77dd189005839d72caeb0e66a7ad5c8a1b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097154"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Obtenir les métadonnées de contrat pour le contrat Microsoft Cloud

**S’applique à**

- Espace partenaires

> [!NOTE]
> La ressource **AgreementMetaData** est actuellement prise en charge par l’espace partenaires dans le cloud public Microsoft uniquement. Elle ne s’applique pas aux éléments suivants :
> - Espace partenaires géré par 21Vianet
> - Espace partenaires de Microsoft Cloud Germany
> - Espace partenaires de Microsoft Cloud for US Government

## <a name="prerequisites"></a>Prérequis

- Si vous utilisez le kit de développement logiciel (SDK) .NET de l’espace partenaires, la version 1,9 ou une version ultérieure est requise.

- Si vous utilisez le kit de développement logiciel (SDK) Java de l’espace partenaires, la version 1,8 ou une version ultérieure est requise.

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](./partner-center-authentication.md). Ce scénario prend en charge l’authentification d’application + utilisateur.

## <a name="net-version-114-or-newer"></a>.NET (version 1,14 ou ultérieure)

Pour récupérer les métadonnées de l’accord pour Microsoft Cloud accord :

1. Tout d’abord, récupérez la collection **collection iaggregatepartner. AgreementDetails** .

2. Appelez la méthode **ByAgreementType** pour filtrer la collection afin de Microsoft Cloud accord.

3. Enfin **, appelez la** méthode **GetAsync** .

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Un exemple complet est disponible dans la classe [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) à partir du projet d' [application de test console](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) .

## <a name="net-version-19---113"></a>.NET (version 1,9-1,13)

Pour récupérer les métadonnées d’accord pour l’accord de Microsoft Cloud :

Récupérez d’abord la collection **collection iaggregatepartner. AgreementDetails** , puis appelez les méthodes **obtenir** ou **GetAsync** . Recherchez ensuite l’élément dans la collection, qui correspond au contrat de Microsoft Cloud :

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Pour récupérer les métadonnées d’accord pour l’accord de Microsoft Cloud :

Appelez d’abord la fonction **collection iaggregatepartner. getAgreementDetails** , puis appelez la fonction d' **extraction** . Recherchez ensuite l’élément dans la collection, qui correspond au contrat de Microsoft Cloud :

```java
// IAggregatePartner partnerOperations;

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

Un exemple complet est disponible dans la classe [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) à partir du projet d' [application de test console](https://github.com/Microsoft/Partner-Center-Java-Samples) .

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Pour récupérer les métadonnées d’accord pour l’accord de Microsoft Cloud :

Utilisez la commande [**PartnerAgreementDetail**](https://docs.microsoft.com/powershell/module/partnercenter/get-partneragreementdetail) . Recherchez ensuite l’élément dans la collection, qui correspond au contrat de Microsoft Cloud :

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>Demande REST

Pour récupérer les métadonnées d’accord pour Microsoft Cloud accord, commencez par créer une demande REST pour récupérer la collection **AgreementMetaData** . Recherchez ensuite l’élément dans la collection qui correspond au contrat de Microsoft Cloud.

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de demande                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [* \{ BASEURL \} *](partner-center-rest-urls.md)/v1/Agreements http/1.1 |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une collection de ressources **AgreementMetaData** dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

Pour identifier la ressource dans la réponse qui correspond au contrat de Microsoft Cloud, recherchez la ressource dont la propriété **agreementType** a la valeur « MicrosoftCloudAgreement ».

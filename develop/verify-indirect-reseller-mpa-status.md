---
title: Vérifier l’état de signature du Contrat Partenaire Microsoft d’un revendeur indirect
description: Vous pouvez utiliser l’API AgreementStatus pour vérifier si un revendeur indirect a signé le Contrat Partenaire Microsoft.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4836a5e0646e1f00807966d3d8d332c026276c61
ms.sourcegitcommit: 68a5497a7350e135358aeb7f2a54c75707f922c5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87261938"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Vérifier l’état de signature du Contrat Partenaire Microsoft d’un revendeur indirect

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud for US Government

Vous pouvez vérifier si un revendeur indirect a signé le Contrat Partenaire Microsoft avec son ID Microsoft Partner Network (MPN) ou son ID de locataire de fournisseur de solutions Cloud (ID Microsoft). Vous pouvez utiliser l’un de ces identificateurs pour vérifier l’état de signature du Contrat Partenaire Microsoft à l’aide de l’API **AgreementStatus**.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID MPN ou ID de locataire de fournisseur de solutions Microsoft Cloud (ID Microsoft) du revendeur indirect. *Vous devez utiliser l’un de ces deux identificateurs.*

## <a name="c"></a>C\#

Pour connaître l’état de signature du Contrat Partenaire Microsoft d’un revendeur indirect :

1. Utilisez votre collection **IAggregatePartner.Compliance** pour appeler la propriété **AgreementSignatureStatus**.

2. Appelez la méthode [**Get()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) ou [**GetAsync()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync).

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Exemple : **[Application de test de console](console-test-app.md)**
- Projet : **PartnerCenterSDK.FeaturesSamples**
- Class: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode | URI de requête |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)* /v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>Paramètres d’URI

Vous devez fournir l’un des deux paramètres de requête suivants pour identifier le partenaire. Si vous ne fournissez pas l’un de ces deux paramètres de requête, vous recevez une erreur **400 (requête incorrecte)** .

| Nom | Type | Obligatoire | Description |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | Non | ID Microsoft Partner Network qui identifie le revendeur indirect. |
| **TenantId** | GUID | Non | ID Microsoft identifiant le compte de fournisseur de solutions Cloud du revendeur indirect. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](https://docs.microsoft.com/partner-center/develop/headers).

### <a name="request-examples"></a>Exemples de demande

#### <a name="request-using-mpn-id"></a>Requête avec l’ID MPN

L’exemple de requête suivant obtient l’état de signature du Contrat Partenaire Microsoft du revendeur indirect en utilisant l’ID Microsoft Partner Network de ce dernier.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Requête avec l’ID de locataire de fournisseur de solutions Cloud

L’exemple de requête suivant obtient l’état de signature du Contrat Partenaire Microsoft du revendeur indirect en utilisant l’ID de locataire de fournisseur de solutions Cloud de ce dernier.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](https://docs.microsoft.com/partner-center/develop/error-codes).

### <a name="response-example-success"></a>Exemple de réponse (réussite)

L’exemple de réponse suivant indique correctement si le revendeur indirect a signé ou non le Contrat Partenaire Microsoft.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a>Exemples de réponse (échecs)

Vous pouvez recevoir des réponses semblables aux exemples suivants lorsque l’état de signature du Contrat Partenaire Microsoft du revendeur indirect ne peut pas être retourné.

#### <a name="non-guid-formatted-csp-tenant-id"></a>ID de locataire de fournisseur de solutions Cloud au format non-GUID

L’exemple de réponse suivant est retourné quand l’ID de locataire de fournisseur de solutions Cloud que vous avez passé à l’API n’est pas un GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a>ID MPN non numérique

L’exemple de réponse suivant est retourné quand l’ID MPN que vous avez passé à l’API n’est pas numérique.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Aucun ID MPN ou ID de locataire de fournisseur de solutions Cloud

L’exemple de réponse suivant est retourné quand vous n’avez pas passé d’ID MPN ni d’ID de locataire de fournisseur de solutions Cloud à l’API. Vous devez passer l’un de ces deux types d’ID à l’API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>ID MPN et ID de locataire de fournisseur de solutions Cloud transmis

L’exemple de réponse suivant est retourné quand vous avez passé à la fois un ID MPN et un ID de locataire de fournisseur de solutions Cloud à l’API. Vous devez passer *un seul* des deux types d’identificateur à l’API.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>L’ID MPN du CSP Indirect Reseller n’est pas valide ou n’est pas migré du Partner Membership Center vers l’Espace partenaires

L’exemple de réponse suivant est retourné lorsque l’ID MPN du revendeur indirect transmis n’est pas valide ou n’est pas migré du Partner Membership Center vers l’Espace partenaires. [En savoir plus](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>La région du CSP Indirect Provider et la région du CSP Indirect Reseller ne correspondent pas

L’exemple de réponse suivant est retourné lorsque la région de l’ID MPN du revendeur indirect ne correspond pas à la région du fournisseur indirect. [En savoir plus](https://docs.microsoft.com/partner-center/regional-authorization-overview) sur les régions CSP.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>Le compte du CSP Indirect Reseller existe dans l’Espace partenaires, mais n’a pas signé le MPA

L’exemple de réponse suivant est retourné lorsque le compte du CSP Indirect Reseller dans l’Espace partenaires n’a pas signé le MPA. [En savoir plus](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Aucun compte de CSP Indirect Reseller n’est associé à l’ID MPN donné

L’exemple de réponse suivant est retourné lorsque l’Espace partenaires peut reconnaître l’ID MPN passé dans la demande, mais qu’aucune inscription CSP n’est associée à l’ID MPN donné. [En savoir plus](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>ID de locataire non valide

L’exemple de réponse suivant est retourné lorsque l’Espace partenaires ne trouve pas de compte associé à l’ID de locataire passé dans la demande.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>MPA introuvable avec l’ID de locataire donné

L’exemple de réponse suivant est retourné lorsque l’Espace partenaires ne peut pas trouver de signature MPA avec l’ID de locataire donné.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```

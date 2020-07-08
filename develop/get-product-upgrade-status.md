---
title: Obtenir l’état de mise à niveau du produit pour un client
description: Vous pouvez utiliser la ressource ProductUpgradeRequest pour déterminer l’état d’une mise à niveau de produit pour un client vers une nouvelle famille de produits, par exemple d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097638"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Obtenir l’état de mise à niveau du produit pour un client

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser la ressource [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) pour obtenir l’état d’une mise à niveau vers une nouvelle famille de produits. Cette ressource s’applique lorsque vous mettez à niveau un client à partir d’un abonnement Microsoft Azure (MS-AZR-0145P) à un plan Azure. Une demande réussie retourne la ressource [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) .

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur. Suivez le [modèle d’application sécurisée](enable-secure-app-model.md) lors de l’utilisation de l’authentification d’application + utilisateur avec les API de l’espace partenaires.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Famille de produits.

- L’ID de mise à niveau d’une demande de mise à niveau.

## <a name="c"></a>C\#

Pour vérifier si un client est éligible pour la mise à niveau vers Azure plan :

1. Créez un objet **ProductUpgradesRequest** et spécifiez l’identificateur du client et « Azure » comme famille de produits.

2. Utilisez la collection **collection iaggregatepartner. ProductUpgrades** .

3. Appelez la méthode **méthode BYID** et transmettez l' **ID de mise à niveau**.

4. Appelez la méthode **CheckStatus** et transmettez l’objet **ProductUpgradesRequest** , qui renverra un objet **ProductUpgradeStatus** .

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{Upgrade-ID}/Status http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour spécifier le client pour lequel vous obtenez un état de mise à niveau de produit.

| Nom               | Type | Obligatoire | Description                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **Upgrade-ID** | GUID | Oui | La valeur est un identificateur de mise à niveau au format GUID. Vous pouvez utiliser cet identificateur pour spécifier une mise à niveau à suivre. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir une ressource [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) .

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une ressource [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) dans le corps.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```

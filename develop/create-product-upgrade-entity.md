---
title: Créer une entité de mise à niveau de produit pour un client
description: Vous pouvez utiliser la ressource ProductUpgradeRequest pour créer une entité de mise à niveau de produit afin de mettre à niveau un client vers une famille de produits donnée.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 45661cd259981ae7e737ee3d74cbc2dbfb285054
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155401"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Créer une entité de mise à niveau de produit pour un client

**S’applique à :**

- Espace partenaires

Vous pouvez créer une entité de mise à niveau de produit pour mettre à niveau un client vers une famille de produits donnée (par exemple, Azure plan) à l’aide de la ressource **ProductUpgradeRequest** .

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur. Suivez le [modèle d’application sécurisée](enable-secure-app-model.md) lors de l’utilisation de l’authentification d’application + utilisateur avec les API de l’espace partenaires.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- Famille de produits pour laquelle vous souhaitez mettre à niveau le client.

## <a name="c"></a>C\#

Pour mettre à niveau un client vers Azure plan :

1. Créez un objet **ProductUpgradesRequest** et spécifiez l’identificateur du client et « Azure » comme famille de produits.

2. Utilisez la collection **collection iaggregatepartner. ProductUpgrades** .

3. Appelez la méthode **Create** et transmettez l’objet **ProductUpgradesRequest** , qui renverra une chaîne d' **en-tête d’emplacement** .

4. Extrayez l' **ID de mise à niveau** de la chaîne d’en-tête d’emplacement qui peut être utilisée pour [interroger l’état de mise à niveau](get-product-upgrade-status.md).

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades http/1.1 |

#### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

#### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir une ressource [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) .

#### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a>Response REST

En cas de réussite, la réponse contient un en-tête d' **emplacement** qui a un URI qui peut être utilisé pour récupérer l’état de la mise à niveau du produit. Enregistrez cet URI pour une utilisation avec d’autres API REST associées.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```

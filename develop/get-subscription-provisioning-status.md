---
title: Obtenir l’état de provisionnement d’un abonnement
description: Obtention de l’état d’approvisionnement de l’abonnement pour un abonnement client.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c35730d6b6734ca69f3ffa21a78ff209fbc5ecb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927515"
---
# <a name="get-subscription-provisioning-status"></a>Obtenir l’état de provisionnement d’un abonnement

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtention de l’état d’approvisionnement de l’abonnement pour un abonnement client.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur d’abonnement.

- Les autorisations d’administrateur déléguées sur l’abonnement sont requises pour effectuer cette opération.

## <a name="c"></a>C\#

Pour obtenir l’état d’approvisionnement d’un abonnement, commencez par utiliser la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID client pour identifier le client. Ensuite, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**Subscriptions. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.customerusers.icustomerusercollection.BYID) avec l’ID d’abonnement. Ensuite, utilisez la propriété [**ProvisioningStatus**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.ISubscription.provisioningstatus) pour obtenir une interface pour les opérations d’état d’approvisionnement de l’abonnement actuel, puis appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptionprovisioningstatus.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) pour récupérer l’objet [**SubscriptionProvisioningStatus**/dotnet/API/Microsoft.Store.partnercenter.Models.subscriptions.subscriptionprovisioningstatus).

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/provisioningstatus http/1.1 |

### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement.

| Nom            | Type   | Obligatoire | Description                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| customer-id     | string | Oui      | Chaîne au format GUID qui identifie le client.     |
| subscription-id | string | Oui      | Chaîne au format GUID qui identifie l’abonnement. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une ressource [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>Notes

- Pendant une attribution de modification de licence, le champ État dans [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) est défini sur « en attente ».

- Le champ d’État est mis à jour toutes les quinze minutes.

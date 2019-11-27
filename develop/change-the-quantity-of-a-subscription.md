---
title: Modifier la quantité d’un abonnement
description: Mettez à jour un abonnement pour augmenter ou diminuer le nombre de licences d’un client.
ms.assetid: 10535C45-63BF-4E75-A6E5-E03ADC1DF8DC
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3d4d94d244ca6d2f4c10054f9486e8fd04c514b1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488999"
---
# <a name="change-the-quantity-of-a-subscription"></a>Modifier la quantité d’un abonnement

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Met à jour un [abonnement](subscription-resources.md) pour augmenter ou diminuer la quantité de licences.

Dans le tableau de bord espace partenaires, vous pouvez effectuer cette opération en [sélectionnant d’abord un client](get-a-customer-by-name.md). Sélectionnez ensuite l’abonnement en question que vous souhaitez renommer. Pour terminer, modifiez la valeur dans le champ **quantité** , puis sélectionnez **Envoyer.**

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID d’abonnement.

## <a name="c"></a>\# C

Pour modifier la quantité de l’abonnement d’un client, commencez par [obtenir l’abonnement](get-a-subscription-by-id.md), puis modifiez la propriété [**Quantity**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) de l’abonnement. Une fois la modification effectuée, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode **méthode BYID ()** . Appelez ensuite la propriété [**Subscriptions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) , suivie de la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) . Ensuite, terminez en appelant la méthode **patch ()** .

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: UpdateSubscription.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **CORRECTIF** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{ID-for-subscription} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie le paramètre de requête requis pour modifier la quantité de l’abonnement.

| Nom                    | Type     | Obligatoire | Description                               |
|-------------------------|----------|----------|-------------------------------------------|
| **client-locataire-ID**  | **uniques** | Y        | GUID correspondant au client.     |
| **ID-pour l’abonnement** | **uniques** | Y        | GUID correspondant à l’abonnement. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes](headers.md) .

### <a name="request-body"></a>Corps de la requête

Une ressource d' **abonnement** complète est requise dans le corps de la demande. Assurez-vous que la propriété **Quantity** a été mise à jour.

### <a name="request-example"></a>Exemple de requête

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne le code d’état **HTTP 200** et les propriétés de [ressource d’abonnement](subscription-resources.md) mises à jour dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse retourne un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire le code d’État, le type d’erreur et les paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

Lorsque l’opération de patch prend plus de temps que le délai prévu, l’espace partenaires envoie un code d’état **http état 202** et un en-tête d’emplacement qui pointe vers l’emplacement où récupérer l’abonnement. Vous pouvez interroger régulièrement l’abonnement pour surveiller les modifications d’État et de quantité.

### <a name="response-examples"></a>Exemples de réponse

#### <a name="response-example-1"></a>Exemple de réponse 1

Demande réussie avec un code d’état **http état 200** :

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

#### <a name="response-example-2"></a>Exemple de réponse 2

Demande réussie avec un code d’état **http état 202** :

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```

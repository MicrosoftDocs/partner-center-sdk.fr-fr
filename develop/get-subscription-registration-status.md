---
title: Obtenir l’état d’inscription d’un abonnement
description: Obtenir l’état d’un abonnement inscrit pour une utilisation avec Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7a8683aa93702403ab6e6ae5912802ebfb1da4e7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097510"
---
# <a name="get-subscription-registration-status"></a>Obtenir l’état d’inscription d’un abonnement

**S’applique à**

- Espace partenaires

Comment obtenir l’état d’inscription d’un abonnement client qui a été activé pour l’achat de Azure Reserved VM Instances.

Pour acheter une instance de machine virtuelle réservée Azure à l’aide de l’API espace partenaires, vous devez disposer d’au moins un abonnement Azure CSP existant. La méthode [inscrire un abonnement](register-a-subscription.md) vous permet d’inscrire votre abonnement Azure CSP existant et de l’activer pour l’achat de Azure reserved VM instances. Cette méthode vous permet de récupérer l’état de cette inscription.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- ID d’abonnement.

## <a name="c"></a>C\#

Pour obtenir l’état d’inscription d’un abonnement, commencez par utiliser la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**subscription. méthode BYID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) avec l’ID d’abonnement pour identifier l’abonnement. Ensuite, utilisez la propriété RegistrationStatus pour obtenir une interface pour les opérations d’état d’inscription de l’abonnement actuel et appelez la méthode **obtenir** ou **GetAsync** pour récupérer l’objet **SubscriptionRegistrationStatus** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **GET**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/RegistrationStatus http/1.1 |

### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement.

| Nom                    | Type       | Obligatoire | Description                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| customer-id             | string     | Oui      | Chaîne au format GUID qui identifie le client.         |
| subscription-id         | string     | Oui      | Chaîne au format GUID qui identifie l’abonnement.     |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient une ressource [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```

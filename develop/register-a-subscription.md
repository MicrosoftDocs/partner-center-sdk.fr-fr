---
title: Inscrire un abonnement
description: Inscrire un abonnement existant afin qu’il soit activé pour la commande des réservations Azure.
ms.assetid: 9B853BF2-855C-4EB3-BBE5-7ECC1336AE08
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3c5fd478782fa9437fabddf7fd4391069d12739f
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415492"
---
# <a name="register-a-subscription"></a>Inscrire un abonnement


**S’applique à**

- Centre pour partenaires

Inscrire un [abonnement](subscription-resources.md) existant afin qu’il soit activé pour la commande des réservations Azure.  

Pour acheter une réservation Azure, vous devez disposer d’au moins un abonnement Azure CSP existant. Cette méthode vous permet d’inscrire votre abonnement Azure CSP existant et de l’activer pour l’achat de réservations Azure. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID d’abonnement.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour inscrire l’abonnement d’un client, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, appelez la méthode [**subscription. méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) avec l’ID d’abonnement pour identifier l’abonnement que vous inscrivez. 

Enfin, appelez la méthode **Registration. Register ()** pour inscrire l’abonnement et récupérer un URI qui peut être utilisé pour obtenir l’état d’inscription de l’abonnement. Pour plus d’informations, consultez [obtenir l’état de l’inscription de l’abonnement](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode    | URI de demande                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/Registrations http/1.1 |

 

**Paramètres d’URI**

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement. 

| Nom                    | Type       | Obligatoire | Description                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| ID client             | chaîne     | Oui      | Chaîne au format GUID qui identifie le client.         |
| ID d’abonnement         | chaîne     | Oui      | Chaîne au format GUID qui identifie l’abonnement.     |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

None.

**Exemple de requête**

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


En cas de réussite, la réponse contient un en-tête d' **emplacement** avec un URI qui peut être utilisé pour récupérer l’état d’inscription de l’abonnement. Enregistrez cet URI pour une utilisation avec d’autres API REST associées. Pour obtenir un exemple de récupération de l’État, consultez [obtenir l’État](get-subscription-registration-status.md)de l’inscription de l’abonnement. 

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```

 

 





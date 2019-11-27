---
title: Afficher l’état d’inscription de l’abonnement
description: Obtenir l’état d’un abonnement inscrit pour une utilisation avec Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: fe9ea6d21465996b28367ff2fe5d374ac551bfe2
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487119"
---
# <a name="get-subscription-registration-status"></a>Afficher l’état d’inscription de l’abonnement 

**S’applique à**

- Espace partenaires

Comment obtenir l’état d’inscription d’un abonnement client qui a été activé pour l’achat de Azure Reserved VM Instances.  

Pour acheter une instance de machine virtuelle réservée Azure à l’aide de l’API espace partenaires, vous devez disposer d’au moins un abonnement Azure CSP existant. La méthode [inscrire un abonnement](register-a-subscription.md) vous permet d’inscrire votre abonnement Azure CSP existant et de l’activer pour l’achat de Azure reserved VM instances. Cette méthode vous permet de récupérer l’état de cette inscription. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- ID d’abonnement.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour obtenir l’état d’inscription d’un abonnement, commencez par utiliser la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**subscription. méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) avec l’ID d’abonnement pour identifier l’abonnement. Ensuite, utilisez la propriété RegistrationStatus pour obtenir une interface pour les opérations d’état d’inscription de l’abonnement actuel et appelez la méthode **obtenir** ou **GetAsync** pour récupérer l’objet **SubscriptionRegistrationStatus** .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST

**Syntaxe de la requête**

| Méthode    | URI de requête                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Télécharger**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/RegistrationStatus http/1.1 |

**Paramètres d’URI**

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement. 

| Nom                    | Type       | Obligatoire | Description                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| ID client             | chaîne     | Oui      | Chaîne au format GUID qui identifie le client.         |
| ID d’abonnement         | chaîne     | Oui      | Chaîne au format GUID qui identifie l’abonnement.     |

 
**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

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

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST

En cas de réussite, le corps de la réponse contient une ressource [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) .  

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

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
---
title: Inscrire un abonnement
description: Inscrire un abonnement existant afin qu’il soit activé pour la commande des réservations Azure.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cabfd9d2bba309d773f15b2de2a4b33e4575241
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926664"
---
# <a name="register-a-subscription"></a>Inscrire un abonnement

**S’applique à**

- Espace partenaires

Inscrire un [abonnement](subscription-resources.md) existant afin qu’il soit activé pour la commande des réservations Azure.

Pour acheter une réservation Azure, vous devez disposer d’au moins un abonnement Azure CSP existant. Cette méthode vous permet d’inscrire votre abonnement Azure CSP existant et de l’activer pour l’achat de réservations Azure.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- ID d’abonnement.

## <a name="c"></a>C\#

Pour inscrire l’abonnement d’un client, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID client pour identifier le client. Ensuite, appelez la méthode [**subscription. méthode BYID ()**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptioncollection.BYID) avec l’ID d’abonnement pour identifier l’abonnement que vous inscrivez.

Enfin, appelez la méthode **Registration. Register ()** pour inscrire l’abonnement et récupérer un URI qui peut être utilisé pour obtenir l’état d’inscription de l’abonnement. Pour plus d’informations, consultez [obtenir l’état de l’inscription de l’abonnement](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode    | URI de requête                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/Registrations http/1.1 |

### <a name="uri-parameters"></a>Paramètres URI

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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, la réponse contient un en-tête d' **emplacement** avec un URI qui peut être utilisé pour récupérer l’état d’inscription de l’abonnement. Enregistrez cet URI pour une utilisation avec d’autres API REST associées. Pour obtenir un exemple de récupération de l’État, consultez [obtenir l’État](get-subscription-registration-status.md)de l’inscription de l’abonnement.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```

---
title: Activer un abonnement sandbox pour les produits de la place de marché commercial
description: Activez un abonnement sandbox pour les produits de la place de marché commercial.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ec5046131369b68eb958b8143982abb65addbd09
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488749"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-products"></a>Activer un abonnement sandbox pour les produits de la place de marché commercial

S’applique à :

- Espace partenaires

Comment activer l’abonnement pour les produits SaaS (Software as a service) de la place de marché commercial à partir de comptes sandbox d’intégration pour activer la facturation.

>[!NOTE]
>Il est uniquement possible d’activer un abonnement pour les produits SaaS de la place de marché commercial à partir de comptes sandbox d’intégration. Si vous avez un abonnement de production, vous devez visiter le site de l’éditeur pour terminer le processus d’installation. La facturation de l’abonnement commence uniquement une fois l’installation terminée.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Un compte de partenaire du bac à sable (sandbox) d’intégration avec un client ayant un abonnement actif aux produits SaaS de la place de marché commercial.
- Pour les partenaires qui utilisent le kit de développement logiciel (SDK) .NET Partner Center, vous devez utiliser le SDK version 1.14.0 ou ultérieure pour accéder à cette fonctionnalité.

## <a name="c"></a>C#

Procédez comme suit pour activer un abonnement pour les produits SaaS de la place de marché commercial :

1. Rendez une interface avec les opérations d’abonnement disponibles. Vous devez identifier le client et spécifier l’identificateur d’abonnement de l’abonnement d’évaluation.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

2. Activate the subscription using the **Activate** operation.

    ``` csharp
    var subscriptionActivationResult = subscriptionOperations.Activate();
## REST request

### Request syntax

| Method     | Request URI                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### URI parameter

| Name                   | Type     | Required | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | The value is a GUID-formatted customer tenant identifier (**customer-tenant-id**), which allows you to specify a customer. |
| **subscription-id** | **guid** | Y | The value is a GUID-formatted subscription identifier (**subscription-id**), which allows you to specify a subscription. |

### Request headers

See [Partner Center REST headers](headers.md) for more information.

### Request body

None.

### Request example

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>Réponse REST

Cette méthode retourne les propriétés d' **État** et d' **ID d’abonnement** .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```

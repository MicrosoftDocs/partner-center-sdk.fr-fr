---
title: Activer un abonnement de bac à sable pour des produits de la place de marché commerciale
description: Activez un abonnement sandbox pour les produits de la place de marché commercial.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cee833f110c45e8f53a47aed3d8a8c3b1ccd6946
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154371"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-products"></a>Activer un abonnement de bac à sable pour des produits de la place de marché commerciale

**S’applique à :**

- Espace partenaires

Comment activer l’abonnement pour les produits SaaS (Software as a service) de la place de marché commercial à partir de comptes sandbox d’intégration pour activer la facturation.

> [!NOTE]
> Il est uniquement possible d’activer un abonnement pour les produits SaaS de la place de marché commercial à partir de comptes sandbox d’intégration. Si vous avez un abonnement de production, vous devez visiter le site de l’éditeur pour terminer le processus d’installation. La facturation de l’abonnement commence uniquement une fois l’installation terminée.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un compte de partenaire du bac à sable (sandbox) d’intégration avec un client ayant un abonnement actif aux produits SaaS de la place de marché commercial.

- Pour les partenaires qui utilisent le kit de développement logiciel (SDK) .NET Partner Center, vous devez utiliser le SDK version 1.14.0 ou ultérieure pour accéder à cette fonctionnalité.

## <a name="c"></a>C\#

Procédez comme suit pour activer un abonnement pour les produits SaaS de la place de marché commercial :

1. Rendez une interface avec les opérations d’abonnement disponibles. Vous devez identifier le client et spécifier l’identificateur d’abonnement de l’abonnement d’évaluation.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Activez l’abonnement à l’aide de l’opération d' **activation** .

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de requête                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/subscriptions/{subscription-ID}/Activate http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

| Nom                   | Type     | Obligatoire | Description                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O | La valeur est un identificateur de locataire client au format GUID (**Customer-client-ID**), qui vous permet de spécifier un client. |
| **ID d’abonnement** | **guid** | O | La valeur est un identificateur d’abonnement au format GUID (**ID d’abonnement**), qui vous permet de spécifier un abonnement. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>Response REST

Cette méthode retourne les propriétés d' **État** et d' **ID d’abonnement** .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

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

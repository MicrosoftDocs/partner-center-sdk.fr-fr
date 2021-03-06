---
title: Événements du webhook de l’espace partenaires
description: Documentation pour tous les événements de webhook pris en charge par l’espace partenaires.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926853"
---
# <a name="partner-center-webhook-events"></a>Événements du webhook de l’espace partenaires

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les événements de webhook de l’espace partenaires sont des événements de modification de ressources remis sous forme de publications HTTP à une URL inscrite. Pour recevoir un événement de l’espace partenaires, vous hébergez un rappel dans lequel Partner Center peut poster l’événement. L’événement est signé numériquement, ce qui vous permet de vérifier qu’il a été envoyé à partir de l’espace partenaires.

Pour plus d’informations sur la réception d’événements, l’authentification d’un rappel et l’utilisation des API de webhook de l’espace partenaires pour créer, afficher et mettre à jour une inscription d’événement, consultez la page des [webhooks de l’espace partenaires](partner-center-webhooks.md).

## <a name="supported-events"></a>Événements pris en charge

Les événements de webhook suivants sont pris en charge par l’espace partenaires.

### <a name="test-event"></a>Événement de test

Cet événement vous permet d’auto-intégrer et de tester votre inscription en demandant un événement de test, puis en effectuant le suivi de sa progression. Vous serez en mesure de voir les messages d’erreur reçus de Microsoft lors de la tentative de remise de l’événement. Cela s’applique uniquement aux événements « test créés » et les données datant de plus de 7 jours sont purgées.

>[!NOTE]
>Il existe une limite de 2 requêtes par minute lors de la publication d’un événement créé par test.

#### <a name="properties"></a>Propriétés

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « test créé ».                                          |
| URI               | URI                                | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Registration/validationEvents/{{CorrelationId}} » |
| Nom_ressource              | string                             | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « test ».                                  |
| AuditUri                  | URI                                | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} » |
| ResourceChangeUtcDate     | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite.                                                         |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Événement de mise à jour d’abonnement

Cet événement est déclenché lorsque l’abonnement spécifié est modifié. Un événement de mise à jour d’abonnement est généré en cas de modification interne en plus de lorsque des modifications sont apportées via l’API espace partenaires.  Cet événement est généré uniquement en cas de modification du niveau de commerce, par exemple lorsque le nombre de licences est modifié et lorsque l’état de l’abonnement change. Elle ne sera pas générée lors de la création de ressources dans l’abonnement.

>[!NOTE]
>Il y a un délai de 48 heures entre le moment où un abonnement est modifié et le moment où l’événement mis à jour de l’abonnement est déclenché.

#### <a name="properties"></a>Propriétés

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « subscripted-updated ».                                  |
| URI               | URI                                | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/{{CustomerID}}/subscriptions/{{SubscriptionId}} » |
| Nom_ressource              | string                             | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « Subscription ».                          |
| AuditUri                  | URI                                | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} » |
| ResourceChangeUtcDate     | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite.                                                         |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Événement seuil dépassé

Cet événement se déclenche lorsque la quantité d’utilisation de Microsoft Azure d’un client dépasse son budget de dépenses d’utilisation (son seuil). Pour plus d’informations, consultez [définir un budget de dépenses Azure pour vos clients/Partner-Center/Set-an-Azure-Pass-budget-for-your-clients).

#### <a name="properties"></a>Propriétés

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « usagerecords-thresholdExceeded ».                                  |
| URI               | URI                                | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/Customers/usagerecords » |
| Nom_ressource              | string                             | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « usagerecords ».                          |
| AuditUri                  | URI                                | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} » |
| ResourceChangeUtcDate     | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite.                                                         |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Événement créé par la référence

Cet événement est déclenché lorsque la référence est créée.

#### <a name="properties"></a>Propriétés

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « redirection-created ».                                  |
| URI               | URI                                | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/Referrals/{{ReferralID}} » |
| Nom_ressource              | string                             | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « Referral ».                          |
| AuditUri                  | URI                                | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} » |
| ResourceChangeUtcDate     | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite.                                                         |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Événement mis à jour de référence

Cet événement est déclenché lorsque la référence est mise à jour.

#### <a name="properties"></a>Propriétés

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | string                             | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « Referral-updated ».                                  |
| URI               | URI                                | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/Referrals/{{ReferralID}} » |
| Nom_ressource              | string                             | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « Referral ».                          |
| AuditUri                  | URI                                | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} » |
| ResourceChangeUtcDate     | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite.                                                         |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Événement de facturation opérationnelle

Cet événement est déclenché lorsque la nouvelle facture est prête.

| Propriété                  | Type                               | Description                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | string | Nom de l’événement. Sous la forme {Resource}-{action}. Pour cet événement, la valeur est « prêt pour la facturation ». |
| URI | URI | URI permettant d’accéder à la ressource. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{{InvoiceId}} » |
| Nom_ressource | string | Nom de la ressource qui déclenchera l’événement. Pour cet événement, la valeur est « Invoice ». |
| AuditUri |  URI | Facultatif URI permettant d’accéder à l’enregistrement d’audit, le cas échéant. Utilise la syntaxe : «[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/AuditRecords/{{AuditId}} ») |
| ResourceChangeUtcDate | chaîne au format date/heure UTC | Date et heure auxquelles la modification de ressource s’est produite. |

#### <a name="example"></a>Exemple

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```

---
title: Mettre à jour le contact de support d’un abonnement
description: Comment mettre à jour le contact de support d’un abonnement à l’un des revendeurs ajoutés de la valeur du partenaire.
ms.assetid: 6DE6EF60-6F8B-46F2-8278-CD706081B180
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 96cb4ae8bd938b5ab486e2bd81602132c449be55
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486419"
---
# <a name="update-a-subscriptions-support-contact"></a>Mettre à jour le contact de support d’un abonnement


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Comment mettre à jour le contact de support d’un abonnement à l’un des revendeurs ajoutés de la valeur du partenaire.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Identificateur du client.
- Identificateur d’abonnement.
- Informations sur le nouveau contact de support : identificateur de locataire, identificateur de Microsoft Partner Network et nom. Le contact du support technique doit être l’un des revendeurs à valeur ajoutée du partenaire.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour mettre à jour le contact de support d’un abonnement, commencez par instancier et remplir un objet [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) avec les nouvelles valeurs. Utilisez ensuite la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client. Ensuite, récupérez une interface pour les opérations d’abonnement en appelant la méthode [**Subscriptions. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) avec l’ID d’abonnement. Ensuite, utilisez la propriété [**SupportContact**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) pour obtenir une interface afin de prendre en charge les opérations de contact. Enfin, appelez la méthode [**Update**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) ou [**UpdateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) avec l’objet SupportContact rempli pour mettre à jour le contact de support.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId; 

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : UpdateSubscriptionSupportContact.cs

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **POSÉ** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscriptions/{subscription-ID}/supportcontact http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’abonnement.

| Nom            | Type   | Obligatoire | Description                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| ID client     | chaîne | Oui      | Chaîne au format GUID qui identifie le client.           |
| ID d’abonnement | chaîne | Oui      | Chaîne au format GUID qui identifie l’abonnement d’évaluation. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Vous devez inclure une ressource [SupportContact](subscription-resources.md#supportcontact) remplie dans le corps de la demande. Le contact du support technique doit être un revendeur existant disposant d’une relation avec le partenaire.

**Exemple de requête**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST


En cas de réussite, le corps de la réponse contient la ressource [SupportContact](subscription-resources.md#supportcontact) .

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez Codes d’erreur de l' [espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```

 

 




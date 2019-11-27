---
title: Créer une nouvelle stratégie de configuration pour le client spécifié
description: Comment créer une nouvelle stratégie de configuration pour le client spécifié.
ms.assetid: 95649991-A950-4F43-87E8-3EB1E7D06FCD
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 0ad89c0fe5e6b3c182315bf5343d78941f7cdd2d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489499"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a>Créer une nouvelle stratégie de configuration pour le client spécifié

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment créer une nouvelle stratégie de configuration pour le client spécifié.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client.

## <a name="c"></a>\# C

Pour créer une nouvelle stratégie de configuration pour le client spécifié :

1. Instanciez un nouvel objet [**ConfigurationPolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) comme indiqué dans l’extrait de code suivant. Appelez ensuite la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié.
2. Récupérez la propriété [**ConfigurationPolicies**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) pour obtenir une interface pour les opérations de collecte de stratégie de configuration.
3. Appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) pour créer la stratégie de configuration.

### <a name="c-example"></a>Exemple de\# C

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CreateConfigurationPolicy.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                              |
|----------|------------------------------------------------------------------------------------------|
| **Publier** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Policies http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID client | chaîne | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la requête

Le corps de la demande doit contenir un objet avec les informations de stratégie de configuration, comme décrit dans le tableau suivant :

| Nom           | Type             | Obligatoire | Description                      |
|----------------|------------------|----------|----------------------------------|
| name           | chaîne           | Oui      | Nom convivial de la stratégie. |
| catégorie       | chaîne           | Oui      | Catégorie de stratégie.             |
| description    | chaîne           | Non       | Description de la stratégie.          |
| policySettings | Tableau de chaînes | Oui      | Paramètres de stratégie.             |

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient la ressource [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pour la nouvelle stratégie.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
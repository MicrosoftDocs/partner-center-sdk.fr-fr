---
title: Mettre à jour une stratégie de configuration pour le client spécifié
description: Comment mettre à jour la stratégie de configuration spécifiée pour le client spécifié.
ms.assetid: E2B91AC4-B8E8-4A77-AFB7-0CCEF5136621
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a3258c9bd288535299347080b407054cf6786037
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415022"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Mettre à jour une stratégie de configuration pour le client spécifié


**S’applique à**

- Centre pour partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment mettre à jour la stratégie de configuration spécifiée pour le client spécifié.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client.
- Identificateur de la stratégie.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour mettre à jour une stratégie de configuration existante pour le client spécifié, instanciez un nouvel objet [**ConfigurationPolicy**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) comme indiqué dans l’extrait de code suivant. Les valeurs de ce nouvel objet remplacent les valeurs correspondantes dans l’objet existant. Ensuite, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, appelez la méthode [**ConfigurationPolicies. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) avec l’ID de stratégie pour récupérer une interface pour les opérations de stratégie de configuration pour la stratégie spécifiée. Enfin, appelez la méthode [**patch**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) ou [**PatchAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) pour mettre à jour la stratégie de configuration.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() { 
        PolicySettingsType.OobeUserNotLocalAdmin, 
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy = 
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : UpdateConfigurationPolicy.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode  | URI de demande                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Policies/{Policy-ID} http/1.1 |

 

**Paramètre URI**

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| ID client | chaîne | Oui      | Chaîne au format GUID qui identifie le client.         |
| ID de stratégie   | chaîne | Oui      | Chaîne au format GUID qui identifie la stratégie à mettre à jour. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Le corps de la demande doit contenir un objet qui fournit les informations de stratégie.

| Nom            | Type             | Obligatoire | Peut être mise à jour | Description                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | chaîne           | Oui      | Non        | Chaîne au format GUID qui identifie la stratégie.                                                                                                    |
| nom            | chaîne           | Oui      | Oui       | Nom convivial de la stratégie.                                                                                                                         |
| category        | chaîne           | Oui      | Non        | Catégorie de stratégie.                                                                                                                                     |
| description     | chaîne           | Non       | Oui       | Description de la stratégie.                                                                                                                                  |
| devicesAssigned | nombre           | Non       | Non        | Nombre d’appareils.                                                                                                                                   |
| policySettings  | tableau de chaînes | Oui      | Oui       | Les paramètres de stratégie : « aucun », « supprimer\_\_préinstallations OEM », « OOBE\_utilisateur\_pas\_administrateur de\_local », « ignorer les paramètres de\_Express », « ignorer les\_\_l’inscription OEM », « ignorer\_CLUF ».\_ |

 

**Exemple de requête**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, le corps de la réponse contient la ressource [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pour la nouvelle stratégie.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```

 

 





---
title: Mettre à jour une stratégie de configuration pour le client spécifié
description: Comment mettre à jour la stratégie de configuration spécifiée pour le client spécifié.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d29319ebf8561487fa279ef3e87664f3007bb778
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925714"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a>Mettre à jour une stratégie de configuration pour le client spécifié

**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment mettre à jour la stratégie de configuration spécifiée pour le client spécifié.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur de la stratégie.

## <a name="c"></a>C\#

Pour mettre à jour une stratégie de configuration existante pour le client spécifié, instanciez un nouvel objet [**ConfigurationPolicy**/dotnet/API/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) comme indiqué dans l’extrait de code suivant. Les valeurs de ce nouvel objet remplacent les valeurs correspondantes dans l’objet existant. Ensuite, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, appelez la méthode [**ConfigurationPolicies. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.iconfigurationpolicycollection.BYID) avec l’ID de stratégie pour récupérer une interface pour les opérations de stratégie de configuration pour la stratégie spécifiée. Enfin, appelez la méthode [**patch**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) ou [**PatchAsync**/dotnet/API/Microsoft.Store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) pour mettre à jour la stratégie de configuration.

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

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de demande                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Policies/{Policy-ID} http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez les paramètres de chemin d’accès suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| customer-id | string | Oui      | Chaîne au format GUID qui identifie le client.         |
| ID de stratégie   | string | Oui      | Chaîne au format GUID qui identifie la stratégie à mettre à jour. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Le corps de la demande doit contenir un objet qui fournit les informations de stratégie.

| Nom            | Type             | Obligatoire | Peut être mise à jour | Description                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| id              | string           | Oui      | Non        | Chaîne au format GUID qui identifie la stratégie.                                                                                                    |
| name            | string           | Oui      | Oui       | Nom convivial de la stratégie.                                                                                                                         |
| catégorie        | string           | Oui      | Non        | Catégorie de stratégie.                                                                                                                                     |
| description     | string           | Non       | Oui       | Description de la stratégie.                                                                                                                                  |
| devicesAssigned | nombre           | Non       | Non        | Nombre d’appareils.                                                                                                                                   |
| policySettings  | tableau de chaînes | Oui      | Oui       | Les paramètres de stratégie : « aucun », « supprimer les \_ \_ préinstallations OEM », \_ « \_ l’utilisateur OOBE n’est pas \_ \_ administrateur local », « ignorer les \_ \_ paramètres Express », « ignorer \_ \_ l’inscription OEM », ignorer le \_ CLUF. |

### <a name="request-example"></a>Exemple de requête

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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, le corps de la réponse contient la ressource [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) pour la nouvelle stratégie.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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

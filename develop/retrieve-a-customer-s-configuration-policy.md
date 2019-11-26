---
title: Récupérer la stratégie de configuration d’un client
description: Comment récupérer la stratégie de configuration spécifiée pour le client spécifié.
ms.assetid: A26B5CDA-C23C-4DC3-BC56-A27F3DDDCFB1
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 38420d6d1edac94db0c2e3d4800a62bc48dc7e96
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486559"
---
# <a name="retrieve-a-customers-configuration-policy"></a>Récupérer la stratégie de configuration d’un client


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany

Comment récupérer la stratégie de configuration spécifiée pour le client spécifié.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.
- Identificateur du client.
- Identificateur de la stratégie.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour récupérer une stratégie de configuration pour le client spécifié, appelez d’abord la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour récupérer une interface pour les opérations sur le client spécifié. Ensuite, appelez la méthode [**ConfigurationPolicies. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) avec l’ID de stratégie pour récupérer une interface pour les opérations de stratégie de configuration pour la stratégie spécifiée. Enfin, appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) pour [**récupérer la stratégie**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) de configuration.

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy = 
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : GetConfigurationPolicy.cs

## <a name="span-idrequestspan-idrequestspan-idrequestrequest"></a><span id="Request"/><span id="request"/><span id="REQUEST"/>demande


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Policies/{Policy-ID} http/1.1 |

 

**Paramètre URI**

Utilisez le chemin d’accès et les paramètres de requête suivants lors de la création de la demande.

| Nom        | Type   | Obligatoire | Description                                           |
|-------------|--------|----------|-------------------------------------------------------|
| ID client | chaîne | Oui      | Chaîne au format GUID qui identifie le client. |
| ID de stratégie   | chaîne | Oui      | Chaîne au format GUID qui identifie la stratégie.   |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Aucune

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>réponse


En cas de réussite, la réponse contient la ressource [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) demandée.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```

 

 





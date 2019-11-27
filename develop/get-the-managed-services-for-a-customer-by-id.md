---
title: Obtenir les services managés pour un client par ID
description: Obtient les services managés pour un client. En d’autres termes, obtenir des liens vers tous les abonnements du client pour lesquels vous avez délégué des privilèges d’administrateur. Vous pouvez utiliser ces liens pour fournir une prise en charge et des demandes de service de fichiers avec Microsoft.
ms.assetid: 32554787-4232-4574-9FC9-5E9F26411233
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 3ae9315a4f199ec45f1cbc84ca7415d224ea6234
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487129"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a>Obtenir les services managés pour un client par ID


**S’applique à**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Obtient les services managés pour un client. En d’autres termes, obtenir des liens vers tous les abonnements du client pour lesquels vous avez délégué des privilèges d’administrateur. Vous pouvez utiliser ces liens pour fournir une prise en charge et des demandes de service de fichiers avec Microsoft.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour afficher la liste de tous les services gérés pour un client, utilisez votre collection **collection iaggregatepartner. Customers** et appelez la méthode [**méthode BYID ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) . Appelez ensuite la propriété [**ManagedServices**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) , suivie des méthodes d' [**extraction ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) ou de [**GetAsync ()** ](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) .

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerCenterSDK. FeaturesSamples, **classe**: CustomerManagedServices.cs

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST


**Syntaxe de la requête**

| Méthode  | URI de requête                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Télécharger** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/managedservices http/1.1 |

 

**Paramètre URI**

Utilisez le paramètre de requête suivant pour obtenir les services gérés du client.

| Nom                   | Type     | Obligatoire | Description                           |
|------------------------|----------|----------|---------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | GUID correspondant au client. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Aucun.

**Exemple de requête**

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST

En cas de réussite, cette méthode retourne une collection d’objets de **service managés** dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
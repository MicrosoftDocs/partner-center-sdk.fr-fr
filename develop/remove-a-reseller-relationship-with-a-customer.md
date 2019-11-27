---
title: Supprimer une relation de revendeur avec un client
description: Comment supprimer une relation de revendeur avec un client pour lequel vous n’avez plus de transactions.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 950b4c275acbbc699504344108799f6662de607e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486709"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Supprimer une relation de revendeur avec un client


**S’applique à**

- Espace partenaires  


Supprimer une relation de revendeur avec un client pour lequel vous n’avez plus de transactions. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables


- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- ID client (client-locataire-ID). Si vous n’avez pas d’ID de client, vous pouvez rechercher l’ID dans l’espace partenaires en choisissant le client dans la liste clients, en sélectionnant compte, puis en enregistrant son ID Microsoft.
- Toutes les commandes d’instance de machine virtuelle réservées Azure doivent être annulées avant la suppression d’une relation de revendeur. Appelez le support Azure pour annuler les commandes de l’instance de machine virtuelle réservée Azure.

## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


Pour supprimer la relation de revendeur pour un client, vous devez d’abord vous assurer que les Azure Reserved VM Instances actifs pour ce client sont annulés et que tous les abonnements actifs pour ce client sont suspendus. Pour ce faire, déterminez l’ID du client pour lequel vous souhaitez supprimer la relation du revendeur (dans l’exemple de code suivant, l’utilisateur est invité à fournir l’identificateur du client). 

Pour déterminer si des Azure Reserved VM Instances pour le client doivent être annulées, récupérez la collection de droits en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) à l’aide de l’identificateur de client pour spécifier le client et la propriété de [**droits**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pour récupérer une interface pour les opérations de collecte d’habilitation. Appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) pour [**récupérer la collection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) de droits. Filtrez la collection pour toutes les habilitations dont la valeur [**EntitlementType**](entitlement-resources.md#entitlementtype) est [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) et, le cas échéant, annulez-les en appelant la prise en charge avant de continuer. 

Ensuite, récupérez une collection des abonnements du client en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) à l’aide de l’identificateur du client pour spécifier le client et la propriété [**Subscriptions**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) pour récupérer une interface pour les opérations de collecte d’abonnement. Enfin, appelez la méthode [**GetAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) pour [**récupérer la collection**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) d’abonnements du client. Parcourez la collection d’abonnements et assurez-vous qu’aucun des abonnements n’a une valeur de propriété [**subscription. Status**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) de [**SubscriptionStatus. active**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus). Si un abonnement est toujours actif, consultez [suspendre un abonnement](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) pour plus d’informations sur la façon de le suspendre. 

Après avoir confirmé que tous les Azure Reserved VM Instances actifs pour ce client sont annulés et que tous les abonnements actifs sont suspendus, vous pouvez supprimer la relation du revendeur pour le client. Tout d’abord, créez un nouvel objet [Customer](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer) avec la propriété [Customer. RelationshipToPartner](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer.relationshiptopartner) définie sur [**CustomerPartnerRelationship. None**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerpartnerrelationship). Appelez ensuite la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) à l’aide de l’identificateur du client pour spécifier le client et appelez la méthode **patch** , en transmettant le nouvel objet Customer.

Pour rétablir la relation, répétez le processus de [demande d’une relation de revendeur](https://docs.microsoft.com/partner-center/develop/request-reseller-relationship). 


``` csharp
// IAggregatePartner partnerOperations;

// Prompt the user the enter the customer ID.
var customerIdToDeleteRelationshipOf = this.Context.ConsoleHelper.ReadNonEmptyString("Please enter the ID of the customer you want to delete the relationship with", "The customer ID can't be empty");

// Determine if there are any active Azure Reserved VM Instances for this customer.
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Entitlements.Get();

If (entitlements.Items.Where(x => x.EntitlementType == EntitlementType.VirtualMachineReservedInstance).Any())
{
    this.Context.ConsoleHelper.Warning("Please cancel Azure Reserved Virtual Machine Instance orders through support and try again. Aborting the delete customer relationship operation");
               return;
}

// Verify that there are no active subscriptions.
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Subscriptions.Get();
IList<Subscription> subscriptions = new List<Subscription>(customerSubscriptions.Items);

foreach (Subscription customerSubscription in subscriptions)
{
    if (customerSubscription.Status == SubscriptionStatus.Active)
    {
        this.Context.ConsoleHelper.Warning(String.Format("Subscription with ID :{0}  OfferName: {1} cannot be in active state, ", customerSubscription.Id, customerSubscription.OfferName));
        this.Context.ConsoleHelper.Warning("Please Suspend all the Subscriptions and try again. Aborting the delete customer relationship operation");
               return;
    }
}

// Delete the customer's relationship to the partner.
Customer customer = new Customer();
customer.RelationshipToPartner = CustomerPartnerRelationship.None;
customer = partnerOperations.Customers.ById(customerIdToDeleteRelationshipOf).Patch(customer);

if (customer.RelationshipToPartner == CustomerPartnerRelationship.None)
{
    this.Context.ConsoleHelper.Success("Customer Partner Relationship successfully deleted");
}
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSample, **classe**: DeletePartnerCustomerRelationship.cs


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>demande REST   


**Syntaxe de la requête**

| Méthode     | URI de requête                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **CORRECTIF**  | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/http/1.1 |

 

**Paramètre URI**

Ce tableau répertorie les paramètres de requête requis pour supprimer une relation de revendeur.

| Nom                   | Type     | Obligatoire | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **client-locataire-ID** | **uniques** | Y        | La valeur est un GUID **client-ID-client-ID** qui identifie le client. |

 

**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

**Corps de la demande**

Une ressource **client** est requise dans le corps de la demande. Vérifiez que la propriété **RelationshipToPartner** a été définie sur aucun.

**Exemple de requête**

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Authorization: Bearer <token>
Content-Length: 74
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
MS-RequestId: 9fef8b23-6e3e-45d2-8678-e9fe89c35af5
Date: Fri, 12 Jan 2018 00:31:55 GMT

{
    "relationshipToPartner":"none",
    "attributes":{
        "objectType":"Customer"
    }
}
```

## <a name="span-idrest_responsespan-idrest_responsespan-idrest_responserest-response"></a><span id="REST_Response"/><span id="rest_response"/><span id="REST_RESPONSE"/>réponse REST


En cas de réussite, cette méthode supprime une relation de revendeur pour le client spécifié.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
MS-RequestId: 7988dde4-b516-472c-b226-6d53fb18f04e
MS-CorrelationId: 9b4bf2ca-f374-4d51-9113-781ca87b8380
X-Locale: en-US
Content-Type: application/json
Content-Length: 242
Expect: 100-continue

{
    "Id":null,
    "CommerceId":null,
    "CompanyProfile":null,
    "BillingProfile":null,
    "RelationshipToPartner":"none",
    "AllowDelegatedAccess":null,
    "UserCredentials":null,
    "CustomDomains":null,
    "AssociatedPartnerId":null,
    "Attributes":{
        "ObjectType":"Customer"
    }
}
```
---
title: Supprimer une relation de revendeur avec un client
description: Comment supprimer une relation de revendeur avec un client pour lequel vous n’avez plus de transactions.
ms.date: 01/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 786dbeef91e51b2f7830a6d49e47e29121a7c38b
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926782"
---
# <a name="remove-a-reseller-relationship-with-a-customer"></a>Supprimer une relation de revendeur avec un client

**S’applique à**

- Espace partenaires

Supprimer une relation de revendeur avec un client pour lequel vous n’avez plus de transactions.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Toutes les commandes d’instance de machine virtuelle réservées Azure doivent être annulées avant la suppression d’une relation de revendeur. Appelez le support Azure pour annuler les commandes de l’instance de machine virtuelle réservée Azure.

## <a name="c"></a>C\#

Pour supprimer la relation du revendeur pour un client, assurez-vous d’abord que les Azure Reserved VM Instances actifs pour ce client sont annulés. Ensuite, assurez-vous que tous les abonnements actifs pour ce client sont suspendus. Pour ce faire, déterminez l’ID du client pour lequel vous souhaitez supprimer la relation du revendeur. Dans l’exemple de code suivant, l’utilisateur est invité à fournir l’identificateur du client.

Pour déterminer si des Azure Reserved VM Instances pour le client doivent être annulées, récupérez la collection de droits en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) à l’aide de l’identificateur de client pour spécifier le client, et la propriété [**droits**/dotnet/API/Microsoft.Store.partnercenter.Customers.ICustomer.subscriptions) pour récupérer une interface pour les opérations de collecte d’habilitation. Appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptioncollection.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptioncollection.getasync) pour récupérer la collection de droits. Filtrez la collection pour toutes les habilitations dont la valeur [**EntitlementType**](entitlement-resources.md#entitlementtype) est [**EntitlementType. VirtualMachineReservedInstance**](entitlement-resources.md#entitlementtype) et, le cas échéant, annulez-les en appelant la prise en charge avant de continuer.

Ensuite, récupérez une collection des abonnements du client en appelant la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) à l’aide de l’identificateur du client pour spécifier le client et la propriété [**Subscriptions**/dotnet/API/Microsoft.Store.partnercenter.Customers.ICustomer.subscriptions) pour récupérer une interface pour les opérations de collecte d’abonnement. Enfin, appelez la méthode [**obtenir**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptioncollection.Get) ou [**GetAsync**/dotnet/API/Microsoft.Store.partnercenter.subscriptions.isubscriptioncollection.getasync) pour récupérer la collection d’abonnements du client. Parcourez la collection d’abonnements et assurez-vous qu’aucun des abonnements n’a une valeur de propriété [**Subscriptions. Status**/dotnet/API/Microsoft.Store.partnercenter.Models.subscriptions.Subscription.Status) de [**SubscriptionStatus. active**/dotnet/API/Microsoft.Store.partnercenter.Models.subscriptions.subscriptionstatus). Si un abonnement est toujours actif, consultez [suspendre un abonnement](https://review.docs.microsoft.com/partner-center/develop/suspend-a-subscription) pour plus d’informations sur la façon de le suspendre.

Après avoir confirmé que tous les Azure Reserved VM Instances actifs pour ce client sont annulés et que tous les abonnements actifs sont suspendus, vous pouvez supprimer la relation du revendeur pour le client. Tout d’abord, créez un objet [Customer/dotnet/API/Microsoft. Store. partnercenter. Models. Customers. Customer) avec la propriété [Customer. RelationshipToPartner/dotnet/API/Microsoft. Store. partnercenter. Models. Customers. Customer. RelationshipToPartner) définie sur [**CustomerPartnerRelationship. None**/dotnet/API/Microsoft.Store.partnercenter.Models.Customers.customerpartnerrelationship). Appelez ensuite la méthode [**collection iaggregatepartner. Customers. méthode BYID**/dotnet/API/Microsoft.Store.partnercenter.Customers.icustomercollection.BYID) à l’aide de l’identificateur du client pour spécifier le client, puis appelez la méthode **patch** , en transmettant le nouvel objet Customer.

Pour rétablir la relation, répétez le processus de [demande d’une relation de revendeur/partenaire-centre/développement/demande-revendeur-relation).

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

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **PATCH**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie les paramètres de requête requis pour supprimer une relation de revendeur.

| Nom                   | Type     | Obligatoire | Description                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | O        | La valeur est un GUID **client-ID-client-ID** qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Une ressource **client** est requise dans le corps de la demande. Vérifiez que la propriété **RelationshipToPartner** a été définie sur aucun.

### <a name="request-example"></a>Exemple de requête

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

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode supprime une relation de revendeur pour le client spécifié.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

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

---
title: Supprimer un compte client du bac à sable d’intégration
description: Comment supprimer un compte client du bac à sable (sandbox) d’intégration test en production (TIP).
ms.assetid: B95431F6-EA7F-4C21-835F-6D6C303B05A5
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d81341f46d9131ac19ba5ae48e424423b4b761e5
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155441"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a>Supprimer un compte client du bac à sable d’intégration

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cet article explique comment supprimer un compte client du bac à sable (sandbox) d’intégration test en production (TIP).

> [!IMPORTANT]
> Lorsque vous supprimez un compte client, toutes les ressources associées à ce locataire client sont purgées.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- Un ID client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le Rechercher dans le tableau de [bord](https://partner.microsoft.com/dashboard)de l’espace partenaires. Sélectionnez **CSP** dans le menu espace partenaires, puis **clients**. Sélectionnez le client dans la liste des clients, puis sélectionnez **compte**. Dans la page compte du client, recherchez l' **ID Microsoft** dans la section **informations sur le compte client** . L’ID Microsoft est le même que l’ID de client`customer-tenant-id`().

- Tous les Azure Reserved Virtual Machine Instances et les bons de commande logiciels doivent être annulés avant de supprimer un client du bac à sable (sandbox) d’intégration Tip.

## <a name="c"></a>C\#

Pour supprimer un client du bac à sable (sandbox) d’intégration Tip :

1. Transmettez les informations d’identification de votre compte Tip à la méthode [**CreatePartnerOperations**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) pour récupérer une interface [**collection ipartner**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.ipartner) pour les opérations de partenaire.

2. Utilisez l’interface opérateur partenaire pour récupérer la collection de droits :

    1. Appelez la méthode [**Customers. méthode BYID ()**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client pour spécifier le client.

    2. Appelez la propriété de **droits** .

    3. Appelez la méthode **GetAsync** pour **récupérer la collection** de [**droits**](entitlement-resources.md) .

3. Assurez-vous que tous les Azure Reserved Virtual Machine Instances et les bons de commande logiciels pour ce client sont annulés. Pour chaque [**droit**](entitlement-resources.md) du regroupement :

    1. Utilisez le [**droit. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) pour obtenir une copie locale de la [commande](order-resources.md#order) correspondante à partir de la collection de commandes du client.

    2. Définissez la propriété [**Order. Status**](order-resources.md#order) sur « Cancelled ».

    3. Utilisez la méthode **patch ()** pour mettre à jour la commande.

4. Annulez toutes les commandes. Par exemple, l’exemple de code suivant utilise une boucle pour interroger chaque commande jusqu’à ce que son état soit « annulé ».

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were cancelled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. Assurez-vous que toutes les commandes sont annulées en appelant la méthode **Delete** pour le client.

**Exemple**: [application de test console](console-test-app.md). **Projet**: Partner Center PartnerCenterSDK. FeaturesSamples, **classe**: DeleteCustomerFromTipAccount.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode     | URI de demande                                                                            |
|------------|----------------------------------------------------------------------------------------|
| Suppression     | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID} http/1.1 |

#### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de requête suivant pour supprimer un client.

| Nom                   | Type     | Obligatoire | Description                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| customer-tenant-id     | GUID     | O        | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a>Response REST

En cas de réussite, cette méthode retourne une réponse vide.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```

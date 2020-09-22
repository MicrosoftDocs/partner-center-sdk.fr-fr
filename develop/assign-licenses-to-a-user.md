---
title: Attribuer des licences à un utilisateur
description: Comment attribuer des licences à un utilisateur client.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c0b01525f6865411cc069677b7a7481f20ba87c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927432"
---
# <a name="assign-licenses-to-a-user"></a>Attribuer des licences à un utilisateur

**S’applique à :**

- Espace partenaires

Comment attribuer des licences à un utilisateur client.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

- Identificateur d’utilisateur du client. Cet ID identifie l’utilisateur auquel attribuer la licence.

- Identificateur SKU du produit qui identifie le produit de la licence.

## <a name="assigning-licenses-through-code"></a>Attribution de licences à l’aide de code

Lorsque vous affectez des licences à un utilisateur, vous devez choisir parmi le regroupement du client des références (SKU) souscrites. Ensuite, après avoir identifié les produits que vous souhaitez affecter, vous devez obtenir l’ID de référence du produit pour chaque produit afin d’effectuer les attributions. Chaque instance [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) contient une propriété [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) à partir de laquelle vous pouvez référencer l’objet [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) et obtenir l' [**ID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

Une demande d’attribution de licence doit contenir des licences d’un seul groupe de licences. Par exemple, vous ne pouvez pas attribuer des licences du [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) et du **Group2** dans la même demande. Toute tentative pour attribuer dans une seule demande des licences de plusieurs groupes échouera en générant l’erreur appropriée. Pour savoir quelles licences sont disponibles par groupe de licences, consultez [obtenir une liste des licences disponibles par groupe de licences](get-a-list-of-available-licenses-by-license-group.md).

Voici les étapes à suivre pour attribuer des licences par le biais du code :

1. Instanciez un objet [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) . Vous utilisez cet objet pour spécifier la référence SKU du produit et les plans de service à affecter.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Renseignez les propriétés de l’objet comme indiqué ci-dessous. Ce code part du principe que vous disposez déjà de l’ID de référence du produit et que tous les plans de service disponibles seront affectés (c’est-à-dire qu’aucun ne sera exclu).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Si vous ne disposez pas de l’ID de référence du produit, vous devez récupérer la collection de références (SKU) souscrites et obtenir l’ID de référence du produit à partir de l’un d’eux. Voici un exemple si vous connaissez le nom de référence du produit.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Ensuite, instanciez une nouvelle liste de type [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)et ajoutez l’objet de licence. Vous pouvez attribuer plusieurs licences en les ajoutant individuellement à la liste. Les licences incluses dans cette liste doivent provenir du même groupe de licences.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Créez une instance [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) et affectez la liste des attributions de licence à la propriété [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Appelez la méthode [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) ou [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) et transmettez l’objet de mise à jour de licence comme indiqué ci-dessous pour affecter les licences.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Pour attribuer une licence à un utilisateur client, commencez par instancier un objet [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) et renseignez les propriétés [**SkuID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) et [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) . Vous utilisez cet objet pour spécifier la référence SKU du produit à assigner et les plans de service à exclure. Ensuite, instanciez une nouvelle liste de type **LicenseAssignment**et ajoutez l’objet de licence à la liste. Créez ensuite une instance [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) et affectez la liste des attributions de licence à la propriété [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

Ensuite, utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**users. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) avec l’ID d’utilisateur pour identifier l’utilisateur. Ensuite, accédez à une interface pour les opérations de mise à jour de licence utilisateur client à partir de la propriété [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .

Enfin, appelez la méthode [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) ou [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) et transmettez l’objet de mise à jour de licence pour affecter la licence.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: **classe**d’exemples du kit de développement logiciel (SDK) Partner Center : CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>Paramètres URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’utilisateur.

| Nom        | Type   | Obligatoire | Description                                       |
|-------------|--------|----------|---------------------------------------------------|
| customer-id | string | Oui      | ID au format GUID qui identifie le client. |
| user-id     | string | Oui      | ID au format GUID qui identifie l’utilisateur.     |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Incluez une ressource [LicenseUpdate](license-resources.md#licenseupdate) dans le corps de la requête qui spécifie les licences à affecter.

### <a name="request-example"></a>Exemple de requête

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, un code d’état de réponse HTTP 201 est retourné et le corps de la réponse contient une ressource [LicenseUpdate](license-resources.md#licenseupdate) avec les informations de licence.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example-success"></a>Exemple de réponse (réussite)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a>Exemple de réponse (la licence n’est pas disponible)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```

---
title: Attribuer des licences à un utilisateur
description: Comment attribuer des licences à un utilisateur client.
ms.assetid: 872C7444-DF89-4EB5-8C1E-1D8E2934A40E
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 615e2dba04556647c358d5b382047e37e70606f8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489189"
---
# <a name="assign-licenses-to-a-user"></a>Attribuer des licences à un utilisateur

S’applique à :

- Espace partenaires

Comment attribuer des licences à un utilisateur client.

## <a name="prerequisites"></a>Conditions préalables

- Informations d’identification, comme décrit dans [authentification de l’espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application + utilisateur uniquement.
- Identificateur du client. Le client doit disposer d’un abonnement avec une licence disponible à affecter.
- Identificateur d’utilisateur du client. Cela identifie l’utilisateur auquel attribuer la licence.
- Identificateur SKU du produit qui identifie le produit de la licence.

## <a name="assigning-licenses-through-code"></a>Attribution de licences à l’aide de code

Lorsque vous affectez des licences à un utilisateur, vous devez choisir parmi le regroupement du client des références (SKU) souscrites. Ensuite, après avoir identifié les produits que vous souhaitez affecter, vous devez obtenir l’ID de référence du produit pour chaque produit afin d’effectuer les attributions. Chaque instance [**SubscribedSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) contient une propriété [**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) à partir de laquelle vous pouvez référencer l’objet [**ProductSku**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) et obtenir l' [**ID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

Une demande d’attribution de licence doit contenir des licences d’un seul groupe de licences. Par exemple, vous ne pouvez pas attribuer des licences à partir de [**Group1**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) et de **Group2** dans la même demande. Une tentative d’attribution de licences à partir de plusieurs groupes dans une demande unique échouera avec une erreur appropriée. Pour savoir quelles licences sont disponibles par groupe de licences, consultez [obtenir une liste des licences disponibles par groupe de licences](get-a-list-of-available-licenses-by-license-group.md).

Voici les étapes à suivre pour attribuer des licences par le biais du code :

1. Instanciez un objet [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) . Vous utilisez cet objet pour spécifier la référence SKU du produit et les plans de service à affecter.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Renseignez les propriétés de l’objet comme indiqué ci-dessous. Ce code part du principe que vous disposez déjà de l’ID de référence du produit et que tous les plans de service disponibles seront affectés (c.-à-d. aucun sera exclu).
  
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

4. Ensuite, instanciez une nouvelle liste de type [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)et ajoutez l’objet de licence. Vous pouvez attribuer plusieurs licences en les ajoutant individuellement à la liste. Les licences incluses dans cette liste doivent provenir du même groupe de licences.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Créez une instance [**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) et affectez la liste des attributions de licence à la propriété [**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) et transmettez l’objet de mise à jour de licence comme indiqué ci-dessous pour affecter les licences.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>\# C

Pour attribuer une licence à un utilisateur client, commencez par instancier un objet [**LicenseAssignment**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) et renseignez les propriétés [**SkuID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) et [**ExcludedPlans**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) . Vous utilisez cet objet pour spécifier la référence SKU du produit à assigner et les plans de service à exclure. Ensuite, instanciez une nouvelle liste de type **LicenseAssignment**et ajoutez l’objet de licence à la liste. Créez ensuite une instance [**LicenseUpdate**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) et affectez la liste des attributions de licence à la propriété [**LicensesToAssign**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) .

Ensuite, utilisez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’ID client pour identifier le client et la méthode [**users. méthode BYID**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) avec l’ID d’utilisateur pour identifier l’utilisateur. Ensuite, accédez à une interface pour les opérations de mise à jour de licence utilisateur client à partir de la propriété [**LicenseUpdates**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) .

Enfin, appelez la méthode [**Create**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) ou [**CreateAsync**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) et transmettez l’objet de mise à jour de licence pour affecter la licence.

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

## <a name="request"></a>Requête

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Publier** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>Paramètres d’URI

Utilisez les paramètres de chemin d’accès suivants pour identifier le client et l’utilisateur.

| Nom        | Type   | Obligatoire | Description                                       |
|-------------|--------|----------|---------------------------------------------------|
| ID client | chaîne | Oui      | ID au format GUID qui identifie le client. |
| ID utilisateur     | chaîne | Oui      | ID au format GUID qui identifie l’utilisateur.     |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [en-têtes REST de l’espace partenaires](headers.md) .

### <a name="request-body"></a>Corps de la requête

Vous devez inclure une ressource [LicenseUpdate](license-resources.md#licenseupdate) dans le corps de la requête qui spécifie les licences à affecter.

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

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec, ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

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

### <a name="response-example-license-is-not-available"></a>Exemple de réponse (licence non disponible)

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
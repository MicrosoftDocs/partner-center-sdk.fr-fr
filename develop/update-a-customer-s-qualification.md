---
title: Mettre à jour la qualification d’un client
description: Met à jour la qualification d’un client, y compris l’adresse associée au profil.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0896c44ab193ca564ee210f48f536382c8070305
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414955"
---
# <a name="update-a-customers-qualification"></a>Mettre à jour la qualification d’un client


**S’applique à**

- Centre pour partenaires

Met à jour la qualification d’un client.

Un partenaire peut mettre à jour la qualification d’un client pour qu’il soit « Education » ou « GovernmentCommunityCloud ». Les autres valeurs, « None » et « imbutistes », ne peuvent pas être définies.

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>conditions préalables

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application et de l’utilisateur uniquement.
- ID client (client-locataire-ID).


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#

Pour mettre à jour la qualification d’un client vers « Education », appelez **[Update](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification.update)** sur un [**client**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customer?view=partnercenter-dotnet-latest)existant.

``` csharp
// CustomerQualification is an enum

var eduCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.Education);
```

**Exemple**: [application de test console](console-test-app.md). **Projet**: PartnerSDK. FeatureSamples, **classe**: CustomerQualificationOperations.cs

Pour mettre à jour la qualification d’un client vers **GovernmentCommunityCloud** sur un client existant sans qualification.  Le partenaire doit également inclure le [**ValidationCode**](utility-resources.md#validationcode)du client. 
``` csharp
// CustomerQualification is an enum
// GCC validation is type ValidationCode

var gccCustomerQualification = partnerOperations.Customers.ById(existingCustomer.Id).Qualification.Update(CustomerQualification.GovernmentCommunityCloud, gccValidation);
```


## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> demande REST

**Syntaxe de la requête**

| Méthode  | URI de demande                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/Customers/{customer_id}/qualification ? code = {VALIDATIONCODE} http/1.1 |


**Paramètre URI**

Utilisez le paramètre de requête suivant pour mettre à jour la qualification.

| Nom                   | Type | Obligatoire | Description                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **client-locataire-ID** | GUID | Oui      | La valeur est un GUID **client-ID-client-ID** qui permet au revendeur de filtrer les résultats pour un client donné qui appartient au revendeur. |
| **validationCode**     | int  | Non       | Nécessaire uniquement pour le Cloud de la communauté gouvernementale.                                                                                                            |


**En-têtes de demande**

- Pour plus d’informations, consultez [en-têtes](headers.md) .

**Corps de la demande**

Valeur entière de l’énumération [**CustomerQualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) .

**Exemple de requête**

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

3
```

## <a name="span-id_responsespan-id_responsespan-id_response-rest-response"></a><span id="_Response"/><span id="_response"/><span id="_RESPONSE"/> réponse REST

En cas de réussite, cette méthode retourne la propriété de [**qualification**](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) mise à jour dans le corps de la réponse.

**Codes d’erreur et de réussite de la réponse**

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

**Exemple de réponse**

```http
HTTP/1.1 200 OK
Content-Length: 14
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
"governmentcommunitycloud"
```

## <a name="related-topics"></a>Rubriques connexes

- [Obtenir la qualification d’un client](get-a-customer-s-qualification.md)
- [Obtenir les codes de validation d’un partenaire](get-a-partner-s-validation-codes.md)
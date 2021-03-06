---
title: Obtenir la qualification d’un client
description: Comment obtenir la qualification d’un client.
ms.date: 08/07/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: ac0d1ba8d17fbbfcd0d0c8870a4722fe89010749
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927775"
---
# <a name="get-a-customers-qualification"></a>Obtenir la qualification d’un client

**S’applique à**

- Espace partenaires

Comment obtenir la qualification d’un client.

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="c"></a>C\#

Pour obtenir la qualification d’un client, appelez la méthode [**collection iaggregatepartner. Customers. méthode BYID**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) avec l’identificateur du client. Utilisez ensuite la propriété [**qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) pour récupérer une interface [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) . Enfin, appelez [**obtenir**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) ou [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) pour récupérer la qualification du client.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode  | URI de requête                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-tenant-ID}/qualification http/1.1 |

### <a name="uri-parameter"></a>Paramètre d’URI

Ce tableau répertorie le paramètre de requête requis pour obtenir toutes les qualifications.

| Nom               | Type   | Obligatoire | Description                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **customer-tenant-id** | string | Oui      | Chaîne au format GUID qui identifie le client. |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Aucun.

### <a name="request-example"></a>Exemple de requête

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne une valeur de qualification dans le corps de la réponse.  Voici un exemple de l’appel de la fonction **obtenir** sur un client avec la qualification **Education** .

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur REST de l’Espace partenaires](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a>Articles connexes

- [Mettre à jour la qualification d’un client](update-a-customer-s-qualification.md)

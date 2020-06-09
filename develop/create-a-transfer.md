---
title: Créer un transfert
description: Comment créer un transfert d’abonnements pour un client.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7d6e8efddc64bc2b4b36005f0892927f5b3454f8
ms.sourcegitcommit: e39e8dccf25020cccda8bcea83b72e7ef8a6a7c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84489176"
---
# <a name="create-a-transfer"></a>Créer un transfert

**S’applique à :**

- Espace partenaires

## <a name="prerequisites"></a>Prérequis

- Informations d’identification, comme décrit dans [Authentification auprès de l’Espace partenaires](partner-center-authentication.md). Ce scénario prend en charge l’authentification avec les informations d’identification de l’application autonome et de l’application + utilisateur.

- ID du client (`customer-tenant-id`). Si vous ne connaissez pas l’ID du client, vous pouvez le rechercher dans le [tableau de bord](https://partner.microsoft.com/dashboard) de l’Espace partenaires. Sélectionnez **CSP** dans le menu Espace partenaires, puis **Clients**. Sélectionnez le client dans la liste des clients, puis **Compte**. Dans la page du compte du client, recherchez l’**ID Microsoft** dans la section **Informations sur le compte client**. L’ID Microsoft est le même que l’ID de client (`customer-tenant-id`).

## <a name="rest-request"></a>Demande REST

### <a name="request-syntax"></a>Syntaxe de la requête

| Méthode   | URI de requête                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers http/1.1                    |

### <a name="uri-parameter"></a>Paramètre d’URI

Utilisez le paramètre de chemin d’accès suivant pour identifier le client.

| Nom            | Type     | Obligatoire | Description                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ID client** | string   | Oui      | ID client au format GUID qui identifie le client.             |

### <a name="request-headers"></a>En-têtes de requête

Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

### <a name="request-body"></a>Corps de demande

Ce tableau décrit les propriétés [TransferEntity](transfer-entity-resources.md) dans le corps de la demande.

| Propriété              | Type          | Obligatoire  | Description                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | string        | Non    | Identificateur transferEntity qui est fourni lors de la création réussie du transferEntity.                               |
| createdTime           | DateTime      | Non    | Date à laquelle le transferEntity a été créé, au format date/heure. Appliqué en cas de création réussie du transferEntity.      |
| lastModifiedTime      | DateTime      | Non    | Date à laquelle le transferEntity a été mis à jour pour la dernière fois au format date-heure. Appliqué en cas de création réussie du transferEntity. |
| lastModifiedUser      | string        | Non    | Utilisateur qui a mis à jour la transferEntity. Appliqué en cas de réussite de la création de transferEntity.                          |
| customerName          | string        | Non    | facultatif. Nom du client dont les abonnements sont en cours de transfert.                                              |
| customerTenantId      | string        | Non    | ID client au format GUID qui identifie le client. Appliqué en cas de création réussie du transferEntity.         |
| partnertenantid       | string        | Non    | Identificateur de partenaire au format GUID qui identifie le partenaire.                                                                   |
| sourcePartnerName     | string        | Non    | facultatif. Nom de l’organisation partenaire qui lance le transfert.                                           |
| sourcePartnerTenantId | string        | Oui   | Un ID de partenaire au format GUID qui identifie le partenaire qui lance le transfert.                                           |
| targetPartnerName     | string        | Non    | facultatif. Nom de l’organisation du partenaire à laquelle le transfert est destiné.                                         |
| targetPartnerTenantId | string        | Oui   | Un ID de partenaire au format GUID qui identifie le partenaire auquel le transfert est destiné.                                  |
| lineItems             | Tableau d’objets | Oui| Tableau de ressources [TransferLineItem](transfer-entity-resources.md#transferlineitem) .                                   |
| status                | string        | Non    | État du transferEntity. Les valeurs possibles sont « active » (peut être supprimée/envoyée) et « Completed » (a déjà été effectué). Appliqué en cas de création réussie du transferEntity.|

Ce tableau décrit les propriétés [TransferLineItem](transfer-entity-resources.md#transferlineitem) dans le corps de la demande.

|      Propriété       |            Type             | Obligatoire | Description                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | string                     | No       | Identificateur unique pour un élément de ligne de transfert. Appliqué en cas de création réussie du transferEntity.|
| subscriptionId       | string                     | Oui      | Identificateur de l’abonnement.                                                                         |
| quantité             | int                        | Non       | Nombre de licences ou d’instances.                                                                 |
| billingCycle         | Object                     | Non        | Type de cycle de facturation défini pour la période actuelle.                                                |
| friendlyName         | string                     | Non       | facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                |
| partnerIdOnRecord    | string                     | No       | Partenaire sur l’enregistrement (MPNID) de l’achat qui se produit lorsque le transfert est accepté.              |
| offerId              | string                     | No       | Identificateur de l’offre.                                                                                |
| addonItems           | Liste d’objets **TransferLineItem** | Non | Collection d’éléments de ligne transferEntity pour les modules complémentaires qui seront transférés avec l’abonnement de base en cours de transfert. Appliqué en cas de création réussie du transferEntity.|
| transferError        | string                     | No       | Appliqué après l’acceptation de transferEntity en cas d’erreur.                                        |
| status               | string                     | No       | État de l’LineItem dans transferEntity.                                                    |

### <a name="request-example"></a>Exemple de requête

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>Réponse REST

En cas de réussite, cette méthode retourne la ressource [TransferEnity](transfer-entity-resources.md) remplie dans le corps de la réponse.

### <a name="response-success-and-error-codes"></a>Codes d’erreur et de réussite de la réponse

Chaque réponse est accompagnée d’un code d’état HTTP qui indique la réussite ou l’échec ainsi que des informations de débogage supplémentaires. Utilisez un outil de trace réseau pour lire ce code, le type d’erreur et des paramètres supplémentaires. Pour obtenir la liste complète, consultez [Codes d’erreur](error-codes.md).

### <a name="response-example"></a>Exemple de réponse

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```

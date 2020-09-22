---
title: Ressources de droits
description: Décrit les ressources associées au droit.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927303"
---
# <a name="entitlement-resources"></a>Ressources de droits

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

## <a name="entitlement"></a>Entitlement

Cette ressource représente les produits que le client a le droit d’utiliser en raison de l’achat d’un partenaire sur les éléments du catalogue.

| Propriété | Type | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Référence de commande qui a donné le droit. |
| productId | string | ID du produit. |
| skuID | string | ID de la référence (SKU). |
| quantité | int | La quantité de droits (exclut les droits non remplis/transférés). |
| quantityDetails | [QuantityDetail](#quantitydetail) IEnumerable<> | Liste des détails sur la quantité de droits (nombre d’articles et état de chaque quantité). |
| entitlementType | string | Type de droit. (Mis à jour vers la chaîne de [EntitlementType](#entitlementtype) dans le kit de développement logiciel 1,8.) |
| entitledArtifacts | [Artefact](#artifact)<IEnumerable> | Liste des artefacts associés au droit. |
| IncludedEntitlements | [Droits](#artifact) d'<IEnumerable> | Liste des habilitations, qui sont implicitement incluses à la suite de l’achat ProductId/SkuId à partir du catalogue. |
| ExpiryDate | chaîne au format date-heure UTC  | Date d’expiration du droit (le cas échéant). |

## <a name="referenceorder"></a>ReferenceOrder

Référence de commande d’un droit.

| Propriété | Type | Description |
|----------|------|-------------|
| id | string | ID de l’ordre référencé. |
| lineItemId | string | ID de l’élément de ligne de commande référencé. |
| alternateId | string | Autre ID de l’élément de ligne de commande référencé. |

## <a name="quantitydetail"></a>QuantityDetail

Représente les détails d’une quantité de droit.

| Propriété | Type | Description |
|----------|------|-------------|
| quantité | int | Nombre d'éléments. |
| status | string | État de la quantité. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

[Énumération](/dotnet/api/system.enum) avec des valeurs qui indiquent le type de droit.

| Valeur | Description |
|-------|-------------|
| Logiciel | Indique le type de droit lié au logiciel. |
| VirtualMachineReservedInstance | Indique le type de droit lié à Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefact

Artefact associé au droit.

| Propriété | Type | Description |
|----------|------|-------------|
| artifactType | string | Type d’artefact. (Mis à jour vers la chaîne à partir de [artifactType](#artifacttype) dans le SDK v 1.8) |
| dynamicAttributes | Dictionnaire&lt;chaîne, objet&gt; | Attributs dynamiques contenant des valeurs spécifiques artifactType. Par exemple, lorsque artifactType = "reservedinstance", cette propriété contient "reservationType" = "VirtualMachines" ou "reservationType" = "sqldatabases" qui dénote l’instance réservée de machine virtuelle ou l’instance réservée SQL Azure. (Disponible à partir du SDK v 1.9) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

[Énumération](/dotnet/api/system.enum) avec des valeurs qui indiquent le type d’artefact d’habilitation.

| Valeur                          | Description                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Indique que l’artefact facilite la récupération de Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefact associé à un droit d’instance réservée Azure. Elle hérite de la classe d' [artefact](#artifact) .

| Propriété   | Type                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [Lien](./utility-resources.md#link) | Lien permettant d’accéder à tous les détails d’artefact associés.   |
| resourceID | string                         | ID de la ressource ou de l’ordre de réservation Azure. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Représente l’entité retournée lors de l’appel du lien d’artefact d’instance réservée Azure.

|   Propriété   |           Type           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     Type d’artefact.                     |
| reservations | IEnumerable<Reservation> | Indique l’identifiant de la ressource ou de l’ordre de réservation Azure. |

## <a name="reservation"></a>Réservation

Représente une réservation individuelle.

| Propriété          | Type                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | ID de la réservation.                                         |
| scopeType         | string                         | Type d’étendue associé à la réservation d’ordinateur virtuel. |
| displayName       | string                         | Nom complet de la réservation.                               |
| appliedScopes     | IEnumerable                    | Liste des étendues appliquées associées à la réservation. (Disponible uniquement quand scopeType n’est pas partagé.) |
| quantité          | int                            | Nombre de machines virtuelles dans la réservation.                 |
| expiryDateTime    | chaîne au format date-heure UTC | Date d’expiration de la réservation.                                |
| effectiveDateTime | chaîne au format date-heure UTC | Date d’effet de la réservation.                             |
| provisioningState | string                         | État d’approvisionnement de la réservation.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Artefact associé à une instance de machine virtuelle réservée Azure. Elle hérite de la classe d' [artefact](#artifact) .

| Propriété   | Type                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [Lien](utility-resources.md#link) | Lien permettant d’accéder à tous les détails d’artefact associés.   |
| resourceID | string                            | ID de la ressource ou de l’ordre de réservation Azure. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Représente l’entité retournée lors de l’appel du lien d’artefact d’instance de machine virtuelle réservée Azure.

| Propriété                    | Type                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | Type d’artefact. |
| virtualMachineReservations  | [VirtualMachineReservation](#virtualmachinereservation) IEnumerable<> | Indique l’identifiant de la ressource ou de l’ordre de réservation Azure. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Représente une réservation d’ordinateur virtuel individuelle.

|     Propriété      |              Type              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         ID de la réservation.                                         |
|     scopeType     |             string             |                     Type d’étendue associé à la réservation d’ordinateur virtuel.                     |
|    displayName    |             string             |                                    Nom complet de la réservation.                                    |
|   appliedScopes   |      IEnumerable<string>       | Liste des étendues appliquées associées à la réservation. (Disponible uniquement quand scopeType n’est pas partagé.) |
|     quantité      |              int               |                             Nombre de machines virtuelles dans la réservation.                             |
|  expiryDateTime   | chaîne au format date-heure UTC |                                    Date d’expiration de la réservation.                                     |
| effectiveDateTime | chaîne au format date-heure UTC |                                   Date d’effet de la réservation.                                   |
| provisioningState |             string             |                                 État d’approvisionnement de la réservation.                                 |

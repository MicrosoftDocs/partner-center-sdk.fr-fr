---
title: Ressources de la stratégie libre-service
description: Un partenaire définit des stratégies de libre-service pour un client.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dc0da58debb7ea0c32272bf180f26d535110d4a5
ms.sourcegitcommit: f71c7fb2fef51ac7ca0a28717d5f7276bd20ec56
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82564317"
---
# <a name="selfservepolicy-resource"></a>Ressource SelfServePolicy

**S’applique à :**

- Espace partenaires

Un partenaire définit des stratégies de libre-service pour un client.

## <a name="selfservepolicy"></a>SelfServePolicy

Décrit un panier.

| Propriété              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | Identificateur de stratégie libre-service fourni lors de la création réussie de la stratégie de libre-service.     |
| SelfServeEntity       | SelfServeEntity  | Entité libre-service à laquelle l’accès est accordé.                                                     |
| Fournisseur d'autorisations               | Fournisseur d'autorisations          | Fournisseur d’autorisations qui accorde l’accès.                                                                    |
| Autorisations           | Tableau d’autorisations| Tableau de ressources d' [autorisation](#permission) .                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Représente l’entité à laquelle des autorisations sont accordées.

| Propriété             | Type|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | string                           | Entité à laquelle l’accès est accordé, valeurs acceptées : client.                                 |
| ID de locataire             | string                           | Identificateur du locataire de l’entité à laquelle l’accès est accordé.                                   |

## <a name="grantor"></a>Fournisseur d'autorisations

Représente l’accordeur accordant les autorisations.

| Propriété             | Type|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | string                           | Accordeur accordant l’accès, valeurs acceptées : BillToPartner.                               |
| ID de locataire             | string                           | Identificateur de locataire de l’entité qui accorde l’accès.                                       |


## <a name="permission"></a>Autorisation

Représente une autorisation dans la stratégie libre-service.

| Propriété             | Type|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Ressource             | string                           | L’accès aux ressources est également accordé : AzureReservedInstances.                          |
| Action               | string                           | L’accès à l’action est accordé pour : achat                                           |

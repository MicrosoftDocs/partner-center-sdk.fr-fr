---
title: Ressources de relations
description: Décrit les ressources liées aux relations.
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3e444653a8b5acd5dafbebe8e4526c50e7951155
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124432"
---
# <a name="relationships-resources"></a>Ressources de relations

**S’applique à**

- Espace partenaires

Décrit les ressources liées aux relations.

## <a name="partnerrelationship"></a>PartnerRelationship

Représente une relation entre deux partenaires.

| Propriété         | Type                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | Identificateur du partenaire. L’identificateur de partenaire spécifie l’ID de locataire du partenaire qui se trouve dans le côté destinataire (de) de la relation. |
| location         | string                                                         | Emplacement du partenaire.                                                                                                                   |
| mpnId            | string                                                         | Identificateur Microsoft Partner Network (MPN) du partenaire.                                                                                 |
| name             | string                                                         | Nom du partenaire.                                                                                                                       |
| relationshipType | string                                                         | Type de relation.                                                                                                                      |
| state            | string                                                         | État de la relation (par exemple `active`).                                                                                                 |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Fournit l’URL permettant à un client d’établir une relation avec un partenaire.

| Propriété   | Type                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | URL de demande de relation. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.      |

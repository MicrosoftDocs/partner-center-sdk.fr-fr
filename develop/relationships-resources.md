---
title: Ressources de relations
description: Décrit les ressources liées aux relations.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094927"
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
| state            | string                                                         | État de la relation (par exemple `active` ).                                                                                                 |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Fournit l’URL permettant à un client d’établir une relation avec un partenaire.

| Propriété   | Type                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | URL de demande de relation. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.      |

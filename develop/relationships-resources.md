---
title: Ressources de relations
description: Décrit les ressources liées aux relations.
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1d6d41256c081f3ef5ce7b27d89498839d8f5c8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488099"
---
# <a name="relationships-resources"></a>Ressources de relations


**S’applique à**

- Espace partenaires

Décrit les ressources liées aux relations.

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


Représente une relation entre deux partenaires.

| Propriété         | Type                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | chaîne                                                         | Identificateur du partenaire. L’identificateur de partenaire spécifie l’ID de locataire du partenaire qui se trouve dans le côté destinataire (de) de la relation. |
| location         | chaîne                                                         | Emplacement du partenaire.                                                                                                                   |
| mpnId            | chaîne                                                         | Identificateur Microsoft Partner Network (MPN) du partenaire.                                                                                 |
| name             | chaîne                                                         | Nom du partenaire.                                                                                                                       |
| relationshipType | chaîne                                                         | Type de relation.                                                                                                                      |
| Département            | chaîne                                                         | État de la relation (par exemple, « actif »).                                                                                                 |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


Fournit l’URL permettant à un client d’établir une relation avec un partenaire.

| Propriété   | Type                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | chaîne                                                         | URL de demande de relation. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.      |

 

 

 





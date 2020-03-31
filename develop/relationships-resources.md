---
title: Ressources de relations
description: Décrit les ressources liées aux relations.
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8050b8afa3b92007dbcad2869050b6f2a8c248f7
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415467"
---
# <a name="relationships-resources"></a>Ressources de relations


**S’applique à**

- Centre pour partenaires

Décrit les ressources liées aux relations.

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


Représente une relation entre deux partenaires.

| Propriété         | Type                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | chaîne                                                         | Identificateur du partenaire. L’identificateur de partenaire spécifie l’ID de locataire du partenaire qui se trouve dans le côté destinataire (de) de la relation. |
| emplacement         | chaîne                                                         | Emplacement du partenaire.                                                                                                                   |
| mpnId            | chaîne                                                         | Identificateur Microsoft Partner Network (MPN) du partenaire.                                                                                 |
| nom             | chaîne                                                         | Nom du partenaire.                                                                                                                       |
| relationshipType | chaîne                                                         | Type de relation.                                                                                                                      |
| state            | chaîne                                                         | État de la relation (par exemple, « actif »).                                                                                                 |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


Fournit l’URL permettant à un client d’établir une relation avec un partenaire.

| Propriété   | Type                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | chaîne                                                         | URL de demande de relation. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées.      |

 

 

 





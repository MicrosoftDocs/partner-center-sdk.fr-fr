---
title: Relationships resources
description: Describes resources related to relationships.
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
# <a name="relationships-resources"></a>Relationships resources


**Applies To**

- Espace partenaires

Describes resources related to relationships.

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


Represents a relationship between two partners.

| Propriété         | Tapez                                                           | Description                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | chaîne                                                         | The partner identifier. The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship. |
| location         | chaîne                                                         | The location of the partner.                                                                                                                   |
| mpnId            | chaîne                                                         | The Microsoft Partner Network (MPN) identifier of the partner.                                                                                 |
| name             | chaîne                                                         | The name of the partner.                                                                                                                       |
| relationshipType | chaîne                                                         | The type of relationship.                                                                                                                      |
| state            | chaîne                                                         | The state of the relationship (e.g. "active").                                                                                                 |
| attributs       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


Provides the URL by which a customer can establish a relationship with a partner.

| Propriété   | Tapez                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | chaîne                                                         | The relationship request URL. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.      |

 

 

 





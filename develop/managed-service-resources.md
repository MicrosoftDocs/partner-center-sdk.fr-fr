---
title: Ressources de service managées
description: Les services gérés sont des services auxquels un partenaire a délégué des privilèges d’administrateur. Les partenaires peuvent assurer la prise en charge des demandes de service de fichiers et pour le compte de leurs services gérés.
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 32cc11190425c2cdfdbf6c793ef75091915e5d69
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486899"
---
# <a name="managed-service-resources"></a>Ressources de service managées


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les services gérés sont des services auxquels un partenaire a délégué des privilèges d’administrateur. Les partenaires peuvent assurer la prise en charge des demandes de service de fichiers et pour le compte de leurs services gérés.

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


Décrit un service managé.

| Propriété   | Type                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | chaîne              | ID de service managé.                                  |
| Nom       | chaîne              | Nom du service managé.                         |
| GroupName  | chaîne              | Nom du groupe auquel appartient le service.      |
| Liens      | ManagedServiceLinks | Liens vers les ressources correspondant au service géré. |
| Attributs | ResourceAttributes  | Attributs de métadonnées correspondant à l’accord.  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


Contient les liens qui permettent au partenaire disposant d’autorisations d’administrateur déléguées de prendre en charge le service.

| Propriété      | Type | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Lien | URI du service d’administration.      |
| ServiceHealth | Lien | URI d’intégrité du service.     |
| ServiceTicket | Lien | URI de ticket de service.     |
| Self (Auto)          | Lien | URI auto.               |
| Suivant          | Lien | Page suivante des éléments.     |
| Précédent      | Lien | Page d’éléments précédente. |

 

 

 





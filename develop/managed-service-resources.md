---
title: Ressources de service managées
description: Les services gérés sont des services auxquels un partenaire a délégué des privilèges d’administrateur. Les partenaires peuvent assurer la prise en charge des demandes de service de fichiers et pour le compte de leurs services gérés.
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a4de6e373748026c56599f8e7153569f04a0c9cf
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118645"
---
# <a name="managed-service-resources"></a>Ressources de service managées

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les services gérés sont des services auxquels un partenaire a délégué des privilèges d’administrateur. Les partenaires peuvent assurer la prise en charge des demandes de service de fichiers et pour le compte de leurs services gérés.

## <a name="managedservice"></a>ManagedService

Décrit un service managé.

| Propriété   | Type                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | ID de service managé.                                  |
| Nom       | string              | Nom du service managé.                         |
| GroupName  | string              | Nom du groupe auquel appartient le service.      |
| Liens      | ManagedServiceLinks | Liens vers les ressources correspondant au service géré. |
| Attributs | ResourceAttributes  | Attributs de métadonnées correspondant à l’accord.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Contient les liens qui permettent au partenaire disposant d’autorisations d’administrateur déléguées de prendre en charge le service.

| Propriété      | Type | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Lien | URI du service d’administration.      |
| ServiceHealth | Lien | URI d’intégrité du service.     |
| ServiceTicket, | Lien | URI de ticket de service.     |
| Self          | Lien | URI auto.               |
| Suivant          | Lien | Page suivante des éléments.     |
| Previous      | Lien | Page d’éléments précédente. |


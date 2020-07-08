---
title: Ressources de service managées
description: Les services gérés sont des services auxquels un partenaire a délégué des privilèges d’administrateur. Les partenaires peuvent assurer la prise en charge des demandes de service de fichiers et pour le compte de leurs services gérés.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094796"
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
| Précédente      | Lien | Page d’éléments précédente. |


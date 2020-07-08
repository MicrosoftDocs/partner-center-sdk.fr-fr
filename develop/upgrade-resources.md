---
title: Mettre à niveau les ressources
description: Décrit les ressources utilisées pour mettre à niveau un utilisateur à partir d’un abonnement source vers un abonnement cible.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096558"
---
# <a name="upgrade-resources"></a>Mettre à niveau les ressources

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit les ressources utilisées pour mettre à niveau un utilisateur à partir d’un abonnement source vers un abonnement cible.

## <a name="upgrade"></a>Mettre à niveau

Décrit le comportement d’une ressource de mise à niveau individuelle.

| Propriété      | Type                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Offre                  | L’offre de l’abonnement cible.                                                        |
| UpgradeType   | string                 | Type de mise à niveau : « aucun », « mettre à niveau \_ uniquement » ou « mettre à niveau \_ avec le \_ transfert de licence \_ ».         |
| IsEligible    | boolean                | Indique si la mise à niveau peut être effectuée.                                                  |
| Quantité      | entier                | Quantification de la nouvelle offre à acheter. La valeur par défaut est la quantité de l’abonnement source. |
| UpgradeErrors | Tableau de UpgradeErrors | Raisons pour lesquelles la mise à niveau ne peut pas être effectuée, le cas échéant.                                      |
| Attributs    | ResourceAttributes     | Attributs de métadonnées correspondant à la mise à niveau.                                        |

## <a name="upgradeerror"></a>UpgradeError

Décrit une raison pour laquelle une mise à niveau ne peut pas être effectuée.

| Propriété          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | string             | Code d’erreur associé au problème : « autre « », « autorisations d' \_ administrateur déléguées \_ \_ désactivées », « état de l’abonnement \_ \_ non \_ actif », « \_ \_ types de service en conflit », « \_ conflits d’accès concurrentiel », « \_ contexte utilisateur \_ requis », « \_ \_ modules complémentaires d’abonnement \_ présents », « abonnement \_ n' \_ \_ a pas \_ de \_ chemin de mise à niveau \_ », « offre de cible d’abonnement \_ \_ \_ \_ introuvable » \_ \_ |
| Description       | chaîne             | Texte convivial décrivant l’erreur.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | Détails supplémentaires concernant l’erreur.                                                                                                                                                                                                                                                                                                                                                         |
| Attributs        | ResourceAttributes | Attributs de métadonnées correspondant à l’erreur.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Décrit le résultat du processus de mise à niveau d’abonnement.

| Propriété             | Type                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | Identificateur de l’abonnement source.                                           |
| TargetSubscriptionID | string                      | Identificateur de l’abonnement cible.                                           |
| UpgradeType          | string                      | Type de mise à niveau : « aucun », « mettre à niveau \_ uniquement » ou « mettre à niveau \_ avec le \_ transfert de licence \_ ». |
| UpgradeErrors        | Tableau de UpgradeErrors      | Des erreurs se sont produites lors de la tentative d’exécution de la mise à niveau, le cas échéant.           |
| LicenseErrors        | Tableau de UserLicenseErrrors | Des erreurs se sont produites lors de la tentative de migration des licences utilisateur, le cas échéant.          |
| Attributs           | ResourceAttributes          | Attributs de métadonnées correspondant à la licence.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Décrit les erreurs dues à un échec de transfert de licence utilisateur.

| Propriété     | Type                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | Unique identifié de l’objet utilisateur.                                 |
| Nom         | string                 | Nom de l'utilisateur.                                                     |
| Courrier        | string                 | L’e-mail de l’utilisateur.                                                    |
| Errors       | Tableau de ServiceFaults | Liste des exceptions levées lors de la tentative de transfert de la licence utilisateur. |
| Attributs   | ResourceAttributes     | Attributs de métadonnées correspondant à la licence.                     |


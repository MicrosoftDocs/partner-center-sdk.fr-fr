---
title: Mettre à niveau les ressources
description: Décrit les ressources utilisées pour mettre à niveau un utilisateur à partir d’un abonnement source vers un abonnement cible.
ms.assetid: 869007B3-D6D4-4E79-B4F0-445CA5D88D2C
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cc89d1a4c4d31becbe3ec0f38c597d7f8aba9a0f
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118095"
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
| UpgradeType   | string                 | Type de mise à niveau : « aucun », «\_mettre à niveau uniquement » ou\_«\_mettre\_à niveau avec le transfert de licence ».         |
| IsEligible    | boolean                | Indique si la mise à niveau peut être effectuée.                                                  |
| Quantité      | entier                | Quantification de la nouvelle offre à acheter. La valeur par défaut est la quantité de l’abonnement source. |
| UpgradeErrors | Tableau de UpgradeErrors | Raisons pour lesquelles la mise à niveau ne peut pas être effectuée, le cas échéant.                                      |
| Attributs    | ResourceAttributes     | Attributs de métadonnées correspondant à la mise à niveau.                                        |

## <a name="upgradeerror"></a>UpgradeError

Décrit une raison pour laquelle une mise à niveau ne peut pas être effectuée.

| Propriété          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | string             | Code d'\_erreur associé au problème : « autre « », « autorisations\_\_d’administrateur déléguées désactivées »\_,\_«\_état de l’abonnement non actif\_»\_, « types de service en\_conflit », « conflits\_d'\_accès concurrentiel », «\_contexte\_utilisateur\_requis », « modules\_complémentaires\_d'\_abonnement\_présents\_»\_, « abonnement n’a\_pas\_de\_chemin\_de mise à niveau »,\_«\_offre de cible d’abonnement introuvable » |
| Description       | string             | Texte convivial décrivant l’erreur.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | Détails supplémentaires concernant l’erreur.                                                                                                                                                                                                                                                                                                                                                         |
| Attributs        | ResourceAttributes | Attributs de métadonnées correspondant à l’erreur.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Décrit le résultat du processus de mise à niveau d’abonnement.

| Propriété             | Type                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | Identificateur de l’abonnement source.                                           |
| TargetSubscriptionID | string                      | Identificateur de l’abonnement cible.                                           |
| UpgradeType          | string                      | Type de mise à niveau : « aucun », «\_mettre à niveau uniquement » ou\_«\_mettre\_à niveau avec le transfert de licence ». |
| UpgradeErrors        | Tableau de UpgradeErrors      | Des erreurs se sont produites lors de la tentative d’exécution de la mise à niveau, le cas échéant.           |
| LicenseErrors        | Tableau de UserLicenseErrrors | Des erreurs se sont produites lors de la tentative de migration des licences utilisateur, le cas échéant.          |
| Attributs           | ResourceAttributes          | Attributs de métadonnées correspondant à la licence.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Décrit les erreurs dues à un échec de transfert de licence utilisateur.

| Propriété     | Type                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | Unique identifié de l’objet utilisateur.                                 |
| Nom         | string                 | Nom de l'utilisateur.                                                     |
| E-mail        | string                 | L’e-mail de l’utilisateur.                                                    |
| Erreurs       | Tableau de ServiceFaults | Liste des exceptions levées lors de la tentative de transfert de la licence utilisateur. |
| Attributs   | ResourceAttributes     | Attributs de métadonnées correspondant à la licence.                     |


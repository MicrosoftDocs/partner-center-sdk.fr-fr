---
title: Mettre à niveau les ressources
description: Décrit les ressources utilisées pour mettre à niveau un utilisateur à partir d’un abonnement source vers un abonnement cible.
ms.assetid: 869007B3-D6D4-4E79-B4F0-445CA5D88D2C
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b085e6598ce9585e0bcea72724817b0b76b589a1
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486279"
---
# <a name="upgrade-resources"></a>Mettre à niveau les ressources


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Décrit les ressources utilisées pour mettre à niveau un utilisateur à partir d’un abonnement source vers un abonnement cible.

## <a name="span-idupgradespan-idupgradespan-idupgradeupgrade"></a>Mise à niveau de <span id="Upgrade"/><span id="upgrade"/><span id="UPGRADE"/>


Décrit le comportement d’une ressource de mise à niveau individuelle.

| Propriété      | Type                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Offre                  | L’offre de l’abonnement cible.                                                        |
| UpgradeType   | chaîne                 | Le type de mise à niveau : « None », « Upgrade\_Only » ou « Upgrade\_with\_License\_Transfer ».         |
| isEligible    | booléen                | Indique si la mise à niveau peut être effectuée.                                                  |
| Quantité      | Entier                | Quantification de la nouvelle offre à acheter. La valeur par défaut est la quantité de l’abonnement source. |
| UpgradeErrors | Tableau de UpgradeErrors | Raisons pour lesquelles la mise à niveau ne peut pas être effectuée, le cas échéant.                                      |
| Attributs    | ResourceAttributes     | Attributs de métadonnées correspondant à la mise à niveau.                                        |

 

## <a name="span-idupgradeerrorspan-idupgradeerrorspan-idupgradeerrorupgradeerror"></a><span id="UpgradeError"/><span id="upgradeerror"/><span id="UPGRADEERROR"/>UpgradeError


Décrit une raison pour laquelle une mise à niveau ne peut pas être effectuée.

| Propriété          | Type               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code              | chaîne             | Code d’erreur associé au problème : « autre « », « délégué\_autorisations de\_administrateur\_désactivé », « état de\_d’abonnement\_pas de\_actif », « types de\_de service\_en conflit », « conflits de\_d’accès concurrentiel », «\_de contexte utilisateur\_requis », « abonnement\_ajouter des\_des\_de mise à niveau » , « abonnement\_\_cible de l’offre\_pas\_trouvé », ou « abonnement\_pas configuré ».\_\_\_\_\_\_\_ |
| Description       | chaîne             | Texte convivial décrivant l’erreur.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | chaîne             | Détails supplémentaires concernant l’erreur.                                                                                                                                                                                                                                                                                                                                                         |
| Attributs        | ResourceAttributes | Attributs de métadonnées correspondant à l’erreur.                                                                                                                                                                                                                                                                                                                                             |

 

## <a name="span-idupgraderesultspan-idupgraderesultspan-idupgraderesultupgraderesult"></a><span id="UpgradeResult"/><span id="upgraderesult"/><span id="UPGRADERESULT"/>UpgradeResult


Décrit le résultat du processus de mise à niveau d’abonnement.

| Propriété             | Type                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | chaîne                      | Identificateur de l’abonnement source.                                           |
| TargetSubscriptionID | chaîne                      | Identificateur de l’abonnement cible.                                           |
| UpgradeType          | chaîne                      | Le type de mise à niveau : « None », « Upgrade\_Only » ou « Upgrade\_with\_License\_Transfer ». |
| UpgradeErrors        | Tableau de UpgradeErrors      | Des erreurs se sont produites lors de la tentative d’exécution de la mise à niveau, le cas échéant.           |
| LicenseErrors        | Tableau de UserLicenseErrrors | Des erreurs se sont produites lors de la tentative de migration des licences utilisateur, le cas échéant.          |
| Attributs           | ResourceAttributes          | Attributs de métadonnées correspondant à la licence.                                |

 

## <a name="span-iduserlicenseerrorspan-iduserlicenseerrorspan-iduserlicenseerroruserlicenseerror"></a><span id="UserLicenseError"/><span id="userlicenseerror"/><span id="USERLICENSEERROR"/>UserLicenseError


Décrit les erreurs dues à un échec de transfert de licence utilisateur.

| Propriété     | Type                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | chaîne                 | Unique identifié de l’objet utilisateur.                                 |
| Nom         | chaîne                 | Le nom de l'utilisateur.                                                     |
| E-mail        | chaîne                 | Adresse de messagerie de l’utilisateur.                                                    |
| Erreurs       | Tableau de ServiceFaults | Liste des exceptions levées lors de la tentative de transfert de la licence utilisateur. |
| Attributs   | ResourceAttributes     | Attributs de métadonnées correspondant à la licence.                     |

 

 

 





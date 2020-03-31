---
title: Ressources de document de contrat
description: La ressource AgreementDocument représente un document de contrat.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 917bb25ab5cb20b5148af056c5f433a8b62e9cc9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412680"
---
# <a name="agreement-document-resources"></a>Ressources de document de contrat

S'applique à :

- Centre pour partenaires

La ressource **AgreementDocument** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La ressource **AgreementDocument** représente un document de contrat Microsoft disponible pour l’aperçu et le téléchargement.

## <a name="agreementdocument"></a>AgreementDocument

Une ressource **AgreementDocument** comprend les propriétés suivantes :

| Propriété       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | chaîne | Pays ou marché auquel s’applique ce document. |
| language | chaîne | Langue dans laquelle ce document est localisé. |
| displayUri | chaîne | Lien pour afficher un aperçu du document de contrat dans un navigateur.  |
| downloadUri |chaîne | Un lien pour télécharger le document de contrat (au format Microsoft Word). |

---
title: Ressources de document de contrat
description: La ressource AgreementDocument représente un document de contrat.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ac079822a2ddb45310148c16101fa25a38ec492
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488929"
---
# <a name="agreement-document-resources"></a>Ressources de document de contrat

S’applique à :

- Espace partenaires

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

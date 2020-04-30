---
title: Ressources de document de contrat
description: La ressource AgreementDocument représente un document de contrat.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 21035d465094ab306d65ce3f24a006a97bf96354
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665151"
---
# <a name="agreement-document-resources"></a>Ressources de document de contrat

**S’applique à :**

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
| country | string | Pays ou marché auquel s’applique ce document. |
| langage | string | Langue dans laquelle ce document est localisé. |
| displayUri | string | Lien pour afficher un aperçu du document de contrat dans un navigateur.  |
| downloadUri |string | Un lien pour télécharger le document de contrat (au format Microsoft Word). |

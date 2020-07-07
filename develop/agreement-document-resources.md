---
title: Ressources de document de contrat
description: La ressource AgreementDocument représente un document de contrat.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 233277daece48cebe434ea3f458fd98fe6436de7
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022597"
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

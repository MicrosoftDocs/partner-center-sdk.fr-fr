---
title: Ressources TransferEligibility
description: Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 739631a4870268001c14f95490985ba18896e418
ms.sourcegitcommit: 4b1c10f91962861244c9349d5b9a9ba354b35b24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2020
ms.locfileid: "81220715"
---
# <a name="transfereligibility-resources"></a>Ressources TransferEligibility

S'applique à :

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.

## <a name="transfereligibility"></a>TransferEligibility

Décrit un transferEligibility.

| Propriété              | Type             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | chaîne           | Identificateur d’abonnement du client.                                                  |
| isEligible            | bool             | Indique si l’abonnement est éligible pour le transfert.                         |
| Raison                | chaîne           | Raison expliquant le ineligiblity si l’abonnement n’est pas éligible pour le transfert. |
---
title: Ressources TransferEligibility
description: Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095981"
---
# <a name="transfereligibility-resources"></a>Ressources TransferEligibility

**S’applique à :**

- Espace partenaires

Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.

## <a name="transfereligibility"></a>TransferEligibility

Décrit un transferEligibility.

| Propriété              | Type             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | Identificateur d’abonnement du client.                                                  |
| isEligible            | bool             | Indique si l’abonnement est éligible pour le transfert.                         |
| Motif                | string           | La propriété Reason explique pourquoi l’abonnement n’est pas éligible pour le transfert. |
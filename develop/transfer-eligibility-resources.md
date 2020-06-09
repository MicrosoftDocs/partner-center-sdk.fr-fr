---
title: Ressources TransferEligibility
description: Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 32ea176b079c48d7c48d114f6cfc96468699928f
ms.sourcegitcommit: e39e8dccf25020cccda8bcea83b72e7ef8a6a7c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84489186"
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
---
title: Ressources TransferEligibility
description: Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cb0ba6a4ff0daf6fa3ed04561aeb997822b5bc2b
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124314"
---
# <a name="transfereligibility-resources"></a>Ressources TransferEligibility

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.

## <a name="transfereligibility"></a>TransferEligibility

Décrit un transferEligibility.

| Propriété              | Type             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | Identificateur d’abonnement du client.                                                  |
| isEligible            | bool             | Indique si l’abonnement est éligible pour le transfert.                         |
| Motif                | string           | La propriété Reason explique pourquoi l’abonnement n’est pas éligible pour le transfert. |
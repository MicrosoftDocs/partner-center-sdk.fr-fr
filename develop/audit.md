---
title: Opérations d’audit
description: Obtenir un enregistrement de l’activité espace partenaires à l’aide d’opérations d’audit.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e31990df06a67d4f02b97dab8422ee498a09b43
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095393"
---
# <a name="audit-operations"></a>Opérations d’audit

Les API de l’espace partenaires fournissent des fonctionnalités d’audit afin que vous puissiez obtenir un enregistrement de l’activité espace partenaires.

Vous pouvez récupérer des enregistrements d’audit pour les 30 derniers jours à partir de la date actuelle ou pour une plage de dates spécifiée en incluant la date de début et/ou la date de fin. Notez, toutefois, que pour des raisons de performances, la disponibilité des données du journal d’activité est limitée aux 90 jours précédents. Les demandes avec une date de début supérieure à 90 jours avant la date actuelle recevront une exception de demande incorrecte (code d’erreur : 400) et un message approprié.

## <a name="retrieve-audit-records"></a>Récupérer les enregistrements d’audit

Obtenir des enregistrements d’audit historiques détaillés des opérations effectuées par un utilisateur partenaire ou une application :

- [Obtenir un enregistrement le l’activité de l’Espace partenaires](get-a-record-of-partner-center-activity-by-user.md)
- [Audit des ressources](auditing-resources.md)
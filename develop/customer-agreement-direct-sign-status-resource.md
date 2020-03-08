---
title: État de signature directe (acceptation directe) d’un contrat client.
description: La ressource DirectSignedCustomerAgreementStatus représente l’état de la signature directe (acceptation directe) d’un contrat client.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 25c24a9ed444663901126feb13a909fd7f2709ea
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78909085"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Statut de signature directe (acceptation directe) d’un contrat client

S'applique à :

- Centre pour partenaires

La ressource **DirectSignedCustomerAgreementStatus** est actuellement prise en charge par l’espace partenaires uniquement dans le cloud public Microsoft.

Cette ressource ne s' *applique pas* aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La ressource **DirectSignedCustomerAgreementStatus** représente l’état de l’acceptation directe d’un contrat client.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

Une ressource **DirectSignedCustomerAgreementStatus** comprend les propriétés suivantes :

| Propriété       | Type   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | booléen | Indique si le contrat client a été directement signé (accepté) par le client. |

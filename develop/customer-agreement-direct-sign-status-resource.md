---
title: État de signature directe (acceptation directe) d’un contrat client.
description: La ressource DirectSignedCustomerAgreementStatus représente l’état de la signature directe (acceptation directe) d’un contrat client.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 539d395aa096632dd7e15edeb2b2c98035c191ca
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412459"
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

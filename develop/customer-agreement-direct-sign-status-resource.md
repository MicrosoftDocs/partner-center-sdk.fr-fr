---
title: État de signature directe (acceptation directe) d’un contrat client.
description: La ressource DirectSignedCustomerAgreementStatus représente l’état de la signature directe (acceptation directe) d’un contrat client.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094316"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Statut de signature directe (acceptation directe) d’un contrat client

**S’applique à :**

- Espace partenaires

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
| isSigned | boolean | Indique si le contrat client a été directement signé (accepté) par le client. |

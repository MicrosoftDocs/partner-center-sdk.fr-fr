---
title: État de signature directe (acceptation directe) d’un contrat client.
description: La ressource DirectSignedCustomerAgreementStatus représente l’état de la signature directe (acceptation directe) d’un contrat client.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7575d5654cd8de9a65d4ee9ed484ff8cc0df2b0e
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022616"
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

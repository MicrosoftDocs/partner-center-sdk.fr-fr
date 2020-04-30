---
title: État de signature directe (acceptation directe) d’un contrat client.
description: La ressource DirectSignedCustomerAgreementStatus représente l’état de la signature directe (acceptation directe) d’un contrat client.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 23397ab479f32879b00c04a817ef889221a6f091
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665984"
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

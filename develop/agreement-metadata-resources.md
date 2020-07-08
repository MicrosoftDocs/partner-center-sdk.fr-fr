---
title: Ressources de métadonnées d’accord
description: La collection de ressources AgreementMetadata décrit les types de contrat que les partenaires peuvent utiliser pour fournir la confirmation de l’acceptation du client.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094586"
---
# <a name="agreement-metadata-resources"></a>Ressources de métadonnées d’accord

**S’applique à :**

- Espace partenaires

La ressource **AgreementMetaData** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La collection **AgreementMetaData** fournit des métadonnées sur tous les types de contrat. Les partenaires peuvent utiliser ce regroupement pour confirmer l’acceptation par le client des contrats. La collection **AgreementMetaData** retourne des métadonnées pour les deux types de contrat (**contrat de Microsoft Cloud** et contrat de **client Microsoft**).

## <a name="agreementmetadata"></a>AgreementMetaData

Les métadonnées d’accord retournées incluent les propriétés suivantes :

| Propriété      | Type               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | Identificateur unique d’un modèle de contrat.                                       |
| type          | string             | Type de contrat. Actuellement, les valeurs prises en charge sont **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement** (version préliminaire). |
| agreementLink | string             | URL du modèle d’accord.                                                    |

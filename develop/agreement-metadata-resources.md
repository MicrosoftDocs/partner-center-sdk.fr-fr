---
title: Ressources de métadonnées d’accord
description: La collection de ressources AgreementMetadata décrit les types de contrat que les partenaires peuvent utiliser pour fournir la confirmation de l’acceptation du client.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 642c3d079020d423db48aa8d3e1c0c1e12280fe3
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022603"
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

---
title: Ressources de métadonnées d’accord
description: La collection de ressources AgreementMetadata décrit les types de contrat que les partenaires peuvent utiliser pour fournir la confirmation de l’acceptation du client.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b147b44d4f4c1d986f7e3290c71ddbf0af54de70
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488709"
---
# <a name="agreement-metadata-resources"></a>Ressources de métadonnées d’accord

S’applique à :

- Espace partenaires

La ressource **AgreementMetaData** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La collection **AgreementMetaData** fournit des métadonnées sur tous les types de contrat. Les partenaires peuvent utiliser ce regroupement pour confirmer l’acceptation par le client des contrats. Actuellement, la collection **AgreementMetaData** retourne uniquement les métadonnées d’un type d’accord, qui est l' **accord Microsoft Cloud**.

## <a name="agreementmetadata"></a>AgreementMetaData

Les métadonnées d’accord retournées incluent les éléments suivants :

| Propriété      | Type               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | chaîne             | Identificateur unique d’un modèle de contrat.                                       |
| type          | chaîne             | Type de contrat. Actuellement, les valeurs prises en charge sont **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement** (version préliminaire). |
| agreementLink | chaîne             | URL du modèle d’accord.                                                    |

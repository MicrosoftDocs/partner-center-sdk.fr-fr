---
title: Ressources de métadonnées d’accord
description: La collection de ressources AgreementMetadata décrit les types de contrat que les partenaires peuvent utiliser pour fournir la confirmation de l’acceptation du client.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c772bb5554a551563befe0f40ab8e800a422ee2e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412748"
---
# <a name="agreement-metadata-resources"></a>Ressources de métadonnées d’accord

S'applique à :

- Centre pour partenaires

La ressource **AgreementMetaData** est actuellement prise en charge par l’espace partenaires uniquement dans le *cloud public Microsoft*. Cette ressource ne s’applique pas aux éléments suivants :

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La collection **AgreementMetaData** fournit des métadonnées sur tous les types de contrat. Les partenaires peuvent utiliser ce regroupement pour confirmer l’acceptation par le client des contrats. La collection **AgreementMetaData** retourne des métadonnées pour les deux types de contrat (**contrat de Microsoft Cloud** et contrat de **client Microsoft**).

## <a name="agreementmetadata"></a>AgreementMetaData

Les métadonnées d’accord retournées incluent les éléments suivants :

| Propriété      | Type               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | chaîne             | Identificateur unique d’un modèle de contrat.                                       |
| type          | chaîne             | Type de contrat. Actuellement, les valeurs prises en charge sont **MicrosoftCloudAgreement** et **MicrosoftCustomerAgreement** (version préliminaire). |
| agreementLink | chaîne             | URL du modèle d’accord.                                                    |

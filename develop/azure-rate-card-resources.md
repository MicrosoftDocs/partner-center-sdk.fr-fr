---
title: Ressources de la carte de tarifs Azure
description: La carte de tarifs Azure fournit des tarifs en temps réel pour les offres Azure.
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: amitravat
ms.author: amrava
ms.openlocfilehash: d3bc9b6e93bfbfbf49b1c900c9ace15cd586864d
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022776"
---
# <a name="azure-rate-card-resources"></a>Ressources de la carte de tarifs Azure

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La carte de tarifs Azure fournit des tarifs en temps réel pour les offres Azure. La tarification Azure est assez dynamique et elle change fréquemment. Microsoft publie des mises à jour sur l’espace partenaires, mais l’API REST offre aux partenaires du fournisseur de solutions Cloud le moyen le plus rapide d’obtenir les prix actuels.

Pour suivre l’utilisation et aider à prédire votre facture mensuelle et les factures des clients individuels, vous pouvez combiner une requête de carte à tarif pour [obtenir les prix de Microsoft Azure](get-prices-for-microsoft-azure.md) avec une demande d' [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md).

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, l’API utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, et ces paramètres sont personnalisables. La sensibilisation à l’emplacement est particulièrement pertinente si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé.

## <a name="azureratecard"></a>AzureRateCard

Décrit les propriétés d’une ressource de carte de tarifs Azure.

| Propriété      | Type                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | string                                    | Devise dans laquelle les tarifs sont fournis.                     |
| isTaxIncluded | boolean                                   | Tous les tarifs étant tarif, cette propriété retourne la valeur `false` . |
| locale        | string                                    | Culture dans laquelle les informations sur les ressources sont localisées.       |
| compteurs        | tableau d’objets                          | Tableau d’objets [AzureMeter](#azuremeter) .                       |
| offerTerms    | tableau d’objets                          | Tableau d’objets [AzureOfferTerm](#azureofferterm) .               |
| attributs    | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Comprend`"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Opérations sur la ressource AzureRateCard

- [Obtenir les prix de Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Propriété         | Type             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | string           | Identificateur unique du compteur.                                                                    |
| name             | string           | Nom convivial du compteur.                                                                   |
| tarifs            | object           | Taux de mesure. La clé est la quantité de compteur (chaîne) et la valeur est la fréquence du compteur (nombre). |
| tags             | tableau de chaînes | Balises de compteur facultatives. Ce tableau peut être vide.                                                 |
| catégorie         | string           | Catégorie de la ressource.                                                                     |
| sous-catégorie      | string           | Sous-catégorie de la ressource.                                                                 |
| region           | string           | Région de l’ID.                                                                             |
| unité             | string           | Type de quantité (heures, octets, etc.)                                                     |
| includedQuantity | nombre           | Nombre de compteurs inclus gratuitement.                                               |
| effectiveDate    | string           | Date à laquelle ce compteur est appliqué.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Propriété         | Type             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | string           | Nom convivial du terme de l’offre.        |
| discount         | nombre           | Remise appliquée, le cas échéant.           |
| excludedMeterIds | tableau de chaînes | Compteurs exclus de l’offre, le cas échéant. |
| effectiveDate    | string           | Date d’effet de l’offre.        |

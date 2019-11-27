---
title: Ressources de la carte de tarifs Azure
description: La carte de tarifs Azure fournit des tarifs en temps réel pour les offres Azure.
ms.assetid: A42B4FFA-278E-41FF-B51E-E48C2CA70EEF
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e81debb15c30ba024d897a00075bffe28be3acaf
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489139"
---
# <a name="azure-rate-card-resources"></a>Ressources de la carte de tarifs Azure

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

La carte de tarifs Azure fournit des tarifs en temps réel pour les offres Azure. La tarification Azure est relativement dynamique et change fréquemment. Microsoft publie des mises à jour sur l’espace partenaires, mais l’API REST offre aux partenaires du fournisseur de solutions Cloud le moyen le plus rapide d’obtenir les prix actuels.

Pour suivre l’utilisation et aider à prédire votre facture mensuelle et les factures des clients individuels, vous pouvez combiner une requête de carte à tarif pour [obtenir les prix de Microsoft Azure](get-prices-for-microsoft-azure.md) avec une demande d' [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md).

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, il utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, mais ceux-ci sont personnalisables. Cela s’avère particulièrement utile si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé.

## <a name="azureratecard"></a>AzureRateCard

Décrit les propriétés d’une ressource de carte de tarifs Azure.

| Propriété      | Type                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| accès      | chaîne                                    | Devise dans laquelle les tarifs sont fournis.                     |
| isTaxIncluded | booléen                                   | Tous les tarifs étant tarif, ils sont toujours retournés en tant que « false ». |
| paramètres régionaux        | chaîne                                    | Culture dans laquelle les informations sur les ressources sont localisées.       |
| compteurs        | Tableau d’objets                          | Tableau d’objets [AzureMeter](#azuremeter) .                       |
| offerTerms    | Tableau d’objets                          | Tableau d’objets [AzureOfferTerm](#azureofferterm) .               |
| attributs    | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. Contient « objectType » : « AzureRateCard »   |


### <a name="operations-on-the-azureratecard-resource"></a>Opérations sur la ressource AzureRateCard

- [Obtenir des prix pour Microsoft Azure](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Propriété         | Type             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | chaîne           | Identificateur unique du compteur.                                                                    |
| name             | chaîne           | Nom convivial du compteur.                                                                   |
| tarifs            | objet           | Taux de mesure. La clé est la quantité de compteur (chaîne) et la valeur est la fréquence du compteur (nombre). |
| tags             | Tableau de chaînes | Balises de compteur facultatives. Ce tableau peut être vide.                                                 |
| catégorie         | chaîne           | Catégorie de la ressource.                                                                     |
| sous-catégorie      | chaîne           | Sous-catégorie de la ressource.                                                                 |
| région           | chaîne           | Région de l’ID.                                                                             |
| unités             | chaîne           | Type de quantité (heures, octets, etc.)                                                     |
| includedQuantity | nombre           | Nombre de compteurs inclus gratuitement.                                               |
| effectiveDate    | chaîne           | Date à laquelle ce compteur est appliqué.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Propriété         | Type             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | chaîne           | Nom convivial du terme de l’offre.        |
| remises         | nombre           | Remise appliquée, le cas échéant.           |
| excludedMeterIds | Tableau de chaînes | Compteurs exclus de l’offre, le cas échéant. |
| effectiveDate    | chaîne           | Date d’effet de l’offre.        |
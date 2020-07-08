---
title: Ressources de l’enregistrement d’utilisation Azure
description: L’enregistrement d’utilisation Azure contient des détails sur l’utilisation d’une ressource d’abonnement Azure.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094562"
---
# <a name="azure-utilization-record-resources"></a>Ressources de l’enregistrement d’utilisation Azure

**S’applique à :**

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’enregistrement d’utilisation Azure contient des détails sur l’utilisation d’une ressource d’abonnement Azure. Si vous êtes un partenaire de fournisseur de services Cloud qui est propriétaire de la relation de facturation pour les abonnements Azure de vos clients, vous pouvez utiliser cette API REST pour fournir un moyen évolutif d’effectuer le suivi de l’utilisation des abonnements, afin d’envoyer une facture à vos clients à la fin de chaque cycle de facturation.

Pour suivre l’utilisation et aider à prédire votre facture mensuelle et les factures des clients individuels, vous pouvez combiner une requête de carte à tarif pour [obtenir les prix de Microsoft Azure](get-prices-for-microsoft-azure.md) avec une demande d' [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md).

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, l’API utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, et ces paramètres sont personnalisables. La sensibilisation à l’emplacement est particulièrement pertinente si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Décrit les propriétés d’une ressource d’enregistrement d’utilisation Azure.

| Propriété       | Type                                      | Obligatoire | Description                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | Yes      | Début de la plage horaire d’agrégation de l’utilisation. La réponse est regroupée en fonction de la durée de la consommation (lorsque la ressource était réellement utilisée par rapport au moment où elle a été signalée au système de facturation). |
| usageEndTime   | string                                    | Yes      | Fin de la plage horaire d’agrégation de l’utilisation. La réponse est regroupée en fonction de l’heure de la consommation. Autrement dit, lorsque la ressource était réellement utilisée par rapport à quand elle était signalée au système de facturation.   |
| resource       | object                                    | Yes      | Contient un objet [AzureResource](#azureresource) .                                                                                                                                     |
| quantité       | nombre                                    | Oui      | Quantité consommée du [AzureResource.](#azureresource)                                                                                                                           |
| unité           | string                                    | No       | Type de quantité (heures, octets, etc.) Cette propriété est facultative.                                                                                                                     |
| infoFields     | object                                    | Yes      | Paires clé-valeur des détails au niveau de l’instance. Cet objet peut être vide.                                                                                                                    |
| instanceData   | object                                    | Non       | Contient un objet [AzureInstanceData](#azureinstancedata) qui contient des paires clé-valeur de détails au niveau de l’instance. Cette propriété est facultative et ne peut pas être incluse.                  |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Yes      | Attributs de métadonnées. Contient « objectType » : « AzureUtilizationRecord »                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Opérations sur la ressource AzureUtilizationRecord

- [Obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Décrit les propriétés d’une ressource Azure.

| Propriété    | Type   | Obligatoire | Description                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | string | Yes      | Identificateur unique de la ressource Azure. Également appelé resourceID ou GUID de ressource. |
| name        | string | No       | Nom convivial de la ressource consommée. Cette propriété est facultative.            |
| catégorie    | string | No       | Catégorie de la ressource consommée. Cette propriété est facultative.                   |
| sous-catégorie | string | No       | Sous-catégorie de la ressource consommée. Cette propriété est facultative.               |
| region      | string | No       | Région de la ressource consommée. Cette propriété est facultative.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Décrit les propriétés d’une ressource de données d’instance Azure.

| Propriété       | Type             | Obligatoire | Description                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | Yes      | L’ID de ressource Azure complet, qui comprend les groupes de ressources et le nom de l’instance.                   |
| location       | string           | Yes      | Région dans laquelle le service a été exécuté.                                                                               |
| partNumber     | object           | Yes      | Espace de noms unique utilisé pour identifier la ressource pour une utilisation tierce de la place de marché commercial. Cette propriété peut être une chaîne vide. |
| orderNumber    | nombre           | Oui      | Espace de noms unique utilisé pour identifier l’ordre tiers pour la place de marché commercial. Cette propriété peut être une chaîne vide.          |
| tags           | tableau de chaînes | No       | Balises de ressource spécifiées par l’utilisateur. Cette propriété est facultative et ne peut pas être incluse.                            |
| additionalInfo | tableau de chaînes | No       | Données supplémentaires pour une ressource Azure. Cette propriété est facultative et ne peut pas être incluse.                          |
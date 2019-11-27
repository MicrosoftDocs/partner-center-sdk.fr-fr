---
title: Ressources de l’enregistrement d’utilisation Azure
description: L’enregistrement d’utilisation Azure contient des détails sur l’utilisation d’une ressource d’abonnement Azure.
ms.assetid: 4C1EEEB3-DB25-4D61-BFED-C4AB5D3BB5CF
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8874ce3a9dd3c6f8b0745baafd0f6a09fdbeb842
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489129"
---
# <a name="azure-utilization-record-resources"></a>Ressources de l’enregistrement d’utilisation Azure

S’applique à :

- Espace partenaires
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

L’enregistrement d’utilisation Azure contient des détails sur l’utilisation d’une ressource d’abonnement Azure. Si vous êtes un partenaire de fournisseur de services Cloud qui possède la relation de facturation pour les abonnements Azure de vos clients, vous pouvez utiliser cette API REST pour fournir un moyen évolutif de suivre l’utilisation des abonnements afin d’envoyer une facture à vos clients à la fin de chaque cycle de facturation.

Pour suivre l’utilisation et aider à prédire votre facture mensuelle et les factures des clients individuels, vous pouvez combiner une requête de carte à tarif pour [obtenir les prix de Microsoft Azure](get-prices-for-microsoft-azure.md) avec une demande d' [obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md).

Les prix varient selon le marché et la devise, et cette API prend en compte l’emplacement. Par défaut, il utilise vos paramètres de profil de partenaire dans l’espace partenaires et la langue de votre navigateur, mais ceux-ci sont personnalisables. Cela s’avère particulièrement utile si vous gérez les ventes sur plusieurs marchés à partir d’un seul bureau centralisé.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Décrit les propriétés d’une ressource d’enregistrement d’utilisation Azure.

| Propriété       | Type                                      | Obligatoire | Description                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | chaîne                                    | Oui      | Début de la plage horaire d’agrégation de l’utilisation. La réponse est regroupée en fonction de la durée de la consommation (lorsque la ressource était réellement utilisée par rapport au moment où elle a été signalée au système de facturation). |
| usageEndTime   | chaîne                                    | Oui      | Fin de la plage horaire d’agrégation de l’utilisation. La réponse est regroupée en fonction de la durée de la consommation (lorsque la ressource était réellement utilisée par rapport au moment où elle a été signalée au système de facturation).   |
| ressource       | objet                                    | Oui      | Contient un objet [AzureResource](#azureresource) .                                                                                                                                     |
| quantity       | nombre                                    | Oui      | Quantité consommée du [AzureResource.](#azureresource)                                                                                                                           |
| unités           | chaîne                                    | Non       | Type de quantité (heures, octets, etc.) Cette propriété est facultative.                                                                                                                     |
| infoFields     | objet                                    | Oui      | Paires clé-valeur des détails au niveau de l’instance. Cet objet peut être vide.                                                                                                                    |
| instanceData   | objet                                    | Non       | Contient un objet [AzureInstanceData](#azureinstancedata) qui contient des paires clé-valeur de détails au niveau de l’instance. Cette propriété est facultative et ne peut pas être incluse.                  |
| attributs     | [ResourceAttributes](utility-resources.md#resourceattributes) | Oui      | Attributs de métadonnées. Contient « objectType » : « AzureUtilizationRecord »                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Opérations sur la ressource AzureUtilizationRecord

- [Obtenir les enregistrements d’utilisation d’un client pour Azure](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Décrit les propriétés d’une ressource Azure.

| Propriété    | Type   | Obligatoire | Description                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | chaîne | Oui      | Identificateur unique de la ressource Azure. Également appelé resourceID ou GUID de ressource. |
| name        | chaîne | Non       | Nom convivial de la ressource consommée. Cette propriété est facultative.            |
| catégorie    | chaîne | Non       | Catégorie de la ressource consommée. Cette propriété est facultative.                   |
| sous-catégorie | chaîne | Non       | Sous-catégorie de la ressource consommée. Cette propriété est facultative.               |
| région      | chaîne | Non       | Région de la ressource consommée. Cette propriété est facultative.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Décrit les propriétés d’une ressource de données d’instance Azure.

| Propriété       | Type             | Obligatoire | Description                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| URI    | chaîne           | Oui      | L’ID de ressource Azure complet, qui comprend les groupes de ressources et le nom de l’instance.                   |
| location       | chaîne           | Oui      | Région dans laquelle le service a été exécuté.                                                                               |
| partNumber     | objet           | Oui      | Espace de noms unique utilisé pour identifier la ressource pour une utilisation tierce de la place de marché commercial. Il peut s’agir d’une chaîne vide. |
| orderNumber    | nombre           | Oui      | Espace de noms unique utilisé pour identifier la commande tierce pour la place de marché commercial. Il peut s’agir d’une chaîne vide.          |
| tags           | Tableau de chaînes | Non       | Balises de ressource spécifiées par l’utilisateur. Cette propriété est facultative et ne peut pas être incluse.                            |
| AdditionalInfo | Tableau de chaînes | Non       | Données supplémentaires pour une ressource Azure. Cette propriété est facultative et ne peut pas être incluse.                          |
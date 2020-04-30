---
title: Ressources TransferEntity
description: Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c9b891673fb933ae787f8231e36158ed69224a04
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81666618"
---
# <a name="transferentity-resources"></a>Ressources TransferEntity

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Un partenaire crée un transfert lorsqu’un client souhaite que son abonnement au partenaire soit transféré à un autre partenaire.

## <a name="transferentity"></a>TransferEntity

Décrit un transferEntity.

| Propriété              | Type             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | Identificateur transferEntity qui est fourni lors de la création réussie du transferEntity.                               |
| createdTime           | DateTime         | Date à laquelle le transferEntity a été créé, au format date/heure. Appliqué en cas de création réussie du transferEntity.      |
| lastModifiedTime      | DateTime         | Date à laquelle le transferEntity a été mis à jour pour la dernière fois au format date-heure. Appliqué en cas de création réussie du transferEntity. |
| lastModifiedUser      | string           | Utilisateur qui a mis à jour la transferEntity. Appliqué en cas de réussite de la création de transferEntity.                          |
| customerName          | string           | facultatif. Nom du client dont les abonnements sont en cours de transfert.                                              |
| customerTenantId      | string           | ID client au format GUID qui identifie le client. Appliqué en cas de création réussie du transferEntity.         |
| partnertenantid       | string           | Identificateur de partenaire au format GUID qui identifie le partenaire.                                                                   |
| sourcePartnerName     | string           | facultatif. Nom de l’organisation partenaire qui lance le transfert.                                           |
| sourcePartnerTenantId | string           | Un ID de partenaire au format GUID qui identifie le partenaire qui lance le transfert.                                           |
| targetPartnerName     | string           | facultatif. Nom de l’organisation du partenaire à laquelle le transfert est destiné.                                         |
| targetPartnerTenantId | string           | Un ID de partenaire au format GUID qui identifie le partenaire auquel le transfert est destiné.                                  |
| lineItems             | Tableau d’objets | Tableau de ressources [TransferLineItem](#transferlineitem) .                                                   |
| status                | string           | État du transferEntity. Les valeurs possibles sont « active » (peut être supprimée/envoyée) et « Completed » (a déjà été effectué). Appliqué en cas de création réussie du transferEntity.|

## <a name="transferlineitem"></a>TransferLineItem

Représente un élément contenu dans un transferEntity.

| Propriété             | Type                             | Description                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | string                           | Identificateur unique pour un élément de ligne de transfert. Appliqué en cas de création réussie du transferEntity.   |
| subscriptionId       | string                           | Identificateur de l’abonnement.                                                                            |
| quantité             | int                              | Nombre de licences ou d’instances.                                                                    |
| billingCycle         | Object                           | Type de cycle de facturation défini pour la période actuelle.                                                   |
| friendlyName         | string                           | facultatif. Nom convivial de l’élément défini par le partenaire pour aider à lever toute ambiguïté.                   |
| partnerIdOnRecord    | string                           | Partenaire sur l’enregistrement (MPNID) de l’achat qui se produit lorsque le transfert est accepté.                 |
| offerId              | string                           | Identificateur de l’offre.    |
| addonItems           | Liste d’objets **TransferLineItem** | Collection d’éléments de ligne transferEntity pour les modules complémentaires qui seront transférés avec l’abonnement de base en cours de transfert. Appliqué en cas de création réussie du transferEntity.|
| transferError        | string                           | Appliqué après l’acceptation de transferEntity en cas d’erreur.                |
| status               | string           | État de l’LineItem dans transferEntity.|

## <a name="transfersubmitresult"></a>TransferSubmitResult

Représente le résultat d’une acceptation de transfert.

| Propriété          | Type                                                  | Description                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| orders            | Liste d’objets de [commande](order-resources.md#order) .    | Collection de commandes.          |
| transferErrors    | Liste d’objets [TransferError](#transfererror) .      | Collection d’erreurs de transfert. |

## <a name="transfererror"></a>TransferError

Représente une erreur qui se produit lorsqu’un transfert est accepté.

| Propriété          | Type   | Description                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | string | ID du groupe de commandes avec l’erreur. |
| code              | int    | Code d'erreur.                                 |
| description       | string | Description de l'erreur.                   |
| lineItems         | Liste d’objets **TransferLineItem** | Collection d’éléments de ligne transferEntity qui font partie de l’erreur de transfert.|

## <a name="transfererrorcode"></a>TransferErrorCode

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent un type d’erreur de commande.

| Valeur | Position | Description |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | Jeton de partenaire manquant dans le contexte de la requête. |
| InvalidInput | 800002 | Entrée de demande non valide. |
| ServiceException | 800003 | Erreur de service inattendue. |
| InvalidOfferId | 800004 | ID d’offre non valide. |
| CreateOrderError | 800005 | Échec de la création d’une commande. |
| MpnIdNotFound | 800015 | ID MPN introuvable. |
| NotValidIndirectResellerMpnId | 800016 | L’ID MPN n’est pas un revendeur indirect valide. |
| TransferIdNotFound | 900100   | Demande de transfert introuvable.   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | La demande de transfert est déjà en cours.|
| TransferNotAllowedIfStatusIsCompleted | 900102 | La demande de transfert est déjà terminée.|
| TransferCreateOrderError | 900103 | L’ordre de transfert est incorrect.|
| TransferProcessedByAnotherRequest | 900104 | Le transfert est en cours de traitement par une autre demande.|
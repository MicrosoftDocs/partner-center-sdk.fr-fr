---
title: Ressources de droits
description: Décrit les ressources associées au droit.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc291e4d286e6eeeb1ce4ae6faeb965f59bb1c33
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082856"
---
# <a name="entitlement-resources"></a>Ressources de droits


**S’applique à**

- Centre pour partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government


## <a name="span-identitlementspan-identitlementspan-identitlemententitlement"></a><span id="Entitlement"/><span id="entitlement"/><span id="ENTITLEMENT"/>habilitation


Cette ressource représente les produits que le client a le droit d’utiliser en raison de l’achat d’un partenaire sur les éléments du catalogue. 

| Propriété | Type | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Référence de commande qui a donné le droit. |
| productId | chaîne | ID du produit. |
| skuID | chaîne | ID de la référence (SKU). |
| quantity | int | La quantité de droits (exclut les droits non remplis/transférés). |
| quantityDetails | IEnumerable <[QuantityDetail](#quantitydetail)> | Liste des détails sur la quantité de droits (nombre d’articles et état de chaque quantité). |
| entitlementType | chaîne | Type de droit. (Mis à jour vers la chaîne de [EntitlementType](#entitlementtype) dans le kit de développement logiciel 1,8.) |
| entitledArtifacts | >[artefact](#artifact) IEnumerable < | Liste des artefacts associés au droit. |
| IncludedEntitlements | IEnumerable <[habilitation](#artifact)> | Liste des droits qui sont implicitement inclus à la suite de l’achat ProductId/SkuId à partir du catalogue. |
| ExpiryDate | chaîne au format date-heure UTC  | Date d’expiration du droit (le cas échéant). |


## <a name="span-idreferenceorderspan-idreferenceorderspan-idreferenceorderreferenceorder"></a><span id="ReferenceOrder"/><span id="referenceorder"/><span id="REFERENCEORDER"/>ReferenceOrder

Référence de commande d’un droit. 

| Propriété | Type | Description |
|----------|------|-------------|
| id | chaîne | ID de l’ordre référencé. |
| lineItemId | chaîne | ID de l’élément de ligne de commande référencé. |
| AlternateId | chaîne | Autre ID de l’élément de ligne de commande référencé. |


## <a name="span-idquantitydetailspan-idquantitydetailspan-idquantitydetailquantitydetail"></a><span id="QuantityDetail"/><span id="quantitydetail"/><span id="QUANTITYDETAIL"/>QuantityDetail

Représente les détails d’une quantité de droit.

| Propriété | Type | Description |
|----------|------|-------------|
| quantity | int | Nombre d'éléments. |
| statut | chaîne | État de la quantité. |


## <a name="span-identitlementtypespan-identitlementtypespan-identitlementtypeentitlementtype"></a><span id="EntitlementType"/><span id="entitlementtype"/><span id="ENTITLEMENTTYPE"/>EntitlementType

> [!IMPORTANT]  
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent le type de droit.

| Valeur | Description |
|-------|-------------|
| Logiciels | Indique le type de droit lié au logiciel. |
| VirtualMachineReservedInstance | Indique le type de droit lié à Azure Reserved Virtual Machine Instances. |


## <a name="span-idartifactspan-idartifactspan-idartifactartifact"></a><span id="Artifact"/><span id="artifact"/><span id="ARTIFACT"/>artefact

Artefact associé au droit.  

| Propriété | Type | Description |
|----------|------|-------------|
| artifactType | chaîne | Type d’artefact. (Mis à jour vers la chaîne à partir de [artifactType](#artifacttype) dans le SDK v 1.8) |
| dynamicAttributes | Dictionary&lt;String, Object&gt; | Attributs dynamiques contenant des valeurs spécifiques artifactType. Par exemple, lorsque artifactType = "reservedinstance", cela contient "reservationType" = "VirtualMachines" ou "reservationType" = "sqldatabases" qui dénote l’instance réservée de machine virtuelle ou l’instance réservée SQL Azure. (Disponible à partir du SDK v 1.9) |


## <a name="span-idartifacttypespan-idartifacttypespan-idartifacttypeartifacttype"></a><span id="ArtifactType"/><span id="artifacttype"/><span id="ARTIFACTTYPE"/>ArtifactType

> [!IMPORTANT]  
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

[Énumération](https://docs.microsoft.com/dotnet/api/system.enum) avec des valeurs qui indiquent le type d’artefact d’habilitation.

| Valeur                          | Description                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Indique que l’artefact facilite la récupération de Azure Reserved Virtual Machine Instances. |


## <a name="span-idreservedinstanceartifactspan-idreservedinstanceartifactspan-idreservedinstanceartifactreservedinstanceartifact"></a><span id="ReservedInstanceArtifact"/><span id="reservedinstanceartifact"/><span id="RESERVEDINSTANCEARTIFACT"/>ReservedInstanceArtifact

Artefact associé à un droit d’instance réservée Azure. Elle hérite de la classe d' [artefact](#artifact) . 

| Propriété   | Type                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| lien       | [Lien](./utility-resources.md#link) | Lien permettant d’accéder à tous les détails d’artefact associés.   |
| IDRessource | chaîne                         | ID de la ressource ou de l’ordre de réservation Azure. |


## <a name="span-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsreservedinstanceartifactdetails"></a><span id="ReservedInstanceArtifactDetails"/><span id="reservedinstanceartifactdetails"/><span id="RESERVEDINSTANCEARTIFACTDETAILS"/>ReservedInstanceArtifactDetails

Représente l’entité retournée lors de l’appel du lien d’artefact d’instance réservée Azure. 


|   Propriété   |           Type           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          chaîne          |                     Type d’artefact.                     |
| effectuées | <Reservation> IEnumerable | Indique l’identifiant de la ressource ou de l’ordre de réservation Azure. |

## <a name="span-idreservationspan-idreservationspan-idreservationreservation"></a><span id="Reservation"/><span id="reservation"/><span id="RESERVATION"/>réservation

Représente une réservation individuelle.

| Propriété          | Type                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | chaîne                         | ID de la réservation.                                         |
| scopeType         | chaîne                         | Type d’étendue associé à la réservation d’ordinateur virtuel. |
| displayName       | chaîne                         | Nom complet de la réservation.                               |
| appliedScopes     | IEnumerable                    | Liste des étendues appliquées associées à la réservation. (Disponible uniquement quand scopeType n’est pas partagé.) |
| quantity          | int                            | Nombre de machines virtuelles dans la réservation.                 |
| expiryDateTime    | chaîne au format date-heure UTC | Date d’expiration de la réservation.                                |
| effectiveDateTime | chaîne au format date-heure UTC | Date d’effet de la réservation.                             |
| provisioningState | chaîne                         | État d’approvisionnement de la réservation.                         |


## <a name="span-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedartifactvirtualmachinereservedinstanceartifact"></a><span id="VirtualMachineReservedInstanceArtifact"/><span id="virtualmachinereservedinstanceartifact"/><span id="VIRTUALMACHINERESERVEDARTIFACT"/>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]  
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Artefact associé à une instance de machine virtuelle réservée Azure. Elle hérite de la classe d' [artefact](#artifact) .  

| Propriété   | Type                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| lien       | [Lien](utility-resources.md#link) | Lien permettant d’accéder à tous les détails d’artefact associés.   |
| IDRessource | chaîne                            | ID de la ressource ou de l’ordre de réservation Azure. |


## <a name="span-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedartifactdetailsvirtualmachinereservedinstanceartifactdetails"></a><span id="VirtualMachineReservedInstanceArtifactDetails"/><span id="virtualmachinereservedinstanceartifactdetails"/><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"/>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]  
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Représente l’entité retournée lors de l’appel du lien d’artefact d’instance de machine virtuelle réservée Azure.  

| Propriété                    | Type                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | Type d’artefact. |
| virtualMachineReservations  | IEnumerable <[VirtualMachineReservation](#virtualmachinereservation)> | Indique l’identifiant de la ressource ou de l’ordre de réservation Azure. |


## <a name="span-idvirtualmachinereservationspan-idvirtualmachinereservationspan-idvirtualmachinereservationvirtualmachinereservation"></a><span id="VirtualMachineReservation"/><span id="virtualmachinereservation"/><span id="VIRTUALMACHINERESERVATION"/>VirtualMachineReservation

> [!IMPORTANT]  
> Déconseillé dans le kit de développement logiciel (SDK) v 1.9

Représente une réservation d’ordinateur virtuel individuelle.


|     Propriété      |              Type              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             chaîne             |                                         ID de la réservation.                                         |
|     scopeType     |             chaîne             |                     Type d’étendue associé à la réservation d’ordinateur virtuel.                     |
|    displayName    |             chaîne             |                                    Nom complet de la réservation.                                    |
|   appliedScopes   |      <string> IEnumerable       | Liste des étendues appliquées associées à la réservation. (Disponible uniquement quand scopeType n’est pas partagé.) |
|     quantity      |              int               |                             Nombre de machines virtuelles dans la réservation.                             |
|  expiryDateTime   | chaîne au format date-heure UTC |                                    Date d’expiration de la réservation.                                     |
| effectiveDateTime | chaîne au format date-heure UTC |                                   Date d’effet de la réservation.                                   |
| provisioningState |             chaîne             |                                 État d’approvisionnement de la réservation.                                 |


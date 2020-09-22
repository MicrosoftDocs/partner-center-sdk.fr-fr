---
title: Notes de publication du kit de développement logiciel (SDK) .NET Partner Center
description: Notes de publication de la dernière version du kit de développement logiciel (SDK) .NET de l’espace partenaires.
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 082364100a922cd12e93d36c378435c2ef283842
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927314"
---
# <a name="net-sdk-release-notes"></a>Notes de publication du SDK .NET

Les notes de publication suivantes sont disponibles pour les nouvelles versions du [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). Vous trouverez des [exemples du kit de développement logiciel (SDK) .net](https://github.com/Microsoft/Partner-Center-DotNet-Samples) sur GitHub. Vous trouverez les informations de référence sur l' [API .net de l’espace partenaires](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) dans le navigateur de l’API .net.

## <a name="version-1162"></a>Version 1.16.2

Le [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 est désormais disponible. Des [exemples GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) mis à jour sont également disponibles. Les modifications suivantes sont incluses dans cette version :

* Met à jour les types d’opération pris en charge pour l’enregistrement d’audit. Les nouveaux éléments ajoutés sont les suivants :
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* La création de la demande de service est maintenant dépréciée
* Les rubriques de support sont désormais déconseillées


## <a name="version-1161"></a>Version 1.16.1

Le [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 est désormais disponible. Des [exemples GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) mis à jour sont également disponibles. Les modifications suivantes sont incluses dans cette version :

Nous avons migré le kit de développement logiciel (SDK) Microsoft Partner Center existant de .NET Framework vers .NET Standard plateforme 2,0. Le kit de développement logiciel (SDK) sera compatible avec les applications existantes à l’aide de .NET Framework 4.6.1 et versions ultérieures. Le kit de développement logiciel (SDK) prend en charge .NET Core 2,0 et versions ultérieures. Vérifiez la [prise en charge de l’implémentation .net](/dotnet/standard/net-standard) avant de la porter aux applications existantes.   


## <a name="version-1153"></a>Version 1.15.3
Le [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 est désormais disponible. Des API REST et des [exemples GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) mis à jour sont également disponibles. Les modifications suivantes sont incluses dans cette version :

* Accord de partenariat
  * Ajout de la capacité des fournisseurs indirects à [vérifier l’état de l’accord partenaire Microsoft des revendeurs indirects](verify-indirect-reseller-mpa-status.md).
* Produits
  * Les deux interfaces suivantes ont été placées de manière incorrecte sous l’espace de noms Microsoft. Store. PartnerCenter. Products. À présent, ils se trouvent sous l’espace de noms Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope

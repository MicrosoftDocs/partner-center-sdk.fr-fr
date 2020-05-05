---
title: Notes de publication du kit de développement logiciel (SDK) .NET Partner Center
description: Notes de publication de la dernière version du kit de développement logiciel (SDK) .NET de l’espace partenaires.
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e11e5d6f7f2372b3230d8ac26e02d00b2b554edc
ms.sourcegitcommit: 506c69986f3d1ea650c935c42880048d6c4241f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82784704"
---
# <a name="net-sdk-release-notes"></a>Notes de publication du SDK .NET

Les notes de publication suivantes sont disponibles pour les nouvelles versions du [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). Vous trouverez des [exemples du kit de développement logiciel (SDK) .net](https://github.com/Microsoft/Partner-Center-DotNet-Samples) sur GitHub. Vous trouverez les informations de référence sur l' [API .net de l’espace partenaires](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest) dans le navigateur de l’API .net.

## <a name="version-1153"></a>Version 1.15.3

Le [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.3 est désormais disponible. Des API REST et des [exemples GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) mis à jour sont également disponibles. Les modifications suivantes sont incluses dans cette version :

* Accord de partenariat
  * Ajout de la capacité des fournisseurs indirects à [vérifier l’état de l’accord partenaire Microsoft des revendeurs indirects](verify-indirect-reseller-mpa-status.md).
* Products
  * Les deux interfaces suivantes ont été placées de manière incorrecte sous l’espace de noms Microsoft. Store. PartnerCenter. Products. À présent, ils se trouvent sous l’espace de noms Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope

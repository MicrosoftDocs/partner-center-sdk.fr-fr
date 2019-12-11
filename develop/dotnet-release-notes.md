---
title: Notes de publication du kit de développement logiciel (SDK) .NET Partner Center
description: Notes de publication de la dernière version du kit de développement logiciel (SDK) .NET de l’espace partenaires.
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b98c6ef23b08947a7dec219ba40b7e19a3e5026
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995616"
---
# <a name="net-sdk-release-notes"></a>Notes de publication du SDK .NET

Les notes de publication suivantes sont disponibles pour les nouvelles versions du [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter). Vous trouverez des [exemples du kit de développement logiciel (SDK) .net](https://github.com/Microsoft/Partner-Center-DotNet-Samples) sur GitHub. Vous trouverez les informations de référence sur l' [API .net de l’espace partenaires](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest) dans le navigateur de l’API .net.

## <a name="version-1152"></a>Version 1.15.2

Le [Kit de développement logiciel (SDK) .net pour Microsoft Partner Center](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.2 est désormais disponible. Des API REST et des [exemples GitHub](https://github.com/Microsoft/Partner-Center-DotNet-Samples) mis à jour sont également disponibles. Les modifications suivantes sont incluses dans cette version :

* Accord de partenariat
  * Ajout de la capacité des fournisseurs indirects à [vérifier l’état de l’accord partenaire Microsoft des revendeurs indirects](verify-indirect-reseller-mpa-status.md).
* Produits
  * Les deux interfaces suivantes ont été placées de manière incorrecte sous l’espace de noms Microsoft. Store. PartnerCenter. Products. À présent, ils se trouvent sous l’espace de noms Microsoft. Store. PartnerCenter. Customers. Products.
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope

---
title: Managed service resources
description: Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 32cc11190425c2cdfdbf6c793ef75091915e5d69
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486899"
---
# <a name="managed-service-resources"></a>Managed service resources


**Applies To**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


Describes a managed service.

| Propriété   | Tapez                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | chaîne              | The managed service id.                                  |
| Nom       | chaîne              | The name of the managed service.                         |
| GroupName  | chaîne              | The name of the group to which the service belongs.      |
| Liens      | ManagedServiceLinks | The resource links corresponding to the managed service. |
| Attributs | ResourceAttributes  | The metadata attributes corresponding to the agreement.  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


Contains the links that allow the partner with delegated admin permissions to provide support for the service.

| Propriété      | Tapez | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Lier | The admin service URI.      |
| ServiceHealth | Lier | The service health URI.     |
| ServiceTicket | Lier | The service ticket URI.     |
| Self (Auto)          | Lier | The self URI.               |
| Suivant          | Lier | The next page of items.     |
| Previous      | Lier | The previous page of items. |

 

 

 





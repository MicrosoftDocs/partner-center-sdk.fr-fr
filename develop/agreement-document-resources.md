---
title: Agreement document resources
description: The AgreementDocument resource represents an agreement document.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ac079822a2ddb45310148c16101fa25a38ec492
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488929"
---
# <a name="agreement-document-resources"></a>Agreement document resources

S'applique à :

- Espace partenaires

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource not applicable to:

- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.

## <a name="agreementdocument"></a>AgreementDocument

An **AgreementDocument** resource includes the following properties:

| Propriété       | Tapez   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | chaîne | The country or market to which this document applies. |
| language | chaîne | The language in which this document is localized. |
| displayUri | chaîne | A link to preview the agreement document in a browser.  |
| downloadUri |chaîne | A link to download the agreement document (in Microsoft Word format). |

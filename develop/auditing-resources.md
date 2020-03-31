---
title: Audit des ressources
description: Ressources utilisées avec les opérations d’audit de l’espace partenaires.
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 719ddd1b2e5003842ea85e0f4710c2cf01970564
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413653"
---
# <a name="auditing-resources"></a>Audit des ressources

S'applique à :

- Centre pour partenaires

Vous pouvez utiliser les ressources suivantes avec des opérations d’audit.

## <a name="auditrecord"></a>AuditRecord

Représente un enregistrement d’une opération effectuée par un utilisateur partenaire ou une application.

| Propriété | Type | Description |
| --- | --- | ---|
| customerId | chaîne | Chaîne au format GUID qui identifie le client. |
| customerName | chaîne | Nom du client. |
| userPrincipalName | chaîne | Nom d’utilisateur principal ou identificateur d’utilisateur. En règle générale, il s’agit d’un nom de connexion de style Internet pour un utilisateur dans un format d’adresse de messagerie basé sur Internet standard RFC 822. |
| applicationId | chaîne | Chaîne qui identifie l’application qui a effectué l’opération. |
| resourceType | chaîne | Type de ressource traité par l’opération. Les valeurs possibles sont les suivantes : &quot;Customer&quot;, &quot;customer_user&quot;, &quot;Order&quot;, &quot;subscription&quot;, &quot;&quot;&quot;, third_party_add_on&quot;&quot;, mpn_association&quot;&quot;,&quot;&quot;&quot;, &quot;application_credential&quot;.&quot;&quot;&quot;&quot; |
| resourceOldValue | chaîne | Ancienne valeur de la ressource. |
| resourceNewValue | chaîne | Nouvelle valeur de la ressource. |
| operationType | chaîne | Type d’opération effectuée. Valeurs possibles : &quot;update_customer_qualification&quot;, &quot;update_subscription&quot;, &quot;upgrade_subscription&quot;, &quot;convert_trial_subscription&quot;&quot;add_customer&quot;&quot;update_customer_billing_profile&quot;(comptes d’intégration sandbox) &quot;update_customer_partner_contract_company_name&quot;&quot;update_customer_spending_budget uniquement), &quot;remove_partner_customer_relationship&quot;, &quot;create_order&quot;, &quot;update_order&quot;, &quot;create_customer_user&quot;, &quot;delete_customer_user&quot;, &quot;update_customer_user&quot;, &quot;update_customer_user_licenses&quot;, &quot;reset_customer_user_password&quot;, &quot;update_customer_user_principal_name&quot;, &quot;restore_customer_user&quot;, &quot;create_mpn_association&quot;, &quot;update_mpn_association&quot;, &quot;update_sfb_customer_user_licenses&quot;, &quot;update_transfer&quot;, &quot;create_partner_relationship&quot;, &quot;register_application&quot;, &quot;unregister_application&quot;, &quot;add_application_credential&quot;, &quot;remove_application_credential&quot;, &quot;create_partner_user&quot;, @no_ _t_58_ update_partner_user&quot;, &quot;remove_partner_user&quot;.&quot;&quot;&quot;&quot; |
| operationDate | chaîne au format date-heure UTC | Date et heure auxquelles l’opération a été effectuée. |
| operationStatus | chaîne | État de l’opération en cours d’audit. Valeurs possibles : &quot;réussie&quot;, &quot;&quot;en échec ou &quot;progression&quot;, ce qui signifie que l’opération est toujours en cours. |
| customizedData  | Tableau d’objets | Informations supplémentaires. Chaque objet contient deux paires clé-valeur JSON : la première est &quot;clé&quot; et une valeur de chaîne, la deuxième est &quot;valeur&quot; et une valeur de chaîne. Le nombre d’objets dans le tableau dépend du type d’opération qui a été effectuée. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |
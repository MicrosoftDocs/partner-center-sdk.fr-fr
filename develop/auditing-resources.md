---
title: Audit des ressources
description: Ressources utilisées avec les opérations d’audit de l’espace partenaires.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5a9cb01af9d0ea027ed55716515dcbad251dacdb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095388"
---
# <a name="auditing-resources"></a>Audit des ressources

**S’applique à :**

- Espace partenaires

Vous pouvez utiliser les ressources suivantes avec des opérations d’audit.

## <a name="auditrecord"></a>AuditRecord

Représente un enregistrement d’une opération effectuée par un utilisateur partenaire ou une application.

| Propriété | Type | Description |
| --- | --- | ---|
| customerId | string | Chaîne au format GUID qui identifie le client. |
| customerName | string | Nom du client. |
| userPrincipalName | string | Nom d’utilisateur principal ou identificateur d’utilisateur. En général, cette propriété est un nom de connexion de style Internet pour un utilisateur dans un format d’adresse de messagerie basé sur Internet standard RFC 822. |
| applicationId | string | Chaîne qui identifie l’application qui a effectué l’opération. |
| resourceType | string | Type de ressource traité par l’opération. Valeurs possibles : `customer` , `customer_user` , `order` , `subscription` , `license` , `third_party_add_on` , `mpn_association` , `transfer` , `application` , `application_credential` , `partner_user` , `partner_relationship` . |
| resourceOldValue | string | Ancienne valeur de la ressource. |
| resourceNewValue | string | Nouvelle valeur de la ressource. |
| operationType | string | Type d’opération effectuée. Valeurs possibles : `update_customer_qualification` , `update_subscription` , `upgrade_subscription` , `convert_trial_subscription` , `add_customer` , `update_customer_billing_profile` , `update_customer_partner_contract_company_name` , `update_customer_spending_budget` , `delete_customer` (comptes d’intégration Sandbox uniquement),,,,,,, `remove_partner_customer_relationship` `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` , `reset_customer_user_password` , `update_customer_user_principal_name` ,,,,,,,, `restore_customer_user` , `create_mpn_association` , `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `remove_partner_user` ,,,,,,,,,,,,,,,,. |
| operationDate | chaîne au format date-heure UTC | Date et heure d'exécution de l'opération |
| operationStatus | string | État de l’opération en cours d’audit. Valeurs possibles : `succeeded` , `failed` ou `progress` , ce qui signifie que l’opération est toujours en cours. |
| customizedData  | tableau d’objets | Informations supplémentaires. Chaque objet contient deux paires clé-valeur JSON : la première est `key` et une valeur de chaîne, la deuxième est `value` et une valeur de chaîne. Le nombre d’objets dans le tableau dépend du type d’opération qui a été effectuée. |
| attributs | [ResourceAttributes](utility-resources.md#resourceattributes) | Attributs de métadonnées. |

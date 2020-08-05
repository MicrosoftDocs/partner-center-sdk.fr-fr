---
title: Tester et déboguer
description: Pour tester votre code, vous devez utiliser votre compte de bac à sable (sandbox) d’intégration dans l’espace partenaires (et les jetons correspondants) afin de ne pas occasionner accidentellement de nouveaux frais que votre entreprise est responsable du paiement.
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ad5ee9e6e7045ecb9eb7e295bc4ec03737fdfe0a
ms.sourcegitcommit: 57620e249e218edc4af7c83c2ce8a3008a4adf4e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557340"
---
# <a name="test-and-debug"></a>Tester et déboguer

**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Pour tester votre code, vous devez utiliser votre compte de bac à sable (sandbox) d’intégration dans l’espace partenaires (et les jetons correspondants) afin de ne pas occasionner accidentellement de nouveaux frais que votre entreprise est responsable du paiement. Pour plus d’informations sur cet environnement de test en production (TiP), consultez [configurer l’accès aux API dans l’espace partenaires](set-up-api-access-in-partner-center.md).

## <a name="integration-sandbox-constraints"></a>Contraintes du bac à sable d’intégration

Si vous exécutez des tests de vérification de build automatisés, effectuez des tests en production ou effectuez des tests manuels dans le bac à sable d’intégration, vous pouvez atteindre les limites maximales du bac à sable d’intégration. Ces limites sont 75 clients, 5 abonnements par client et 25 licences par abonnement.

- La limite de 25 licences signifie que vous ne pouvez pas acquérir une offre dans le bac à sable (sandbox) dont la licence minimale est supérieure à 25 licences. Cette limitation comprend des versions d’évaluation.

- Le résumé de l’utilisation ne peut pas être obtenu sur les comptes sandbox, car ces comptes sont à des fins de test.

- Les API liées à la facturation et à la facturation ne fonctionneront pas dans le bac à sable (sandbox), car aucune facture n’est générée pour le compte de test.


### <a name="azure-plan"></a>Plan Azure

Par défaut, les partenaires ne peuvent pas approvisionner des plans Azure à l’aide de leurs comptes sandbox. Les partenaires qui doivent le faire avec leur compte sandbox doivent s’appliquer à l’accès. Pour demander l’accès, contactez votre responsable de compte Microsoft ou votre contact professionnel. Les partenaires qui ont précédemment demandé l’accès aux abonnements Microsoft Azure (MS-AZR-0145P) dans leurs comptes sandbox n’ont pas besoin de s’appliquer à nouveau à l’accès. Ils se voient accorder l’accès pour approvisionner les plans Azure automatiquement.

Pour les partenaires dont les comptes bac à sable (sandbox) ont été approuvés pour approvisionner des plans Azure, les limites suivantes s’appliquent :

- Chaque compte de partenaire bac à sable peut avoir jusqu’à 10 plans Azure sur tous les locataires clients (quelle que soit la façon dont les plans sont répartis entre les clients).

- Un partenaire de facturation directe peut créer jusqu’à un seul plan Azure par locataire client.

- Un fournisseur indirect peut créer jusqu’à trois plans Azure par locataire client (pour différents revendeurs indirects spécifiés comme étant le partenaire d’enregistrement).

- Chaque plan Azure peut avoir jusqu’à trois abonnements Azure.

- Chaque abonnement Azure CSP sous votre compte de bac à sable (sandbox) est limité à quatre cœurs de machines virtuelles par centre de données. Par conséquent, vous ne pouvez pas approvisionner des références de machine virtuelle qui nécessitent plus de quatre cœurs de machine virtuelle. Certaines références (SKU) de machine virtuelle, telles que les cœurs de GPU, sont également exclues.

- Chaque compte de partenaire bac à sable (sandbox) a une limite de dépense de $2000 USD par cycle de facturation pour tous les plans Azure. Une fois qu’un partenaire atteint la limite de dépense, tous les plans Azure sont temporairement désactivés jusqu’au prochain cycle de facturation.

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>Offres d’abonnement Azure du fournisseur de solutions Cloud (CSP)

Les offres d’abonnement Azure CSP ne sont plus disponibles par défaut pour les comptes sandbox. Celles-ci incluent MS-AZR-0146P, MS-AZR-DE-0146P et MS-AZR-gouvernement américain-0146P pour les abonnements Azure CSP dans le cloud public Microsoft, le Cloud allemand et le Cloud Government. Les partenaires ayant besoin d’accéder à ces offres avec leur compte de bac à sable doivent demander un accès. Pour demander l’accès, discutez avec votre responsable de compte Microsoft ou votre contact professionnel.

Pour les partenaires dont les comptes bac à sable (sandbox) ont été approuvés pour les offres d’abonnement Azure CSP, les limites suivantes s’appliquent :

- Vous pouvez disposer d’un maximum de 375 abonnements actifs (75 clients x 5 abonnements par client). Toutefois, seuls 10 peuvent être des abonnements Azure CSP.

- Lorsqu’un abonnement Azure CSP atteint $200 de l’utilisation d’Azure, ses ressources sont temporairement désactivées jusqu’au prochain cycle de facturation. Il est toujours considéré comme un abonnement actif et est compté dans la limite de 10 abonnements Azure actifs.

- Chaque abonnement Azure CSP sous votre compte de bac à sable (sandbox) est limité à quatre cœurs de machines virtuelles par centre de données. Par conséquent, vous ne pouvez pas approvisionner des références de machine virtuelle qui nécessitent plus de quatre cœurs de machine virtuelle. Certaines références (SKU) de machine virtuelle, telles que les cœurs de GPU, sont également exclues.

> [!Important]
> Tous les abonnements Azure CSP existants approvisionnés avec des comptes sandbox antérieurs au 1er août 2018 ne sont plus pris en charge et seront annulés par Microsoft entre le 16 octobre au 31 octobre 2018. Une fois les abonnements arrêtés, ils ne peuvent pas être réactivés et les données associées ne sont plus accessibles. Les partenaires possédant des données importantes stockées dans ces abonnements doivent sauvegarder des données avant le 16 octobre 2018.

### <a name="azure-reserved-vm-instance"></a>Instance de machine virtuelle réservée Azure

Si vous [achetez une instance de machine virtuelle réservée Azure](purchase-azure-reservations.md) avec votre compte sandbox, vous êtes limité à deux instances de machine virtuelle par client. Vous êtes également limité à la sélection des références SKU de produit de l’instance de machine virtuelle réservée Azure suivantes :

| Titre du produit  | Date d'effet  | Titre de la référence                                               | Région [ArmRegionName] | Clé d’instance [ArmSkuName] | Duration | ID du compteur de consommation       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| Série B       | 12/1/2017 0:00  | Instance de machine virtuelle réservée, Standard_B1s, sud du KR, 1 an    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| Série B       | 12/1/2017 0:00  | Instance de machine virtuelle réservée, Standard_B1s, est des États-Unis, 1 an     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| Série B       | 12/1/2017 0:00  | Instance de machine virtuelle réservée, Standard_B1s, ouest des États-Unis 2, 1 an   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| Série B       | 12/1/2017 0:00  | Instance de machine virtuelle réservée, Standard_B1s, nord du Centre des États-Unis, 1 an    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| Série B       | 12/1/2017 0:00  | Instance de machine virtuelle réservée, Standard_B1s, est de l’autorité de certification, 1 an     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>Abonnements pour les produits de la place de marché commercial

En production, après avoir [créé un abonnement aux produits Saas de la place de marché commercial](create-subscription-azure-marketplace-products.md), vous devez récupérer un lien d’activation personnalisé auprès de l’espace partenaires et visiter le site de l’éditeur pour terminer le processus d’installation. La facturation de l’abonnement commence uniquement une fois l’installation terminée.

Dans l’environnement du bac à sable (sandbox) CSP, il n’existe aucune intégration avec les éditeurs de logiciels indépendants. Si vous essayez de récupérer un lien d’activation à partir de l’espace partenaires, un lien factice est renvoyé. Vous ne pouvez pas utiliser ce lien factice pour terminer le processus d’installation sur le site de l’éditeur. Pour utiliser le compte de bac à sable (sandbox) d’intégration pour tester la facturation des abonnements aux produits SaaS de la place de marché commercial, consultez [activer un abonnement sandbox pour les produits de la place de marché commerciale](activate-sandbox-subscription-azure-marketplace-products.md) . La facturation de l’abonnement commencera après l’activation réussie.

Pour effectuer un nettoyage à la fin de votre série de tests, il y a de l’espace pour l’essai suivant, consultez les articles suivants :

- [Supprimer un compte client du bac à sable d’intégration](delete-a-customer-account-from-the-integration-sandbox.md)

- [Réduire la quantité d’un abonnement](change-the-quantity-of-a-subscription.md)

- [Suspendez un abonnement](suspend-a-subscription.md) afin de pouvoir le supprimer.

## <a name="best-practices-for-rest-development"></a>Meilleures pratiques pour le développement REST

- Utilisez un outil de trace réseau pour voir votre demande, la réponse et, si le code d’état HTTP comportait des erreurs dans la réponse. Pour plus d’informations sur la gestion des erreurs, consultez [codes d’erreur REST de l’espace partenaires](error-codes.md).

- Utilisez un nouvel ID de corrélation pour chaque appel effectué à l’API REST de l’espace partenaires. Cette pratique garantit une meilleure journalisation et vous aidera lors du débogage. Pour plus d’informations, consultez [En-têtes REST de l’Espace Partenaires](headers.md).

## <a name="troubleshooting-tips-for-common-rest-problems"></a>Conseils de résolution des problèmes REST courants

- Examinez toutes les propriétés d’en-tête, y compris l’URL et la version de l’API.

- Vérifiez que les propriétés sont incluses si nécessaire et correctement mises en forme.

- Une mise en forme de tableau incorrecte est une erreur courante.

- Les **ETags** sont temporaires et, par conséquent, ne doivent pas être stockés. Quand un appel de fonction requiert des **ETags**, utilisez la dernière valeur **ETags** en obtenant à nouveau la ressource. Les valeurs des **ETags** doivent être comprises entre guillemets doubles, comme une chaîne :

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```

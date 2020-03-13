---
title: Scénarios
description: Cette section décrit les manières dont les partenaires du programme Fournisseur de solutions Cloud peuvent utiliser l’API de l’Espace partenaires pour gérer programmatiquement les comptes client, les comptes partenaire, les commandes, les abonnements, le support et la facturation.
ms.assetid: D278B9D1-D5B9-4FAD-89D8-44244715D6C9
ms.date: 02/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: a6eef30501fc3e6b4cf018bfeaf84a7a92c2caaf
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899946"
---
# <a name="scenarios"></a>Scénarios

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette section décrit les manières dont les partenaires du programme Fournisseur de solutions Cloud peuvent utiliser l’API de l’Espace partenaires pour gérer programmatiquement les comptes client, les comptes partenaire, les commandes, les abonnements, le support et la facturation.

Notez qu’il existe différentes versions de l’Espace partenaires disponibles qui incluent des fonctionnalités différentes. Tous les scénarios ne sont pas pris en charge dans toutes les versions de l’Espace partenaires. Pour en savoir plus, consultez [Développement de l’Espace partenaires pour les clouds nationaux Microsoft](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Scénarios pris en charge par le SDK de l’Espace Partenaires

Tous les scénarios suivants peuvent être suivis de trois façons différentes :

- Manuellement avec le tableau de bord de l’[Espace partenaires](https://go.microsoft.com/fwlink/p/?LinkId=620294).
- Programmatiquement avec l’API gérée de l’Espace partenaires.
- Programmatiquement avec l’API REST de l’Espace partenaires.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p><a href="usage-analytics.md">Analytique</a></p></td>
<td><p>Récupérer l’analytique</p>
<ul>
<li><p><a href="partner-center-analytics-resources.md">Analytique de l’Espace partenaires - Ressources</a></p></li>
<li><p><a href="get-all-azure-usage-analytics.md">Obtenir toutes les informations analytiques sur l’utilisation d’Azure</a></p></li>
<li><p><a href="get-all-indirect-resellers-analytics.md">Obtenir toutes les informations analytiques sur les revendeurs indirects</a></p></li>
<li><p><a href="get-all-referrals-analytics.md">Obtenir toutes les informations analytiques sur les références</a></p></li>
<li><p><a href="get-all-search-analytics.md">Obtenir toutes les informations analytiques sur la recherche</a></p></li>
<li><p><a href="get-all-subscription-analytics.md">Obtenir toutes les informations analytiques sur l’abonnement</a></p></li>
<li><p><a href="get-subscription-analytics-by-search-query.md">Obtenir des informations analytiques d’abonnement filtrées par une requête de recherche</a></p></li>
<li><p><a href="get-subscription-analytics-grouped-by-dates-or-terms.md">Obtenir des informations analytiques d’abonnement regroupées par dates ou périodes</a></p></li>
<li><p><a href="get-licenses-deployment-information.md">Obtenir des informations sur le déploiement des licences</a></p></li>
<li><p><a href="get-licenses-usage-information.md">Obtenir des informations sur l’utilisation des licences</a></p></li>
<li><p><a href="get-customer-licenses-deployment-information.md">Obtenir des informations sur le déploiement des licences client</a></p></li>
<li><p><a href="get-customer-licenses-usage-information.md">Obtenir des informations sur l’utilisation des licences client</a></p></li>
<li><p><a href="get-partner-licenses-deployment-information.md">Obtenir des informations sur le déploiement des licences partenaire</a></p></li>
<li><p><a href="get-partner-licenses-usage-information.md">Obtenir des informations sur l’utilisation des licences partenaire</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="device-deployment.md">Déploiement d’appareil</a></p></td>
<td><p>Stratégies de configuration</p>
<p>Ajoutez, supprimez, mettez à jour et récupérez des stratégies de configuration d’appareil.</p>
<ul>
<li><p><a href="create-a-new-configuration-policy-for-the-specified-customer.md">Créer une stratégie de configuration pour le client spécifié</a></p></li>
<li><p><a href="delete-a-configuration-policy-for-the-specified-customer.md">Supprimer une stratégie de configuration pour le client spécifié</a></p></li>
<li><p><a href="get-a-list-of-a-customer-s-policies.md">Obtenir la liste des stratégies d’un client</a></p></li>
<li><p><a href="retrieve-a-customer-s-configuration-policy.md">Récupérer la stratégie de configuration d’un client</a></p></li>
<li><p><a href="update-a-configuration-policy-for-the-specified-customer.md">Mettre à jour une stratégie de configuration pour le client spécifié</a></p></li>
</ul>
<p>Périphériques</p>
<p>Utiliser et charger des lots d’appareils et des métadonnées d’appareils.</p>
<ul>
<li><p><a href="get-the-status-of-a-device-batch-upload.md">Obtenir l’état d’un chargement de lot d’appareils</a></p></li>
<li><p><a href="get-the-list-of-device-batches-for-the-specified-customer.md">Obtenir la liste des lots d’appareils pour le client spécifié</a></p></li>
<li><p><a href="get-a-list-of-devices-for-the-specified-batch-and-customer.md">Obtenir la liste des appareils pour le client et le lot spécifiés</a></p></li>
<li><p><a href="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md">Charger la liste des appareils afin de créer un lot pour le client spécifié</a></p></li>
<li><p><a href="upload-a-list-of-devices-for-the-specified-customer.md">Charger la liste des appareils dans un lot existant pour le client spécifié</a></p></li>
<li><p><a href="delete-a-device-for-the-specified-customer.md">Supprimer un appareil pour le client spécifié</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-profiles-and-information.md">Gérer les comptes et les profils</a></p></td>
<td><p>Utiliser des comptes et des profils</p>
<ul>
<li><p><a href="get-legal-business-profile.md">Obtenir le profil d’entreprise juridique du partenaire</a></p></li>
<li><p><a href="get-an-organization-profile.md">Obtenir un profil d’organisation</a></p></li>
<li><p><a href="get-partner-billing-profile.md">Obtenir le profil de facturation du partenaire</a></p></li>
<li><p><a href="get-partner-network-profile.md">Obtenir le profil Microsoft Partner Network</a></p></li>
<li><p><a href="get-support-profile.md">Obtenir le profil de prise en charge</a></p></li>
<li><p><a href="update-legal-business-profile.md">Mettre à jour le profil d’entreprise juridique du partenaire</a></p></li>
<li><p><a href="update-partner-billing-profile.md">Mettre à jour le profil de facturation du partenaire</a></p></li>
<li><p><a href="update-support-profile.md">Mettre à jour le profil de prise en charge</a></p></li>
<li><p><a href="update-an-organization-profile.md">Mettre à jour un profil d’organisation</a></p></li>
<li><p><a href="get-partner-by-mpn-id.md">Vérifier l’ID MPN d’un partenaire</a></p></li>
<li><p><a href="get-all-subscriptions-by-partner.md">Obtenir les abonnements d’un client par l’ID MPN partenaire</a></p></li>
<li><p><a href="get-customers-of-an-indirect-reseller.md">Obtenir les clients d’un revendeur indirect</a></p></li>
<li><p><a href="get-indirect-resellers-of-a-customer.md">Obtenir les revendeurs indirects d’un client</a></p></li>
<li><p><a href="retrieve-a-list-of-indirect-resellers.md">Récupérer la liste des revendeurs indirects</a></p></li>
</ul></td>
</tr>
<tr>
<td>
<p><a href="manage-billing.md">Gérer la facturation</a></p></td>
<td><p>Cycle de facturation</p>
<ul>
<li><p><a href="change-the-billing-cycle.md">Changer le cycle de facturation</a></p></li>
</ul>
<p>Tarifs Azure et enregistrements de l’utilisation</p>
<ul>
<li><p><a href="get-prices-for-microsoft-azure.md">Obtenir les prix de Microsoft Azure</a></p></li>
<li><p><a href="get-a-customer-s-utilization-record-for-azure.md">Obtenir les enregistrements de l’utilisation d’Azure d’un client</a></p></li>
</ul>
<p>Factures</p>
<ul>
<li><p><a href="get-a-collection-of-invoices.md">Obtenir une collection de factures</a></p></li>
<li><p><a href="get-invoice-estimate-links.md">Obtenir des liens d’estimation de facture</a></p></li>
<li><p><a href="get-invoice-billed-consumption-lineitems.md">Obtenir les éléments de ligne de consommation de la place de marché commerciale facturés</a></p></li>
<li><p><a href="get-invoice-by-id.md">Obtenir une facture par ID</a></p></li>
<li><p><a href="get-invoiceline-items.md">Obtenir des éléments de ligne de facture</a></p></li>
<li><p><a href="get-invoice-receipt-statement.md">Obtenir l’instruction de réception de facture</a></p></li>
<li><p><a href="get-invoice-statement.md">Obtenir l’instruction de facture</a></p></li>
<li><p><a href="get-invoice-summaries.md">Obtenir des récapitulatifs de facture</a></p></li>
<li><p><a href="get-invoice-unbilled-consumption-lineitems.md">Obtenir les éléments de ligne de consommation de la place de marché commerciale non facturés</a></p></li>
<li><p><a href="get-invoice-unbilled-recon-lineitems.md">Obtenir les éléments de ligne de rapprochement non facturés</a></p></li>
<li><p><a href="get-the-reseller-s-current-account-balance.md">Obtenir le solde du compte courant d’un partenaire</a></p></li>
</ul>
<p>Budget des dépenses Azure</p>
<ul>
<li><p><a href="get-all-monthly-usage-records-for-a-subscription.md">Obtenir les données d’utilisation d’un abonnement</a></p></li>
<li><p><a href="get-a-customer-usage-summary.md">Obtenir un récapitulatif d’utilisation pour tous les abonnements d’un client</a></p></li>
</ul>
<p>Coûts de service</p>
<ul>
<li><p><a href="get-a-customer-s-service-costs-summary.md">Obtenir un récapitulatif des coûts de service d’un client</a></p></li>
<li><p><a href="get-a-customer-s-service-costs-line-items.md">Obtenir les éléments de la ligne des coûts de service d’un client</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-customers.md">Gérer des comptes client</a></p></td>
<td><p>Créer un client</p>
<ul>
<li><p><a href="create-a-customer.md">Créer un client</a></p></li>
<li><p><a href="create-a-customer-for-an-indirect-reseller.md">Créer un client pour un revendeur indirect</a></p></li>
<li><p><a href="request-reseller-relationship.md">Récupérer une URL de demande de relation</a></p></li>
<li><p><a href="remove-a-reseller-relationship-with-a-customer.md">Supprimer une relation de revendeur avec un client</a></p></li> 
</ul>
<p>Rechercher un client</p>
<ul>
<li><p><a href="get-a-customer-by-id.md">Obtenir un client par ID</a></p></li>
<li><p><a href="get-a-customer-by-name.md">Obtenir la liste des clients filtrée par un champ de recherche</a></p></li>
<li><p><a href="get-a-list-of-customers.md">Obtenir la liste des clients</a></p></li>
</ul>
<p>Gérer les commandes et les abonnements des clients</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-orders.md">Obtenir toutes les commandes d’un client</a></p></li>
<li><p><a href="get-a-list-of-orders-by-customer-and-billing-cycle-type.md">Obtenir la liste des commandes par client et le type de cycle de facturation</a></p></li>
<li><p><a href="get-a-collection-of-entitlements.md">Obtenir une collection de droits</a></p></li> 
<li><p><a href="get-all-of-a-customer-s-subscriptions.md">Obtenir les abonnements d’un client</a></p></li>
<li><p><a href="update-the-nickname-for-a-subscription.md">Mettre à jour le pseudo d’un abonnement</a></p></li>
</ul>
<p>Gérer les détails d’un compte client</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-billing-profiles.md">Obtenir le profil de facturation d’un client</a></p></li>
<li><p><a href="update-a-customer-s-billing-profile.md">Mettre à jour le profil de facturation d’un client</a></p></li>
<li><p><a href="get-a-customer-s-company-profile.md">Obtenir le profil d’entreprise d’un client</a></p></li>
<li><p><a href="update-a-customer-s-usage-spending-budget.md">Mettre à jour le budget des dépenses d’utilisation d’un client</a></p></li>
<li><p><a href="add-a-verified-domain-for-a-customer.md">Ajouter un domaine vérifié pour un client</a></p></li>
<li><p><a href="confirm-customer-consent-customer-agreement.md">Confirmer que le client a accepté le Contrat client Microsoft</a></p></li>
<li><p><a href="get-agreement-metadata.md">Obtenir les métadonnées de contrat pour le contrat Microsoft Cloud</a></p></li>
<li><p><a href="get-confirmation-of-customer-consent.md">Obtenir une confirmation de l'acceptation du contrat Microsoft Cloud par le client</a></p></li>
<li><p><a href="get-direct-sign-status-of-customer-agreement.md">Obtenir l’état de la signature directe (acceptation directe) du Contrat client Microsoft</a></p></li>
<li><p><a href="get-customer-agreement-metadata.md">Obtenir les métadonnées du Contrat client Microsoft</a></p></li>
<li><p><a href="get-a-partner-s-validation-codes.md">Obtenir les codes de validation d’un partenaire</a></p></li>
<li><p><a href="get-a-customer-s-qualification.md">Obtenir la qualification d’un client</a></p></li>
<li><p><a href="update-a-customer-s-qualification.md">Mettre à jour la qualification d’un client</a></p></li>
</ul>
<p>Gérer les comptes d’utilisateur et attribuer des licences</p>
<ul>
<li><p><a href="get-a-user-account-by-id.md">Obtenir un compte d’utilisateur par ID</a></p></li>
<li><p><a href="create-user-accounts-for-a-customer.md">Créer des comptes d’utilisateur pour un client</a></p></li>
<li><p><a href="delete-user-accounts-for-a-customer.md">Créer un compte d’utilisateur pour un client</a></p></li>
<li><p><a href="update-user-accounts-for-a-customer.md">Mettre à jour des comptes d’utilisateur pour un client</a></p></li>
<li><p><a href="view-a-deleted-user.md">Voir les utilisateurs supprimés d’un client</a></p></li>
<li><p><a href="restore-a-user-for-a-customer.md">Restaurer un utilisateur supprimé pour un client</a></p></li>
<li><p><a href="get-a-list-of-all-user-accounts-for-a-customer.md">Obtenir la liste de tous les comptes d’utilisateur d’un client</a></p></li>
<li><p><a href="reset-user-password-for-a-customer.md">Réinitialiser le mot de passe utilisateur d’un client</a></p></li>
<li><p><a href="get-user-roles-for-a-customer.md">Obtenir les rôles d’utilisateur d’un client</a></p></li>
<li><p><a href="set-user-roles-for-a-customer.md">Définir des rôles d’utilisateur pour un client</a></p></li>
<li><p><a href="remove-customer-user-from-a-role.md">Supprimer un utilisateur client d’un rôle</a></p></li>
<li><p><a href="get-a-list-of-available-licenses.md">Obtenir la liste des licences disponibles</a></p></li>
<li><p><a href="assign-licenses-to-a-user.md">Attribuer des licences à un utilisateur</a></p></li>
<li><p><a href="check-which-licenses-are-assigned-to-a-user.md">Obtenir les licences attribuées à un utilisateur</a></p></li>
<li><p><a href="get-licenses-assigned-to-a-user-by-license-group.md">Obtenir les licences attribuées à un utilisateur par groupe de licences</a></p></li>
<li><p><a href="get-a-list-of-available-licenses-by-license-group.md">Obtenir la liste des licences disponibles par groupe de licences</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-orders.md">Gérer les commandes</a></p></td>
<td><p>Acheter Azure Reserved VM Instances</p>
<ul>
<li><p><a href="purchase-azure-reservations.md">Acheter des réservations Azure</a></p></li>
</ul>
<p>Effectuer un achat ponctuel</p>
<ul>
<li><p><a href="make-a-one-time-purchase.md">Effectuer un achat ponctuel</a></p></li> 
</ul>
<p>Recevoir des offres du catalogue</p>
<ul>
<li><p><a href="get-a-list-of-offer-categories-by-country-and-locale.md">Obtenir la liste des catégories d’offre par marché</a></p></li>
<li><p><a href="get-a-list-of-offers-for-a-market.md">Obtenir la liste des offres d’un marché</a></p></li>
<li><p><a href="get-an-offer-by-id.md">Obtenir une offre par ID</a></p></li>
<li><p><a href="get-addon-offers-by-offer-id.md">Obtenir les extensions d’un ID d’offre</a></p></li>
<li><p><a href="get-a-list-of-products.md">Obtenir la liste des produits</a></p></li>
<li><p><a href="get-a-product-by-id.md">Obtenir un produit par ID</a></p></li>
<li><p><a href="get-a-list-of-skus-for-a-product.md">Obtenir la liste des références SKU d’un produit</a></p></li>
<li><p><a href="get-a-sku-by-id.md">Obtenir la liste des disponibilités d’une référence SKU</a></p></li>
<li><p><a href="get-an-availability-by-id.md">Obtenir une disponibilité par ID</a></p></li>
<li><p><a href="check-inventory.md">Vérifier le stock</a></p></li>
</ul>
<p>Gérer une commande</p>
<ul>
<li><p><a href="cancel-an-order-from-the-integration-sandbox.md">Annuler une commande du bac à sable d’intégration</a></p></li>
<li><p><a href="checkout-a-cart.md">Valider un panier</a></p></li>
<li><p><a href="create-a-cart.md">Créer un panier</a></p></li>
<li><p><a href="create-a-cart-with-add-ons.md">Créer un panier avec des extensions</a></p></li>
<li><p><a href="create-an-order.md">Créer une commande</a></p></li>
<li><p><a href="create-an-order-for-a-customer-of-an-indirect-reseller.md">Créer une commande pour un client d’un revendeur indirect</a></p></li>
<li><p><a href="get-activation-link-by-order-line-item.md">Obtenir un lien d’activation par élément de ligne de commande</a></p></li>
<li><p><a href="get-an-order-by-id.md">Obtenir une commande par ID</a></p></li>
<li><p><a href="purchase-an-add-on-to-a-subscription.md">Acheter une extension d’abonnement</a></p></li>
<li><p><a href="purchase-catalog-items.md">Acheter des éléments de catalogue</a></p></li>
<li><p><a href="update-a-cart.md">Mettre à jour un panier</a></p></li>
</ul>
<p>Activer un abonnement pour les achats Azure Reserved VM Instances</p>
<ul>
<li><p><a href="register-a-subscription.md">Inscrire un abonnement</a></p></li>
<li><p><a href="get-subscription-registration-status.md">Obtenir l’état d’inscription d’un abonnement</a></p></li>
</ul>
<p>Conversions d’essai</p>
<ul>
<li><p><a href="get-a-list-of-trial-conversion-offers.md">Obtenir la liste des offres de conversion d’essai</a></p></li>
<li><p><a href="convert-a-trial-subscription-to-paid.md">Convertir un abonnement d’essai en abonnement payant</a></p></li>
</ul>
<p>Obtenir les détails de l’abonnement</p>
<ul>
<li><p><a href="get-a-subscription-by-id.md">Obtenir un abonnement par ID</a></p></li>
<li><p><a href="get-a-list-of-subscriptions-by-order.md">Obtenir une liste d’abonnements par commande</a></p></li>
<li><p><a href="get-a-list-of-add-ons-for-a-subscription.md">Obtenir la liste des extensions d’un abonnement</a></p></li>
<li><p><a href="get-subscription-provisioning-status.md">Obtenir l’état de provisionnement d’un abonnement</a></p></li>
</ul>
<p>Gérer un abonnement</p>
<ul>
<li><p><a href="change-the-quantity-of-a-subscription.md">Changer la quantité d’un abonnement</a></p></li>
<li><p><a href="update-autorenew-for-an-azure-marketplace-subscription.md">Mettre à jour le renouvellement automatique d’un abonnement de la place de marché commerciale</a></p></li>
<li><p><a href="suspend-a-subscription.md">Suspendre un abonnement</a></p></li>
<li><p><a href="reactivate-a-suspended-a-subscription.md">Réactiver un abonnement suspendu</a></p></li>
<li><p><a href="transition-a-subscription.md">Changer un abonnement</a></p></li>
<li><p><a href="cancel-an-azure-marketplace-subscription.md">Annuler un abonnement de la place de marché commerciale</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="provide-support.md">Fournir un support</a></p></td>
<td><p>Administrer des services pour un client</p>
<ul>
<li><p><a href="get-the-managed-services-for-a-customer-by-id.md">Obtenir les services managés d’un client par ID</a></p></li>
</ul>
<p>Gérer les contacts de support</p>
<ul>
<li><p><a href="get-a-subscription-s-support-contact.md">Obtenir le contact de support d’un abonnement</a></p></li>
<li><p><a href="update-a-subscription-s-support-contact.md">Mettre à jour le contact de support d’un abonnement</a></p></li>
</ul>
<p>Gérer les demandes de service</p>
<ul>
<li><p><a href="create-a-service-request-.md">Créer une demande de service</a></p></li>
<li><p><a href="get-service-request-support-topics--pending-.md">Obtenir les rubriques de support des demandes de service</a></p></li>
<li><p><a href="get-all-service-requests-for-a-customer.md">Obtenir des demandes de service pour un client</a></p></li>
<li><p><a href="get-service-request-details-by-id.md">Obtenir les détails de la demande de service par ID</a></p></li> 
<li><p><a href="update-a-service-request.md">Mettre à jour une demande de service</a></p></li>
</ul></td>
</tr>
<tr>
  <td><p><a href="https://docs.microsoft.com/partner/develop/referrals">Références</a></p></td>
  <td><p>Références</p>
    <ul>
      <li><p><a href="https://docs.microsoft.com/partner/develop/create-a-referral">Créer une référence</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-list-of-referrals">Obtenir la liste de références</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-referral-by-id">Obtenir une référence par ID</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/update-a-referral">Mettre à jour une référence</a></p></li> 
    </ul>
  </td>
</tr>
<tr>
<td><p><a href="utilities.md">Utilitaires</a></p></td>
<td><p>Outils</p>
<ul>
<li><p><a href="validate-an-address.md">Valider une adresse</a></p></li>
<li><p><a href="get-market-specific-validation-data.md">Obtenir les règles de mise en forme des adresses par marché</a></p></li>
<li><p><a href="verify-domain-availability.md">Vérifier la disponibilité du domaine</a></p></li>
<li><p><a href="delete-a-customer-account-from-the-integration-sandbox.md">Supprimer un compte client du bac à sable d’intégration</a></p></li>
<li><p><a href="get-a-record-of-partner-center-activity-by-user.md">Obtenir un enregistrement le l’activité de l’Espace partenaires</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="background"></a>Contexte

### <a name="who-is-involved-in-the-order-process"></a>Qui est impliqué dans le processus de commande ?

Microsoft, distributeurs, revendeurs et clients. Les distributeurs et les revendeurs sont souvent appelés **partenaires**.

Parfois, Microsoft travaille directement avec les revendeurs qui vendent aux clients. Microsoft travaille également avec les distributeurs, et ces derniers travaillent avec leur propre ensemble ou réseau de revendeurs qui vendent aux clients.

### <a name="whats-getting-sold"></a>Que vendent-ils ?

Microsoft fournit la liste des **offres**. Il s’agit de références SKU spécifiques de produits comme Office 365 ou Intune. Les offres sont soit **basées sur une licence** (le coût dépend du nombre de machines sur lesquelles elles sont installées), soit **basées sur l’utilisation** (le coût dépend de la quantité de mémoire et de calcul utilisée). Pour plus d’informations, consultez [Offres pour les partenaires du programme Fournisseur de solutions Cloud](https://docs.microsoft.com/partner-center/csp-offers).

Les partenaires du programme Fournisseur de solutions Cloud sont des revendeurs qui ont des clients auxquels ils vendent des produits Microsoft figurant dans la liste des offres en cours. Une fois que les clients ont signé leur contrat, le revendeur passe une **commande** d’une ou plusieurs offres. Certaines offres incluent des **extensions** comme de l’espace ou des fonctionnalités supplémentaires, suivies dans le cadre de l’offre parente. Les commandes sont traitées, puis le client peut utiliser ses **abonnements**. Microsoft facture le revendeur ou le distributeur chaque mois en fonction du nombre de licences et de l’utilisation de chaque client.

Il est possible d’ajouter des abonnements et le nombre de postes ou d’extensions peut augmenter ou baisser. Si un client n’honore pas un paiement, utilise l’abonnement de manière incorrecte ou illégale, Microsoft, le distributeur ou le revendeur sont tous en mesure de suspendre l’abonnement. Cette suspension est définitive si l’abonnement n’est pas réactivé dans les délais stipulés par le programme Fournisseur de solutions Cloud.

Vous pouvez vérifier quels abonnements un client est **autorisé** à utiliser (par ex., ceux qui ont été payés, qui ne sont pas suspendus ni remplacés par une commande plus récente).

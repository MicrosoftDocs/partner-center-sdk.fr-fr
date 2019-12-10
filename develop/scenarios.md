---
title: Scénarios
description: Cette section décrit les manières dont les partenaires du programme fournisseur de solutions Cloud peuvent utiliser l’API espace partenaires pour gérer par programmation les comptes clients, les comptes de partenaires, les commandes, les abonnements, le support et la facturation.
ms.assetid: D278B9D1-D5B9-4FAD-89D8-44244715D6C9
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e51b6d9893a8755725953a571525377939d270f8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486539"
---
# <a name="scenarios"></a>Scénarios

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette section décrit les manières dont les partenaires du programme fournisseur de solutions Cloud peuvent utiliser l’API espace partenaires pour gérer par programmation les comptes clients, les comptes de partenaires, les commandes, les abonnements, le support et la facturation.

Notez qu’il existe différentes versions de l’espace partenaires disponibles qui incluent des fonctionnalités différentes. Tous les scénarios ne sont pas pris en charge dans toutes les versions de l’espace partenaires. Pour plus d’informations, consultez [développement pour l’espace partenaires pour Microsoft national Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>Scénarios pris en charge par le kit de développement logiciel (SDK) Partner Center

Tous les scénarios suivants peuvent être effectués de trois façons différentes :

- Manuellement dans le tableau de bord [espace partenaires](http://go.microsoft.com/fwlink/p/?LinkId=620294) .
- Par programme, à l’aide de l’API gérée par l’espace partenaires.
- Par programmation à l’aide de l’API REST de l’espace partenaires.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p><a href="usage-analytics.md">Analyses</a></p></td>
<td><p>Récupérer des analyses</p>
<ul>
<li><p><a href="partner-center-analytics-resources.md">Analyse de l’espace partenaires-Ressources</a></p></li>
<li><p><a href="get-all-azure-usage-analytics.md">Récupération de toutes les informations d’analyse d’utilisation Azure</a></p></li>
<li><p><a href="get-all-indirect-resellers-analytics.md">Obtient toutes les informations d’analyse des revendeurs indirects</a></p></li>
<li><p><a href="get-all-referrals-analytics.md">Obtient toutes les informations analytiques de références</a></p></li>
<li><p><a href="get-all-search-analytics.md">Récupération de toutes les informations analytiques de recherche</a></p></li>
<li><p><a href="get-all-subscription-analytics.md">Récupération de toutes les informations d’analyse d’abonnement</a></p></li>
<li><p><a href="get-subscription-analytics-by-search-query.md">Obtenir des informations d’analyse d’abonnement filtrées par une requête de recherche</a></p></li>
<li><p><a href="get-subscription-analytics-grouped-by-dates-or-terms.md">Obtient les informations d’analyse d’abonnement regroupées par dates ou termes</a></p></li>
<li><p><a href="get-licenses-deployment-information.md">Obtient les informations de déploiement des licences</a></p></li>
<li><p><a href="get-licenses-usage-information.md">Recevoir des informations sur l’utilisation des licences</a></p></li>
<li><p><a href="get-customer-licenses-deployment-information.md">Recevoir les informations de déploiement de licences client</a></p></li>
<li><p><a href="get-customer-licenses-usage-information.md">Recevoir des informations sur l’utilisation des licences client</a></p></li>
<li><p><a href="get-partner-licenses-deployment-information.md">Accéder aux informations de déploiement des licences du partenaire</a></p></li>
<li><p><a href="get-partner-licenses-usage-information.md">Informations sur l’utilisation des licences du partenaire</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="device-deployment.md">Déploiement de l’appareil</a></p></td>
<td><p>Stratégies de configuration</p>
<p>Ajoutez, supprimez, mettez à jour et récupérez des stratégies de configuration d’appareil.</p>
<ul>
<li><p><a href="create-a-new-configuration-policy-for-the-specified-customer.md">Créer une nouvelle stratégie de configuration pour le client spécifié</a></p></li>
<li><p><a href="delete-a-configuration-policy-for-the-specified-customer.md">Supprimer une stratégie de configuration pour le client spécifié</a></p></li>
<li><p><a href="get-a-list-of-a-customer-s-policies.md">Obtenir la liste des stratégies d'&#39;un client</a></p></li>
<li><p><a href="retrieve-a-customer-s-configuration-policy.md">Récupérer une stratégie&#39;de configuration de client</a></p></li>
<li><p><a href="update-a-configuration-policy-for-the-specified-customer.md">Mettre à jour une stratégie de configuration pour le client spécifié</a></p></li>
</ul>
<p>Appareils</p>
<p>Utiliser et charger des lots d’appareils et des métadonnées d’appareil.</p>
<ul>
<li><p><a href="get-the-status-of-a-device-batch-upload.md">Obtenir l’état d’un téléchargement par lots d’appareils</a></p></li>
<li><p><a href="get-the-list-of-device-batches-for-the-specified-customer.md">Obtenir la liste des lots d’appareils pour le client spécifié</a></p></li>
<li><p><a href="get-a-list-of-devices-for-the-specified-batch-and-customer.md">Obtenir la liste des appareils pour le lot et le client spécifiés</a></p></li>
<li><p><a href="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md">Télécharger une liste d’appareils pour créer un lot pour le client spécifié</a></p></li>
<li><p><a href="upload-a-list-of-devices-for-the-specified-customer.md">Télécharger une liste d’appareils vers un lot existant pour le client spécifié</a></p></li>
<li><p><a href="delete-a-device-for-the-specified-customer.md">Supprimer un appareil pour le client spécifié</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-profiles-and-information.md">Gérer les comptes et les profils</a></p></td>
<td><p>Utiliser des comptes et des profils</p>
<ul>
<li><p><a href="get-legal-business-profile.md">Procurez-vous le profil d’entreprise juridique partenaire</a></p></li>
<li><p><a href="get-an-organization-profile.md">Récupération d’un profil d’organisation</a></p></li>
<li><p><a href="get-partner-billing-profile.md">Télécharger le profil de facturation du partenaire</a></p></li>
<li><p><a href="get-partner-network-profile.md">Télécharger le profil de Microsoft Partner Network</a></p></li>
<li><p><a href="get-support-profile.md">Accéder au profil de support</a></p></li>
<li><p><a href="update-legal-business-profile.md">Mettre à jour le profil d’entreprise juridique partenaire</a></p></li>
<li><p><a href="update-partner-billing-profile.md">Mettre à jour le profil de facturation du partenaire</a></p></li>
<li><p><a href="update-support-profile.md">Mettre à jour le profil de support</a></p></li>
<li><p><a href="update-an-organization-profile.md">Mettre à jour un profil d’organisation</a></p></li>
<li><p><a href="get-partner-by-mpn-id.md">Vérifier un ID MPN de partenaire</a></p></li>
<li><p><a href="get-all-subscriptions-by-partner.md">Obtenir les abonnements du client&#39;par ID MPN du partenaire</a></p></li>
<li><p><a href="get-customers-of-an-indirect-reseller.md">Procurez-vous des clients d’un revendeur indirect</a></p></li>
<li><p><a href="get-indirect-resellers-of-a-customer.md">Obtenir des revendeurs indirects d’un client</a></p></li>
<li><p><a href="retrieve-a-list-of-indirect-resellers.md">Récupérer une liste de revendeurs indirects</a></p></li>
</ul></td>
</tr>
<tr>
<td>
<p><a href="manage-billing.md">Gérer la facturation</a></p></td>
<td><p>Cycle de facturation</p>
<ul>
<li><p><a href="change-the-billing-cycle.md">Modifier le cycle de facturation</a></p></li>
</ul>
<p>Enregistrements des taux et de l’utilisation Azure</p>
<ul>
<li><p><a href="get-prices-for-microsoft-azure.md">Obtenir des prix pour Microsoft Azure</a></p></li>
<li><p><a href="get-a-customer-s-utilization-record-for-azure.md">Obtenir les enregistrements&#39;d’utilisation des clients pour Azure</a></p></li>
</ul>
<p>Factures</p>
<ul>
<li><p><a href="get-a-collection-of-invoices.md">Obtenir une collection de factures</a></p></li>
<li><p><a href="get-invoice-estimate-links.md">Obtenir des liens d’estimation de facture</a></p></li>
<li><p><a href="get-invoice-billed-consumption-lineitems.md">Obtient les éléments de ligne de la consommation de la place de marché commercial facturés</a></p></li>
<li><p><a href="get-invoice-by-id.md">Recevoir une facture par ID</a></p></li>
<li><p><a href="get-invoiceline-items.md">Récupérer les éléments de ligne de facture</a></p></li>
<li><p><a href="get-invoice-receipt-statement.md">Instruction de réception de facture</a></p></li>
<li><p><a href="get-invoice-statement.md">Instruction d’extraction de facture</a></p></li>
<li><p><a href="get-invoice-summaries.md">Recevoir des résumés de facture</a></p></li>
<li><p><a href="get-invoice-unbilled-consumption-lineitems.md">Obtient les éléments de ligne de facturation de la place de marché commercial non facturés</a></p></li>
<li><p><a href="get-invoice-unbilled-recon-lineitems.md">Obtient les éléments de ligne de rapprochement non facturés de facture</a></p></li>
<li><p><a href="get-the-reseller-s-current-account-balance.md">Obtient le solde&#39;actuel du compte du partenaire</a></p></li>
</ul>
<p>Budget des dépenses Azure</p>
<ul>
<li><p><a href="get-all-monthly-usage-records-for-a-subscription.md">Obtenir les données d’utilisation d’un abonnement</a></p></li>
<li><p><a href="get-a-customer-usage-summary.md">Obtenir un récapitulatif de l’utilisation de tous les&#39;abonnements des clients</a></p></li>
</ul>
<p>Coûts de service</p>
<ul>
<li><p><a href="get-a-customer-s-service-costs-summary.md">Obtenir un résumé&#39;des coûts des services du client</a></p></li>
<li><p><a href="get-a-customer-s-service-costs-line-items.md">Obtenir les éléments&#39;de ligne des coûts des services du client</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-customers.md">Gérer les comptes client</a></p></td>
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
<li><p><a href="get-a-customer-by-name.md">Obtenir la liste des clients filtrés à l’aide d’un champ de recherche</a></p></li>
<li><p><a href="get-a-list-of-customers.md">Obtenir une liste de clients</a></p></li>
</ul>
<p>Gérer les commandes client et les abonnements</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-orders.md">Obtenir toutes les commandes d'&#39;un client</a></p></li>
<li><p><a href="get-a-list-of-orders-by-customer-and-billing-cycle-type.md">Obtenir une liste de commandes par client et type de cycle de facturation</a></p></li>
<li><p><a href="get-a-collection-of-entitlements.md">Obtenir une collection de droits</a></p></li> 
<li><p><a href="get-all-of-a-customer-s-subscriptions.md">Obtenir les abonnements des clients&#39;</a></p></li>
<li><p><a href="update-the-nickname-for-a-subscription.md">Mettre à jour le surnom d’un abonnement</a></p></li>
</ul>
<p>Gérer les détails du compte client</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-billing-profiles.md">Obtenir un profil&#39;de facturation client</a></p></li>
<li><p><a href="update-a-customer-s-billing-profile.md">Mettre à jour&#39;un profil de facturation client</a></p></li>
<li><p><a href="get-a-customer-s-company-profile.md">Obtenir un profil&#39;de société client</a></p></li>
<li><p><a href="update-a-customer-s-usage-spending-budget.md">Mettre à jour&#39;le budget des dépenses d’utilisation du client</a></p></li>
<li><p><a href="add-a-verified-domain-for-a-customer.md">Ajouter un domaine vérifié pour un client</a></p></li>
<li><p><a href="confirm-customer-consent.md">Confirmer l'acceptation du contrat Microsoft Cloud par le client</a></p></li>
<li><p><a href="get-agreement-metadata.md">Obtenir les métadonnées de l’accord pour le contrat Microsoft Cloud</a></p></li>
<li><p><a href="get-confirmation-of-customer-consent.md">Obtenir une confirmation de l'acceptation du contrat Microsoft Cloud par le client</a></p></li>
<li><p><a href="get-a-partner-s-validation-codes.md">Obtenir les codes de validation d’un partenaire</a></p></li>
<li><p><a href="get-a-customer-s-qualification.md">Obtenir la qualification d’un client</a></p></li>
<li><p><a href="update-a-customer-s-qualification.md">Mettre à jour la qualification d’un client</a></p></li>
</ul>
<p>Gérer les comptes d’utilisateur et attribuer des licences</p>
<ul>
<li><p><a href="get-a-user-account-by-id.md">Obtenir un compte d’utilisateur par ID</a></p></li>
<li><p><a href="create-user-accounts-for-a-customer.md">Créer des comptes d’utilisateur pour un client</a></p></li>
<li><p><a href="delete-user-accounts-for-a-customer.md">Supprimer un compte d’utilisateur pour un client</a></p></li>
<li><p><a href="update-user-accounts-for-a-customer.md">Mettre à jour des comptes d’utilisateur pour un client</a></p></li>
<li><p><a href="view-a-deleted-user.md">Afficher les utilisateurs supprimés pour un client</a></p></li>
<li><p><a href="restore-a-user-for-a-customer.md">Restaurer un utilisateur supprimé pour un client</a></p></li>
<li><p><a href="get-a-list-of-all-user-accounts-for-a-customer.md">Obtenir la liste de tous les comptes d’utilisateur pour un client</a></p></li>
<li><p><a href="reset-user-password-for-a-customer.md">Réinitialiser le mot de passe de l’utilisateur pour un client</a></p></li>
<li><p><a href="get-user-roles-for-a-customer.md">Obtenir des rôles d’utilisateur pour un client</a></p></li>
<li><p><a href="set-user-roles-for-a-customer.md">Définir des rôles d’utilisateur pour un client</a></p></li>
<li><p><a href="remove-customer-user-from-a-role.md">Supprimer un utilisateur client d’un rôle</a></p></li>
<li><p><a href="get-a-list-of-available-licenses.md">Obtenir une liste des licences disponibles</a></p></li>
<li><p><a href="assign-licenses-to-a-user.md">Attribuer des licences à un utilisateur</a></p></li>
<li><p><a href="check-which-licenses-are-assigned-to-a-user.md">Obtenir les licences attribuées à un utilisateur</a></p></li>
<li><p><a href="get-licenses-assigned-to-a-user-by-license-group.md">Obtenir les licences attribuées à un utilisateur par groupe de licences</a></p></li>
<li><p><a href="get-a-list-of-available-licenses-by-license-group.md">Obtenir une liste des licences disponibles par groupe de licences</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-orders.md">Gérer les commandes</a></p></td>
<td><p>Acheter Azure Reserved VM Instances</p>
<ul>
<li><p><a href="purchase-azure-reservations.md">Acheter des réservations Azure</a></p></li>
</ul>
<p>Effectuer un achat unique</p>
<ul>
<li><p><a href="make-a-one-time-purchase.md">Effectuer un achat unique</a></p></li> 
</ul>
<p>Recevoir des offres du catalogue</p>
<ul>
<li><p><a href="get-a-list-of-offer-categories-by-country-and-locale.md">Obtenir la liste des catégories d’offres par marché</a></p></li>
<li><p><a href="get-a-list-of-offers-for-a-market.md">Obtenir la liste des offres pour un marché</a></p></li>
<li><p><a href="get-an-offer-by-id.md">Recevoir une offre par ID</a></p></li>
<li><p><a href="get-addon-offers-by-offer-id.md">Obtenir des modules complémentaires pour un ID d’offre</a></p></li>
<li><p><a href="get-a-list-of-products.md">Obtenir une liste de produits</a></p></li>
<li><p><a href="get-a-product-by-id.md">Obtenir un produit par ID</a></p></li>
<li><p><a href="get-a-list-of-skus-for-a-product.md">Obtenir la liste des références (SKU) d’un produit</a></p></li>
<li><p><a href="get-a-sku-by-id.md">Obtenir la liste des disponibilités pour une référence (SKU)</a></p></li>
<li><p><a href="get-an-availability-by-id.md">Recevoir une disponibilité par ID</a></p></li>
<li><p><a href="check-inventory.md">Vérifier l’inventaire</a></p></li>
</ul>
<p>Gérer une commande</p>
<ul>
<li><p><a href="cancel-an-order-from-the-integration-sandbox.md">Annuler une commande à partir du bac à sable (sandbox) d’intégration</a></p></li>
<li><p><a href="checkout-a-cart.md">Extraire un panier</a></p></li>
<li><p><a href="create-a-cart.md">Créer un panier</a></p></li>
<li><p><a href="create-a-cart-with-add-ons.md">Créer un panier avec des extensions</a></p></li>
<li><p><a href="create-an-order.md">Créer une commande</a></p></li>
<li><p><a href="create-an-order-for-a-customer-of-an-indirect-reseller.md">Créer une commande pour un client d’un revendeur indirect</a></p></li>
<li><p><a href="get-activation-link-by-order-line-item.md">Recevoir le lien d’activation par élément de ligne de commande</a></p></li>
<li><p><a href="get-an-order-by-id.md">Recevoir une commande par ID</a></p></li>
<li><p><a href="purchase-an-add-on-to-a-subscription.md">Acheter un module complémentaire à un abonnement</a></p></li>
<li><p><a href="purchase-catalog-items.md">Éléments du catalogue d’achat</a></p></li>
<li><p><a href="update-a-cart.md">Mettre à jour un panier</a></p></li>
</ul>
<p>Activer un abonnement pour les achats de l’instance de machine virtuelle réservée Azure</p>
<ul>
<li><p><a href="register-a-subscription.md">Inscrire un abonnement</a></p></li>
<li><p><a href="get-subscription-registration-status.md">Afficher l’état d’inscription de l’abonnement</a></p></li>
</ul>
<p>Conversions d’essai</p>
<ul>
<li><p><a href="get-a-list-of-trial-conversion-offers.md">Obtenir une liste des offres de conversion de version d’évaluation</a></p></li>
<li><p><a href="convert-a-trial-subscription-to-paid.md">Convertir un abonnement d'évaluation en abonnement payant</a></p></li>
</ul>
<p>Récupérer les détails de l’abonnement</p>
<ul>
<li><p><a href="get-a-subscription-by-id.md">Obtenir un abonnement par ID</a></p></li>
<li><p><a href="get-a-list-of-subscriptions-by-order.md">Obtenir une liste d’abonnements par commande</a></p></li>
<li><p><a href="get-a-list-of-add-ons-for-a-subscription.md">Obtenir la liste des modules complémentaires pour un abonnement</a></p></li>
<li><p><a href="get-subscription-provisioning-status.md">Obtenir l’état d'approvisionnement d’abonnements</a></p></li>
</ul>
<p>Gérer un abonnement</p>
<ul>
<li><p><a href="change-the-quantity-of-a-subscription.md">Modifier la quantité d’un abonnement</a></p></li>
<li><p><a href="update-autorenew-for-an-azure-marketplace-subscription.md">Mettre à jour le renouvellement autorenouvelé pour un abonnement à la place de marché commercial</a></p></li>
<li><p><a href="suspend-a-subscription.md">Suspendre un abonnement</a></p></li>
<li><p><a href="reactivate-a-suspended-a-subscription.md">Réactiver un abonnement suspendu</a></p></li>
<li><p><a href="transition-a-subscription.md">Transition d’un abonnement</a></p></li>
<li><p><a href="cancel-an-azure-marketplace-subscription.md">Annuler un abonnement au marché commercial</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="provide-support.md">Fournir un support</a></p></td>
<td><p>Administration des services pour un client</p>
<ul>
<li><p><a href="get-the-managed-services-for-a-customer-by-id.md">Obtenir les services managés pour un client par ID</a></p></li>
</ul>
<p>Gérer les contacts de support</p>
<ul>
<li><p><a href="get-a-subscription-s-support-contact.md">Obtenir un contact&#39;de support pour les abonnements</a></p></li>
<li><p><a href="update-a-subscription-s-support-contact.md">Mettre à jour&#39;un contact de support pour les abonnements</a></p></li>
</ul>
<p>Gérer les demandes de service</p>
<ul>
<li><p><a href="create-a-service-request-.md">Créer une demande de service</a></p></li>
<li><p><a href="get-service-request-support-topics--pending-.md">Obtenir les rubriques de support des demandes de service</a></p></li>
<li><p><a href="get-all-service-requests-for-a-customer.md">Obtenir toutes les demandes de service pour un client</a></p></li>
<li><p><a href="get-service-request-details-by-id.md">Obtenir les détails de la demande de service par ID</a></p></li> 
<li><p><a href="update-a-service-request.md">Mettre à jour une demande de service</a></p></li>
</ul></td>
</tr>
<tr>
  <td><p><a href="https://docs.microsoft.com/partner/develop/referrals">Références</a></p></td>
  <td><p>Références</p>
    <ul>
      <li><p><a href="https://docs.microsoft.com/partner/develop/create-a-referral">Créer une référence</a></p></li> 
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-list-of-referrals">Obtenir une liste de références</a></p></li> 
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
<li><p><a href="get-market-specific-validation-data.md">Recevez les règles de mise en forme des adresses par marché</a></p></li>
<li><p><a href="verify-domain-availability.md">Vérifier la disponibilité du domaine</a></p></li>
<li><p><a href="delete-a-customer-account-from-the-integration-sandbox.md">Supprimer un compte client du bac à sable (sandbox) d’intégration</a></p></li>
<li><p><a href="get-a-record-of-partner-center-activity-by-user.md">Obtenir un enregistrement des activités de l'Espace partenaires</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="background"></a>Arrière-plan

### <a name="who-is-involved-in-the-order-process"></a>Qui est impliqué dans le processus de commande ?

Microsoft, serveurs de distribution, revendeurs et clients. Les serveurs de distribution et les revendeurs sont souvent désignés sous le terme de « **partenaires**».

Parfois, Microsoft travaille directement avec les revendeurs qui vendent aux clients. Microsoft travaille également avec les serveurs de distribution, et ces derniers travaillent avec leur propre ensemble ou canal de revendeurs qui vendent aux clients.

### <a name="whats-getting-sold"></a>Que se passe-t-il ?

Microsoft fournit une liste d' **offres**. Il s’agit de références SKU spécifiques de produits comme Office 365 ou Intune. Les offres sont **basées** sur une licence (le coût dépend du nombre de machines sur lesquelles elles sont installées) ou sur **l’utilisation** (le coût dépend de la quantité de mémoire et de calcul utilisée). Pour plus d’informations, consultez [offres partenaires dans le programme du fournisseur de solutions Cloud](https://docs.microsoft.com/partner-center/csp-offers).

Les partenaires CSP sont des revendeurs qui ont des clients et vendent des produits Microsoft à partir de la liste des offres actuelles. Une fois que les clients ont signé leur contrat, le revendeur passe une **commande** pour une ou plusieurs offres. Certaines offres incluent des **modules** complémentaires comme davantage d’espace ou de fonctionnalités supplémentaires, qui sont suivies avec l’offre parente. Les commandes sont traitées, puis le client peut utiliser leurs **abonnements**. Microsoft facture le revendeur ou le distributeur chaque mois en fonction du nombre de licences et de l’utilisation de chaque client.

Des abonnements peuvent être ajoutés, et le nombre de sièges ou de modules complémentaires peut être augmenté ou réduit. Si un client ne peut pas payer, utilise l’abonnement ou s’est engagé en fraude, Microsoft, le serveur de distribution ou le revendeur sont tous en mesure de suspendre l’abonnement. Elle sera permanente si elle n’est pas réactivée dans les limites du programme CSP.

Vous pouvez vérifier les abonnements qu’un client est **autorisé** à utiliser (par ex., ceux qui sont actuellement payés, non suspendus et non remplacés par un ordre plus récent).
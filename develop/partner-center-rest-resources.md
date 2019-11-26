---
title: Ressources REST de l’espace partenaires
description: Cette section fournit des définitions pour les éléments JSON nécessaires à la création de requêtes et à l’analyse des réponses à l’aide de l’API REST de l’espace partenaires.
ms.assetid: E7C51D19-C6A7-4A4C-9F17-B4D39195972A
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 4be969f9bced111c3ba95f773920f4aecfc4942d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486819"
---
# <a name="partner-center-rest-resources"></a>Ressources REST de l’espace partenaires


**S’applique à**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Cette section fournit des définitions pour les éléments JSON nécessaires à la création de requêtes et à l’analyse des réponses à l’aide de l’API REST de l’espace partenaires. Pour plus d’informations sur l’utilisation de ces éléments, y compris des exemples de code, consultez la section [scénarios](scenarios.md) et la section Exemples de l' [espace partenaires](partner-center-samples.md) .

## <a name="span-idin_this_sectionspan-idin_this_sectionspan-idin_this_sectionin-this-section"></a><span id="In_this_section"/><span id="in_this_section"/><span id="IN_THIS_SECTION"/>dans cette section


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><a href="analytics-resources.md">Analyses</a></td>
<td><ul>
<li>PartnerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
<li>CustomerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="auditing-resources.md">Audit</a></td>
<td><ul>
<li>AuditRecord</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="azure-rate-card-resources.md">Carte de tarifs Azure</a></td>
<td><ul>
<li>AzureRateCard</li>
<li>AzureMeter</li>
<li>AzureOfferTerm</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="azure-utilization-record-resources.md">Enregistrement d’utilisation Azure</a></td>
<td><ul>
<li>AzureUtilizationRecord</li>
<li>AzureResource</li>
<li>AzureInstanceData</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="cart-resources.md">Caddie</a></td>
<td><ul>
<li>Caddie</li>
<li>CartLineItem</li>
<li>CartError</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="conversions-resources.md">Conversions</a></td>
<td><ul>
<li>Conversion</li>
<li>ConversionError</li>
<li>ConversionResult</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="country-information-resources.md">CountryInformation</a></td>
<td><ul>
<li>CountryInformation</li>
<li>CountryValidationRules</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="customer-resources.md">Assistance</a></td>
<td><ul>
<li>Client</li>
<li>CustomerCompanyProfile</li>
<li>CustomerBillingProfile</li>
<li>CustomerRelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="customer-usage-resources.md">Budgétisation de l’utilisation du client</a></td>
<td><ul>
<li>CustomerMonthlyUsageRecord</li>
<li>CustomerUsageSummary</li>
<li>PartnerUsageSummary</li>
<li>SpendingBudget</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="entitlement-resources.md">Droit</a></td>
<td><ul>
<li>Droit</li>
<li>ReferenceOrder</li>
<li>entitlementType</li>
<li>Artefact</li>
<li>artifactType</li>
<li>VirtualMachineReservedInstanceArtifact</li>
<li>VirtualMachineReservedInstanceArtifactDetails</li>
<li>VirtualMachineReservation</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="invoice-resources.md">Facture</a></td>
<td><ul>
<li>Facture</li>
<li>InvoiceDetail</li>
<li>InvoiceLineItem</li>
<li>InvoiceSummary</li>
<li>InvoiceSummaryDetail</li>
<li>InvoiceSummaries</li>
<li>LicenseBasedLineItem</li>
<li>UsageBasedLineItem</li>
<li>InvoiceStatement</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="license-resources.md">Licence</a></td>
<td><ul>
<li>Licence</li>
<li>LicenseUpdate</li>
<li>LicenseAssignment</li>
<li>LicenseWarning</li>
<li>ProductSku</li>
<li>ServicePlan</li>
<li>SubscribedSku</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="managed-service-resources.md">ManagedService</a></td>
<td><ul>
<li>ManagedService</li>
<li>ManagedServiceLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="offer-resources.md">Offre</a></td>
<td><ul>
<li>Offre</li>
<li>OfferCategory</li>
<li>OfferLinks</li>
<li>OfferProduct</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="order-resources.md">Ordre</a></td>
<td><ul>
<li>Ordre</li>
<li>OrderLineItem</li>
<li>OrderLinks</li>
<li>OrderLineItemLinks</li>
<li>OrderStatus</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="profile-resources.md">Profil</a></td>
<td><ul>
<li>BillingProfile</li>
<li>LegalBusinessProfile</li>
<li>MpnProfile</li>
<li>OrganizationProfile</li>
<li>SupportProfile</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="product-resources.md">Produits</a></td>
<td><ul>
<li>Produit</li>
<li>ItemType</li>
<li>ProductLinks</li>
<li>Paire</li>
<li>Disponibilité</li>
<li>InventoryCheckRequest</li>
<li>InventoryItem</li>
<li>InventoryRestriction</li>
<li>BillingCycleType</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="relationships-resources.md">Relations</a></td>
<td><ul>
<li>PartnerRelationship</li>
<li>RelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="service-costs-resources.md">ServiceCosts</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="service-request-resources.md">ServiceRequest</a></td>
<td><ul>
<li>ServiceRequest</li>
<li>ServiceRequestContact</li>
<li>ServiceRequestNote</li>
<li>ServiceRequestOrganization</li>
<li>SupportTopic</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="subscription-resources.md">Récurrent</a></td>
<td><ul>
<li>Abonnement</li>
<li>SubscriptionLinks</li>
<li>SubscriptionProvisioningStatus</li>
<li>SubscriptionRegistrationStatus</li>
<li>SupportContact</li>
<li>RegisterSubscription</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="subscription-usage-resources.md">Utilisation de l’abonnement</a></td>
<td><ul>
<li>SubscriptionDailyUsageRecord <em>(obsolète)</em></li>
<li>SubscriptionMonthlyUsageRecord</li>
<li>SubscriptionUsageSummary</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="upgrade-resources.md">Installation</a></td>
<td><ul>
<li>Mettre à niveau/Mise à niveau</li>
<li>UpgradeError</li>
<li>UpgradeResult</li>
<li>UserLicenseError</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="user-resources.md">Utilisateur</a></td>
<td><ul>
<li>Utilisateur</li>
<li>CustomerUser</li>
<li>UserCredentials</li>
<li>UserMember</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="utility-resources.md">Ressources de l’utilitaire</a></td>
<td><ul>
<li>Address</li>
<li>Contact</li>
<li>FieldFilter</li>
<li>FileInfo</li>
<li>Lien</li>
<li>PasswordProfile</li>
<li>ResourceLinks</li>
<li>ResourceAttributes</li>
<li>SecureString</li>
<li>ValidationCode</li>
</ul></td>
</tr>
</tbody>
</table>

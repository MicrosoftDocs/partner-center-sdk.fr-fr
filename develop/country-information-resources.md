---
title: Ressources d’informations sur le pays
description: Métadonnées descriptives pour un pays ou une région.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed744cf131c2d5956575ab1aa2c79f0303b226fc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86096314"
---
# <a name="country-information-resources"></a>Ressources d’informations sur le pays

**S’applique à :**

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources suivantes sont des métadonnées descriptives pour un pays ou une région.

## <a name="countryinformation"></a>CountryInformation

| Propriété                      | Type               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | Données d’extension.                                                                                |
| Iso2Code                      | string             | Code ISO-2.                                                                                     |
| Iso3Code                      | string             | Code ISO-3.                                                                                     |
| DefaultCulture                | string             | Culture par défaut.                                                                               |
| IsStateRequired               | boolean            | Indique si un État/une province est requis ou non.                                             |
| SupportedStatesList           | tableau de chaînes   | Si un État/une province est requis, retourne la liste complète de ce pays/cette région.                    |
| SupportedLanguagesList        | tableau de chaînes   | Liste des langues prises en charge.                                                                     |
| SupportedCulturesList         | tableau de chaînes   | Liste des cultures prises en charge.                                                                      |
| IsPostalCodeRequired          | boolean            | Indique si un code postal est requis ou non.                                    |
| PostalCodeRegex               | string             | Expression régulière qui définit le code postal.                                          |
| IsCityRequired                | boolean            | Indique si une ville est obligatoire ou non.                                                       |
| IsVatIdSupported              | boolean            | Indique si un ID de TVA est requis ou non.                                                     |
| TaxIdFormat                   | string             | Format de l’ID de taxe.                                                                                 |
| TaxIdSample                   | string             | Exemple d’ID de taxe.                                                                                 |
| VatIdRegex                    | string             | Expression régulière de l’ID de taxe.                                                                     |
| PhoneNumberRegex              | string             | Expression régulière de numéro de téléphone.                                                               |
| IsRegistrationNumberSupported | boolean            | Indique si un numéro d’enregistrement est pris en charge ou non.                                       |
| IsTaxIdSupported              | boolean            | Indique si un ID de taxe est pris en charge ou non. Cela diffère de IsVatIdSupported. |
| ResellerAgreementRegion       | string             | Région du revendeur.                                                                     |
| GeographicRegion              | string             | Région géographique.                                                                             |
| CountryCallingCodesList       | tableau de chaînes   | Codes d’appel pris en charge dans le pays ou la région.                                                 |
| Attributs                    | ResourceAttributes | Attributs de métadonnées correspondant à la ressource CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Décrit les règles de mise en forme des adresses pour un pays ou une région.

| Propriété                | Type               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | Code ISO-2.                                                                                     |
| DefaultCulture          | string             | Culture par défaut.                                                                               |
| IsStateRequired         | boolean            | Indique si un État/une province est requis ou non.                                             |
| SupportedStatesList     | tableau de chaînes   | Si un État/une province est requis, retourne la liste complète de ce pays/cette région.                    |
| SupportedLanguagesList  | tableau de chaînes   | Liste des langues prises en charge.                                                                     |
| SupportedCulturesList   | tableau de chaînes   | Liste des cultures prises en charge.                                                                      |
| IsPostalCodeRequired    | boolean            | Indique si un code postal est requis ou non.                                    |
| PostalCodeRegex         | string             | Expression régulière qui définit le code postal.                                          |
| IsCityRequired          | boolean            | Indique si une ville est obligatoire ou non.                                                       |
| IsVatIdSupported        | boolean            | Indique si un ID de TVA est requis ou non.                                                     |
| TaxIdFormat             | string             | Format de l’ID de taxe.                                                                                 |
| TaxIdSample             | string             | Exemple d’ID de taxe.                                                                                 |
| VatIdRegex              | string             | Expression régulière de l’ID de taxe.                                                                     |
| PhoneNumberRegex        | string             | Expression régulière de numéro de téléphone.                                                               |
| IsTaxIdSupported        | boolean            | Indique si un ID de taxe est pris en charge ou non. Cette propriété est différente de IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Indique si un ID de taxe est facultatif ou non.                                                     |
| CountryCallingCodesList | tableau de chaînes   | Codes d’appel pris en charge dans le pays ou la région.                                                 |
| Attributs              | ResourceAttributes | Attributs de métadonnées correspondant à la ressource CountryInformation.                          |

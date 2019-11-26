---
title: Country information resources
description: Descriptive metadata for a country/region.
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 321e05ff2f65746ae2e555bf35b4aa8d298c20af
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488809"
---
# <a name="country-information-resources"></a>Country information resources

S'applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

The following resources are descriptive metadata for a country/region.

## <a name="countryinformation"></a>CountryInformation

| Propriété                      | Tapez               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | chaîne             | The extension data.                                                                                |
| Iso2Code                      | chaîne             | An ISO-2 code.                                                                                     |
| Iso3Code                      | chaîne             | An ISO-3 code.                                                                                     |
| DefaultCulture                | chaîne             | The default culture.                                                                               |
| IsStateRequired               | booléen            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList           | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList        | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList         | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired          | booléen            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex               | chaîne             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired                | booléen            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported              | booléen            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat                   | chaîne             | The tax ID format.                                                                                 |
| TaxIdSample                   | chaîne             | The tax ID sample.                                                                                 |
| VatIdRegex                    | chaîne             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex              | chaîne             | The phone number regular expression.                                                               |
| IsRegistrationNumberSupported | booléen            | Indicates whether a registration number is supported or not.                                       |
| IsTaxIdSupported              | booléen            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| ResellerAgreementRegion       | chaîne             | The reseller agreement region.                                                                     |
| GeographicRegion              | chaîne             | The geographic region.                                                                             |
| CountryCallingCodesList       | array of strings   | The calling codes supported in the country/region.                                                 |
| Attributs                    | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Describes the address formatting rules for a country/region.

| Propriété                | Tapez               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | chaîne             | An ISO-2 code.                                                                                     |
| DefaultCulture          | chaîne             | The default culture.                                                                               |
| IsStateRequired         | booléen            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList     | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList  | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList   | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired    | booléen            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex         | chaîne             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired          | booléen            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported        | booléen            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat             | chaîne             | The tax ID format.                                                                                 |
| TaxIdSample             | chaîne             | The tax ID sample.                                                                                 |
| VatIdRegex              | chaîne             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex        | chaîne             | The phone number regular expression.                                                               |
| IsTaxIdSupported        | booléen            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| IsTaxIdOptional         | booléen            | Indicates whether a tax ID is optional or not.                                                     |
| CountryCallingCodesList | array of strings   | The calling codes supported in the country/region.                                                 |
| Attributs              | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |
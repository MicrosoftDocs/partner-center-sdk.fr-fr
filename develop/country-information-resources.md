---
title: Ressources d’informations sur le pays
description: Métadonnées descriptives pour un pays ou une région.
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
# <a name="country-information-resources"></a>Ressources d’informations sur le pays

S’applique à :

- Espace partenaires
- Espace partenaires géré par 21Vianet
- Espace partenaires de Microsoft Cloud Germany
- Espace partenaires de Microsoft Cloud for US Government

Les ressources suivantes sont des métadonnées descriptives pour un pays ou une région.

## <a name="countryinformation"></a>CountryInformation

| Propriété                      | Type               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | chaîne             | Données d’extension.                                                                                |
| Iso2Code                      | chaîne             | Code ISO-2.                                                                                     |
| Iso3Code                      | chaîne             | Code ISO-3.                                                                                     |
| DefaultCulture                | chaîne             | Culture par défaut.                                                                               |
| IsStateRequired               | booléen            | Indique si un État/une province est requis ou non.                                             |
| SupportedStatesList           | Tableau de chaînes   | Si un État/une province est requis, retourne la liste complète de ce pays/cette région.                    |
| SupportedLanguagesList        | Tableau de chaînes   | Liste des langues prises en charge.                                                                     |
| SupportedCulturesList         | Tableau de chaînes   | Liste des cultures prises en charge.                                                                      |
| IsPostalCodeRequired          | booléen            | Indique si un code postal est requis ou non.                                    |
| PostalCodeRegex               | chaîne             | Expression régulière qui définit le code postal.                                          |
| IsCityRequired                | booléen            | Indique si une ville est obligatoire ou non.                                                       |
| IsVatIdSupported              | booléen            | Indique si un ID de TVA est requis ou non.                                                     |
| TaxIdFormat                   | chaîne             | Format de l’ID de taxe.                                                                                 |
| TaxIdSample                   | chaîne             | Exemple d’ID de taxe.                                                                                 |
| VatIdRegex                    | chaîne             | Expression régulière de l’ID de taxe.                                                                     |
| PhoneNumberRegex              | chaîne             | Expression régulière de numéro de téléphone.                                                               |
| IsRegistrationNumberSupported | booléen            | Indique si un numéro d’enregistrement est pris en charge ou non.                                       |
| IsTaxIdSupported              | booléen            | Indique si un ID de taxe est pris en charge ou non. Notez que cela est différent de IsVatIdSupported. |
| ResellerAgreementRegion       | chaîne             | Région du revendeur.                                                                     |
| GeographicRegion              | chaîne             | Région géographique.                                                                             |
| CountryCallingCodesList       | Tableau de chaînes   | Codes d’appel pris en charge dans le pays ou la région.                                                 |
| Attributs                    | ResourceAttributes | Attributs de métadonnées correspondant à la ressource CountryInformation.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Décrit les règles de mise en forme des adresses pour un pays ou une région.

| Propriété                | Type               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | chaîne             | Code ISO-2.                                                                                     |
| DefaultCulture          | chaîne             | Culture par défaut.                                                                               |
| IsStateRequired         | booléen            | Indique si un État/une province est requis ou non.                                             |
| SupportedStatesList     | Tableau de chaînes   | Si un État/une province est requis, retourne la liste complète de ce pays/cette région.                    |
| SupportedLanguagesList  | Tableau de chaînes   | Liste des langues prises en charge.                                                                     |
| SupportedCulturesList   | Tableau de chaînes   | Liste des cultures prises en charge.                                                                      |
| IsPostalCodeRequired    | booléen            | Indique si un code postal est requis ou non.                                    |
| PostalCodeRegex         | chaîne             | Expression régulière qui définit le code postal.                                          |
| IsCityRequired          | booléen            | Indique si une ville est obligatoire ou non.                                                       |
| IsVatIdSupported        | booléen            | Indique si un ID de TVA est requis ou non.                                                     |
| TaxIdFormat             | chaîne             | Format de l’ID de taxe.                                                                                 |
| TaxIdSample             | chaîne             | Exemple d’ID de taxe.                                                                                 |
| VatIdRegex              | chaîne             | Expression régulière de l’ID de taxe.                                                                     |
| PhoneNumberRegex        | chaîne             | Expression régulière de numéro de téléphone.                                                               |
| IsTaxIdSupported        | booléen            | Indique si un ID de taxe est pris en charge ou non. Notez que cela est différent de IsVatIdSupported. |
| IsTaxIdOptional         | booléen            | Indique si un ID de taxe est facultatif ou non.                                                     |
| CountryCallingCodesList | Tableau de chaînes   | Codes d’appel pris en charge dans le pays ou la région.                                                 |
| Attributs              | ResourceAttributes | Attributs de métadonnées correspondant à la ressource CountryInformation.                          |
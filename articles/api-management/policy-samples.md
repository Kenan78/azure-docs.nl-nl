---
title: Voorbeelden van Azure API Management-beleid | Microsoft Docs
description: Meer informatie over het beschikbare beleid voor gebruik in Azure API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: cflower
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: sample
ms.date: 10/31/2017
ms.author: apimpm
ms.custom: mvc
ms.openlocfilehash: 3f1d9a96888732e6221722102a687e09f37333c0
ms.sourcegitcommit: d98d99567d0383bb8d7cbe2d767ec15ebf2daeb2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/10/2018
---
# <a name="api-management-policy-samples"></a>Voorbeelden van API Management-beleid

[Beleidsregels](api-management-howto-policies.md) zijn een krachtige mogelijkheid van API Management waarmee de uitgever het gedrag van de API via configuratie kan wijzigen. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op de aanvraag of het antwoord van een API. De volgende tabel bevat koppelingen naar voorbeelden en geeft u een korte beschrijving van elk voorbeeld.

|||
|---|---|
|**Inkomende beleidsregels**||
|[Voegt een Forwarded-koptekst zodat de back-end API de juiste URL's kan maken](./policies/set-header-to-enable-backend-to-construct-urls.md?toc=api-management/toc.json) |Demonstreert hoe u een Forwarded-koptekst toevoegt in de binnenkomende aanvraag zodat de back-end-API de juiste URL's kan maken.|
|[Een header met een correlatie-id toevoegen](./policies/add-correlation-id.md?toc=api-management/toc.json) |Demonstreert hoe u een koptekst met een correlatie-id kunt toevoegen aan de binnenkomende aanvraag.|
|[Mogelijkheden toevoegen aan een back-endservice en de reactie in cache opslaan](./policies/cache-response.md?toc=api-management/toc.json) |Laat zien hoe u mogelijkheden kunt toevoegen aan een back-endservice. Bijvoorbeeld, een naam van de locatie accepteren in plaats van de breedtegraad en lengtegraad in een weerprognose-API.|
|[Toegang verlenen op basis van JWT-claims ](./policies/authorize-request-based-on-jwt-claims.md?toc=api-management/toc.json) |Laat zien hoe u toegang verleent aan specifieke HTTP-methoden op een API op basis van JWT-claims.|
|[Toestaan van toegang met behulp van Google-OAuth-token](./policies/use-google-as-oauth-token-provider.md?toc=api-management/toc.json) |Laat zien hoe u toegang verleent aan uw eindpunten met Google als een provider van OAuth-token.|
|[Shared Access Signature genereren en aanvraag doorsturen naar Azure-opslag](./policies/generate-shared-access-signature.md?toc=api-management/toc.json) |Laat zien hoe u [Shared Access Signature](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) genereert met expressies en de aanvraag doorstuurt naar Azure-opslag met beleid voor herschrijven van URI. |
|[OAuth2 toegangstoken ophalen uit AAD en dit doorsturen naar de back-end](./policies/use-oauth2-for-authorization.md?toc=api-management/toc.json) |Biedt een voorbeeld van het gebruik van OAuth2 voor autorisatie tussen de gateway en een back-end. Er wordt weergegeven hoe u een toegangstoken van AAD kunt verkrijgen en dit door kunt sturen naar de back-end.|
|[X-CSRF-token ophalen uit SAP-gateway met behulp van beleid voor verbindingsaanvragen verzenden](./policies/get-x-csrf-token-from-sap-gateway.md?toc=api-management/toc.json) |Laat zien hoe u een X-CSRF-patroon implementeert dat wordt gebruikt door veel API's. Dit voorbeeld is specifiek voor SAP-Gateway. |
|[De aanvraag op basis van de grootte van de hoofdtekst routeren](./policies/route-requests-based-on-size.md?toc=api-management/toc.json) |Demonstreert hoe u aanvragen op basis van de grootte van hun hoofdtekst routeert.|
|[Aanvraag contextinformatie sturen naar de back-endservice](./policies/send-request-context-info-to-backend-service.md?toc=api-management/toc.json) |Laat zien hoe u bepaalde contextgegevens kunt verzenden naar de back-endservice voor logboekregistratie of voor verwerking.|
|[Duur antwoordcache instellen](./policies/set-cache-duration.md?toc=api-management/toc.json) |Demonstreert hoe u de duur van het antwoord instelt met de maxAge-waarde in Cache-Control-header die door de back-end is verstuurd.|
|**Uitgaand beleid**||
|[Antwoordinhoud filteren](./policies/filter-response-content.md?toc=api-management/toc.json) | Demonstreert hoe u gegevenselementen van de nettolading van de reactie moet filteren op basis van het product dat is gekoppeld aan de aanvraag.|
|**Beleid op fout**||
|[Fouten registreren in Stackify](./policies/log-errors-to-stackify.md?toc=api-management/toc.json) |Laat zien hoe u een beleid voor logboekregistratie van fouten toevoegt voor het verzenden van fouten naar Stackify voor logboekregistratie.|

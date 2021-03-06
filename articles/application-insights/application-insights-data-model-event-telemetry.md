---
title: Azure Application Insights telemetrie gegevensmodel - gebeurtenis telemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor telemetrie van gebeurtenis
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: mbullwin; sergkanz
ms.openlocfilehash: 4f6b5c35b65b4aff2dbe8dafbb2eb07d75c2382a
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/08/2018
---
# <a name="event-telemetry-application-insights-data-model"></a>Gebeurtenis telemetrie: Application Insights-gegevensmodel

Kunt u de gebeurtenis telemetrie-items maken (in [Application Insights](app-insights-overview.md)) vertegenwoordigt een gebeurtenis die is opgetreden in uw toepassing. Het is doorgaans een gebruikersinteractie zoals knop klikt u op of afhandeling bestellen. Het kan ook een gebeurtenis van de levenscyclus van de toepassing zoals configuratie of de initialisatie van de update zijn. 

Semantisch, gebeurtenissen kunnen of kunnen niet worden gecorreleerd met aanvragen. Gebeurtenis telemetrie is echter belangrijker dan de wijzigingsaanvragen of traceringen als goed gebruikt. Gebeurtenissen vertegenwoordigen de zakelijke Telemetrie en moet een onderwerp te scheiden, minder agressieve [steekproeven](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Naam

De naam van de gebeurtenis. Zodat juiste groepering en nuttige meetwaarden door uw toepassing te beperken, zodat er een klein aantal afzonderlijke gebeurtenisnamen gegenereerd. Bijvoorbeeld, gebruik niet een afzonderlijke naam voor elk gegenereerde exemplaar van een gebeurtenis.

Maximale lengte: 512 tekens

## <a name="custom-properties"></a>Aangepaste eigenschappen

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Aangepaste metingen

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Volgende stappen

- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- [Aangepaste gebeurtenis telemetrie schrijven](app-insights-api-custom-events-metrics.md#trackevent)
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.

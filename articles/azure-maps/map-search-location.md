---
title: Zoekresultaten met Azure-kaarten weergeven | Microsoft Docs
description: Het uitvoeren van een zoekopdracht met Azure Maps aanvragen en vervolgens de resultaten weergeven op een kaart Javascrip
author: jingjing-z
ms.author: jinzh
ms.date: 05/07/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: b77737b16b23ed00c8f12f84e6a8558a665a7d15
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/01/2018
ms.locfileid: "34599878"
---
# <a name="show-search-results-on-the-map"></a>Zoekresultaten weergeven op de kaart

In dit artikel leest u hoe een zoekaanvraag en weergeven van de zoekresultaten op de kaart. 

## <a name="understand-the-code"></a>De code begrijpen

<iframe height='500' scrolling='no' title='Zoekresultaten op een kaart weergeven' src='//codepen.io/azuremaps/embed/KQbaeM/?height=519&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Zie de Pen <a href='https://codepen.io/azuremaps/pen/KQbaeM/'>zoekresultaten weergeven op een kaart</a> door Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) op <a href='https://codepen.io'>CodePen</a>.
</iframe>

De eerste blok van code wordt in de code wordt een toewijzingsobject. U kunt zien [maken van een kaart](./map-create.md) voor instructies.

Het tweede codeblok maakt en voegt een laag van de zoekactie pincodes op de kaart. U kunt zien [toevoegen van een pincode op de kaart](./map-add-pin.md) voor instructies.

Het derde codeblok verzendt een [XMLHttpRequest](https://xhr.spec.whatwg.org/) naar [Azure kaarten Fuzzy zoeken-API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy).

Het laatste blok van code parseert de binnenkomende reactie. Deze verzamelt de breedtegraad en lengtegraad informatie voor elke locatie die is geretourneerd voor een geslaagde reactie. Deze voegt alle punten van de locatie toe aan de kaart als pincodes en past u de grenzen van de kaart voor het weergeven van alle pincodes.


## <a name="next-steps"></a>Volgende stappen

Meer informatie over de klassen en methoden die worden gebruikt in dit artikel: 

* [Azure toegewezen Fuzzy zoeken-API](https://docs.microsoft.com/rest/api/maps/search/getsearchfuzzy)
* [Kaart](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest)
    * [addPins](https://docs.microsoft.com/javascript/api/azure-maps-javascript/map?view=azure-iot-typescript-latest#addpins)
    
Zie de volgende artikelen voor meer voorbeelden van programmacode toevoegen aan uw maps: 
* [Informatie ophalen uit een coördinaat](./map-get-information-from-coordinate.md)
* [Richtlijnen voor het weergeven van A naar B](./map-route.md)

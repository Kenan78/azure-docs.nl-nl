---
title: Een Azure Container Service-cluster met Sysdig bewaken
description: Een Azure Container Service-cluster met Sysdig bewaken.
services: container-service
author: sauryadas
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 0c0f4fd1f3a8242061e198d7b5447656f9008e96
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2018
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Een Azure Container Service-cluster met Sysdig bewaken

In dit artikel implementeren we Sysdig-agents op alle agentknooppunten in uw Azure Container Service-cluster. Voor deze configuratie hebt u een Sysdig-account nodig. 

## <a name="prerequisites"></a>Vereisten
[Implementeer](container-service-deployment.md) en [verbind](../container-service-connect.md) een cluster dat door Azure Container Service is geconfigureerd. Verken de [Marathon-gebruikersinterface](container-service-mesos-marathon-ui.md). Ga naar [ http://app.sysdigcloud.com ](http://app.sysdigcloud.com) voor het instellen van een Sysdig cloud-account. 

## <a name="sysdig"></a>Sysdig
Sysdig is een bewakingsservice waarmee u de containers in uw cluster kunt bewaken. Sysdig is handig bij het oplossen van problemen, maar biedt ook algemene bewakingswaarden voor CPU, netwerk, geheugen en I/O. Met Sysdig kunt u gemakkelijk zien welke containers het hardst werken of in wezen het geheugen en de CPU het meest gebruiken. Deze weergave vindt u in de sectie ‘Overview’ (Overzicht), die zich momenteel in de bètafase bevindt. 

![Gebruikersinterface van Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Een Sysdig-implementatie met Marathon configureren
Deze stappen geven aan hoe u met Marathon Sysdig-toepassingen in uw cluster configureert en implementeert. 

Toegang tot uw DC/OS-Webgebruikersinterface via [ http://localhost:80/ ](http://localhost:80/) eenmaal Navigeer naar de 'Universe', die zich op de linksonder in de DC/OS-gebruikersinterface en zoek naar 'Sysdig'.

![Sysdig in het DC/OS-universum](./media/container-service-monitoring-sysdig/sysdig1.png)

Om nu de configuratie te voltooien, hebt u een Sysdig-cloudaccount of gratis proefaccount nodig. Nadat u bent aangemeld bij de Sysdig-cloudwebsite, klikt u op uw gebruikersnaam. Op de pagina ziet u uw ‘toegangssleutel’. 

![Sysdig API-sleutel](./media/container-service-monitoring-sysdig/sysdig2.png) 

Voer vervolgens in het DC/OS-universum uw toegangssleutel in de Sysdig-configuratie in. 

![Sysdig-configuratie in het DC/OS-universum](./media/container-service-monitoring-sysdig/sysdig3.png)

Stel nu de exemplaren in op 10000000, zodat telkens wanneer aan het cluster een nieuw knooppunt wordt toegevoegd, Sysdig automatisch op dat nieuwe knooppunt een agent implementeert. Dit is een tijdelijke oplossing om ervoor te zorgen dat Sysdig op alle nieuwe agents binnen het cluster wordt geïmplementeerd. 

![Sysdig-configuratie in de instanties van het DC/OS-universum](./media/container-service-monitoring-sysdig/sysdig4.png)

Nadat u het pakket hebt geïnstalleerd, navigeert u terug naar de Sysdig-gebruikersinterface en kunt u de verschillende gebruikswaarden voor de containers in uw cluster verkennen. 

U kunt ook Mesos- en Marathon-specifieke dashboards installeren via de [wizard Nieuw dashboard](https://app.sysdigcloud.com/#/dashboards/new).

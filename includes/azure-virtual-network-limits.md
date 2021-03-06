---
title: bestand opnemen
description: bestand opnemen
services: networking
author: jimdial
ms.service: networking
ms.topic: include
ms.date: 06/05/2018
ms.author: jdial
ms.custom: include file
ms.openlocfilehash: f4071f2555607b6035352a2aec38c986941c41a9
ms.sourcegitcommit: 6cf20e87414dedd0d4f0ae644696151e728633b6
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34826528"
---
<a name="virtual-networking-limits-classic"></a>De volgende beperkingen gelden alleen voor netwerkresources die worden beheerd via het klassieke implementatiemodel voor elk abonnement. Meer informatie over hoe [weergeven van het actuele Resourcegebruik op basis van uw abonnementen](../articles/networking/check-usage-against-limits.md).

| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Virtuele netwerken |50 |100 |
| Lokale netwerksites |20 |contact met ondersteuning |
| DNS-servers per virtueel netwerk |20 |100 |
| Privé-IP-adressen per virtueel netwerk |4096 |4096 |
| Gelijktijdige TCP of UDP loopt per NIC van een virtuele machine of rolinstantie |500.000 |500.000 |
| Netwerkbeveiligingsgroepen (NSG's) |100 |200 |
| NSG-regels per NSG |200 |400 |
| Door de gebruiker gedefinieerde routetabellen |100 |200 |
| Door de gebruiker gedefinieerde routes per routetabel |100 |400 |
| Openbare IP-adressen (dynamisch) |5 |contact met ondersteuning |
| Gereserveerde openbare IP-adressen |20 |contact met ondersteuning |
| Openbare VIP per implementatie |5 |contact met ondersteuning |
| Privé-VIP (ILB) per implementatie |1 |1 |
| Toegangsbeheerlijsten voor eindpunt (ACL's) |50 |50 |

#### <a name="azure-resource-manager-virtual-networking-limits"></a>Netwerklimieten - Azure Resource Manager
De volgende beperkingen gelden alleen voor netwerkresources die worden beheerd via Azure Resource Manager. De beperkingen gelden per regio en per abonnement. Meer informatie over hoe [weergeven van het actuele Resourcegebruik op basis van uw abonnementen](../articles/networking/check-usage-against-limits.md).

| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Virtuele netwerken |50 |1000 |
| Subnetten per virtueel netwerk |1000 |10.000 |
| Virtueel netwerk peerings per virtueel netwerk |10 |50 |
| DNS-servers per virtueel netwerk |9 |25 |
| Privé-IP-adressen per virtueel netwerk |16384 ** |16384 |
| Privé-IP-adressen per netwerkinterface |256 |1024 |
| Gelijktijdige TCP of UDP loopt per NIC van een virtuele machine of rolinstantie |500.000 |500.000 |
| Netwerkinterfaces (NIC) |24000 ** |24000 |
| Netwerkbeveiligingsgroepen (NSG's) |100 |5000 |
| NSG-regels per NSG |1000 ** |1000 |
| IP-adressen en -bereiken die zijn opgegeven voor de bron- of doelserver in een beveiligingsgroep |2000 |4000 |
| Toepassingsbeveiligingsgroepen |200 |500 |
| Beveiligingsgroepen toepassing per IP-configuratie per NIC |10 |20 |
| IP-configuraties per groep van toepassingen-beveiliging |1000 |4000 |
| Toepassing beveiligingsgroepen die kunnen worden opgegeven in alle beveiligingsregels van een netwerkbeveiligingsgroep |50 |100 |
| Door de gebruiker gedefinieerde routetabellen |100 |200 |
| Door de gebruiker gedefinieerde routes per routetabel |100 |400 |
| Openbare IP-adressen - dynamische |60 (standaard) |contact met ondersteuning |
| Openbare IP-adressen - statische |(Basic) 20 |contact met ondersteuning |
| Openbare IP-adressen - statische |(Standard) 20 |contact met ondersteuning |
| Punt-naar-site-basiscertificaten per VPN Gateway |20 |20 |

** Deze standaardlimieten gelden voor abonnementen die niet eerder deze limieten verhoogd door middel van ondersteuning hebben nog

#### <a name="load-balancer"></a>Load Balancer-limieten

| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Load Balancers | 100 | 1000 |
| Regels per resource, Basic | 150 | 250 |
| Regels per resource, standaard | 1250 | 1500 |
| Regels per IP-configuratie | 299 |299 |
| Frontend-IP-adresconfiguraties, Basic | 10 | 200 |
| Frontend-IP-adresconfiguraties, standaard | 10 | 600 |
| Back-endpool Basic | 100, één Beschikbaarheidsset | 100, één Beschikbaarheidsset |
| Back-endpool Standard | 1000, enkel VNet | 1000, enkel VNet |
| HA poorten, Standard | 1 per interne frontend | 1 per interne frontend |

[Neem contact op met de ondersteuning](../articles/azure-supportability/resource-manager-core-quotas-request.md ) als u de standaardlimieten wilt verhogen.


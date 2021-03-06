---
title: Beveiligt virtuele machines van Azure naar een on-premises site | Microsoft Docs
description: U kunt een failback naar on-premises om virtuele machines starten na een failover van virtuele machines naar Azure. Informatie over het opnieuw te beveiligen voordat u een failback.
services: site-recovery
author: rajani-janaki-ram
manager: gauravd
ms.service: site-recovery
ms.topic: article
ms.date: 03/05/2018
ms.author: rajanaki
ms.openlocfilehash: 4ee6eefa431b06e0cb694635e188c87a8a4175c9
ms.sourcegitcommit: c722760331294bc8532f8ddc01ed5aa8b9778dec
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2018
ms.locfileid: "34737262"
---
# <a name="reprotect-machines-from-azure-to-an-on-premises-site"></a>Machines van Azure naar een on-premises site opnieuw beveiligen

Na [failover](site-recovery-failover.md) van lokale virtuele VMware-machines of fysieke servers naar Azure, de eerste stap in mislukken terug naar uw on-premises site is de Azure VM's die zijn gemaakt tijdens de failover opnieuw beveiligen. Dit artikel wordt beschreven hoe u dit doet. 

Bekijk de volgende video over het failover van Azure naar een on-premises site voor een snel overzicht.<br /><br />
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="before-you-begin"></a>Voordat u begint

Als u een sjabloon voor het maken van uw virtuele machines, zorg ervoor dat elke virtuele machine heeft een eigen UUID voor de schijven gebruikt. Als de UUID van de lokale virtuele machine veroorzaakt een met de UUID van het hoofddoel conflict omdat beide zijn gemaakt met dezelfde sjabloon, mislukt de beveiligingspoging. Een andere hoofddoelserver is niet op basis van dezelfde sjabloon gemaakt implementeren. Let op de volgende informatie:
- Als u een failback naar een alternatieve vCenter wilt, ervoor zorgen dat uw nieuwe vCenter en de hoofddoelserver worden gedetecteerd. Een typische symptoom is dat de datastores zijn niet toegankelijk of niet zichtbaar zijn in de **beveiligt** in het dialoogvenster.
- Als u wilt repliceren naar on-premises, moet u een beleid voor failback. Dit beleid wordt automatisch gemaakt wanneer u een beleid vooruit maken. Let op de volgende informatie:
    - Dit beleid is gekoppeld aan de configuratieserver tijdens het maken van automatische.
    - Dit beleid niet meer worden bewerkt.
    - De setwaarden van het beleid zijn (RPO drempelwaarde = 15 minuten, herstel bewaarperiode = 24 uur, de frequentie van momentopnamen voor consistentie App = 60 minuten).
- Tijdens het beveiligingspoging en failback moet de lokale configuratie-server actief en verbonden.
- Als u een vCenter-server wordt beheerd voor de virtuele machines waarop u hebt een failback uit op, zorg ervoor dat u hebt de [machtigingen vereist](vmware-azure-tutorial-prepare-on-premises.md#prepare-an-account-for-automatic-discovery) voor detectie van virtuele machines op de vCenter-servers.
- Verwijder momentopnamen op de hoofddoelserver voordat u opnieuw beveiligen. Als u momentopnamen zijn aanwezig op het hoofddoel lokaal of op de virtuele machine, mislukt de beveiligingspoging. De momentopnamen op de virtuele machine worden automatisch samengevoegd tijdens een taak opnieuw beveiligen.
- Alle virtuele machines van een replicatiegroep moet van het hetzelfde type besturingssysteem (alle Windows of Linux alle). Een replicatiegroep met gemengde besturingssystemen momenteel wordt niet ondersteund voor beveiligt en failback naar on-premises. Dit is omdat het hoofddoel van hetzelfde besturingssysteem als de virtuele machine moet. De virtuele machines van een replicatiegroep moet het dezelfde hoofddoel hebben. 
- Een configuratieserver is vereist on-premises wanneer u een failback uit. Tijdens de failback, moet de virtuele machine zich in de configuratiedatabase van de server. Anders wordt de failback is mislukt. Zorg ervoor dat u regelmatig geplande back-ups van uw configuratieserver maken. Als er een ramp, de server met hetzelfde IP-adres herstellen zodat failback werkt.
- Opnieuw beveiliging inschakelen en failback moet een site-naar-site (S2S) VPN om gegevens te repliceren. Geef het netwerk zodat de failover virtuele machines in Azure (ping) de configuratie van de lokale server kunnen bereiken. Ook raadzaam om een processerver in de Azure-netwerk van de failover-virtuele machine te implementeren. Dit processerver moet ook communiceren met de lokale configuratie-server.
- Zorg ervoor dat u de volgende poorten voor failover en failback openen:

    ![Poorten voor failover en failback](./media/vmware-azure-reprotect/failover-failback.png)

- Lees alle de [vereisten voor de poorten en URL whitelisting](vmware-azure-deploy-configuration-server.md#prerequisites).

## <a name="deploy-a-process-server-in-azure"></a>Een processerver in Azure implementeren

Mogelijk moet u een processerver in Azure voordat u een failback naar uw on-premises site:
- De processerver ontvangt gegevens van de beveiligde virtuele machine in Azure en vervolgens verzendt gegevens naar de lokale site.
- Een traag netwerk is vereist tussen de processerver en de beveiligde virtuele machine. In het algemeen moet u rekening houden latentie bij het bepalen of u een processerver in Azure moet:
    - Als u een Azure ExpressRoute-verbinding instellen hebt, kunt u een on-premises processerver om gegevens te verzenden omdat de latentie tussen de virtuele machine en de processerver laag is.
    - Als u alleen een S2S-VPN hebt, is het echter raadzaam te implementeren van de processerver in Azure.
    - U wordt aangeraden met behulp van een op basis van een Azure-processerver tijdens failback. De prestaties van replicaties is hoger als de processerver dichter bij de replicerende virtuele machine (de failover-machine in Azure is). U kunt voor het testen van het concept, de processerver voor lokale en een ExpressRoute gebruiken met persoonlijke peering.

Een processerver in Azure implementeren:

1. Als u een processerver in Azure implementeren wilt, Zie [instellen van een processerver in Azure voor failback](vmware-azure-set-up-process-server-azure.md).
2. De Azure VM's verzenden gegevens van replicatie naar de processerver. Netwerken configureren zodat de Azure VM's de processerver bereiken kan.
3. Houd er rekening mee dat replicatie van Azure met on-premises kan alleen via de S2S VPN-verbinding of de persoonlijke peering van uw netwerk ExpressRoute gebeuren. Zorg ervoor dat er voldoende bandbreedte beschikbaar via dat netwerkkanaal is.

## <a name="deploy-a-separate-master-target-server"></a>Een afzonderlijke hoofddoelserver implementeren

De hoofddoelserver ontvangt failbackgegevens. De hoofddoelserver wordt standaard uitgevoerd op de on-premises configuratieserver. Afhankelijk van het volume is mislukt-back-verkeer moet u mogelijk echter maken van een afzonderlijke hoofddoelserver voor failback. Hier volgt een te maken:

* [Maken van een Linux-hoofddoelserver](vmware-azure-install-linux-master-target.md) voor failback van virtuele Linux-machines. Dit is vereist.
* Maak eventueel een afzonderlijke hoofddoelserver voor failback van virtuele machine van Windows. U doet dit door Unified Setup opnieuw uitvoeren en selecteer een hoofddoelserver maken. [Meer informatie](physical-azure-set-up-source.md#run-azure-site-recovery-unified-setup).

Nadat u een hoofddoelserver hebt gemaakt, kunt u het volgende doen:

- Als de virtuele machine aanwezig op lokaal op de vCenter-server is, moet de hoofddoelserver toegang tot de virtuele Machine schijf (VMDK)-bestand van de lokale virtuele machine. Toegang is vereist voor de gerepliceerde gegevens schrijven naar de schijven van de virtuele machine. Zorg ervoor dat de lokale virtuele machine gegevensopslag op het hoofddoel host met lees-/ schrijftoegang is gekoppeld.
- Als de virtuele machine niet aanwezig op lokaal op de vCenter-server, moet de Site Recovery-service een nieuwe virtuele machine maken tijdens de beveiligingspoging. Deze virtuele machine wordt gemaakt op de ESX-host waarop u het hoofddoel maakt. Kies de ESX-host zorgvuldig, zodat de failback van virtuele machine wordt gemaakt op de host die u wilt.
- U kunt Storage vMotion niet gebruiken voor de hoofddoelserver. Met Storage vMotion voor de hoofddoelserver kan ertoe leiden dat de failback mislukken. De virtuele machine kan niet worden gestart omdat de schijven niet beschikbaar voor deze. Om dit te voorkomen, uitsluiten van de master doelservers uw lijst met vMotion.
- Als een hoofddoel Storage vMotion taak na beveiligingspoging ondergaat, wordt de beveiligde virtuele machine-schijven die zijn gekoppeld aan het hoofddoel migreren naar het doel van de taak vMotion. Als u na deze mislukken, wordt loskoppelen van de schijf mislukt, omdat de schijven zijn niet gevonden. Vervolgens wordt het moeilijk te vinden van de schijven in uw storage-accounts. U moet deze handmatig zoeken en deze koppelt aan de virtuele machine. Hierna is kan de on-premises virtuele machine worden opgestart.
- Een bewaarstation toevoegen aan uw bestaande Windows-hoofddoelserver. Voeg een nieuwe schijf en formatteren van de schijf. Het bewaarstation wordt gebruikt voor het stoppen van de punten in de tijd wanneer de virtuele machine terug naar de lokale site gerepliceerd. Hier volgen enkele criteria van een bewaarstation. Als aan deze criteria zijn niet voldaan, wordt het station niet voor de hoofddoelserver vermeld:
    - Het volume wordt niet gebruikt voor andere doeleinden, zoals een doel van de replicatie.
    - Het volume is niet in de vergrendelingsmodus.
    - Het volume is niet een cachevolume. De installatie van de hoofddoelserver kan niet aanwezig op dat volume. Het volume van de aangepaste installatie voor de doel-proces model en de server is niet in aanmerking komen voor een bewaarvolume. Wanneer de processerver en de hoofddoelserver worden geïnstalleerd op een volume, is het volume een cachevolume van het hoofddoel.
    - Het type van het bestandssysteem van het volume is niet FAT of FAT32.
    - De capaciteit van het volume gelijk is aan nul.
    - Het bewaarvolume standaard voor Windows is het R-volume.
    - Het standaard bewaarvolume voor Linux is /mnt/retention.
- Als u een bestaand proces server of configuratieserver server of een schaal of proces server-master target servermachine, moet u een nieuwe schijf toevoegen. Het nieuwe station moet voldoen aan deze vereisten. Als het bewaarstation niet aanwezig is, wordt het niet weergegeven in de selectielijst van de vervolgkeuzelijst op de portal. Nadat u een station hebt toegevoegd aan het hoofddoel lokale, duurt het 15 minuten duren voordat het station moet worden weergegeven in de selectie op de portal. U kunt ook de configuratieserver vernieuwen als het station niet wordt weergegeven na 15 minuten.
- VMware-hulpprogramma's of open-vm-hulpprogramma's installeren op de hoofddoelserver. Zonder de hulpprogramma's, kan niet de datastores op het hoofddoel ESXi-host worden gedetecteerd.
- Stel de `disk.EnableUUID=true` instellen in de configuratieparameters van het hoofddoel virtuele machine in VMware. Als deze rij niet bestaat, moet u deze toevoegen. Deze instelling is vereist voor een consistente UUID bieden aan de VMDK zodat deze correct koppelt.
- De ESX-host waarop het hoofddoel wordt gemaakt, moet ten minste één virtuele machine file system (VMFS) datastore gekoppeld hebben. Als er geen datastores VMFS zijn gekoppeld, de **Datastore** invoer op de pagina opnieuw beveiligen leeg is en kan niet worden voortgezet.
- De hoofddoelserver kan geen momentopnamen op de schijven hebben. Als er momentopnamen, beveiligingspoging en failback is mislukt.
- Het hoofddoel kan niet een Paravirtuele SCSI-controller hebben. De controller kan alleen worden een LSI Logic-controller. Zonder een domeincontroller LSI Logic mislukt beveiligingspoging.
- Het hoofddoel kan maximaal 60 schijven die zijn gekoppeld aan deze hebben voor elk exemplaar. Als het aantal virtuele machines worden opnieuw beveiligd aan het hoofddoel lokale meer dan het totale aantal 60 schijven heeft reprotects aan het hoofddoel beginnen mislukken. Zorg ervoor dat er voldoende master schijf sleuven doel, of extra hoofddoelservers implementeren.
    

## <a name="enable-reprotection"></a>Beveiligingspoging inschakelen

Nadat een virtuele machine wordt opgestart in Azure, duurt het enige tijd voor de agent registreren terug naar de configuratieserver (maximaal 15 minuten). Gedurende deze periode wordt het niet mogelijk beveiligt en een foutbericht geeft aan dat de agent is niet geïnstalleerd. Als dit gebeurt, wacht een paar minuten en probeer het vervolgens opnieuw beveiligingspoging:


1. Selecteer **kluis** > **gerepliceerde items**. Met de rechtermuisknop op de virtuele machine die een failover uitgevoerd en selecteer vervolgens **opnieuw beveiligen**. Of, vanaf de opdrachtknoppen, selecteer de machine en selecteer vervolgens **opnieuw beveiligen**.
2. Controleer de **Azure met On-premises** richting van de beveiliging is ingeschakeld.
3. In **Hoofddoelserver** en **processerver**, selecteer de on-premises hoofddoelserver en de processerver.  
4. Voor **Datastore**, selecteert u het gegevensarchief waarnaar u herstellen van de schijven wilt on-premises. Deze optie wordt gebruikt wanneer de on-premises virtuele machine is verwijderd en moet u nieuwe schijven te maken. Deze optie wordt genegeerd als de schijven al bestaat. U moet nog steeds een waarde op te geven.
5. Selecteer het station bewaren.
6. Het failback-beleid wordt automatisch geselecteerd.
7. Selecteer **OK** om te beginnen met de beveiligingspoging. Er wordt een taak gestart voor het repliceren van de VM van Azure naar de on-premises site. U kunt de voortgang volgen op het tabblad **Taken**. Als de beveiligingspoging is geslaagd, krijgt de virtuele machine in een beveiligde status.

Let op de volgende informatie:
- Als u wilt herstellen naar een alternatieve locatie (wanneer de on-premises virtuele machine wordt verwijderd), selecteert u de bewaarstation en gegevensopslag die zijn geconfigureerd voor de hoofddoelserver. Wanneer u een failover naar de lokale site, de virtuele VMware-machines in de failback beveiligingsplan het hetzelfde gegevensarchief gebruiken als de hoofddoelserver. Een nieuwe virtuele machine wordt vervolgens gemaakt in vCenter.
- Als u herstellen van de virtuele machine in Azure een bestaande on-premises virtuele machine wilt, koppel datastores van de lokale virtuele machine met lees-/ schrijftoegang op de hoofddoelserver van ESXi-host.

    ![In het dialoogvenster opnieuw beveiligen](./media/vmware-azure-reprotect/reprotectinputs.png)

- U kunt ook op het niveau van een herstelplan beveiligt. Een replicatiegroep kan opnieuw worden beveiligd via een herstelplan alleen. Wanneer u met behulp van een herstelplan beveiligt, moet u de waarden opgeven voor elke beveiligde computer.
- Gebruik de dezelfde hoofddoelserver om een replicatiegroep opnieuw te beveiligen. Als u een andere hoofddoelserver aan een replicatiegroep beveiligt, opgeven niet de server een gemeenschappelijk punt in tijd.
- De on-premises virtuele machine is uitgeschakeld tijdens de beveiligingspoging. Dit helpt ervoor te zorgen dat gegevens tijdens de replicatie consistent blijven. Schakel niet op de virtuele machine nadat beveiligingspoging is voltooid.



## <a name="common-issues"></a>Algemene problemen

- Op dit moment ondersteunt Site Recovery mislukt back alleen naar een gegevensopslag VMFS of virtueel SAN. Een NFS-gegevensopslag wordt niet ondersteund. Vanwege deze beperking, de invoer van de selectie gegevensopslag op het scherm beveiligt is leeg voor NFS datastores of het gegevensarchief virtueel SAN bevat, maar tijdens de taak is mislukt. Als u van plan bent een failback, kunt u lokale voor VMFS gegevensopslag maken en weer terug naar het mislukken. Deze failback zorgt ervoor dat een volledige download van de VMDK.
- Als u een alleen-lezen vCenter-gebruikersdetectie uitvoeren en virtuele machines beveiligen, beveiliging is geslaagd en failover werkt. Tijdens de beveiligingspoging mislukt failover, omdat de datastores kan niet worden gedetecteerd. Een symptoom is dat de datastores tijdens beveiligingspoging worden niet vermeld. U lost dit probleem, kunt u de vCenter-referenties bijwerken met een juiste account dat machtigingen heeft en en probeer het opnieuw. 
- Wanneer u een failback uit op een virtuele Linux-machine en on-premises uitgevoerd, kunt u zien dat het pakket Network Manager is verwijderd van de machine. Deze verwijdering treedt op omdat het pakket Network Manager wordt verwijderd wanneer de virtuele machine in Azure is hersteld.
- Wanneer een virtuele Linux-machine is geconfigureerd met een statisch IP-adres en wordt een failover naar Azure, wordt het IP-adres verkregen van DHCP. Wanneer u een failover naar on-premises, blijft de virtuele machine het IP-adres verkrijgen via DHCP. Handmatig aanmelden bij de computer en vervolgens het IP-adres weer instellen op een statisch adres indien nodig. Het statische IP-adres kunt opnieuw verkrijgen van een virtuele Windows-computer.
- Als u de editie free van ESXi 5.5 of de editie vSphere 6 Hypervisor free, failover is uitgevoerd, maar failback niet lukt. Upgraden naar de evaluatielicentie beide programma zodat failback.
- Als u de configuratieserver van de processerver niet kan bereiken, moet u Telnet gebruiken om te controleren van de verbinding met de configuratieserver op poort 443. U kunt ook de configuratieserver van de processerver te pingen. Een processerver moet ook een heartbeat hebben wanneer deze verbonden met de configuratieserver.
- Een Windows Server 2008 R2 SP1-server die is beveiligd, omdat het een fysieke on-premises-server kan niet worden kan failback vanuit Azure een on-premises site.
- U afkeuren niet terug in de volgende omstandigheden:
    - U machines hebt gemigreerd naar Azure. [Meer informatie](migrate-overview.md#what-do-we-mean-by-migration).
    - U kunt een virtuele machine verplaatst naar een andere resourcegroep.
    - U hebt verwijderd de Azure VM.
    - U de beveiliging van de virtuele machine uitgeschakeld.
    - De virtuele machine die u in Azure handmatig gemaakt. De machine moet zijn in eerste instantie beveiligde lokale en een failover naar Azure voordat beveiligingspoging.
    - U kunt niet alleen een ESXi-host. U kunt geen failback VMware-machines of fysieke servers naar Hyper-V-hosts, fysieke machines of VMware-werkstations.


## <a name="next-steps"></a>Volgende stappen

Nadat de virtuele machine heeft een beschermd zijn ingevoerd, kunt u [initiëren van een failback](vmware-azure-failback.md). De failback van de virtuele machine in Azure wordt afgesloten en de on-premises virtuele machine wordt opgestart. Verwachten enige uitvaltijd voor de toepassing. Kies een tijd voor failback wanneer de toepassing uitvaltijd tolereren kan.



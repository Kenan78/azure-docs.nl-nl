---
title: Azure Monitor metrieken - ondersteunde metrische gegevens per resourcetype | Microsoft Docs
description: Lijst met metrische gegevens beschikbaar zijn voor elk resourcetype met Azure-Monitor.
author: anirudhcavale
manager: ashwink
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: ancav
ms.openlocfilehash: a5c0d529357d8ab92cf63ca4a0293753d55801d6
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/03/2018
---
# <a name="supported-metrics-with-azure-monitor"></a>Ondersteunde metrische gegevens met Azure-Monitor
Azure biedt verschillende manieren om te communiceren met metrische gegevens, inclusief grafieken ze in de portal of opvragen ze toegang hebben tot deze via de REST-API met PowerShell of CLI. Hieronder volgt een volledige lijst met alle metrische gegevens op dit moment met metrische gegevens van de Monitor van het Azure-pipeline. Het is mogelijk dat andere metrische gegevens beschikbaar zijn in de portal of met oudere API's. Deze lijst hieronder bevat alleen beschikbaar via de geconsolideerde Azure Monitor metrische pijplijn metrische gegevens. Zoeken naar en toegang hebben tot deze metrische gegevens gebruik de [2018-01-01-api-versie](https://docs.microsoft.com/rest/api/monitor/metricdefinitions)

> [!NOTE]
> Het verzenden van multidimensionale metrische gegevens via diagnostische instellingen wordt momenteel niet ondersteund. Metrische gegevens met dimensies worden geëxporteerd als platte eendimensionale metrische gegevens, als totaal van alle dimensiewaarden.
>
> *Een voorbeeld*: de metriek 'Binnenkomende berichten' voor een Event Hub kan worden verkend en uitgezet op wachtrijniveau. Maar wanneer de metriek wordt geëxporteerd via diagnostische instellingen, geeft de metriek alle binnenkomende berichten in alle wachtrijen in de Event Hub aan.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|qpu_metric|QPU|Count|Gemiddeld|QPU. Bereik 0-100 voor S1, 0-200 voor S2 en 0-400 voor S4|ServerResourceType|
|memory_metric|Geheugen|Bytes|Gemiddeld|Geheugen. Bereik van 0-25 GB voor S1, 0-50 GB voor S2 en 0-100 GB voor S4|ServerResourceType|
|TotalConnectionRequests|Totaal aantal verbindingsaanvragen|Count|Gemiddeld|Totaal aantal verbindingsaanvragen. Dit zijn ontvangsten.|ServerResourceType|
|SuccessfullConnectionsPerSec|Geslaagde verbindingen Per seconde|CountPerSecond|Gemiddeld|Verhouding van geslaagde verbinding voltooiingen.|ServerResourceType|
|TotalConnectionFailures|Totaal aantal verbindingsfouten|Count|Gemiddeld|Totaal aantal mislukte verbindingspogingen.|ServerResourceType|
|CurrentUserSessions|Huidige gebruikerssessies|Count|Gemiddeld|Huidige aantal gebruikerssessies.|ServerResourceType|
|QueryPoolBusyThreads|Query groepen bezet Threads|Count|Gemiddeld|Het aantal bezet threads in de query-thread-groep.|ServerResourceType|
|CommandPoolJobQueueLength|Opdracht taak wachtrijlengte|Count|Gemiddeld|Het aantal taken in de wachtrij van de threadgroep opdracht.|ServerResourceType|
|ProcessingPoolJobQueueLength|Wachtrijlengte taak verwerken|Count|Gemiddeld|Het aantal niet-I/O-taken in de wachtrij van de thread-pool.|ServerResourceType|
|CurrentConnections|Verbinding: Actieve verbindingen|Count|Gemiddeld|Huidig aantal verbindingen van clients tot stand gebracht.|ServerResourceType|
|CleanerCurrentPrice|Geheugen: Schonere huidige prijs|Count|Gemiddeld|Huidige prijs geheugen, byte-$/ tijd, genormaliseerd tot en met 1000.|ServerResourceType|
|CleanerMemoryShrinkable|Geheugen: Schonere geheugen verkleining|Bytes|Gemiddeld|De hoeveelheid geheugen in bytes, onderworpen aan een schoner opschonen door de achtergrond.|ServerResourceType|
|CleanerMemoryNonshrinkable|Geheugen: Schonere geheugen nonshrinkable|Bytes|Gemiddeld|Hoeveelheid geheugen in bytes niet onderworpen aan een schoner opschonen door de achtergrond.|ServerResourceType|
|MemoryUsage|: Geheugengebruik geheugen|Bytes|Gemiddeld|Het geheugengebruik van de server-proces gebruikt bij het berekenen van de prijs van schonere geheugen. Die gelijk is aan het prestatiemeteritem Process\PrivateBytes plus de grootte van het geheugen toegewezen gegevens, die is toegewezen of door de xVelocity in het geheugen analyse-engine (VertiPaq) die groter zijn dan de engine xVelocity geheugenlimiet toegewezen geheugen wordt genegeerd.|ServerResourceType|
|MemoryLimitHard|Geheugen: Geheugenlimiet harde|Bytes|Gemiddeld|Vaste geheugenlimiet uit het configuratiebestand.|ServerResourceType|
|MemoryLimitHigh|Geheugen: Geheugen beperken hoog|Bytes|Gemiddeld|Maximale geheugenlimiet van configuratiebestand.|ServerResourceType|
|MemoryLimitLow|Geheugen: Geheugen limiet laag|Bytes|Gemiddeld|Lage geheugenlimiet uit het configuratiebestand.|ServerResourceType|
|MemoryLimitVertiPaq|Geheugen: Geheugen limiet VertiPaq|Bytes|Gemiddeld|In het geheugen limiet uit het configuratiebestand.|ServerResourceType|
|Quota|Geheugen: quotum|Bytes|Gemiddeld|Huidige geheugenquotum, in bytes. Geheugenquotum wordt ook wel een grant of geheugen reservering voor geheugen.|ServerResourceType|
|QuotaBlocked|: Geheugenquotum geblokkeerd|Count|Gemiddeld|Huidig aantal quotum aanvragen die worden geblokkeerd totdat het andere Geheugenquota zijn vrijgegeven.|ServerResourceType|
|VertiPaqNonpaged|Geheugen: VertiPaq-wisselbaar geheugen:|Bytes|Gemiddeld|Bytes van geheugen is vergrendeld in de werkset voor gebruik door de engine in het geheugen.|ServerResourceType|
|VertiPaqPaged|Geheugen: VertiPaq wisselbaar geheugen:|Bytes|Gemiddeld|Bytes wisselbaar geheugen in gebruik voor gegevens in het geheugen.|ServerResourceType|
|RowsReadPerSec|Verwerking: Rijen lezen per seconde|CountPerSecond|Gemiddeld|Het aantal rijen van alle relationele databases worden gelezen.|ServerResourceType|
|RowsConvertedPerSec|Verwerking: Rijen geconverteerd per seconde|CountPerSecond|Gemiddeld|Het aantal rijen wordt geconverteerd tijdens de verwerking.|ServerResourceType|
|RowsWrittenPerSec|Verwerking: Rijen geschreven per seconde|CountPerSecond|Gemiddeld|De frequentie van geschreven tijdens het verwerken van rijen.|ServerResourceType|
|CommandPoolBusyThreads|Threads: Opdracht groepen bezet threads|Count|Gemiddeld|Het aantal bezet threads in de opdracht thread-groep.|ServerResourceType|
|CommandPoolIdleThreads|Threads: Opdracht groep niet-actieve threads|Count|Gemiddeld|Het aantal niet-actieve threads in de opdracht thread-groep.|ServerResourceType|
|LongParsingBusyThreads|Threads: Long bezet threads parseren|Count|Gemiddeld|Het aantal bezet threads in de lang parseren thread-groep.|ServerResourceType|
|LongParsingIdleThreads|Threads: Long bij het parseren van niet-actieve threads|Count|Gemiddeld|Het aantal niet-actieve threads in de lang parseren thread-groep.|ServerResourceType|
|LongParsingJobQueueLength|Threads: Parseren lang taak wachtrijlengte|Count|Gemiddeld|Het aantal taken in de wachtrij van de threadgroep lang parseren.|ServerResourceType|
|ProcessingPoolBusyIOJobThreads|Threads: Groepen bezet i/o-taak threads verwerken|Count|Gemiddeld|Het aantal actieve threads i/o-taken in de thread-pool.|ServerResourceType|
|ProcessingPoolBusyNonIOThreads|Threads: Groep bezet niet-I/O-threads verwerkt|Count|Gemiddeld|Het aantal threads worden uitgevoerd van niet-I/O-taken in de thread-pool.|ServerResourceType|
|ProcessingPoolIOJobQueueLength|Threads: Verwerken i/o-taak wachtrijlengte van toepassingen|Count|Gemiddeld|Het aantal i/o-taken in de wachtrij van de thread-pool.|ServerResourceType|
|ProcessingPoolIdleIOJobThreads|Threads: Groep niet-actieve i/o-taak threads verwerken|Count|Gemiddeld|Het aantal niet-actieve threads voor i/o-taken in de thread-pool.|ServerResourceType|
|ProcessingPoolIdleNonIOThreads|Threads: Groep niet-actieve niet-I/O-threads verwerken|Count|Gemiddeld|Het aantal niet-actieve threads in de thread-pool toegewezen aan niet-I/O-taken.|ServerResourceType|
|QueryPoolIdleThreads|Threads: Query groep niet-actieve threads|Count|Gemiddeld|Het aantal niet-actieve threads voor i/o-taken in de thread-pool.|ServerResourceType|
|QueryPoolJobQueueLength|Threads: Query groep taak wachtrij lengt|Count|Gemiddeld|Het aantal taken in de wachtrij van de threadgroep query.|ServerResourceType|
|ShortParsingBusyThreads|Threads: Korte bezet threads parseren|Count|Gemiddeld|Het aantal bezet threads in de korte parseren thread-groep.|ServerResourceType|
|ShortParsingIdleThreads|Threads: Korte bij het parseren van niet-actieve threads|Count|Gemiddeld|Het aantal niet-actieve threads in de korte parseren thread-groep.|ServerResourceType|
|ShortParsingJobQueueLength|Threads: Korte wachtrijlengte taak parseren|Count|Gemiddeld|Het aantal taken in de wachtrij van de threadgroep voor korte parseren.|ServerResourceType|
|memory_thrashing_metric|Geheugen voorkomen|Procent|Gemiddeld|Gemiddelde geheugen thrashing.|ServerResourceType|
|mashup_engine_qpu_metric|M-Engine QPU|Count|Gemiddeld|Gebruik QPU door mashup-engine-processen|ServerResourceType|
|mashup_engine_memory_metric|M-Engine-geheugen|Bytes|Gemiddeld|Geheugengebruik door processen voor mashup-engine|ServerResourceType|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TotalRequests|Totaal aantal Gateway aanvragen|Count|Totaal|Het aantal aanvragen van de gateway|Locatie, hostnaam|
|SuccessfulRequests|De Gateway aanvragen|Count|Totaal|Aantal geslaagde gateway aanvragen|Locatie, hostnaam|
|UnauthorizedRequests|Niet-geautoriseerde Gateway aanvragen|Count|Totaal|Het aantal niet-geautoriseerde gateway aanvragen|Locatie, hostnaam|
|FailedRequests|Mislukte Gateway aanvragen|Count|Totaal|Aantal fouten in gateway aanvragen|Locatie, hostnaam|
|OtherRequests|Andere Gateway aanvragen|Count|Totaal|Aantal andere gateway aanvragen|Locatie, hostnaam|
|Duur|Totale duur van de Gateway aanvragen|Milliseconden|Gemiddeld|Totale duur van de Gateway-aanvragen in milliseconden|Locatie, hostnaam|
|Capaciteit|Capaciteit (Preview)|Procent|Gemiddeld|Gebruik van metrische gegevens voor ApiManagement service|Locatie|

## <a name="microsoftautomationautomationaccounts"></a>Microsoft.Automation/automationAccounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TotalJob|Totaal aantal taken|Count|Totaal|Het totale aantal taken|Runbook-Status|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|CoreCount|Speciale Core-telling|Count|Totaal|Totale aantal toegewezen kernen in de batch-account|Er zijn geen dimensies|
|TotalNodeCount|Aantal toegewezen knooppunten|Count|Totaal|Totale aantal toegewezen knooppunten in het batch-account|Er zijn geen dimensies|
|LowPriorityCoreCount|Core-telling LowPriority|Count|Totaal|Totaal aantal kernen prioriteit laag in de batch-account|Er zijn geen dimensies|
|TotalLowPriorityNodeCount|Aantal knooppunten met lage prioriteit|Count|Totaal|Totale aantal knooppunten in de batch-account lage prioriteit|Er zijn geen dimensies|
|CreatingNodeCount|Aantal knooppunten maken|Count|Totaal|Het aantal knooppunten dat wordt gemaakt|Er zijn geen dimensies|
|StartingNodeCount|Aantal knooppunten wordt gestart|Count|Totaal|Het aantal knooppunten starten|Er zijn geen dimensies|
|WaitingForStartTaskNodeCount|Wachttijd voor begin taak aantal knooppunten|Count|Totaal|Het aantal knooppunten die wachten op de taak starten is voltooid|Er zijn geen dimensies|
|StartTaskFailedNodeCount|Begintaak aantal knooppunten is mislukt|Count|Totaal|Het aantal knooppunten waar de taak starten is mislukt|Er zijn geen dimensies|
|IdleNodeCount|Aantal niet-actieve knooppunten|Count|Totaal|Aantal niet-actieve knooppunten|Er zijn geen dimensies|
|OfflineNodeCount|Aantal offline knooppunten|Count|Totaal|Aantal knooppunten dat offline|Er zijn geen dimensies|
|RebootingNodeCount|Aantal knooppunten aan het opstarten|Count|Totaal|Het aantal knooppunten aan het opstarten|Er zijn geen dimensies|
|ReimagingNodeCount|Aantal knooppunten teruggezet|Count|Totaal|Het aantal knooppunten teruggezet|Er zijn geen dimensies|
|RunningNodeCount|Aantal actieve knooppunten|Count|Totaal|Aantal actieve knooppunten|Er zijn geen dimensies|
|LeavingPoolNodeCount|Aantal van de knooppunten groep verlaten|Count|Totaal|Aantal knooppunten dat de groep verlaten|Er zijn geen dimensies|
|UnusableNodeCount|Aantal onbruikbaar knooppunten|Count|Totaal|Aantal onbruikbaar knooppunten|Er zijn geen dimensies|
|PreemptedNodeCount|Aantal knooppunten afgebroken|Count|Totaal|Aantal afgebroken knooppunten|Er zijn geen dimensies|
|TaskStartEvent|Taak Start gebeurtenissen|Count|Totaal|Totaal aantal taken die zijn gestart|Er zijn geen dimensies|
|TaskCompleteEvent|Taak Complete-gebeurtenissen|Count|Totaal|Totale aantal taken die zijn voltooid|Er zijn geen dimensies|
|TaskFailEvent|Gebeurtenissen van taak mislukt|Count|Totaal|Totaal aantal taken die in een foutstatus voltooid|Er zijn geen dimensies|
|PoolCreateEvent|Gebeurtenissen van toepassingen maken|Count|Totaal|Totale aantal groepen die zijn gemaakt|Er zijn geen dimensies|
|PoolResizeStartEvent|Groep van toepassingen starten formaatwijzigingen|Count|Totaal|Totaal aantal toepassingen Hiermee wordt de grootte die zijn gestart|Er zijn geen dimensies|
|PoolResizeCompleteEvent|Groep formaat Complete-gebeurtenissen|Count|Totaal|Totaal aantal toepassingen Hiermee wordt de grootte die zijn voltooid|Er zijn geen dimensies|
|PoolDeleteStartEvent|Gebeurtenissen van toepassingen starten|Count|Totaal|Totaal aantal toepassingen verwijderen die zijn gestart|Er zijn geen dimensies|
|PoolDeleteCompleteEvent|Toepassingen verwijderen Complete-gebeurtenissen|Count|Totaal|Totaal aantal toepassingen verwijderen die zijn voltooid|Er zijn geen dimensies|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|connectedclients|Gekoppelde clients|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed|Totaal aantal bewerkingen|Count|Totaal||Er zijn geen dimensies|
|cachehits|Cachetreffers|Count|Totaal||Er zijn geen dimensies|
|cachemisses|Cachemissers|Count|Totaal||Er zijn geen dimensies|
|getcommands|Opgehaalde items|Count|Totaal||Er zijn geen dimensies|
|setcommands|Sets|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond|Bewerkingen Per seconde|Count|Totaal||Er zijn geen dimensies|
|evictedkeys|Verwijderde sleutels|Count|Totaal||Er zijn geen dimensies|
|totalkeys|Totaal aantal sleutels|Count|Maximum||Er zijn geen dimensies|
|expiredkeys|Verlopen sleutels|Count|Totaal||Er zijn geen dimensies|
|usedmemory|Gebruikt geheugen|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss|Gebruikt geheugen RSS|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad|Serverbelasting|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite|Cache schrijven|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead|Gelezen uit cache|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime|CPU|Procent|Maximum||Er zijn geen dimensies|
|connectedclients0|Verbonden Clients (Shard 0)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed0|Totaal aantal bewerkingen (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|cachehits0|Treffers in cache (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|cachemisses0|Cachemissers (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|getcommands0|Opgehaald (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|setcommands0|Sets (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond0|Bewerkingen Per seconde (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys0|Verwijderde sleutels (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|totalkeys0|Totale aantal sleutels (Shard 0)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys0|Verlopen sleutels (Shard 0)|Count|Totaal||Er zijn geen dimensies|
|usedmemory0|Gebruikt geheugen (Shard 0)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss0|Gebruikt geheugen RSS (Shard 0)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad0|Belasting van de server (Shard 0)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite0|Cache schrijven (Shard 0)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead0|Cache lezen (Shard 0)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime0|CPU (Shard 0)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients1|Verbonden Clients (Shard 1)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed1|Totaal aantal bewerkingen (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|cachehits1|Treffers in cache (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|cachemisses1|Cachemissers (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|getcommands1|Opgehaald (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|setcommands1|Sets (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond1|Bewerkingen Per seconde (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys1|Verwijderde sleutels (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|totalkeys1|Totale aantal sleutels (Shard 1)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys1|Verlopen sleutels (Shard 1)|Count|Totaal||Er zijn geen dimensies|
|usedmemory1|Gebruikt geheugen (Shard 1)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss1|Gebruikt geheugen RSS (Shard 1)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad1|Belasting van de server (Shard 1)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite1|Cache schrijven (Shard 1)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead1|Cache lezen (Shard 1)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime1|CPU (Shard 1)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients2|Verbonden Clients (Shard 2)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed2|Totaal aantal bewerkingen (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|cachehits2|Treffers in cache (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|cachemisses2|Cachemissers (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|getcommands2|Opgehaald (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|setcommands2|Sets (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond2|Bewerkingen Per seconde (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys2|Verwijderde sleutels (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|totalkeys2|Totale aantal sleutels (Shard 2)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys2|Verlopen sleutels (Shard 2)|Count|Totaal||Er zijn geen dimensies|
|usedmemory2|Gebruikt geheugen (Shard 2)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss2|Gebruikt geheugen RSS (Shard 2)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad2|Belasting van de server (Shard 2)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite2|Cache schrijven (Shard 2)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead2|Cache lezen (Shard 2)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime2|CPU (Shard 2)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients3|Verbonden Clients (Shard 3)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed3|Totaal aantal bewerkingen (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|cachehits3|Treffers in cache (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|cachemisses3|Cachemissers (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|getcommands3|Opgehaald (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|setcommands3|Sets (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond3|Bewerkingen Per seconde (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys3|Verwijderde sleutels (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|totalkeys3|Totale aantal sleutels (Shard 3)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys3|Verlopen sleutels (Shard 3)|Count|Totaal||Er zijn geen dimensies|
|usedmemory3|Gebruikt geheugen (Shard 3)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss3|Gebruikt geheugen RSS (Shard 3)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad3|Belasting van de server (Shard 3)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite3|Cache schrijven (Shard 3)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead3|Cache lezen (Shard 3)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime3|CPU (Shard 3)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients4|Verbonden Clients (Shard 4)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed4|Totaal aantal bewerkingen (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|cachehits4|Treffers in cache (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|cachemisses4|Cachemissers (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|getcommands4|Opgehaald (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|setcommands4|Sets (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond4|Bewerkingen Per seconde (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys4|Verwijderde sleutels (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|totalkeys4|Totale aantal sleutels (Shard 4)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys4|Verlopen sleutels (Shard 4)|Count|Totaal||Er zijn geen dimensies|
|usedmemory4|Gebruikt geheugen (Shard 4)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss4|Gebruikt geheugen RSS (Shard 4)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad4|Belasting van de server (Shard 4)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite4|Cache schrijven (Shard 4)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead4|Cache lezen (Shard 4)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime4|CPU (Shard 4)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients5|Verbonden Clients (Shard 5)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed5|Totaal aantal bewerkingen (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|cachehits5|Treffers in cache (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|cachemisses5|Cachemissers (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|getcommands5|Opgehaald (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|setcommands5|Sets (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond5|Bewerkingen Per seconde (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys5|Verwijderde sleutels (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|totalkeys5|Totale aantal sleutels (Shard 5)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys5|Verlopen sleutels (Shard 5)|Count|Totaal||Er zijn geen dimensies|
|usedmemory5|Gebruikt geheugen (Shard 5)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss5|Gebruikt geheugen RSS (Shard 5)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad5|Belasting van de server (Shard 5)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite5|Cache schrijven (Shard 5)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead5|Cache lezen (Shard 5)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime5|CPU (Shard 5)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients6|Verbonden Clients (Shard 6)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed6|Totaal aantal bewerkingen (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|cachehits6|Treffers in cache (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|cachemisses6|Cachemissers (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|getcommands6|Opgehaald (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|setcommands6|Sets (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond6|Bewerkingen Per seconde (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys6|Verwijderde sleutels (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|totalkeys6|Totale aantal sleutels (Shard 6)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys6|Verlopen sleutels (Shard 6)|Count|Totaal||Er zijn geen dimensies|
|usedmemory6|Gebruikt geheugen (Shard 6)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss6|Gebruikt geheugen RSS (Shard 6)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad6|Belasting van de server (Shard 6)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite6|Cache schrijven (Shard 6)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead6|Cache lezen (Shard 6)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime6|CPU (Shard 6)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients7|Verbonden Clients (Shard 7)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed7|Totaal aantal bewerkingen (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|cachehits7|Treffers in cache (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|cachemisses7|Cachemissers (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|getcommands7|Opgehaald (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|setcommands7|Sets (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond7|Bewerkingen Per seconde (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys7|Verwijderde sleutels (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|totalkeys7|Totale aantal sleutels (Shard 7)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys7|Verlopen sleutels (Shard 7)|Count|Totaal||Er zijn geen dimensies|
|usedmemory7|Gebruikt geheugen (Shard 7)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss7|Gebruikt geheugen RSS (Shard 7)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad7|Belasting van de server (Shard 7)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite7|Cache schrijven (Shard 7)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead7|Cache lezen (Shard 7)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime7|CPU (Shard 7)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients8|Verbonden Clients (Shard 8)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed8|Totaal aantal bewerkingen (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|cachehits8|Treffers in cache (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|cachemisses8|Cachemissers (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|getcommands8|(Shard 8) opgehaald|Count|Totaal||Er zijn geen dimensies|
|setcommands8|Sets (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond8|Bewerkingen Per seconde (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys8|Verwijderde sleutels (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|totalkeys8|Totale aantal sleutels (Shard 8)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys8|Verlopen sleutels (Shard 8)|Count|Totaal||Er zijn geen dimensies|
|usedmemory8|Gebruikt geheugen (Shard 8)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss8|Gebruikt geheugen RSS (Shard 8)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad8|Belasting van de server (Shard 8)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite8|Cache schrijven (Shard 8)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead8|Cache lezen (Shard 8)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime8|CPU (Shard 8)|Procent|Maximum||Er zijn geen dimensies|
|connectedclients9|Verbonden Clients (Shard 9)|Count|Maximum||Er zijn geen dimensies|
|totalcommandsprocessed9|Totaal aantal bewerkingen (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|cachehits9|Treffers in cache (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|cachemisses9|Cachemissers (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|getcommands9|Opgehaald (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|setcommands9|Sets (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|operationsPerSecond9|Bewerkingen Per seconde (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|evictedkeys9|Verwijderde sleutels (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|totalkeys9|Totale aantal sleutels (Shard 9)|Count|Maximum||Er zijn geen dimensies|
|expiredkeys9|Verlopen sleutels (Shard 9)|Count|Totaal||Er zijn geen dimensies|
|usedmemory9|Gebruikt geheugen (Shard 9)|Bytes|Maximum||Er zijn geen dimensies|
|usedmemoryRss9|Gebruikt geheugen RSS (Shard 9)|Bytes|Maximum||Er zijn geen dimensies|
|serverLoad9|Belasting van de server (Shard 9)|Procent|Maximum||Er zijn geen dimensies|
|cacheWrite9|Cache schrijven (Shard 9)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|cacheRead9|Cache lezen (Shard 9)|BytesPerSecond|Maximum||Er zijn geen dimensies|
|percentProcessorTime9|CPU (Shard 9)|Procent|Maximum||Er zijn geen dimensies|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.ClassicCompute/virtualMachines

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Procent|Gemiddeld|Het percentage toegewezen berekeningseenheden dat momenteel door de virtuele machine(s) wordt gebruikt.|Er zijn geen dimensies|
|Netwerk in|Netwerk in|Bytes|Totaal|Het aantal ontvangen bytes op alle netwerkinterfaces door de virtuele machine(s) (binnenkomend verkeer).|Er zijn geen dimensies|
|Netwerk uit|Netwerk uit|Bytes|Totaal|Het aantal verzonden bytes op alle netwerkinterfaces door de virtuele machine(s) (uitgaand verkeer).|Er zijn geen dimensies|
|Gelezen bytes per seconde op de schijf|Schijf lezen|BytesPerSecond|Gemiddeld|Gemiddeld aantal gelezen bytes op de schijf tijdens de controleperiode.|Er zijn geen dimensies|
|Geschreven bytes per seconde|Schijf schrijven|BytesPerSecond|Gemiddeld|Gemiddeld aantal geschreven bytes op de schijf tijdens de controleperiode.|Er zijn geen dimensies|
|Leesbewerkingen op de schijf/seconde|Leesbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Gelezen IOP's op de schijf.|Er zijn geen dimensies|
|Schrijfbewerkingen op de schijf/seconde|Schrijfbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Geschreven IOP's op de schijf.|Er zijn geen dimensies|

## <a name="microsoftclassiccomputedomainnamesslotsroles"></a>Microsoft.ClassicCompute/domainNames/slots/roles

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Procent|Gemiddeld|Het percentage toegewezen berekeningseenheden dat momenteel door de virtuele machine(s) wordt gebruikt.|Er zijn geen dimensies|
|Netwerk in|Netwerk in|Bytes|Totaal|Het aantal ontvangen bytes op alle netwerkinterfaces door de virtuele machine(s) (binnenkomend verkeer).|Er zijn geen dimensies|
|Netwerk uit|Netwerk uit|Bytes|Totaal|Het aantal verzonden bytes op alle netwerkinterfaces door de virtuele machine(s) (uitgaand verkeer).|Er zijn geen dimensies|
|Gelezen bytes per seconde op de schijf|Schijf lezen|BytesPerSecond|Gemiddeld|Gemiddeld aantal gelezen bytes op de schijf tijdens de controleperiode.|Er zijn geen dimensies|
|Geschreven bytes per seconde|Schijf schrijven|BytesPerSecond|Gemiddeld|Gemiddeld aantal geschreven bytes op de schijf tijdens de controleperiode.|Er zijn geen dimensies|
|Leesbewerkingen op de schijf/seconde|Leesbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Gelezen IOP's op de schijf.|Er zijn geen dimensies|
|Schrijfbewerkingen op de schijf/seconde|Schrijfbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Geschreven IOP's op de schijf.|Er zijn geen dimensies|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TotalCalls|Totaal aantal aanroepen|Count|Totaal|Totaal aantal aanroepen.|Er zijn geen dimensies|
|SuccessfulCalls|Geslaagde aanroepen|Count|Totaal|Aantal geslaagde aanroepen.|Er zijn geen dimensies|
|TotalErrors|Totaal aantal fouten|Count|Totaal|Het totaal aantal aanroepen met een foutbericht (HTTP-antwoordcode 4xx of 5xx).|Er zijn geen dimensies|
|BlockedCalls|Geblokkeerde aanroepen|Count|Totaal|Het aantal aanroepen die de tarief- of quotumlimiet hebben overschreden.|Er zijn geen dimensies|
|ServerErrors|Serverfouten|Count|Totaal|Het aantal aanroepen met een interne servicefout (HTTP-responscode 5xx).|Er zijn geen dimensies|
|ClientErrors|Clientfouten|Count|Totaal|Het aantal aanroepen met een fout aan de clientzijde (HTTP-responscode 4xx).|Er zijn geen dimensies|
|DataIn|Inkomende gegevens|Bytes|Totaal|Grootte van inkomende gegevens in bytes.|Er zijn geen dimensies|
|DataOut|Uitgaande gegevens|Bytes|Totaal|Grootte van uitgaande gegevens in bytes.|Er zijn geen dimensies|
|Latentie|Latentie|MilliSeconds|Gemiddeld|Latentie in milliseconden|Er zijn geen dimensies|
|CharactersTranslated|Tekens vertaald|Count|Totaal|Totaal aantal tekens in inkomende tekstaanvraag.|Er zijn geen dimensies|
|SpeechSessionDuration|Duur van de spraaksessie|Seconden|Totaal|Totale duur van de spraaksessie in seconden.|Er zijn geen dimensies|
|TotalTransactions|Totaal aantal transacties|Count|Totaal|Totaal aantal transacties|Er zijn geen dimensies|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Procent|Gemiddeld|Het percentage toegewezen berekeningseenheden dat momenteel door de virtuele machine(s) wordt gebruikt|Er zijn geen dimensies|
|Netwerk in|Netwerk in|Bytes|Totaal|Het aantal ontvangen bytes op alle netwerkinterfaces door de virtuele machine(s) (binnenkomend verkeer)|Er zijn geen dimensies|
|Netwerk uit|Netwerk uit|Bytes|Totaal|Het aantal verzonden bytes op alle netwerkinterfaces door de virtuele machine(s) (uitgaand verkeer)|Er zijn geen dimensies|
|Gelezen bytes op de schijf|Gelezen bytes op de schijf|Bytes|Totaal|Totaal aantal gelezen bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Geschreven bytes op de schijf|Geschreven bytes op de schijf|Bytes|Totaal|Totaal aantal geschreven bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Leesbewerkingen op de schijf/seconde|Leesbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Gelezen IOP's op de schijf|Er zijn geen dimensies|
|Schrijfbewerkingen op de schijf/seconde|Schrijfbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Geschreven IOP's op de schijf|Er zijn geen dimensies|
|Resterend CPU-tegoed|Resterend CPU-tegoed|Count|Gemiddeld|Totale tegoed beschikbaar voor burst|Er zijn geen dimensies|
|Verbruikt CPU-tegoed|Verbruikt CPU-tegoed|Count|Gemiddeld|Totale tegoed gebruikt door de virtuele machine|Er zijn geen dimensies|
|Per gelezen Bytes per seconde|Gegevens van gelezen Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per schijf geschreven Bytes per seconde|Gegevens geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode bewaking|Sleuf|
|Per schijf leesbewerkingen per seconde|Gegevens gelezen-bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per geschreven bewerkingen per seconde|Gegevens geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode bewaking|Sleuf|
|Per schijf Wachtrijdiepte|Gegevensschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Gegevens wachtrijdiepte van schijf (of wachtrijlengte)|Sleuf|
|OS Per schijf gelezen Bytes per seconde|OS-schijf gelezen Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf geschreven Bytes per seconde|OS-schijf geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf leesbewerkingen per seconde|Besturingssysteemschijf leesbewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf schrijfbewerkingen per seconde|OS geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf Wachtrijdiepte|Besturingssysteemschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Besturingssysteemschijf wachtrijdiepte (of wachtrijlengte)|Er zijn geen dimensies|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Procent|Gemiddeld|Het percentage toegewezen berekeningseenheden dat momenteel door de virtuele machine(s) wordt gebruikt|Er zijn geen dimensies|
|Netwerk in|Netwerk in|Bytes|Totaal|Het aantal ontvangen bytes op alle netwerkinterfaces door de virtuele machine(s) (binnenkomend verkeer)|Er zijn geen dimensies|
|Netwerk uit|Netwerk uit|Bytes|Totaal|Het aantal verzonden bytes op alle netwerkinterfaces door de virtuele machine(s) (uitgaand verkeer)|Er zijn geen dimensies|
|Gelezen bytes op de schijf|Gelezen bytes op de schijf|Bytes|Totaal|Totaal aantal gelezen bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Geschreven bytes op de schijf|Geschreven bytes op de schijf|Bytes|Totaal|Totaal aantal geschreven bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Leesbewerkingen op de schijf/seconde|Leesbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Gelezen IOP's op de schijf|Er zijn geen dimensies|
|Schrijfbewerkingen op de schijf/seconde|Schrijfbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Geschreven IOP's op de schijf|Er zijn geen dimensies|
|Resterend CPU-tegoed|Resterend CPU-tegoed|Count|Gemiddeld|Totale tegoed beschikbaar voor burst|Er zijn geen dimensies|
|Verbruikt CPU-tegoed|Verbruikt CPU-tegoed|Count|Gemiddeld|Totale tegoed gebruikt door de virtuele machine|Er zijn geen dimensies|
|Per gelezen Bytes per seconde|Gegevens van gelezen Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per schijf geschreven Bytes per seconde|Gegevens geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode bewaking|Sleuf|
|Per schijf leesbewerkingen per seconde|Gegevens gelezen-bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per geschreven bewerkingen per seconde|Gegevens geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode bewaking|Sleuf|
|Per schijf Wachtrijdiepte|Gegevensschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Gegevens wachtrijdiepte van schijf (of wachtrijlengte)|Sleuf|
|OS Per schijf gelezen Bytes per seconde|OS-schijf gelezen Bytes per seconde|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf geschreven Bytes per seconde|OS-schijf geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf leesbewerkingen per seconde|Besturingssysteemschijf leesbewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf schrijfbewerkingen per seconde|OS geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf Wachtrijdiepte|Besturingssysteemschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Besturingssysteemschijf wachtrijdiepte (of wachtrijlengte)|Er zijn geen dimensies|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Percentage CPU|Percentage CPU|Procent|Gemiddeld|Het percentage toegewezen berekeningseenheden dat momenteel door de virtuele machine(s) wordt gebruikt|Er zijn geen dimensies|
|Netwerk in|Netwerk in|Bytes|Totaal|Het aantal ontvangen bytes op alle netwerkinterfaces door de virtuele machine(s) (binnenkomend verkeer)|Er zijn geen dimensies|
|Netwerk uit|Netwerk uit|Bytes|Totaal|Het aantal verzonden bytes op alle netwerkinterfaces door de virtuele machine(s) (uitgaand verkeer)|Er zijn geen dimensies|
|Gelezen bytes op de schijf|Gelezen bytes op de schijf|Bytes|Totaal|Totaal aantal gelezen bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Geschreven bytes op de schijf|Geschreven bytes op de schijf|Bytes|Totaal|Totaal aantal geschreven bytes op de schijf tijdens de controleperiode|Er zijn geen dimensies|
|Leesbewerkingen op de schijf/seconde|Leesbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Gelezen IOP's op de schijf|Er zijn geen dimensies|
|Schrijfbewerkingen op de schijf/seconde|Schrijfbewerkingen op de schijf/seconde|CountPerSecond|Gemiddeld|Geschreven IOP's op de schijf|Er zijn geen dimensies|
|Resterend CPU-tegoed|Resterend CPU-tegoed|Count|Gemiddeld|Totale tegoed beschikbaar voor burst|Er zijn geen dimensies|
|Verbruikt CPU-tegoed|Verbruikt CPU-tegoed|Count|Gemiddeld|Totale tegoed gebruikt door de virtuele machine|Er zijn geen dimensies|
|Per gelezen Bytes per seconde|Gegevens van gelezen Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per schijf geschreven Bytes per seconde|Gegevens geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode bewaking|Sleuf|
|Per schijf leesbewerkingen per seconde|Gegevens gelezen-bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode bewaking|Sleuf|
|Per geschreven bewerkingen per seconde|Gegevens geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode bewaking|Sleuf|
|Per schijf Wachtrijdiepte|Gegevensschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Gegevens wachtrijdiepte van schijf (of wachtrijlengte)|Sleuf|
|OS Per schijf gelezen Bytes per seconde|OS-schijf gelezen Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde voor het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf geschreven Bytes per seconde|OS-schijf geschreven Bytes per seconde (Preview)|CountPerSecond|Gemiddeld|Totaal aantal Bytes per seconde die zijn geschreven voor één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf leesbewerkingen per seconde|Besturingssysteemschijf leesbewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het lezen van één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf schrijfbewerkingen per seconde|OS geschreven bewerkingen per seconde (Preview)|CountPerSecond|Gemiddeld|Totale aantal IOPS gebeurd tijdens het schrijven naar één schijf tijdens de periode voor de besturingssysteemschijf bewaking|Er zijn geen dimensies|
|OS Per schijf Wachtrijdiepte|Besturingssysteemschijf Wachtrijdiepte (Preview)|Count|Gemiddeld|Besturingssysteemschijf wachtrijdiepte (of wachtrijlengte)|Er zijn geen dimensies|

## <a name="microsoftcontainerinstancecontainergroups"></a>Microsoft.ContainerInstance/containerGroups

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|CpuUsage|CPU-gebruik|Count|Gemiddeld|CPU-gebruik op alle kernen in millicores.|ContainerName|
|MemoryUsage|Geheugengebruik|Bytes|Gemiddeld|Totale geheugengebruik in bytes.|ContainerName|

## <a name="microsoftcontainerservicemanagedclusters"></a>Microsoft.ContainerService/managedClusters

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|kube_node_status_allocatable_cpu_cores|Totaal aantal beschikbare cpu-kernen in een beheerde cluster|Count|Totaal|Totaal aantal beschikbare cpu-kernen in een beheerde cluster|Er zijn geen dimensies|
|kube_node_status_allocatable_memory_bytes|Totale hoeveelheid beschikbaar geheugen in een beheerde cluster|Bytes|Totaal|Totale hoeveelheid beschikbaar geheugen in een beheerde cluster|Er zijn geen dimensies|
|kube_pod_status_ready|Nummer van het gehele product in de status gereed|Count|Totaal|Nummer van het gehele product in de status gereed|naamruimte, schil|
|kube_node_status_condition|Statussen voor verschillende knooppunt voorwaarden|Count|Totaal|Statussen voor verschillende knooppunt voorwaarden|voorwaarde, status, knooppunt|
|kube_pod_status_phase|Nummer van het gehele product door fase|Count|Totaal|Nummer van het gehele product door fase|fase, naamruimte, schil|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|DCIApiCalls|Klant Insights API-aanroepen|Count|Totaal||Er zijn geen dimensies|
|DCIMappingImportOperationSuccessfulLines|Geslaagde bewerkingsregels toewijzing importeren|Count|Totaal||Er zijn geen dimensies|
|DCIMappingImportOperationFailedLines|Toewijzing van de importbewerking is mislukt voor regels|Count|Totaal||Er zijn geen dimensies|
|DCIMappingImportOperationTotalLines|Totaal aantal bewerkingsregels toewijzing importeren|Count|Totaal||Er zijn geen dimensies|
|DCIMappingImportOperationRuntimeInSeconds|Toewijzing importeren bewerking Runtime In seconden|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundProfileExportSucceeded|Uitgaande profiel exporteren is geslaagd|Count|Totaal||Er zijn geen dimensies|
|DCIOutboundProfileExportFailed|Uitgaande profiel exporteren is mislukt|Count|Totaal||Er zijn geen dimensies|
|DCIOutboundProfileExportDuration|Duur van de uitgaande profiel exporteren|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundKpiExportSucceeded|Uitgaande Kpi exporteren is voltooid|Count|Totaal||Er zijn geen dimensies|
|DCIOutboundKpiExportFailed|Uitgaande Kpi exporteren is mislukt|Count|Totaal||Er zijn geen dimensies|
|DCIOutboundKpiExportDuration|Duur van de uitgaande Kpi exporteren|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundKpiExportStarted|Uitgaande Kpi Export gestart|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundKpiRecordCount|Aantal uitgaande Kpi-records|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundProfileExportCount|Telling van uitgaande profiel exporteren|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundInitialProfileExportFailed|Uitgaande profiel exporteren is mislukt|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundInitialProfileExportSucceeded|Uitgaande profiel exporteren is geslaagd|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundInitialKpiExportFailed|Uitgaande initiële Kpi exporteren is mislukt|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundInitialKpiExportSucceeded|Uitgaande initiële Kpi exporteren is voltooid|Seconden|Totaal||Er zijn geen dimensies|
|DCIOutboundInitialProfileExportDurationInSeconds|Uitgaande profiel exporteren duur In seconden|Seconden|Totaal||Er zijn geen dimensies|
|AdlaJobForStandardKpiFailed|De taak Adla voor standaard-Kpi is mislukt In seconden|Seconden|Totaal||Er zijn geen dimensies|
|AdlaJobForStandardKpiTimeOut|De taak Adla voor standaard Kpi time-out In seconden|Seconden|Totaal||Er zijn geen dimensies|
|AdlaJobForStandardKpiCompleted|De taak Adla voor standaard-Kpi voltooid In seconden|Seconden|Totaal||Er zijn geen dimensies|
|ImportASAValuesFailed|Importeren ASA waarden aantal is mislukt|Count|Totaal||Er zijn geen dimensies|
|ImportASAValuesSucceeded|Importeren ASA waarden aantal is voltooid|Count|Totaal||Er zijn geen dimensies|
|DCIProfilesCount|Aantal exemplaren op profiel|Count|Laatste||Er zijn geen dimensies|
|DCIInteractionsPerMonthCount|Interacties aantal per maand|Count|Laatste||Er zijn geen dimensies|
|DCIKpisCount|Aantal van de KPI|Count|Laatste||Er zijn geen dimensies|
|DCISegmentsCount|Aantal eenheden|Count|Laatste||Er zijn geen dimensies|
|DCIPredictiveMatchPoliciesCount|Aantal voorspellende overeenkomsten|Count|Laatste||Er zijn geen dimensies|
|DCIPredictionsCount|Aantal voorspelling|Count|Laatste||Er zijn geen dimensies|

## <a name="microsoftdatafactorydatafactories"></a>Microsoft.DataFactory/datafactories

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|FailedRuns|Mislukte verwerkingen|Count|Totaal||pipelineName, activityName, windowEnd, windowStart|
|SuccessfulRuns|Geslaagde verwerkingen|Count|Totaal||pipelineName, activityName, windowEnd, windowStart|

## <a name="microsoftdatafactoryfactories"></a>Microsoft.DataFactory/factories

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|PipelineFailedRuns|Pijplijn wordt uitgevoerd metrische gegevens is mislukt|Count|Totaal||FailureType, naam|
|PipelineSucceededRuns|Pijplijn wordt uitgevoerd metrische gegevens is voltooid|Count|Totaal||FailureType, naam|
|ActivityFailedRuns|Metrische gegevens van activiteiten wordt uitgevoerd is mislukt|Count|Totaal||ActivityType, PipelineName, FailureType, naam|
|ActivitySucceededRuns|Metrische gegevens van activiteiten wordt uitgevoerd is voltooid|Count|Totaal||ActivityType, PipelineName, FailureType, naam|
|TriggerFailedRuns|Trigger wordt uitgevoerd metrische gegevens is mislukt|Count|Totaal||Naam, FailureType|
|TriggerSucceededRuns|Trigger wordt uitgevoerd metrische gegevens is voltooid|Count|Totaal||Naam, FailureType|
|IntegrationRuntimeCpuPercentage|Integratie runtime CPU-gebruik|Procent|Gemiddeld||IntegrationRuntimeName, NodeName|
|IntegrationRuntimeAvailableMemory|Beschikbaar geheugen in de runtime voor de integratie|Bytes|Gemiddeld||IntegrationRuntimeName, NodeName|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|JobEndedSuccess|Mislukte taken|Count|Totaal|Het aantal mislukte taken.|Er zijn geen dimensies|
|JobEndedFailure|Mislukte taken|Count|Totaal|Het aantal mislukte taken.|Er zijn geen dimensies|
|JobEndedCancelled|Geannuleerde taken|Count|Totaal|Het aantal geannuleerde taken.|Er zijn geen dimensies|
|JobAUEndedSuccess|Geslaagde Australië tijd|Seconden|Totaal|Totale tijd Australië voor mislukte taken.|Er zijn geen dimensies|
|JobAUEndedFailure|Mislukte Australië tijd|Seconden|Totaal|Totale tijd Australië voor mislukte taken.|Er zijn geen dimensies|
|JobAUEndedCancelled|Geannuleerde Australië tijd|Seconden|Totaal|Totale tijd Australië voor geannuleerde taken.|Er zijn geen dimensies|

## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.DataLakeStore/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TotalStorage|Totale opslagruimte|Bytes|Maximum|Totale hoeveelheid gegevens die zijn opgeslagen in het account.|Er zijn geen dimensies|
|dataWritten|Gegevens geschreven|Bytes|Totaal|Totale hoeveelheid gegevens geschreven naar het account.|Er zijn geen dimensies|
|dataRead|Gegevens lezen|Bytes|Totaal|Totale hoeveelheid gegevens gelezen uit het account.|Er zijn geen dimensies|
|WriteRequests|Schrijven van aanvragen|Count|Totaal|Telling van gegevens schrijfaanvragen aan het account.|Er zijn geen dimensies|
|ReadRequests|Alleen aanvragen|Count|Totaal|Telling van gegevens lezen-aanvragen voor het account.|Er zijn geen dimensies|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Er zijn geen dimensies|
|memory_percent|Percentage geheugen|Procent|Gemiddeld|Percentage geheugen|Er zijn geen dimensies|
|io_consumption_percent|I/o-percentage|Procent|Gemiddeld|I/o-percentage|Er zijn geen dimensies|
|storage_percent|Percentage van de opslag|Procent|Gemiddeld|Percentage van de opslag|Er zijn geen dimensies|
|storage_used|Gebruikte opslag|Bytes|Gemiddeld|Gebruikte opslag|Er zijn geen dimensies|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddeld|Opslaglimiet bereikt|Er zijn geen dimensies|
|serverlog_storage_percent|Server-logboek opslag procent|Procent|Gemiddeld|Server-logboek opslag procent|Er zijn geen dimensies|
|serverlog_storage_usage|Opslag voor toepassingslogboeken server gebruikt|Bytes|Gemiddeld|Opslag voor toepassingslogboeken server gebruikt|Er zijn geen dimensies|
|serverlog_storage_limit|Opslaglimiet van server-logboek|Bytes|Gemiddeld|Opslaglimiet van server-logboek|Er zijn geen dimensies|
|active_connections|Totaal aantal actieve verbindingen|Count|Gemiddeld|Totaal aantal actieve verbindingen|Er zijn geen dimensies|
|connections_failed|Totaal aantal mislukte verbindingen|Count|Totaal|Totaal aantal mislukte verbindingen|Er zijn geen dimensies|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Er zijn geen dimensies|
|memory_percent|Percentage geheugen|Procent|Gemiddeld|Percentage geheugen|Er zijn geen dimensies|
|io_consumption_percent|I/o-percentage|Procent|Gemiddeld|I/o-percentage|Er zijn geen dimensies|
|storage_percent|Percentage van de opslag|Procent|Gemiddeld|Percentage van de opslag|Er zijn geen dimensies|
|storage_used|Gebruikte opslag|Bytes|Gemiddeld|Gebruikte opslag|Er zijn geen dimensies|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddeld|Opslaglimiet bereikt|Er zijn geen dimensies|
|serverlog_storage_percent|Server-logboek opslag procent|Procent|Gemiddeld|Server-logboek opslag procent|Er zijn geen dimensies|
|serverlog_storage_usage|Opslag voor toepassingslogboeken server gebruikt|Bytes|Gemiddeld|Opslag voor toepassingslogboeken server gebruikt|Er zijn geen dimensies|
|serverlog_storage_limit|Opslaglimiet van server-logboek|Bytes|Gemiddeld|Opslaglimiet van server-logboek|Er zijn geen dimensies|
|active_connections|Totaal aantal actieve verbindingen|Count|Totaal|Totaal aantal actieve verbindingen|Er zijn geen dimensies|
|connections_failed|Totaal aantal mislukte verbindingen|Count|Totaal|Totaal aantal mislukte verbindingen|Er zijn geen dimensies|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Telemetrie-bericht verzenden pogingen|Count|Totaal|Aantal voor apparaat-naar-cloud-telemetrieberichten worden verzonden naar uw IoT-hub geprobeerd|Er zijn geen dimensies|
|d2c.telemetry.ingress.Success|Telemetrieberichten|Count|Totaal|Aantal voor apparaat-naar-cloud-telemetrieberichten is verzonden naar uw IoT-hub|Er zijn geen dimensies|
|c2d.Commands.egress.complete.Success|Opdrachten voltooid|Count|Totaal|Aantal opdrachten voor cloud-naar-apparaat is voltooid door het apparaat|Er zijn geen dimensies|
|c2d.commands.egress.abandon.success|Opdrachten afgebroken|Count|Totaal|Aantal cloud-naar-apparaatopdrachten afgebroken door het apparaat|Er zijn geen dimensies|
|c2d.commands.egress.reject.success|Opdrachten geweigerd|Count|Totaal|Aantal cloud-naar-apparaatopdrachten geweigerd door het apparaat|Er zijn geen dimensies|
|devices.totalDevices|Totaal aantal apparaten|Count|Totaal|Aantal apparaten geregistreerd bij uw IoT-hub|Er zijn geen dimensies|
|devices.connectedDevices.allProtocol|Verbonden apparaten|Count|Totaal|Aantal apparaten dat is verbonden met uw IoT-hub|Er zijn geen dimensies|
|d2c.telemetry.egress.success|Telemetrieberichten geleverd|Count|Totaal|Aantal keren dat berichten zijn geschreven naar eindpunten (totaal)|Er zijn geen dimensies|
|d2c.telemetry.egress.dropped|Verwijderde berichten|Count|Totaal|Aantal berichten dat is verwijderd omdat het eindpunt voor de levering van inactieve|Er zijn geen dimensies|
|d2c.telemetry.egress.orphaned|Zwevende berichten|Count|Totaal|Het aantal berichten die niet voldoen aan alle routes met inbegrip van de route voor terugval|Er zijn geen dimensies|
|d2c.telemetry.egress.Invalid|Ongeldige-berichten|Count|Totaal|Het aantal berichten niet worden bezorgd omdat ze niet compatibel met het eindpunt|Er zijn geen dimensies|
|d2c.telemetry.egress.fallback|Berichten die overeenkomt met alternatieve voorwaarde|Count|Totaal|Aantal berichten dat is geschreven naar het eindpunt voor terugval|Er zijn geen dimensies|
|d2c.endpoints.egress.eventHubs|Berichten in de Event Hub-eindpunten|Count|Totaal|Aantal keren dat berichten zijn geschreven naar de Event Hub-eindpunten|Er zijn geen dimensies|
|d2c.endpoints.latency.eventHubs|Bericht latentie voor Event Hub-eindpunten|Milliseconden|Gemiddeld|De gemiddelde latentie tussen inkomend bericht met de iothub en inkomend bericht in een Event Hub-eindpunt, in milliseconden|Er zijn geen dimensies|
|d2c.endpoints.egress.serviceBusQueues|Berichten worden afgeleverd bij Service Bus-wachtrij-eindpunten|Count|Totaal|Aantal keren dat berichten zijn geschreven naar Service Bus-wachtrij-eindpunten|Er zijn geen dimensies|
|d2c.endpoints.latency.serviceBusQueues|Bericht latentie voor Service Bus-wachtrij-eindpunten|Milliseconden|Gemiddeld|De gemiddelde latentie tussen inkomend bericht met de iothub en inkomend bericht in een Service Bus-wachtrij eindpunt, in milliseconden|Er zijn geen dimensies|
|d2c.endpoints.egress.serviceBusTopics|Berichten worden afgeleverd bij Service Bus-onderwerp eindpunten|Count|Totaal|Aantal keren dat berichten zijn geschreven naar Service Bus-onderwerp eindpunten|Er zijn geen dimensies|
|d2c.endpoints.latency.serviceBusTopics|Bericht latentie voor Service Bus-onderwerp eindpunten|Milliseconden|Gemiddeld|De gemiddelde latentie tussen inkomend bericht met de iothub en inkomend bericht in een eindpunt Service Bus-onderwerp in milliseconden|Er zijn geen dimensies|
|d2c.endpoints.egress.builtIn.events|Berichten die worden geleverd aan het ingebouwde eindpunt (berichten/gebeurtenissen)|Count|Totaal|Aantal keren dat berichten zijn geschreven naar het ingebouwde eindpunt (berichten/gebeurtenissen)|Er zijn geen dimensies|
|d2c.endpoints.latency.builtIn.events|Bericht latentie voor het ingebouwde eindpunt (berichten/gebeurtenissen)|Milliseconden|Gemiddeld|De gemiddelde latentie tussen inkomend bericht met de iothub en inkomend bericht in het ingebouwde eindpunt (berichten/gebeurtenissen), in milliseconden |Er zijn geen dimensies|
|d2c.endpoints.egress.Storage|Berichten in de opslag-eindpunten|Count|Totaal|Aantal keren dat berichten zijn geschreven naar de opslag-eindpunten|Er zijn geen dimensies|
|d2c.endpoints.Latency.Storage|Bericht latentie voor opslag-eindpunten|Milliseconden|Gemiddeld|De gemiddelde latentie tussen inkomend bericht met de iothub en inkomend bericht in een opslag-eindpunt in milliseconden|Er zijn geen dimensies|
|d2c.endpoints.egress.Storage.bytes|Gegevens die zijn geschreven naar de opslag|Bytes|Totaal|Hoeveelheid gegevens in bytes geschreven naar de opslag-eindpunten|Er zijn geen dimensies|
|d2c.endpoints.egress.Storage.blobs|BLOBs die zijn geschreven naar de opslag|Count|Totaal|Aantal blobs geschreven naar de opslag-eindpunten|Er zijn geen dimensies|
|d2c.twin.read.success|Geslaagde twin leesbewerkingen van apparaten|Count|Totaal|De telling van alle geslaagde apparaat geïnitieerde twin leest.|Er zijn geen dimensies|
|d2c.Twin.Read.failure|Twin leesbewerkingen van apparaten is mislukt|Count|Totaal|De telling van alle apparaat geïnitieerde twin leesbewerkingen mislukt.|Er zijn geen dimensies|
|d2c.twin.read.size|De grootte van de antwoorden twin leesbewerkingen van apparaten|Bytes|Gemiddeld|De gemiddelde min en max van alle geslaagde apparaat geïnitieerde twin leest.|Er zijn geen dimensies|
|d2c.Twin.update.Success|Geslaagde twin updates van apparaten|Count|Totaal|Het aantal updates van alle geslaagde twin apparaat gestart.|Er zijn geen dimensies|
|d2c.Twin.update.failure|Twin updates van apparaten is mislukt|Count|Totaal|De telling van alle apparaat geïnitieerde twin updates mislukt.|Er zijn geen dimensies|
|d2c.Twin.update.Size|Grootte van de updates twin van apparaten|Bytes|Gemiddeld|De gemiddelde min. en max. grootte van alle geslaagde apparaat geïnitieerde twin updates.|Er zijn geen dimensies|
|c2d.Methods.Success|Geslaagde directe methode aanroepen|Count|Totaal|De telling van alle geslaagde directe methodeaanroepen.|Er zijn geen dimensies|
|c2d.Methods.failure|Directe methode aanroepen is mislukt|Count|Totaal|De telling van alle directe methodeaanroepen mislukt.|Er zijn geen dimensies|
|c2d.Methods.requestSize|Aanvraaggrootte van directe methode aanroepen|Bytes|Gemiddeld|De gemiddelde, min en max van alle geslaagde aanvragen voor directe methode.|Er zijn geen dimensies|
|c2d.Methods.responseSize|Reactiegrootte van directe methode aanroepen|Bytes|Gemiddeld|De gemiddelde, min en max van alle geslaagde directe methode antwoorden.|Er zijn geen dimensies|
|c2d.twin.read.success|Geslaagde twin leest uit back-end|Count|Totaal|De telling van alle geslaagde back-end-geïnitieerde twin leest.|Er zijn geen dimensies|
|c2d.twin.read.failure|Mislukte twin leest uit back-end|Count|Totaal|De telling van alle kan geen back-end-geïnitieerde twin leest.|Er zijn geen dimensies|
|c2d.twin.read.size|De grootte van de antwoorden twin leesbewerkingen van back-end|Bytes|Gemiddeld|De gemiddelde min en max van alle geslaagde back-end-geïnitieerde twin leest.|Er zijn geen dimensies|
|c2d.Twin.update.Success|Geslaagde twin updates van de back-end|Count|Totaal|De telling van alle geslaagde back-end-geïnitieerde twin updates.|Er zijn geen dimensies|
|c2d.Twin.update.failure|Mislukte twin updates van de back-end|Count|Totaal|De telling van alle back-end-geïnitieerde twin updates mislukt.|Er zijn geen dimensies|
|c2d.Twin.update.Size|Grootte van twin updates van de back-end|Bytes|Gemiddeld|De gemiddelde min. en max. grootte van alle geslaagde back-end-geïnitieerde twin updates.|Er zijn geen dimensies|
|twinQueries.success|Geslaagde twin query 's|Count|Totaal|De telling van alle geslaagde twin query's.|Er zijn geen dimensies|
|twinQueries.failure|Mislukte twin query 's|Count|Totaal|De telling van alle mislukte twin query's.|Er zijn geen dimensies|
|twinQueries.resultSize|Grootte van query's Twin|Bytes|Gemiddeld|De gemiddelde, min en max van de grootte van het resultaat van alle geslaagde twin query's.|Er zijn geen dimensies|
|jobs.createTwinUpdateJob.success|Geslaagde bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|De telling van alle geslaagde twin update taken worden gemaakt.|Er zijn geen dimensies|
|jobs.createTwinUpdateJob.failure|Mislukte bewerkingen voor het maken van twin taken bijwerken|Count|Totaal|De telling van alle mislukte twin update taken worden gemaakt.|Er zijn geen dimensies|
|jobs.createDirectMethodJob.success|Geslaagde bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|De telling van alle geslaagde directe methode aanroepen taken worden gemaakt.|Er zijn geen dimensies|
|jobs.createDirectMethodJob.failure|Mislukte bewerkingen voor het maken van de methode aanroepen van taken|Count|Totaal|De telling van alle maken van taken voor directe methode-aanroep is mislukt.|Er zijn geen dimensies|
|jobs.listJobs.success|Geslaagde aanroepen naar de lijst met taken|Count|Totaal|De telling van alle geslaagde aanroepen naar de lijst met taken.|Er zijn geen dimensies|
|jobs.listJobs.failure|Kan niet aanroepen voor een lijst met taken|Count|Totaal|De telling van alle mislukte aanroepen naar de lijst met taken.|Er zijn geen dimensies|
|jobs.cancelJob.success|Geslaagde taakannuleringen|Count|Totaal|De telling van alle geslaagde aanroepen naar een taak annuleren.|Er zijn geen dimensies|
|jobs.cancelJob.failure|Mislukte taakannuleringen|Count|Totaal|De telling van alle mislukte aanroepen voor een taak annuleren.|Er zijn geen dimensies|
|jobs.queryJobs.success|Taak query 's|Count|Totaal|De telling van alle geslaagde aanroepen naar query taken.|Er zijn geen dimensies|
|jobs.queryJobs.failure|Taak voert een query is mislukt|Count|Totaal|De telling van alle mislukte aanroepen naar query taken.|Er zijn geen dimensies|
|jobs.completed|Voltooide taken|Count|Totaal|De telling van alle voltooide taken.|Er zijn geen dimensies|
|jobs.failed|Mislukte taken|Count|Totaal|De telling van alle mislukte taken.|Er zijn geen dimensies|
|d2c.telemetry.ingress.sendThrottle|Aantal bandbreedteregeling fouten|Count|Totaal|Beperkt aantal bandbreedteregeling fouten als gevolg van de doorvoer van apparaat|Er zijn geen dimensies|
|dailyMessageQuotaUsed|Totaal aantal berichten dat is gebruikt|Count|Gemiddeld|Het aantal totale aantal berichten die op dit moment gebruikt. Dit is een cumulatieve waarde die is ingesteld op nul op 00:00 UTC elke dag.|Er zijn geen dimensies|
|deviceDataUsage|Totaal aantal devicedata gebruik|Count|Totaal|Bytes overgedragen van en naar alle apparaten die zijn verbonden met IotHub|Er zijn geen dimensies|

## <a name="microsoftdevicesprovisioningservices"></a>Microsoft.Devices/provisioningServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|RegistrationAttempts|Registratie pogingen|Count|Totaal|Aantal apparaat registraties geprobeerd|ProvisioningServiceName, IotHubName, Status|
|DeviceAssignments|Apparaten die zijn toegewezen|Count|Totaal|Aantal apparaten dat is toegewezen aan een IoT-hub|ProvisioningServiceName, IotHubName|
|AttestationAttempts|Attestation pogingen|Count|Totaal|Het aantal apparaten verklaringen geprobeerd|ProvisioningServiceName, Status,-Protocol|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.DocumentDB/databaseAccounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|MetadataRequests|Aanvragen voor metagegevens|Count|Count|Het aantal aanvragen voor metagegevens. Cosmos DB onderhoudt system metagegevensverzameling voor elk account waarmee u opsommen verzamelingen, databases, enzovoort, en de bijbehorende configuraties, gratis.|GlobalDatabaseAccountName, DatabaseName, CollectionName, regio, StatusCode|
|MongoRequestCharge|Mongo aanvraag kosten|Count|Totaal|Mongo Aanvraageenheden verbruikt|GlobalDatabaseAccountName, DatabaseName, CollectionName, regio, CommandName, foutcode|
|MongoRequests|Mongo-aanvragen|Count|Count|Aantal Mongo-aanvragen|GlobalDatabaseAccountName, DatabaseName, CollectionName, regio, CommandName, foutcode|
|TotalRequestUnits|Totaal aantal Aanvraageenheden|Count|Totaal|Eenheden verbruikt aanvragen|GlobalDatabaseAccountName, DatabaseName, CollectionName, regio, StatusCode|
|TotalRequests|Totaal aantal aanvragen|Count|Count|Aantal aanvragen|GlobalDatabaseAccountName, DatabaseName, CollectionName, regio, StatusCode|


## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|SuccessfulRequests|Geslaagde aanvragen (Preview)|Count|Totaal|Voltooide aanvragen voor Microsoft.EventHub. (Preview)|EntityName|
|ServerErrors|Serverfouten. (Preview)|Count|Totaal|Serverfouten voor Microsoft.EventHub. (Preview)|EntityName|
|UserErrors|Gebruikersfouten. (Preview)|Count|Totaal|Gebruikersfouten voor Microsoft.EventHub. (Preview)|EntityName|
|QuotaExceededErrors|Fout met overschreden quotum. (Preview)|Count|Totaal|Fout met overschreden quotum voor Microsoft.EventHub. (Preview)|EntityName|
|ThrottledRequests|Beperkte aanvragen. (Preview)|Count|Totaal|Beperkte aanvragen voor Microsoft.EventHub. (Preview)|EntityName|
|IncomingRequests|Inkomende aanvragen (Preview)|Count|Totaal|Binnenkomende aanvragen voor Microsoft.EventHub. (Preview)|EntityName|
|IncomingMessages|Binnenkomende berichten (Preview)|Count|Totaal|Binnenkomende berichten voor Microsoft.EventHub. (Preview)|EntityName|
|OutgoingMessages|Uitgaande berichten (Preview)|Count|Totaal|Uitgaande berichten voor Microsoft.EventHub. (Preview)|EntityName|
|IncomingBytes|Binnenkomende bytes. (Preview)|Bytes|Totaal|Binnenkomende bytes voor Microsoft.EventHub. (Preview)|EntityName|
|OutgoingBytes|Uitgaande bytes. (Preview)|Bytes|Totaal|Uitgaande bytes voor Microsoft.EventHub. (Preview)|EntityName|
|ActiveConnections|ActiveConnections (Preview)|Count|Gemiddeld|Totaal aantal actieve verbindingen voor Microsoft.EventHub. (Preview)|Er zijn geen dimensies|
|ConnectionsOpened|Geopende verbindingen. (Preview)|Count|Gemiddeld|Geopende verbindingen voor Microsoft.EventHub. (Preview)|EntityName|
|ConnectionsClosed|Gesloten verbindingen. (Preview)|Count|Gemiddeld|Gesloten verbindingen voor Microsoft.EventHub. (Preview)|EntityName|
|CaptureBacklog|Achterstand vastleggen. (Preview)|Count|Totaal|Achterstand vastleggen voor Microsoft.EventHub. (Preview)|EntityName|
|CapturedMessages|Vastgelegde berichten. (Preview)|Count|Totaal|Vastgelegde berichten voor Microsoft.EventHub. (Preview)|EntityName|
|CapturedBytes|Vastgelegde bytes. (Preview)|Bytes|Totaal|Vastgelegde bytes voor Microsoft.EventHub. (Preview)|EntityName|
|Grootte|Grootte (Preview)|Bytes|Gemiddeld|Grootte van een EventHub in Bytes. (Preview)|EntityName|
|INREQS|Binnenkomende aanvragen|Count|Totaal|Totaal aantal inkomende aanvragen voor een naamruimte|Er zijn geen dimensies|
|SUCCREQ|Geslaagde aanvragen|Count|Totaal|Totaal aantal verwerkte aanvragen voor een naamruimte|Er zijn geen dimensies|
|FAILREQ|Mislukte aanvragen|Count|Totaal|Totaal aantal mislukte aanvragen voor een naamruimte|Er zijn geen dimensies|
|SVRBSY|Fouten omdat de server bezet is|Count|Totaal|Totaal aantal server bezet-fouten voor een naamruimte|Er zijn geen dimensies|
|INTERR|Interne serverfouten|Count|Totaal|Totaal aantal interne serverfouten voor een naamruimte|Er zijn geen dimensies|
|MISCERR|Overige fouten|Count|Totaal|Totaal aantal mislukte aanvragen voor een naamruimte|Er zijn geen dimensies|
|INMSGS|Binnenkomende berichten (afgeschaft)|Count|Totaal|Totaal aantal binnenkomende berichten voor een naamruimte. Met deze metriek is afgeschaft. Gebruik in plaats daarvan binnenkomende berichten metrische gegevens|Er zijn geen dimensies|
|EHINMSGS|Binnenkomende berichten|Count|Totaal|Totaal aantal inkomende berichten voor een naamruimte|Er zijn geen dimensies|
|OUTMSGS|Uitgaande berichten (afgeschaft)|Count|Totaal|Totaal aantal uitgaande berichten voor een naamruimte. Met deze metriek is afgeschaft. Gebruik in plaats daarvan de metriek uitgaande berichten|Er zijn geen dimensies|
|EHOUTMSGS|Uitgaande berichten|Count|Totaal|Totaal aantal uitgaande berichten voor een naamruimte|Er zijn geen dimensies|
|EHINMBS|Binnenkomende bytes (afgeschaft)|Bytes|Totaal|Event Hub inkomende bericht doorvoer voor een naamruimte. Met deze metriek is afgeschaft. Gebruik in plaats daarvan binnenkomende bytes metrische gegevens|Er zijn geen dimensies|
|EHINBYTES|Binnenkomende bytes|Bytes|Totaal|Doorvoer van inkomende Event Hub-berichten voor een naamruimte|Er zijn geen dimensies|
|EHOUTMBS|Uitgaande bytes (afgeschaft)|Bytes|Totaal|Event Hub uitgaande bericht doorvoer voor een naamruimte. Met deze metriek is afgeschaft. Gebruik in plaats daarvan uitgaande bytes metrische gegevens|Er zijn geen dimensies|
|EHOUTBYTES|Uitgaande bytes|Bytes|Totaal|Doorvoer van uitgaande Event Hub-berichten voor een naamruimte|Er zijn geen dimensies|
|EHABL|Achterstallige berichten van archief|Count|Totaal|Achterstallige Event Hub-archiefberichten voor een naamruimte|Er zijn geen dimensies|
|EHAMSGS|Berichten archiveren|Count|Totaal|Gearchiveerde Event Hub-berichten in een naamruimte|Er zijn geen dimensies|
|EHAMBS|Berichtdoorvoer van archief|Bytes|Totaal|Doorvoer van gearchiveerde Event Hub-berichtenin een naamruimte|Er zijn geen dimensies|

## <a name="microsofthdinsightclusters"></a>Microsoft.HDInsight/clusters

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|GatewayRequests|Gateway-aanvragen|Count|Totaal|Het aantal aanvragen van de gateway|ClusterDnsName, HttpStatus|
|CategorizedGatewayRequests|Gecategoriseerde Gateway aanvragen|Count|Totaal|Het aantal aanvragen van de gateway in categorieën (1xx/2xx/3xx/4xx/5xx)|ClusterDnsName, HttpStatus|

## <a name="microsoftinsightsautoscalesettings"></a>Microsoft.Insights/AutoscaleSettings

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ObservedMetricValue|Waargenomen metrische waarde|Count|Gemiddeld|De waarde die is berekend door automatisch schalen wanneer deze is uitgevoerd|MetricTriggerSource|
|MetricThreshold|Drempel voor een metrische waarde|Count|Gemiddeld|De geconfigureerde drempelwaarde voor automatisch schalen wanneer automatisch schalen is uitgevoerd.|MetricTriggerRule|
|ObservedCapacity|Waargenomen capaciteit|Count|Gemiddeld|De capaciteit die is gerapporteerd aan automatisch schalen wanneer dit is uitgevoerd.|Er zijn geen dimensies|
|ScaleActionsInitiated|Schaalacties geactiveerd|Count|Totaal|De richting van de schaalbewerking.|ScaleDirection|

## <a name="microsoftkeyvaultvaults"></a>Microsoft.KeyVault/vaults

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ServiceApiHit|Totaalaantal treffers service-API|Count|Count|Totaalaantal treffers voor service-API|ActivityType, ActivityName|
|ServiceApiLatency|Algemene latentie service-API|Milliseconden|Gemiddeld|Algemene latentie van service-API-aanvragen|ActivityType, ActivityName, StatusCode|
|ServiceApiResult|Totaalaantal resultaten service-API|Count|Count|Totaalaantal resultaten voor service-API|ActivityType, ActivityName, StatusCode|

## <a name="microsoftlocationbasedservicesaccounts"></a>Microsoft.LocationBasedServices/accounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Latentie|Latentie|Milliseconden|Gemiddeld|Duur van API-aanroepen|OperationName, OperationResult|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|RunsStarted|Gestarte uitvoeringen|Count|Totaal|Aantal gestarte werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunsCompleted|Voltooide uitvoeringen|Count|Totaal|Aantal voltooide werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunsSucceeded|Geslaagde uitvoeringen|Count|Totaal|Aantal geslaagde werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunsFailed|Mislukte uitvoeringen|Count|Totaal|Aantal mislukte werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunsCancelled|Geannuleerde uitvoeringen|Count|Totaal|Aantal geannuleerde werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunLatency|Latentie van uitvoeringen|Seconden|Gemiddeld|Latentie van voltooide werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunSuccessLatency|Latentie van geslaagde uitvoeringen|Seconden|Gemiddeld|Latentie van geslaagde werkstroomuitvoeringen.|Er zijn geen dimensies|
|RunThrottledEvents|Door uitvoering vertraagde gebeurtenissen|Count|Totaal|Aantal door werkstroomactie of trigger vertraagde gebeurtenissen.|Er zijn geen dimensies|
|RunFailurePercentage|Percentage mislukte uitvoeringen|Procent|Totaal|Percentage mislukte werkstroomuitvoeringen.|Er zijn geen dimensies|
|ActionsStarted|Gestarte acties |Count|Totaal|Aantal gestarte werkstroomacties.|Er zijn geen dimensies|
|ActionsCompleted|Voltooide acties |Count|Totaal|Aantal voltooide werkstroomacties.|Er zijn geen dimensies|
|ActionsSucceeded|Geslaagde acties |Count|Totaal|Aantal geslaagde werkstroomacties.|Er zijn geen dimensies|
|ActionsFailed|Mislukte acties|Count|Totaal|Aantal mislukte werkstroomacties.|Er zijn geen dimensies|
|ActionsSkipped|Overgeslagen acties |Count|Totaal|Aantal overgeslagen werkstroomacties.|Er zijn geen dimensies|
|ActionLatency|Actielatentie |Seconden|Gemiddeld|Latentie van voltooide werkstroomacties.|Er zijn geen dimensies|
|ActionSuccessLatency|Latentie geslaagde acties |Seconden|Gemiddeld|Latentie van geslaagde werkstroomacties.|Er zijn geen dimensies|
|ActionThrottledEvents|Door actie vertraagde gebeurtenissen|Count|Totaal|Aantal door werkstroomactie vertraagde gebeurtenissen.|Er zijn geen dimensies|
|TriggersStarted|Gestarte triggers |Count|Totaal|Aantal gestarte werkstroomtriggers.|Er zijn geen dimensies|
|TriggersCompleted|Voltooide triggers |Count|Totaal|Aantal voltooide werkstroomtriggers.|Er zijn geen dimensies|
|TriggersSucceeded|Geslaagde triggers |Count|Totaal|Aantal geslaagde werkstroomtriggers.|Er zijn geen dimensies|
|TriggersFailed|Mislukte triggers |Count|Totaal|Aantal mislukte werkstroomtriggers.|Er zijn geen dimensies|
|TriggersSkipped|Overgeslagen triggers|Count|Totaal|Aantal overgeslagen werkstroomtriggers.|Er zijn geen dimensies|
|TriggersFired|Geactiveerde triggers |Count|Totaal|Aantal geactiveerde werkstroomtriggers.|Er zijn geen dimensies|
|TriggerLatency|Latentie van trigger |Seconden|Gemiddeld|Latentie van voltooide werkstroomtriggers.|Er zijn geen dimensies|
|TriggerFireLatency|Latentie van triggeractivering |Seconden|Gemiddeld|Latentie van geactiveerde werkstroomtriggers.|Er zijn geen dimensies|
|TriggerSuccessLatency|Latentie van geslaagde triggers |Seconden|Gemiddeld|Latentie van geslaagde werkstroomtriggers.|Er zijn geen dimensies|
|TriggerThrottledEvents|Door trigger vertraagde gebeurtenissen|Count|Totaal|Aantal door werkstroomtrigger vertraagde gebeurtenissen.|Er zijn geen dimensies|
|BillableActionExecutions|Factureerbare uitvoeringen van acties|Count|Totaal|Aantal uitvoeringen van werkstroomacties dat wordt gefactureerd.|Er zijn geen dimensies|
|BillableTriggerExecutions|Factureerbare uitvoeringen van activeringen|Count|Totaal|Aantal uitvoeringen van werkstroomactiveringen dat wordt gefactureerd.|Er zijn geen dimensies|
|TotalBillableExecutions|Totaal aantal factureerbare uitvoeringen|Count|Totaal|Aantal werkstroomuitvoeringen dat wordt gefactureerd.|Er zijn geen dimensies|

## <a name="microsoftnetworkloadbalancers"></a>Microsoft.Network/loadBalancers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|VipAvailability|VIP-beschikbaarheid|Count|Gemiddeld|Beschikbaarheid van de VIP-eindpunten op basis van resultaten van de test|VipAddress, VipPort|
|DipAvailability|Beschikbaarheid van de DIP|Count|Gemiddeld|Beschikbaarheid van de DIP-eindpunten op basis van resultaten van de test|ProtocolType, DipPort, VipAddress, VipPort, DipAddress|
|ByteCount|Aantal bytes|Count|Totaal|Totaal aantal Bytes verzonden binnen een periode|VipAddress, VipPort, richting|
|PacketCount|Aantal|Count|Totaal|Totale aantal pakketten die zijn verzonden binnen een periode|VipAddress, VipPort, richting|
|SYNCount|SYN tellen|Count|Totaal|Totaal aantal SYN-pakketten die zijn verzonden binnen een periode|VipAddress, VipPort, richting|
|SnatConnectionCount|Aantal snat omzetten-verbindingen|Count|Totaal|Totaal aantal nieuwe snat omzetten verbindingen gemaakt binnen een periode|De ConnectionState VipAddress, DipAddress,|

## <a name="microsoftnetworkdnszones"></a>Microsoft.Network/dnszones

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|QueryVolume|Query-Volume|Count|Totaal|Aantal query's worden geleverd voor een DNS-zone|Er zijn geen dimensies|
|RecordSetCount|Set-aantal records|Count|Maximum|Aantal recordsets in een DNS-zone|Er zijn geen dimensies|
|RecordSetCapacityUtilization|Recordset capaciteitsverbruik|Procent|Maximum|Percentage van de recordset capaciteit gebruikt door een DNS-zone|Er zijn geen dimensies|

## <a name="microsoftnetworkpublicipaddresses"></a>Microsoft.Network/publicIPAddresses

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|PacketsInDDoS|Inkomende pakketten DDoS|CountPerSecond|Maximum|Inkomende pakketten DDoS|Er zijn geen dimensies|
|PacketsDroppedDDoS|Inkomende pakketten verwijderd DDoS|CountPerSecond|Maximum|Inkomende pakketten verwijderd DDoS|Er zijn geen dimensies|
|PacketsForwardedDDoS|Inkomende pakketten DDoS doorgestuurd|CountPerSecond|Maximum|Inkomende pakketten DDoS doorgestuurd|Er zijn geen dimensies|
|TCPPacketsInDDoS|Inkomende pakketten dat TCP DDoS|CountPerSecond|Maximum|Inkomende pakketten dat TCP DDoS|Er zijn geen dimensies|
|TCPPacketsDroppedDDoS|Inkomende pakketten dat TCP verwijderd DDoS|CountPerSecond|Maximum|Inkomende pakketten dat TCP verwijderd DDoS|Er zijn geen dimensies|
|TCPPacketsForwardedDDoS|Binnenkomend TCP-pakket doorgestuurd DDoS|CountPerSecond|Maximum|Binnenkomend TCP-pakket doorgestuurd DDoS|Er zijn geen dimensies|
|UDPPacketsInDDoS|Binnenkomend UDP-pakketten DDoS|CountPerSecond|Maximum|Binnenkomend UDP-pakketten DDoS|Er zijn geen dimensies|
|UDPPacketsDroppedDDoS|Binnenkomend UDP-pakketten verwijderd DDoS|CountPerSecond|Maximum|Binnenkomend UDP-pakketten verwijderd DDoS|Er zijn geen dimensies|
|UDPPacketsForwardedDDoS|Binnenkomend UDP-pakketten DDoS doorgestuurd|CountPerSecond|Maximum|Binnenkomend UDP-pakketten DDoS doorgestuurd|Er zijn geen dimensies|
|BytesInDDoS|Binnenkomende bytes DDoS|BytesPerSecond|Maximum|Binnenkomende bytes DDoS|Er zijn geen dimensies|
|BytesDroppedDDoS|Binnenkomende bytes verwijderd DDoS|BytesPerSecond|Maximum|Binnenkomende bytes verwijderd DDoS|Er zijn geen dimensies|
|BytesForwardedDDoS|Binnenkomende bytes DDoS doorgestuurd|BytesPerSecond|Maximum|Binnenkomende bytes DDoS doorgestuurd|Er zijn geen dimensies|
|TCPBytesInDDoS|Binnenkomende TCP bytes DDoS|BytesPerSecond|Maximum|Binnenkomende TCP bytes DDoS|Er zijn geen dimensies|
|TCPBytesDroppedDDoS|Binnenkomend TCP-bytes verwijderd DDoS|BytesPerSecond|Maximum|Binnenkomend TCP-bytes verwijderd DDoS|Er zijn geen dimensies|
|TCPBytesForwardedDDoS|Binnenkomend TCP-bytes DDoS doorgestuurd|BytesPerSecond|Maximum|Binnenkomend TCP-bytes DDoS doorgestuurd|Er zijn geen dimensies|
|UDPBytesInDDoS|Binnenkomend UDP bytes DDoS|BytesPerSecond|Maximum|Binnenkomend UDP bytes DDoS|Er zijn geen dimensies|
|UDPBytesDroppedDDoS|Binnenkomend UDP bytes verwijderd DDoS|BytesPerSecond|Maximum|Binnenkomend UDP bytes verwijderd DDoS|Er zijn geen dimensies|
|UDPBytesForwardedDDoS|Binnenkomend UDP bytes DDoS doorgestuurd|BytesPerSecond|Maximum|Binnenkomend UDP bytes DDoS doorgestuurd|Er zijn geen dimensies|
|IfUnderDDoSAttack|Onder DDoS-aanvallen, of niet|Count|Maximum|Onder DDoS-aanvallen, of niet|Er zijn geen dimensies|
|DDoSTriggerTCPPackets|Inkomende TCP-pakketten voor het activeren van DDoS risicobeperking|CountPerSecond|Maximum|Inkomende TCP-pakketten voor het activeren van DDoS risicobeperking|Er zijn geen dimensies|
|DDoSTriggerUDPPackets|Binnenkomend UDP-pakketten voor het activeren van DDoS risicobeperking|CountPerSecond|Maximum|Binnenkomend UDP-pakketten voor het activeren van DDoS risicobeperking|Er zijn geen dimensies|
|DDoSTriggerSYNPackets|Inkomende pakketten dat SYN DDoS risicobeperking activeren|CountPerSecond|Maximum|Inkomende pakketten dat SYN DDoS risicobeperking activeren|Er zijn geen dimensies|
|VipAvailability|Beschikbaarheid|Count|Gemiddeld|Gemiddelde beschikbaarheid van de IP-adres binnen een periode|Poort|
|ByteCount|Aantal bytes|Count|Totaal|Totaal aantal Bytes verzonden binnen een periode|Poort, richting|
|PacketCount|Aantal|Count|Totaal|Totale aantal pakketten die zijn verzonden binnen een periode|Poort, richting|
|SynCount|SYN tellen|Count|Totaal|Totaal aantal SYN-pakketten die zijn verzonden binnen een periode|Poort, richting|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Doorvoer|Doorvoer|BytesPerSecond|Totaal|Het aantal bytes per seconde is die de toepassingsgateway is geleverd|Er zijn geen dimensies|
|UnhealthyHostCount|Onjuiste telling van de Host|Count|Gemiddeld|Het aantal beschadigde back-end-hosts. U kunt filteren op een per per back-end van toepassingen in orde/slecht hosts in een specifieke back-endpool weergeven.|BackendSettingsPool|
|healthyHostCount|In orde Host tellen|Count|Gemiddeld|Het aantal goede back-end-hosts. U kunt filteren op een per per back-end van toepassingen in orde/slecht hosts in een specifieke back-endpool weergeven.|BackendSettingsPool. |
|TotalRequests|Totaal aantal aanvragen|Count|Totaal|Aantal geslaagde aanvragen voor de toepassingsgateway is geleverd|BackendSettingsPool|
|FailedRequests|Mislukte aanvragen|Count|Totaal|Aantal mislukte aanvragen die Application Gateway is geleverd|BackendSettingsPool|
|ResponseStatus|Response-Status|Count|Totaal|Status van HTTP-antwoord geretourneerd door de toepassingsgateway. De verdeling van antwoord status code kan verder worden categoized om weer te geven van antwoorden in 2xx, 3xx 4xx en 5xx-categorieën.|HttpStatusGroup|
|CurrentConnections|Actieve verbindingen|Count|Totaal|Telling van actieve verbindingen tot stand brengen met Application Gateway|Er zijn geen dimensies|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.Network/virtualNetworkGateways

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TunnelAverageBandwidth|Tunnel-bandbreedte|BytesPerSecond|Gemiddeld|Gemiddelde bandbreedte van een tunnel in bytes per seconde|ConnectionName, RemoteIP|
|TunnelEgressBytes|Tunnel uitgaande Bytes|Bytes|Totaal|Uitgaande bytes van een tunnel|ConnectionName, RemoteIP|
|TunnelIngressBytes|Tunnel inkomend Bytes|Bytes|Totaal|Binnenkomende bytes van een tunnel|ConnectionName, RemoteIP|
|TunnelEgressPackets|Tunnel uitgaande pakketten|Count|Totaal|Aantal uitgaande van een tunnel|ConnectionName, RemoteIP|
|TunnelIngressPackets|Tunnel inkomende pakketten|Count|Totaal|Aantal binnenkomende van een tunnel|ConnectionName, RemoteIP|
|TunnelEgressPacketDropTSMismatch|Tunnel uitgaande TS verschil pakket verwijderen|Count|Totaal|Uitgaande pakket neerzetten-telling van het verkeer selector niet-overeenkomende een tunnel|ConnectionName, RemoteIP|
|TunnelIngressPacketDropTSMismatch|Tunnel inkomend TS verschil pakket verwijderen|Count|Totaal|Binnenkomende pakket neerzetten-telling van het verkeer selector niet-overeenkomende een tunnel|ConnectionName, RemoteIP|

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|BitsInPerSecond|BitsInPerSecond|CountPerSecond|Gemiddeld|Bits ingressing Azure per seconde|Er zijn geen dimensies|
|BitsOutPerSecond|BitsOutPerSecond|CountPerSecond|Gemiddeld|Bits Azure egressing per seconde|Er zijn geen dimensies|

## <a name="microsoftnetworktrafficmanagerprofiles"></a>Microsoft.Network/trafficManagerProfiles

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|QpsByEndpoint|Query's door eindpunt geretourneerd|Count|Totaal|Aantal keren dat een Traffic Manager-eindpunt is geretourneerd in de bepaalde periode|EndpointName|
|ProbeAgentCurrentEndpointStateByProfileResourceId|Status endpoint door eindpunt|Count|Maximum|1 als de status van een eindpunt-test "ingeschakeld", anders 0.|EndpointName|

## <a name="microsoftnetworknetworkwatchersconnectionmonitors"></a>Microsoft.Network/networkWatchers/connectionMonitors

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ProbesFailedPercent|% Tests is mislukt|Procent|Gemiddeld|% van de verbinding tests bewaking is mislukt|Er zijn geen dimensies|
|AverageRoundtripMs|Gem. Round trip-tijd (ms)|MilliSeconds|Gemiddeld|Gemiddelde netwerk round trip-tijd (ms) connectiviteit van de bewaking van tests die worden verzonden tussen de bron- en doelserver|Er zijn geen dimensies|

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Registration.all|Registratiebewerkingen|Count|Totaal|Het aantal registratiebewerkingen (maken, bijwerken, query's uitvoeren en verwijderen). |Er zijn geen dimensies|
|Registration.Create|Bewerkingen voor het maken van registraties|Count|Totaal|Het aantal gemaakte registraties.|Er zijn geen dimensies|
|Registration.update|Bewerkingen voor het bijwerken van registraties|Count|Totaal|Het aantal voltooide registratie-updates.|Er zijn geen dimensies|
|Registration.Get|Bewerkingen voor het lezen van registraties|Count|Totaal|Het aantal uitgevoerde registratiequery's.|Er zijn geen dimensies|
|Registration.Delete|Bewerkingen voor het verwijderen van registraties|Count|Totaal|Het aantal verwijderde registraties.|Er zijn geen dimensies|
|binnenkomende|Binnenkomende berichten|Count|Totaal|Het aantal voltooide verzonden API-aanroepen. |Er zijn geen dimensies|
|Incoming.Scheduled|Geplande pushmeldingen verzonden|Count|Totaal|Geplande pushmeldingen geannuleerd|Er zijn geen dimensies|
|Incoming.Scheduled.Cancel|Geplande pushmeldingen geannuleerd|Count|Totaal|Geplande pushmeldingen geannuleerd|Er zijn geen dimensies|
|Scheduled.Pending|Geplande meldingen in behandeling|Count|Totaal|Geplande meldingen in behandeling|Er zijn geen dimensies|
|Installation.all|Installatiebeheerbewerkingen|Count|Totaal|Installatiebeheerbewerkingen|Er zijn geen dimensies|
|Installation.Get|Installatiebewerkingen ophalen|Count|Totaal|Installatiebewerkingen ophalen|Er zijn geen dimensies|
|Installation.upsert|Installatiebewerkingen maken of bijwerken|Count|Totaal|Installatiebewerkingen maken of bijwerken|Er zijn geen dimensies|
|Installation.patch|Installatiebewerkingen patchen|Count|Totaal|Installatiebewerkingen patchen|Er zijn geen dimensies|
|Installation.Delete|Installatiebewerkingen verwijderen|Count|Totaal|Installatiebewerkingen verwijderen|Er zijn geen dimensies|
|Outgoing.allpns.Success|Voltooide meldingen|Count|Totaal|Het aantal voltooide meldingen.|Er zijn geen dimensies|
|Outgoing.allpns.invalidpayload|Fouten met nettolading|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS een fout met een onjuiste payload heeft geretourneerd.|Er zijn geen dimensies|
|Outgoing.allpns.pnserror|Fouten met het externe meldingssysteem|Count|Totaal|Het aantal pushes dat is mislukt vanwege een probleem in de communicatie met PNS (exclusief verificatieproblemen).|Er zijn geen dimensies|
|Outgoing.allpns.channelerror|Fouten met kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat het kanaal ongeldig is, niet is gekoppeld aan de juiste app, beperkt is of verlopen is.|Er zijn geen dimensies|
|outgoing.allpns.badorexpiredchannel|Fouten met slecht of verlopen kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat het kanaal/het token/de registratie-id in de registratie is verlopen of ongeldig is.|Er zijn geen dimensies|
|Outgoing.WNS.Success|Meldingen over voltooide WNS|Count|Totaal|Het aantal voltooide meldingen.|Er zijn geen dimensies|
|Outgoing.WNS.invalidcredentials|WNS-verificatiefouten (ongeldige referenties)|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert of omdat de referenties zijn geblokkeerd. (Windows Live worden niet herkend door de referenties).|Er zijn geen dimensies|
|outgoing.wns.badchannel|WNS-fout wegens slecht kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de kanaal-URI in de registratie niet is herkend (WNS-status: 404 - Niet gevonden).|Er zijn geen dimensies|
|outgoing.wns.expiredchannel|WNS-fout wegens verlopen kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de kanaal-URI is verlopen (WNS-status: 410 verwijderd).|Er zijn geen dimensies|
|Outgoing.WNS.throttled|Meldingen over beperkte WNS|Count|Totaal|Het aantal pushes dat is mislukt omdat WNS deze app beperkt (WNS-status: 406 niet acceptabel).|Er zijn geen dimensies|
|Outgoing.WNS.tokenproviderunreachable|WNS-verificatiefouten (onbereikbaar)|Count|Totaal|Windows Live is niet bereikbaar.|Er zijn geen dimensies|
|Outgoing.WNS.invalidtoken|WNS-verificatiefouten (ongeldig token)|Count|Totaal|Het token dat is opgegeven voor WNS is niet geldig (WNS-status: 401 - Niet gemachtigd).|Er zijn geen dimensies|
|outgoing.wns.wrongtoken|WNS-verificatiefouten (onjuist token)|Count|Totaal|Het token dat is opgegeven voor WNS is geldig, maar voor een andere toepassing (WNS-status: 403-verboden). Dit kan gebeuren als de ChannelURI in de registratie gekoppeld aan een andere app is. Controleer of de client-app is gekoppeld aan dezelfde app met de referenties die zich in de notification hub.|Er zijn geen dimensies|
|Outgoing.WNS.invalidnotificationformat|Ongeldige indeling van de WNS-melding|Count|Totaal|De indeling van de melding is ongeldig (WNS-status: 400). Houd er rekening mee dat WNS alle ongeldige nettoladingen komt niet afwijzen.|Er zijn geen dimensies|
|Outgoing.WNS.invalidnotificationsize|Fout met ongeldige grootte van de WNS-melding|Count|Totaal|De payload van de melding is te groot (WNS-status: 413).|Er zijn geen dimensies|
|Outgoing.WNS.channelthrottled|De verbinding met het WNS-kanaal is beperkt|Count|Totaal|De melding is verwijderd omdat de kanaal-URI in de registratie is beperkt (WNS-reactieheader: X-WNS-NotificationStatus:channelThrottled).|Er zijn geen dimensies|
|Outgoing.WNS.channeldisconnected|De verbinding met het WNS-kanaal is verbroken|Count|Totaal|De melding is verwijderd omdat de kanaal-URI in de registratie is beperkt (WNS-reactieheader: X-WNS-DeviceConnectionStatus: disconnected).|Er zijn geen dimensies|
|Outgoing.WNS.Dropped|Meldingen over verloren WNS|Count|Totaal|De melding is verwijderd omdat de kanaal-URI in de registratie is beperkt (X-WNS-NotificationStatus: dropped, maar niet X-WNS-DeviceConnectionStatus: disconnected).|Er zijn geen dimensies|
|Outgoing.WNS.pnserror|WNS-fouten|Count|Totaal|De melding is niet afgeleverd omdat er fouten zijn opgetreden in de communicatie met WNS.|Er zijn geen dimensies|
|Outgoing.WNS.authenticationerror|WNS-verificatiefouten|Count|Totaal|De melding is niet afgeleverd omdat er fouten zijn opgetreden in de communicatie met Windows Live, vanwege ongeldige referenties of vanwege een onjuist token.|Er zijn geen dimensies|
|Outgoing.apns.Success|Meldingen over voltooide APNS|Count|Totaal|Het aantal voltooide meldingen.|Er zijn geen dimensies|
|Outgoing.apns.invalidcredentials|APNS-verificatiefouten|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert of omdat de referenties zijn geblokkeerd.|Er zijn geen dimensies|
|outgoing.apns.badchannel|APNS-fout wegens slecht kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat het token ongeldig is (APNS-statuscode: 8).|Er zijn geen dimensies|
|outgoing.apns.expiredchannel|APNS-fout wegens verlopen kanaal|Count|Totaal|Het aantal tokens dat ongeldig is gemaakt door het APNS-feedbackkanaal.|Er zijn geen dimensies|
|Outgoing.apns.invalidnotificationsize|Fout met ongeldige grootte van APNS-melding|Count|Totaal|Het aantal pushes dat is mislukt omdat de payload te groot is (APNS-statuscode: 7).|Er zijn geen dimensies|
|Outgoing.apns.pnserror|APNS-fouten|Count|Totaal|Het aantal pushes dat is mislukt vanwege fouten in de communicatie met APNS.|Er zijn geen dimensies|
|Outgoing.GCM.Success|Meldingen over voltooide GCM|Count|Totaal|Het aantal voltooide meldingen.|Er zijn geen dimensies|
|Outgoing.GCM.invalidcredentials|GCM-verificatiefouten (ongeldige referenties)|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert of omdat de referenties zijn geblokkeerd.|Er zijn geen dimensies|
|outgoing.gcm.badchannel|GCM-fout wegens slecht kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de registratie-id in de registratie niet is herkend (GCM-resultaat: ongeldige registratie).|Er zijn geen dimensies|
|outgoing.gcm.expiredchannel|GCM-fout wegens verlopen kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de registratie-id in de registratie is verlopen (GCM-resultaat: NotRegistered).|Er zijn geen dimensies|
|Outgoing.GCM.throttled|Meldingen over beperkte GCM|Count|Totaal|Het aantal pushes dat is mislukt omdat GCM deze app heeft beperkt (GCM-statuscode: 501-599 of result:Unavailable).|Er zijn geen dimensies|
|Outgoing.GCM.invalidnotificationformat|Ongeldige indeling van GCM-melding|Count|Totaal|Het aantal pushes dat is mislukt omdat de payload niet juist is opgemaakt (GCM-resultaat: InvalidDataKey of InvalidTtl).|Er zijn geen dimensies|
|Outgoing.GCM.invalidnotificationsize|Fout met ongeldige grootte van GCM-melding|Count|Totaal|Het aantal pushes dat is mislukt omdat de payload te groot is (GCM-resultaat: MessageTooBig).|Er zijn geen dimensies|
|outgoing.gcm.wrongchannel|GCM-fout wegens onjuist kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de registratie-id in de registratie niet is gekoppeld aan de huidige app (GCM-resultaat: InvalidPackageName).|Er zijn geen dimensies|
|Outgoing.GCM.pnserror|GCM-fouten|Count|Totaal|Het aantal pushes dat is mislukt vanwege fouten in de communicatie met GCM.|Er zijn geen dimensies|
|Outgoing.GCM.authenticationerror|GCM-verificatiefouten|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert, omdat de referenties zijn geblokkeerd of omdat de id van de afzender niet juist is geconfigureerd in de app (GCM-resultaat: MismatchedSenderId).|Er zijn geen dimensies|
|Outgoing.mpns.Success|Meldingen over voltooide MPNS|Count|Totaal|Het aantal voltooide meldingen.|Er zijn geen dimensies|
|Outgoing.mpns.invalidcredentials|Ongeldige MPNS-referenties|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert of omdat de referenties zijn geblokkeerd.|Er zijn geen dimensies|
|outgoing.mpns.badchannel|MPNS-fout wegens slecht kanaal|Count|Totaal|Het aantal pushes dat is mislukt omdat de kanaal-URI in de registratie niet is herkend (MPNS-status: 404 - Niet gevonden).|Er zijn geen dimensies|
|Outgoing.mpns.throttled|Meldingen over beperkte MPNS|Count|Totaal|Het aantal pushes dat is mislukt omdat MPNS deze app beperkt (WNS MPNS: 406 - Niet geaccepteerd).|Er zijn geen dimensies|
|Outgoing.mpns.invalidnotificationformat|Ongeldige indeling van de MPNS-melding|Count|Totaal|Het aantal pushes dat is mislukt omdat de payload van de melding te groot is.|Er zijn geen dimensies|
|outgoing.mpns.channeldisconnected|De verbinding met het MPNS-kanaal is verbroken|Count|Totaal|Het aantal pushes dat is mislukt omdat de kanaal-URI in de registratie niet is verbonden (MPNS-status: 412 - Niet gevonden).|Er zijn geen dimensies|
|Outgoing.mpns.Dropped|Meldingen over verloren MPNS|Count|Totaal|Het aantal pushes dat is verwijderd door MPNS (MPNS-reactieheader: X-NotificationStatus: QueueFull of Suppressed).|Er zijn geen dimensies|
|Outgoing.mpns.pnserror|MPNS-fouten|Count|Totaal|Het aantal pushes dat is mislukt vanwege fouten in de communicatie met MPNS.|Er zijn geen dimensies|
|Outgoing.mpns.authenticationerror|MPNS-verificatiefouten|Count|Totaal|Het aantal pushes dat is mislukt omdat PNS de opgegeven referenties niet accepteert of omdat de referenties zijn geblokkeerd.|Er zijn geen dimensies|
|notificationhub.pushes|Alle uitgaande meldingen|Count|Totaal|Alle uitgaande meldingen van de Notification Hub|Er zijn geen dimensies|
|Incoming.all.Requests|Alle binnenkomende aanvragen|Count|Totaal|Totaal aantal binnenkomende aanvragen voor een Notification Hub|Er zijn geen dimensies|
|Incoming.all.failedrequests|Alle binnenkomende mislukte aanvragen|Count|Totaal|Totaal aantal binnenkomende mislukte aanvragen voor een Notification Hub|Er zijn geen dimensies|

## <a name="microsoftoperationalinsightsworkspaces"></a>Microsoft.OperationalInsights/workspaces
(Openbare Preview)

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Average_ percentage vrije Inodes|Average_ percentage vrije Inodes|Count|Gemiddeld|Average_ percentage vrije Inodes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ % vrije ruimte|Average_ % vrije ruimte|Count|Gemiddeld|Average_ % vrije ruimte|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage gebruikte Inodes|Average_ percentage gebruikte Inodes|Count|Gemiddeld|Average_ percentage gebruikte Inodes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage gebruikte ruimte|Average_ percentage gebruikte ruimte|Count|Gemiddeld|Average_ percentage gebruikte ruimte|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk gelezen Bytes per seconde|Average_Disk gelezen Bytes per seconde|Count|Gemiddeld|Average_Disk gelezen Bytes per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk Reads/sec|Average_Disk Reads/sec|Count|Gemiddeld|Average_Disk Reads/sec|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk Schijfoverdrachten per seconde|Average_Disk Schijfoverdrachten per seconde|Count|Gemiddeld|Average_Disk Schijfoverdrachten per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk geschreven Bytes per seconde|Average_Disk geschreven Bytes per seconde|Count|Gemiddeld|Average_Disk geschreven Bytes per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk schrijfbewerkingen per seconde|Average_Disk schrijfbewerkingen per seconde|Count|Gemiddeld|Average_Disk schrijfbewerkingen per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Free Megabytes|Average_Free Megabytes|Count|Gemiddeld|Average_Free Megabytes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Logical gelezen Bytes per seconde|Average_Logical gelezen Bytes per seconde|Count|Gemiddeld|Average_Logical gelezen Bytes per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage beschikbaar geheugen|Average_ percentage beschikbaar geheugen|Count|Gemiddeld|Average_ percentage beschikbaar geheugen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Percentage beschikbare wisselruimte Average_|Percentage beschikbare wisselruimte Average_|Count|Gemiddeld|Percentage beschikbare wisselruimte Average_|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage gebruikt geheugen|Average_ percentage gebruikt geheugen|Count|Gemiddeld|Average_ percentage gebruikt geheugen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage gebruikte wisselruimte|Average_ percentage gebruikte wisselruimte|Count|Gemiddeld|Average_ percentage gebruikte wisselruimte|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Geheugen in megabytes Average_Available|Geheugen in megabytes Average_Available|Count|Gemiddeld|Geheugen in megabytes Average_Available|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Available megabytes voor wisselen|Average_Available megabytes voor wisselen|Count|Gemiddeld|Average_Available megabytes voor wisselen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Page leesbewerkingen per seconde|Average_Page leesbewerkingen per seconde|Count|Gemiddeld|Average_Page leesbewerkingen per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Page schrijfbewerkingen per seconde|Average_Page schrijfbewerkingen per seconde|Count|Gemiddeld|Average_Page schrijfbewerkingen per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Pages per seconde|Average_Pages per seconde|Count|Gemiddeld|Average_Pages per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Used megabytes voor wisselen ruimte|Average_Used megabytes voor wisselen ruimte|Count|Gemiddeld|Average_Used megabytes voor wisselen ruimte|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Used geheugen in megabytes|Average_Used geheugen in megabytes|Count|Gemiddeld|Average_Used geheugen in megabytes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total Bytes verzonden|Average_Total Bytes verzonden|Count|Gemiddeld|Average_Total Bytes verzonden|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total Bytes ontvangen|Average_Total Bytes ontvangen|Count|Gemiddeld|Average_Total Bytes ontvangen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total Bytes|Average_Total Bytes|Count|Gemiddeld|Average_Total Bytes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Verzonden Average_Total pakketten|Verzonden Average_Total pakketten|Count|Gemiddeld|Verzonden Average_Total pakketten|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total pakketten ontvangen|Average_Total pakketten ontvangen|Count|Gemiddeld|Average_Total pakketten ontvangen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total Rx-fouten|Average_Total Rx-fouten|Count|Gemiddeld|Average_Total Rx-fouten|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total Tx-fouten|Average_Total Tx-fouten|Count|Gemiddeld|Average_Total Tx-fouten|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Total conflicten|Average_Total conflicten|Count|Gemiddeld|Average_Total conflicten|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Avg. Leestijd schijf|Average_Avg. Leestijd schijf|Count|Gemiddeld|Average_Avg. Leestijd schijf|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Avg. Schijfoverdrachten per seconde|Average_Avg. Schijfoverdrachten per seconde|Count|Gemiddeld|Average_Avg. Schijfoverdrachten per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Avg. Schrijftijd schijf|Average_Avg. Schrijftijd schijf|Count|Gemiddeld|Average_Avg. Schrijftijd schijf|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Physical gelezen Bytes per seconde|Average_Physical gelezen Bytes per seconde|Count|Gemiddeld|Average_Physical gelezen Bytes per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Tijd in beschermde modus Average_Pct|Tijd in beschermde modus Average_Pct|Count|Gemiddeld|Tijd in beschermde modus Average_Pct|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Tijd in gebruikersmodus van Average_Pct|Tijd in gebruikersmodus van Average_Pct|Count|Gemiddeld|Tijd in gebruikersmodus van Average_Pct|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Used geheugen kB|Average_Used geheugen kB|Count|Gemiddeld|Average_Used geheugen kB|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Virtual gedeeld geheugen|Average_Virtual gedeeld geheugen|Count|Gemiddeld|Average_Virtual gedeeld geheugen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage DPC-tijd|Average_ percentage DPC-tijd|Count|Gemiddeld|Average_ percentage DPC-tijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage niet-actieve tijd|Average_ percentage niet-actieve tijd|Count|Gemiddeld|Average_ percentage niet-actieve tijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage Interrupt-tijd|Average_ percentage Interrupt-tijd|Count|Gemiddeld|Average_ percentage Interrupt-tijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ % i/o-wachttijd|Average_ % i/o-wachttijd|Count|Gemiddeld|Average_ % i/o-wachttijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage tijd in Nice|Average_ percentage tijd in Nice|Count|Gemiddeld|Average_ percentage tijd in Nice|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Tijd in beschermde modus Average_ %|Tijd in beschermde modus Average_ %|Count|Gemiddeld|Tijd in beschermde modus Average_ %|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage processortijd|Average_ percentage processortijd|Count|Gemiddeld|Average_ percentage processortijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage tijd in gebruikersmodus|Average_ percentage tijd in gebruikersmodus|Count|Gemiddeld|Average_ percentage tijd in gebruikersmodus|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Free fysiek geheugen|Average_Free fysiek geheugen|Count|Gemiddeld|Average_Free fysiek geheugen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Free ruimte in Wisselgeheugenbestanden|Average_Free ruimte in Wisselgeheugenbestanden|Count|Gemiddeld|Average_Free ruimte in Wisselgeheugenbestanden|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Free virtueel geheugen|Average_Free virtueel geheugen|Count|Gemiddeld|Average_Free virtueel geheugen|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Processes|Average_Processes|Count|Gemiddeld|Average_Processes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Size opgeslagen In Pagineringbestanden|Average_Size opgeslagen In Pagineringbestanden|Count|Gemiddeld|Average_Size opgeslagen In Pagineringbestanden|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Uptime|Average_Uptime|Count|Gemiddeld|Average_Uptime|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Users|Average_Users|Count|Gemiddeld|Average_Users|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Avg. Leestijd schijf|Average_Avg. Leestijd schijf|Count|Gemiddeld|Average_Avg. Leestijd schijf|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Avg. Schrijftijd schijf|Average_Avg. Schrijftijd schijf|Count|Gemiddeld|Average_Avg. Schrijftijd schijf|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Wachtrijlengte voor schijf Average_Current|Wachtrijlengte voor schijf Average_Current|Count|Gemiddeld|Wachtrijlengte voor schijf Average_Current|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk Reads/sec|Average_Disk Reads/sec|Count|Gemiddeld|Average_Disk Reads/sec|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk Schijfoverdrachten per seconde|Average_Disk Schijfoverdrachten per seconde|Count|Gemiddeld|Average_Disk Schijfoverdrachten per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Disk schrijfbewerkingen per seconde|Average_Disk schrijfbewerkingen per seconde|Count|Gemiddeld|Average_Disk schrijfbewerkingen per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Free Megabytes|Average_Free Megabytes|Count|Gemiddeld|Average_Free Megabytes|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ % vrije ruimte|Average_ % vrije ruimte|Count|Gemiddeld|Average_ % vrije ruimte|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Available megabytes (MB)|Average_Available megabytes (MB)|Count|Gemiddeld|Average_Available megabytes (MB)|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage toegewezen Bytes In gebruik|Average_ percentage toegewezen Bytes In gebruik|Count|Gemiddeld|Average_ percentage toegewezen Bytes In gebruik|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Bytes ontvangen per seconde|Average_Bytes ontvangen per seconde|Count|Gemiddeld|Average_Bytes ontvangen per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_Bytes verzonden per seconde|Average_Bytes verzonden per seconde|Count|Gemiddeld|Average_Bytes verzonden per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Totaal aantal Average_Bytes per seconde|Totaal aantal Average_Bytes per seconde|Count|Gemiddeld|Totaal aantal Average_Bytes per seconde|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Average_ percentage processortijd|Average_ percentage processortijd|Count|Gemiddeld|Average_ percentage processortijd|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Wachtrijlengte van Average_Processor|Wachtrijlengte van Average_Processor|Count|Gemiddeld|Wachtrijlengte van Average_Processor|Objectnaam, InstanceName, itempad, SourceSystem-computer|
|Heartbeat|Heartbeat|Count|Gemiddeld|Heartbeat|Computer, besturingssysteemtype, versie, SourceComputerId|
|Update|Update|Count|Gemiddeld|Update|Computer, Product, classificatie, UpdateState, optioneel, goedgekeurde|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|QueryDuration|Duur van de query|Milliseconden|Gemiddeld|Duur van een DAX-Query in de laatste interval|Er zijn geen dimensies|
|QueryPoolJobQueueLength|Threads: Wachtrijlengte taak query uitvoeren|Count|Gemiddeld|Het aantal taken in de wachtrij van de threadgroep query.|Er zijn geen dimensies|
|qpu_high_utilization_metric|Hoog gebruik QPU|Count|Totaal|QPU hoog gebruik In de laatste minuut, 1 voor gebruik van de hoge QPU anders 0|Er zijn geen dimensies|
|memory_metric|Geheugen|Bytes|Gemiddeld|Geheugen. Het bereik 0-3 GB voor A1, 0-5 GB voor de A2, 0-10 GB voor de A3, 0-25 GB voor A4, 0-50 GB voor A5 en 0-100 GB voor A6|Er zijn geen dimensies|
|memory_thrashing_metric|Geheugen voorkomen|Procent|Gemiddeld|Gemiddelde geheugen thrashing.|Er zijn geen dimensies|

## <a name="microsoftrelaynamespaces"></a>Microsoft.Relay/namespaces

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ListenerConnections-Success|ListenerConnections-Success|Count|Totaal|Voltooide ListenerConnections voor Microsoft.Relay.|EntityName|
|ListenerConnections-ClientError|ListenerConnections-ClientError|Count|Totaal|ClientError op ListenerConnections voor Microsoft.Relay.|EntityName|
|ListenerConnections-ServerError|ListenerConnections-ServerError|Count|Totaal|ServerError op ListenerConnections voor Microsoft.Relay.|EntityName|
|SenderConnections-Success|SenderConnections-Success|Count|Totaal|Voltooide SenderConnections voor Microsoft.Relay.|EntityName|
|SenderConnections-ClientError|SenderConnections-ClientError|Count|Totaal|ClientError op SenderConnections voor Microsoft.Relay.|EntityName|
|SenderConnections-ServerError|SenderConnections-ServerError|Count|Totaal|ServerError op SenderConnections voor Microsoft.Relay.|EntityName|
|ListenerConnections-TotalRequests|ListenerConnections-TotalRequests|Count|Totaal|Totale ListenerConnections voor Microsoft.Relay.|EntityName|
|SenderConnections-TotalRequests|SenderConnections-TotalRequests|Count|Totaal|Totale SenderConnections-aanvragen voor Microsoft.Relay.|EntityName|
|ActiveConnections|ActiveConnections|Count|Totaal|Totale ActiveConnections voor Microsoft.Relay.|EntityName|
|ActiveListeners|ActiveListeners|Count|Totaal|Totale ActiveListeners voor Microsoft.Relay.|EntityName|
|BytesTransferred|BytesTransferred|Count|Totaal|Totale BytesTransferred voor Microsoft.Relay.|EntityName|
|ListenerDisconnects|ListenerDisconnects|Count|Totaal|Totale ListenerDisconnects voor Microsoft.Relay.|EntityName|
|SenderDisconnects|SenderDisconnects|Count|Totaal|Total SenderDisconnects for Microsoft.Relay.|EntityName|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|SearchLatency|Latentie zoeken|Seconden|Gemiddeld|Gemiddelde zoeken latentie voor de search-service|Er zijn geen dimensies|
|SearchQueriesPerSecond|Zoekquery's per seconde|CountPerSecond|Gemiddeld|Zoekquery's per seconde voor de search-service|Er zijn geen dimensies|
|ThrottledSearchQueriesPercentage|Percentage beperkte zoekquery's|Procent|Gemiddeld|Percentage van de zoekquery's die zijn beperkt voor de search-service|Er zijn geen dimensies|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|SuccessfulRequests|Geslaagde aanvragen (Preview)|Count|Totaal|Totaal aantal geslaagde aanvragen voor een naamruimte (Preview)|Het EntityName, |
|ServerErrors|Serverfouten. (Preview)|Count|Totaal|Serverfouten voor Microsoft.ServiceBus. (Preview)|Het EntityName, |
|UserErrors|Gebruikersfouten. (Preview)|Count|Totaal|Gebruikersfouten voor Microsoft.ServiceBus. (Preview)|Het EntityName, |
|ThrottledRequests|Beperkte aanvragen. (Preview)|Count|Totaal|Beperkte aanvragen voor Microsoft.ServiceBus. (Preview)|Het EntityName, |
|IncomingRequests|Inkomende aanvragen (Preview)|Count|Totaal|Binnenkomende aanvragen voor Microsoft.ServiceBus. (Preview)|EntityName|
|IncomingMessages|Binnenkomende berichten (Preview)|Count|Totaal|Binnenkomende berichten voor Microsoft.ServiceBus. (Preview)|EntityName|
|OutgoingMessages|Uitgaande berichten (Preview)|Count|Totaal|Uitgaande berichten voor Microsoft.ServiceBus. (Preview)|EntityName|
|ActiveConnections|ActiveConnections (Preview)|Count|Totaal|Totaal aantal actieve verbindingen voor Microsoft.ServiceBus. (Preview)|Er zijn geen dimensies|
|Grootte|Grootte (Preview)|Bytes|Gemiddeld|Grootte van een wachtrij/onderwerp in Bytes. (Preview)|EntityName|
|Berichten|Het aantal berichten in een wachtrij/onderwerp. (Preview)|Count|Gemiddeld|Het aantal berichten in een wachtrij/onderwerp. (Preview)|EntityName|
|ActiveMessages|Het aantal actieve berichten in een wachtrij/onderwerp. (Preview)|Count|Gemiddeld|Het aantal actieve berichten in een wachtrij/onderwerp. (Preview)|EntityName|
|CPUXNS|CPU-gebruik per naamruimte|Procent|Maximum|Metrische gegevens voor het CPU-gebruik van de Premium-naamruimte voor Service Bus|Er zijn geen dimensies|
|WSXNS|Geheugengebruik per naamruimte|Procent|Maximum|Metrische gegevens voor het geheugengebruik van de Premium-naamruimte voor Service Bus|Er zijn geen dimensies|

## <a name="microsoftsignalrservicesignalr"></a>Microsoft.SignalRService/SignalR

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ConnectionCount|Aantal verbindingen|Count|Maximum|De hoeveelheid gebruikersverbinding.|Er zijn geen dimensies|
|ConnectionCountPerSecond|Het aantal verbindingen Per seconde|CountPerSecond|Gemiddeld|Het aantal gemiddelde verbindingen per seconde.|Er zijn geen dimensies|
|MessageCount|Aantal berichten|Count|Maximum|De totale hoeveelheid bericht in de maand|Er zijn geen dimensies|
|MessageCountPerSecond|Aantal berichten Per seconde|CountPerSecond|Gemiddeld|Het gemiddelde aantal bericht|Er zijn geen dimensies|
|MessageUsed|Bericht dat wordt gebruikt|Procent|Maximum|Het percentage van de berichten zijn gebruikt in de maand|Er zijn geen dimensies|
|ConnectionUsed|Verbinding die wordt gebruikt|Procent|Maximum|Het percentage van de verbindingen zijn gebruikt|Er zijn geen dimensies|
|UserErrors|Gebruikersfouten|Procent|Maximum|Het percentage van de gebruikersfouten|Er zijn geen dimensies|
|SystemErrors|Fouten in het bestandssysteem|Procent|Maximum|Het percentage van de fouten in het bestandssysteem|Er zijn geen dimensies|
|SystemLoad|Systeembelasting|Procent|Maximum|Het percentage van de systeembelasting|Er zijn geen dimensies|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Er zijn geen dimensies|
|physical_data_read_percent|Gegevens-I/O-percentage|Procent|Gemiddeld|Gegevens-I/O-percentage|Er zijn geen dimensies|
|log_write_percent|Percentage van logboek-i/o|Procent|Gemiddeld|Percentage van logboek-i/o|Er zijn geen dimensies|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddeld|DTU-percentage|Er zijn geen dimensies|
|opslag|Totale grootte|Bytes|Maximum|Totale grootte|Er zijn geen dimensies|
|connection_successful|Geslaagde verbindingen|Count|Totaal|Geslaagde verbindingen|Er zijn geen dimensies|
|connection_failed|Mislukte verbindingen|Count|Totaal|Mislukte verbindingen|Er zijn geen dimensies|
|blocked_by_firewall|Geblokkeerd door een Firewall|Count|Totaal|Geblokkeerd door een Firewall|Er zijn geen dimensies|
|impasse|Impassen|Count|Totaal|Impassen|Er zijn geen dimensies|
|storage_percent|Databaseomvangpercentage|Procent|Maximum|Databaseomvangpercentage|Er zijn geen dimensies|
|xtp_storage_percent|In het geheugen OLTP opslag procent|Procent|Gemiddeld|In het geheugen OLTP opslag procent|Er zijn geen dimensies|
|workers_percent|Percentage van de werknemers|Procent|Gemiddeld|Percentage van de werknemers|Er zijn geen dimensies|
|sessions_percent|Percentage van sessies|Procent|Gemiddeld|Percentage van sessies|Er zijn geen dimensies|
|dtu_limit|DTU limiet|Count|Gemiddeld|DTU limiet|Er zijn geen dimensies|
|dtu_used|DTU gebruikt|Count|Gemiddeld|DTU gebruikt|Er zijn geen dimensies|
|dwu_limit|DWU-limiet|Count|Maximum|DWU-limiet|Er zijn geen dimensies|
|dwu_consumption_percent|DWU-percentage|Procent|Maximum|DWU-percentage|Er zijn geen dimensies|
|dwu_used|DWU gebruikt|Count|Maximum|DWU gebruikt|Er zijn geen dimensies|
|dw_cpu_percent|DW-knooppuntniveau CPU-percentage|Procent|Gemiddeld|DW-knooppuntniveau CPU-percentage|DwLogicalNodeId|
|dw_physical_data_read_percent|DW knooppunt niveau gegevens IO-percentage|Procent|Gemiddeld|DW knooppunt niveau gegevens IO-percentage|DwLogicalNodeId|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|cpu_percent|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Er zijn geen dimensies|
|physical_data_read_percent|Gegevens-I/O-percentage|Procent|Gemiddeld|Gegevens-I/O-percentage|Er zijn geen dimensies|
|log_write_percent|Percentage van logboek-i/o|Procent|Gemiddeld|Percentage van logboek-i/o|Er zijn geen dimensies|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddeld|DTU-percentage|Er zijn geen dimensies|
|storage_percent|Opslagpercentage|Procent|Gemiddeld|Opslagpercentage|Er zijn geen dimensies|
|workers_percent|Percentage van de werknemers|Procent|Gemiddeld|Percentage van de werknemers|Er zijn geen dimensies|
|sessions_percent|Percentage van sessies|Procent|Gemiddeld|Percentage van sessies|Er zijn geen dimensies|
|eDTU_limit|limiet voor eDTU|Count|Gemiddeld|limiet voor eDTU|Er zijn geen dimensies|
|storage_limit|Opslaglimiet bereikt|Bytes|Gemiddeld|Opslaglimiet bereikt|Er zijn geen dimensies|
|eDTU_used|eDTU gebruikt|Count|Gemiddeld|eDTU gebruikt|Er zijn geen dimensies|
|storage_used|Gebruikte opslag|Bytes|Gemiddeld|Gebruikte opslag|Er zijn geen dimensies|
|xtp_storage_percent|In het geheugen OLTP opslag procent|Procent|Gemiddeld|In het geheugen OLTP opslag procent|Er zijn geen dimensies|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|dtu_consumption_percent|DTU-percentage|Procent|Gemiddeld|DTU-percentage|ElasticPoolResourceId|
|storage_used|Gebruikte opslag|Bytes|Gemiddeld|Gebruikte opslag|ElasticPoolResourceId|

## <a name="microsoftstoragestorageaccounts"></a>Microsoft.Storage/storageAccounts

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|UsedCapacity|Gebruikte capaciteit|Bytes|Gemiddeld|Gebruikte capaciteit van account|Er zijn geen dimensies|
|Transacties|Transacties|Count|Totaal|Het aantal aanvragen voor een opslagservice of de opgegeven API-bewerking. Dit is inclusief geslaagde en mislukte aanvragen als aanvragen die fouten geproduceerd. ResponseType dimensie gebruiken voor het aantal ander type van het antwoord.|ResponseType, GeoType, ApiName|
|Binnenkomend|Binnenkomend|Bytes|Totaal|De hoeveelheid inkomend gegevens, in bytes. Hieronder vallen de inkomende gegevens van een externe client in Azure Storage evenals de inkomende gegevens binnen Azure.|GeoType, ApiName|
|Uitgaand verkeer|Uitgaand verkeer|Bytes|Totaal|De hoeveelheid gegevens van de uitgaande, in bytes. Hieronder vallen de uitgaande gegevens van een externe client in Azure Storage evenals de uitgaande gegevens binnen Azure. Daarom geeft deze hoeveelheid niet de factureerbare uitgaande gegevens weer.|GeoType, ApiName|
|SuccessServerLatency|Geslaagde serverlatentie|Milliseconden|Gemiddeld|De gemiddelde latentie die wordt gebruikt door Azure Storage voor het verwerken van aanvraag is gelukt, in milliseconden. Deze waarde is niet de netwerklatentie die is opgegeven in AverageE2ELatency opgenomen.|GeoType, ApiName|
|SuccessE2ELatency|Geslaagde E2E-latentie|Milliseconden|Gemiddeld|De gemiddelde end-to-end-latentie van geslaagde aanvragen voor een opslagservice of de opgegeven API-bewerking, in milliseconden. Deze waarde bevat de vereiste verwerkingstijd in Azure Storage die nodig is om de aanvraag te lezen, het antwoord te verzenden en bevestiging van het antwoord te ontvangen.|GeoType, ApiName|
|Beschikbaarheid|Beschikbaarheid|Procent|Gemiddeld|Het percentage van de beschikbaarheid van de storage-service of de opgegeven API-bewerking. Beschikbaarheid wordt berekend door de waarde TotalBillableRequests nemen en deze te delen door het aantal van toepassing aanvragen, waaronder de geproduceerd onverwachte fouten. Alle onverwachte fouten leiden tot beperkte beschikbaarheid voor de storage-service of de opgegeven API-bewerking.|GeoType, ApiName|

## <a name="microsoftstoragestorageaccountsblobservices"></a>Microsoft.Storage/storageAccounts/blobServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|BlobCapacity|Blobcapaciteit|Bytes|Totaal|De hoeveelheid opslag die wordt gebruikt door de Blob-service van het opslagaccount (in bytes).|BlobType|
|BlobCount|Aantal blobs|Count|Totaal|Het aantal blobs in de Blob-service van het opslagaccount.|BlobType|
|ContainerCount|Aantal blobcontainers|Count|Gemiddeld|Het aantal containers in de Blob-service van het opslagaccount.|Er zijn geen dimensies|
|Transacties|Transacties|Count|Totaal|Het aantal aanvragen voor een opslagservice of de opgegeven API-bewerking. Dit is inclusief geslaagde en mislukte aanvragen als aanvragen die fouten geproduceerd. ResponseType dimensie gebruiken voor het aantal ander type van het antwoord.|ResponseType, GeoType, ApiName|
|Binnenkomend|Binnenkomend|Bytes|Totaal|De hoeveelheid inkomend gegevens, in bytes. Hieronder vallen de inkomende gegevens van een externe client in Azure Storage evenals de inkomende gegevens binnen Azure.|GeoType, ApiName|
|Uitgaand verkeer|Uitgaand verkeer|Bytes|Totaal|De hoeveelheid gegevens van de uitgaande, in bytes. Hieronder vallen de uitgaande gegevens van een externe client in Azure Storage evenals de uitgaande gegevens binnen Azure. Daarom geeft deze hoeveelheid niet de factureerbare uitgaande gegevens weer.|GeoType, ApiName|
|SuccessServerLatency|Geslaagde serverlatentie|Milliseconden|Gemiddeld|De gemiddelde latentie die wordt gebruikt door Azure Storage voor het verwerken van aanvraag is gelukt, in milliseconden. Deze waarde is niet de netwerklatentie die is opgegeven in AverageE2ELatency opgenomen.|GeoType, ApiName|
|SuccessE2ELatency|Geslaagde E2E-latentie|Milliseconden|Gemiddeld|De gemiddelde end-to-end-latentie van geslaagde aanvragen voor een opslagservice of de opgegeven API-bewerking, in milliseconden. Deze waarde bevat de vereiste verwerkingstijd in Azure Storage die nodig is om de aanvraag te lezen, het antwoord te verzenden en bevestiging van het antwoord te ontvangen.|GeoType, ApiName|
|Beschikbaarheid|Beschikbaarheid|Procent|Gemiddeld|Het percentage van de beschikbaarheid van de storage-service of de opgegeven API-bewerking. Beschikbaarheid wordt berekend door de waarde TotalBillableRequests nemen en deze te delen door het aantal van toepassing aanvragen, waaronder de geproduceerd onverwachte fouten. Alle onverwachte fouten leiden tot beperkte beschikbaarheid voor de storage-service of de opgegeven API-bewerking.|GeoType, ApiName|

## <a name="microsoftstoragestorageaccountstableservices"></a>Microsoft.Storage/storageAccounts/tableServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|TableCapacity|Tabelcapaciteit|Bytes|Gemiddeld|De hoeveelheid opslag die wordt gebruikt door de Table-service van het opslagaccount (in bytes).|Er zijn geen dimensies|
|TableCount|Aantal tabellen|Count|Gemiddeld|Het aantal tabellen in de Table-service van het opslagaccount.|Er zijn geen dimensies|
|TableEntityCount|Aantal tabelentiteiten|Count|Gemiddeld|Het aantal tabelentiteiten in de Table-service van het opslagaccount.|Er zijn geen dimensies|
|Transacties|Transacties|Count|Totaal|Het aantal aanvragen voor een opslagservice of de opgegeven API-bewerking. Dit is inclusief geslaagde en mislukte aanvragen als aanvragen die fouten geproduceerd. ResponseType dimensie gebruiken voor het aantal ander type van het antwoord.|ResponseType, GeoType, ApiName|
|Binnenkomend|Binnenkomend|Bytes|Totaal|De hoeveelheid inkomend gegevens, in bytes. Hieronder vallen de inkomende gegevens van een externe client in Azure Storage evenals de inkomende gegevens binnen Azure.|GeoType, ApiName|
|Uitgaand verkeer|Uitgaand verkeer|Bytes|Totaal|De hoeveelheid gegevens van de uitgaande, in bytes. Hieronder vallen de uitgaande gegevens van een externe client in Azure Storage evenals de uitgaande gegevens binnen Azure. Daarom geeft deze hoeveelheid niet de factureerbare uitgaande gegevens weer.|GeoType, ApiName|
|SuccessServerLatency|Geslaagde serverlatentie|Milliseconden|Gemiddeld|De gemiddelde latentie die wordt gebruikt door Azure Storage voor het verwerken van aanvraag is gelukt, in milliseconden. Deze waarde is niet de netwerklatentie die is opgegeven in AverageE2ELatency opgenomen.|GeoType, ApiName|
|SuccessE2ELatency|Geslaagde E2E-latentie|Milliseconden|Gemiddeld|De gemiddelde end-to-end-latentie van geslaagde aanvragen voor een opslagservice of de opgegeven API-bewerking, in milliseconden. Deze waarde bevat de vereiste verwerkingstijd in Azure Storage die nodig is om de aanvraag te lezen, het antwoord te verzenden en bevestiging van het antwoord te ontvangen.|GeoType, ApiName|
|Beschikbaarheid|Beschikbaarheid|Procent|Gemiddeld|Het percentage van de beschikbaarheid van de storage-service of de opgegeven API-bewerking. Beschikbaarheid wordt berekend door de waarde TotalBillableRequests nemen en deze te delen door het aantal van toepassing aanvragen, waaronder de geproduceerd onverwachte fouten. Alle onverwachte fouten leiden tot beperkte beschikbaarheid voor de storage-service of de opgegeven API-bewerking.|GeoType, ApiName|

## <a name="microsoftstoragestorageaccountsqueueservices"></a>Microsoft.Storage/storageAccounts/queueServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|QueueCapacity|Wachtrijcapaciteit|Bytes|Gemiddeld|De hoeveelheid opslag die wordt gebruikt door de Queue-service van het opslagaccount (in bytes).|Er zijn geen dimensies|
|QueueCount|Aantal wachtrijen|Count|Gemiddeld|Het aantal wachtrijen in de Queue-service van het opslagaccount.|Er zijn geen dimensies|
|QueueMessageCount|Aantal wachtrijberichten|Count|Gemiddeld|Het geschatte aantal wachtrijberichten in de Queue-service van het opslagaccount.|Er zijn geen dimensies|
|Transacties|Transacties|Count|Totaal|Het aantal aanvragen voor een opslagservice of de opgegeven API-bewerking. Dit is inclusief geslaagde en mislukte aanvragen als aanvragen die fouten geproduceerd. ResponseType dimensie gebruiken voor het aantal ander type van het antwoord.|ResponseType, GeoType, ApiName|
|Binnenkomend|Binnenkomend|Bytes|Totaal|De hoeveelheid inkomend gegevens, in bytes. Hieronder vallen de inkomende gegevens van een externe client in Azure Storage evenals de inkomende gegevens binnen Azure.|GeoType, ApiName|
|Uitgaand verkeer|Uitgaand verkeer|Bytes|Totaal|De hoeveelheid gegevens van de uitgaande, in bytes. Hieronder vallen de uitgaande gegevens van een externe client in Azure Storage evenals de uitgaande gegevens binnen Azure. Daarom geeft deze hoeveelheid niet de factureerbare uitgaande gegevens weer.|GeoType, ApiName|
|SuccessServerLatency|Geslaagde serverlatentie|Milliseconden|Gemiddeld|De gemiddelde latentie die wordt gebruikt door Azure Storage voor het verwerken van aanvraag is gelukt, in milliseconden. Deze waarde is niet de netwerklatentie die is opgegeven in AverageE2ELatency opgenomen.|GeoType, ApiName|
|SuccessE2ELatency|Geslaagde E2E-latentie|Milliseconden|Gemiddeld|De gemiddelde end-to-end-latentie van geslaagde aanvragen voor een opslagservice of de opgegeven API-bewerking, in milliseconden. Deze waarde bevat de vereiste verwerkingstijd in Azure Storage die nodig is om de aanvraag te lezen, het antwoord te verzenden en bevestiging van het antwoord te ontvangen.|GeoType, ApiName|
|Beschikbaarheid|Beschikbaarheid|Procent|Gemiddeld|Het percentage van de beschikbaarheid van de storage-service of de opgegeven API-bewerking. Beschikbaarheid wordt berekend door de waarde TotalBillableRequests nemen en deze te delen door het aantal van toepassing aanvragen, waaronder de geproduceerd onverwachte fouten. Alle onverwachte fouten leiden tot beperkte beschikbaarheid voor de storage-service of de opgegeven API-bewerking.|GeoType, ApiName|

## <a name="microsoftstoragestorageaccountsfileservices"></a>Microsoft.Storage/storageAccounts/fileServices

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|FileCapacity|Bestandscapaciteit|Bytes|Gemiddeld|De hoeveelheid opslag die wordt gebruikt door de File-service van het opslagaccount (in bytes).|Er zijn geen dimensies|
|FileCount|Aantal bestanden|Count|Gemiddeld|Het aantal bestanden in de File-service van het opslagaccount.|Er zijn geen dimensies|
|FileShareCount|Aantal bestandsshares|Count|Gemiddeld|Het aantal bestandsshares in de File-service van het opslagaccount.|Er zijn geen dimensies|
|Transacties|Transacties|Count|Totaal|Het aantal aanvragen voor een opslagservice of de opgegeven API-bewerking. Dit is inclusief geslaagde en mislukte aanvragen als aanvragen die fouten geproduceerd. ResponseType dimensie gebruiken voor het aantal ander type van het antwoord.|ResponseType, GeoType, ApiName|
|Binnenkomend|Binnenkomend|Bytes|Totaal|De hoeveelheid inkomend gegevens, in bytes. Hieronder vallen de inkomende gegevens van een externe client in Azure Storage evenals de inkomende gegevens binnen Azure.|GeoType, ApiName|
|Uitgaand verkeer|Uitgaand verkeer|Bytes|Totaal|De hoeveelheid gegevens van de uitgaande, in bytes. Hieronder vallen de uitgaande gegevens van een externe client in Azure Storage evenals de uitgaande gegevens binnen Azure. Daarom geeft deze hoeveelheid niet de factureerbare uitgaande gegevens weer.|GeoType, ApiName|
|SuccessServerLatency|Geslaagde serverlatentie|Milliseconden|Gemiddeld|De gemiddelde latentie die wordt gebruikt door Azure Storage voor het verwerken van aanvraag is gelukt, in milliseconden. Deze waarde is niet de netwerklatentie die is opgegeven in AverageE2ELatency opgenomen.|GeoType, ApiName|
|SuccessE2ELatency|Geslaagde E2E-latentie|Milliseconden|Gemiddeld|De gemiddelde end-to-end-latentie van geslaagde aanvragen voor een opslagservice of de opgegeven API-bewerking, in milliseconden. Deze waarde bevat de vereiste verwerkingstijd in Azure Storage die nodig is om de aanvraag te lezen, het antwoord te verzenden en bevestiging van het antwoord te ontvangen.|GeoType, ApiName|
|Beschikbaarheid|Beschikbaarheid|Procent|Gemiddeld|Het percentage van de beschikbaarheid van de storage-service of de opgegeven API-bewerking. Beschikbaarheid wordt berekend door de waarde TotalBillableRequests nemen en deze te delen door het aantal van toepassing aanvragen, waaronder de geproduceerd onverwachte fouten. Alle onverwachte fouten leiden tot beperkte beschikbaarheid voor de storage-service of de opgegeven API-bewerking.|GeoType, ApiName|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|ResourceUtilization|Gebruikspercentage voor Streaming-eenheden|Procent|Maximum|Gebruikspercentage voor Streaming-eenheden|Er zijn geen dimensies|
|InputEvents|Invoergebeurtenissen|Count|Totaal|Invoergebeurtenissen|Er zijn geen dimensies|
|InputEventBytes|Invoergebeurtenisbytes|Bytes|Totaal|Invoergebeurtenisbytes|Er zijn geen dimensies|
|LateInputEvents|Late invoergebeurtenissen|Count|Totaal|Late invoergebeurtenissen|Er zijn geen dimensies|
|OutputEvents|Uitvoergebeurtenis|Count|Totaal|Uitvoergebeurtenis|Er zijn geen dimensies|
|ConversionErrors|Gegevensconversiefouten|Count|Totaal|Gegevensconversiefouten|Er zijn geen dimensies|
|Fouten|Runtimefouten|Count|Totaal|Runtimefouten|Er zijn geen dimensies|
|DroppedOrAdjustedEvents|Gebeurtenissen met een andere volgorde|Count|Totaal|Gebeurtenissen met een andere volgorde|Er zijn geen dimensies|
|AMLCalloutRequests|Functieaanvragen|Count|Totaal|Functieaanvragen|Er zijn geen dimensies|
|AMLCalloutFailedRequests|Mislukte functieaanvragen|Count|Totaal|Mislukte functieaanvragen|Er zijn geen dimensies|
|AMLCalloutInputEvents|Functiegebeurtenissen|Count|Totaal|Functiegebeurtenissen|Er zijn geen dimensies|
|DeserializationError|Fouten in invoerdeserialisatie|Count|Totaal|Fouten in invoerdeserialisatie|Er zijn geen dimensies|
|EarlyInputEvents|Gebeurtenissen waarvan de toepassingstijd eerder is dan de aankomsttijd.|Count|Totaal|Gebeurtenissen waarvan de toepassingstijd eerder is dan de aankomsttijd.|Er zijn geen dimensies|

## <a name="microsofttimeseriesinsightsenvironments"></a>Microsoft.TimeSeriesInsights/environments

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|IngressReceivedMessages|Inkomende berichten ontvangen|Count|Totaal|Aantal berichten lezen uit alle Event hub of IoT-hub bronnen van gebeurtenissen|Er zijn geen dimensies|
|IngressReceivedInvalidMessages|Inkomend ontvangen ongeldige berichten|Count|Totaal|Aantal ongeldige berichten lezen uit alle Event hub of IoT-hub bronnen van gebeurtenissen|Er zijn geen dimensies|
|IngressReceivedBytes|Inkomend ontvangen Bytes|Bytes|Totaal|Het aantal bytes lezen uit alle bronnen van gebeurtenissen|Er zijn geen dimensies|
|IngressStoredBytes|Inkomend opgeslagen Bytes|Bytes|Totaal|Totale grootte van gebeurtenissen met succes verwerkt en beschikbaar voor query|Er zijn geen dimensies|
|IngressStoredEvents|Inkomend opgeslagen gebeurtenissen|Count|Totaal|Aantal gebeurtenissen dat platte met succes verwerkt en beschikbaar voor query|Er zijn geen dimensies|
|IngressReceivedMessagesTimeLag|Inkomend ontvangen berichten tijdsinterval|Seconden|Maximum|Verschil tussen de tijd die het bericht is in de wachtrij in de gebeurtenisbron en de tijd die wordt verwerkt in inkomend|Er zijn geen dimensies|
|IngressReceivedMessagesCountLag|Inkomend ontvangen berichten, aantal Lag|Count|Gemiddeld|Verschil tussen het volgnummer van de laatste in de wachtrij bericht in de gebeurtenisstroom partitie en volgorde aantal bericht dat wordt verwerkt in inkomend bron|Er zijn geen dimensies|

## <a name="microsofttimeseriesinsightsenvironmentseventsources"></a>Microsoft.TimeSeriesInsights/environments/eventsources

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|IngressReceivedMessages|Inkomende berichten ontvangen|Count|Totaal|Aantal berichten lezen uit de bron van gebeurtenis|Er zijn geen dimensies|
|IngressReceivedInvalidMessages|Inkomend ontvangen ongeldige berichten|Count|Totaal|Aantal ongeldige berichten lezen uit de bron van gebeurtenis|Er zijn geen dimensies|
|IngressReceivedBytes|Inkomend ontvangen Bytes|Bytes|Totaal|Het aantal bytes lezen uit de bron van gebeurtenis|Er zijn geen dimensies|
|IngressStoredBytes|Inkomend opgeslagen Bytes|Bytes|Totaal|Totale grootte van gebeurtenissen met succes verwerkt en beschikbaar voor query|Er zijn geen dimensies|
|IngressStoredEvents|Inkomend opgeslagen gebeurtenissen|Count|Totaal|Aantal gebeurtenissen dat platte met succes verwerkt en beschikbaar voor query|Er zijn geen dimensies|
|IngressReceivedMessagesTimeLag|Inkomend ontvangen berichten tijdsinterval|Seconden|Maximum|Verschil tussen de tijd die het bericht is in de wachtrij in de gebeurtenisbron en de tijd die wordt verwerkt in inkomend|Er zijn geen dimensies|
|IngressReceivedMessagesCountLag|Inkomend ontvangen berichten, aantal Lag|Count|Gemiddeld|Verschil tussen het volgnummer van de laatste in de wachtrij bericht in de gebeurtenisstroom partitie en volgorde aantal bericht dat wordt verwerkt in inkomend bron|Er zijn geen dimensies|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|CpuPercentage|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Exemplaar|
|MemoryPercentage|Geheugenpercentage|Procent|Gemiddeld|Geheugenpercentage|Exemplaar|
|DiskQueueLength|Lengte van de wachtrij voor de schijf|Count|Gemiddeld|Lengte van de wachtrij voor de schijf|Exemplaar|
|HttpQueueLength|Lengte van de HTTP-wachtrij|Count|Gemiddeld|Lengte van de HTTP-wachtrij|Exemplaar|
|BytesReceived|Inkomende gegevens|Bytes|Totaal|Inkomende gegevens|Exemplaar|
|BytesSent|Uitgaande gegevens|Bytes|Totaal|Uitgaande gegevens|Exemplaar|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (met uitzondering van de functies)

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|CpuTime|CPU-tijd|Seconden|Totaal|CPU-tijd|Exemplaar|
|Aanvragen|Aanvragen|Count|Totaal|Aanvragen|Exemplaar|
|BytesReceived|Inkomende gegevens|Bytes|Totaal|Inkomende gegevens|Exemplaar|
|BytesSent|Uitgaande gegevens|Bytes|Totaal|Uitgaande gegevens|Exemplaar|
|Http101|HTTP-fout 101|Count|Totaal|HTTP-fout 101|Exemplaar|
|Http2xx|HTTP 2xx|Count|Totaal|HTTP 2xx|Exemplaar|
|Http3xx|HTTP 3xx|Count|Totaal|HTTP 3xx|Exemplaar|
|Http401|HTTP 401|Count|Totaal|HTTP 401|Exemplaar|
|Http403|HTTP-fout 403|Count|Totaal|HTTP-fout 403|Exemplaar|
|Http404|HTTP-fout 404|Count|Totaal|HTTP-fout 404|Exemplaar|
|Http406|HTTP-fout 406|Count|Totaal|HTTP-fout 406|Exemplaar|
|Http4xx|Http 4xx|Count|Totaal|Http 4xx|Exemplaar|
|Http5xx|HTTP-serverfouten|Count|Totaal|HTTP-serverfouten|Exemplaar|
|MemoryWorkingSet|Geheugenwerkset|Bytes|Gemiddeld|Geheugenwerkset|Exemplaar|
|AverageMemoryWorkingSet|Gemiddeld geheugenwerkset|Bytes|Gemiddeld|Gemiddeld geheugenwerkset|Exemplaar|
|AverageResponseTime|Gemiddelde reactietijd|Seconden|Gemiddeld|Gemiddelde reactietijd|Exemplaar|
|AppConnections|Verbindingen|Count|Gemiddeld|Verbindingen|Exemplaar|
|Ingangen|Aantal ingangen|Count|Gemiddeld|Aantal ingangen|Exemplaar|
|Threads|Aantal threads|Count|Gemiddeld|Aantal threads|Exemplaar|
|IoReadBytesPerSecond|I/o gelezen Bytes Per seconde|BytesPerSecond|Totaal|I/o gelezen Bytes Per seconde|Exemplaar|
|IoWriteBytesPerSecond|I/o geschreven Bytes Per seconde|BytesPerSecond|Totaal|I/o geschreven Bytes Per seconde|Exemplaar|
|IoOtherBytesPerSecond|I/o andere Bytes Per seconde|BytesPerSecond|Totaal|I/o andere Bytes Per seconde|Exemplaar|
|IoReadOperationsPerSecond|I/o-leesbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-leesbewerkingen Per seconde|Exemplaar|
|IoWriteOperationsPerSecond|I/o-schrijfbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-schrijfbewerkingen Per seconde|Exemplaar|
|IoOtherOperationsPerSecond|I/o andere bewerkingen Per seconde|BytesPerSecond|Totaal|I/o andere bewerkingen Per seconde|Exemplaar|
|RequestsInApplicationQueue|Aanvragen In toepassingswachtrij voor de|Count|Gemiddeld|Aanvragen In toepassingswachtrij voor de|Exemplaar|
|CurrentAssemblies|Huidige assembly's|Count|Gemiddeld|Huidige assembly's|Exemplaar|
|TotalAppDomains|Totaal aantal AppDomains|Count|Gemiddeld|Totaal aantal AppDomains|Exemplaar|
|TotalAppDomainsUnloaded|Totaal aantal AppDomains verwijderd|Count|Gemiddeld|Totaal aantal AppDomains verwijderd|Exemplaar|
|Gen0Collections|Garbagecollections van generatie 0|Count|Totaal|Garbagecollections van generatie 0|Exemplaar|
|Gen1Collections|Garbagecollections gen 1|Count|Totaal|Garbagecollections gen 1|Exemplaar|
|Gen2Collections|Garbagecollections gen 2|Count|Totaal|Garbagecollections gen 2|Exemplaar|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (functies)

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|BytesReceived|Inkomende gegevens|Bytes|Totaal|Inkomende gegevens|Exemplaar|
|BytesSent|Uitgaande gegevens|Bytes|Totaal|Uitgaande gegevens|Exemplaar|
|Http5xx|HTTP-serverfouten|Count|Totaal|HTTP-serverfouten|Exemplaar|
|MemoryWorkingSet|Geheugenwerkset|Bytes|Gemiddeld|Geheugenwerkset|Exemplaar|
|AverageMemoryWorkingSet|Gemiddeld geheugenwerkset|Bytes|Gemiddeld|Gemiddeld geheugenwerkset|Exemplaar|
|FunctionExecutionUnits|Functie-uitvoeringseenheden|Count|Totaal|Functie-uitvoeringseenheden|Exemplaar|
|FunctionExecutionCount|Aantal uitvoeringen van functie|Count|Totaal|Aantal uitvoeringen van functie|Exemplaar|
|IoReadBytesPerSecond|I/o gelezen Bytes Per seconde|BytesPerSecond|Totaal|I/o gelezen Bytes Per seconde|Exemplaar|
|IoWriteBytesPerSecond|I/o geschreven Bytes Per seconde|BytesPerSecond|Totaal|I/o geschreven Bytes Per seconde|Exemplaar|
|IoOtherBytesPerSecond|I/o andere Bytes Per seconde|BytesPerSecond|Totaal|I/o andere Bytes Per seconde|Exemplaar|
|IoReadOperationsPerSecond|I/o-leesbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-leesbewerkingen Per seconde|Exemplaar|
|IoWriteOperationsPerSecond|I/o-schrijfbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-schrijfbewerkingen Per seconde|Exemplaar|
|IoOtherOperationsPerSecond|I/o andere bewerkingen Per seconde|BytesPerSecond|Totaal|I/o andere bewerkingen Per seconde|Exemplaar|
|RequestsInApplicationQueue|Aanvragen In toepassingswachtrij voor de|Count|Gemiddeld|Aanvragen In toepassingswachtrij voor de|Exemplaar|
|CurrentAssemblies|Huidige assembly's|Count|Gemiddeld|Huidige assembly's|Exemplaar|
|TotalAppDomains|Totaal aantal AppDomains|Count|Gemiddeld|Totaal aantal AppDomains|Exemplaar|
|TotalAppDomainsUnloaded|Totaal aantal AppDomains verwijderd|Count|Gemiddeld|Totaal aantal AppDomains verwijderd|Exemplaar|
|Gen0Collections|Garbagecollections van generatie 0|Count|Totaal|Garbagecollections van generatie 0|Exemplaar|
|Gen1Collections|Garbagecollections gen 1|Count|Totaal|Garbagecollections gen 1|Exemplaar|
|Gen2Collections|Garbagecollections gen 2|Count|Totaal|Garbagecollections gen 2|Exemplaar|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|CpuTime|CPU-tijd|Seconden|Totaal|CPU-tijd|Exemplaar|
|Aanvragen|Aanvragen|Count|Totaal|Aanvragen|Exemplaar|
|BytesReceived|Inkomende gegevens|Bytes|Totaal|Inkomende gegevens|Exemplaar|
|BytesSent|Uitgaande gegevens|Bytes|Totaal|Uitgaande gegevens|Exemplaar|
|Http101|HTTP-fout 101|Count|Totaal|HTTP-fout 101|Exemplaar|
|Http2xx|HTTP 2xx|Count|Totaal|HTTP 2xx|Exemplaar|
|Http3xx|HTTP 3xx|Count|Totaal|HTTP 3xx|Exemplaar|
|Http401|HTTP 401|Count|Totaal|HTTP 401|Exemplaar|
|Http403|HTTP-fout 403|Count|Totaal|HTTP-fout 403|Exemplaar|
|Http404|HTTP-fout 404|Count|Totaal|HTTP-fout 404|Exemplaar|
|Http406|HTTP-fout 406|Count|Totaal|HTTP-fout 406|Exemplaar|
|Http4xx|Http 4xx|Count|Totaal|Http 4xx|Exemplaar|
|Http5xx|HTTP-serverfouten|Count|Totaal|HTTP-serverfouten|Exemplaar|
|MemoryWorkingSet|Geheugenwerkset|Bytes|Gemiddeld|Geheugenwerkset|Exemplaar|
|AverageMemoryWorkingSet|Gemiddeld geheugenwerkset|Bytes|Gemiddeld|Gemiddeld geheugenwerkset|Exemplaar|
|AverageResponseTime|Gemiddelde reactietijd|Seconden|Gemiddeld|Gemiddelde reactietijd|Exemplaar|
|FunctionExecutionUnits|Functie-uitvoeringseenheden|Count|Totaal|Functie-uitvoeringseenheden|Exemplaar|
|FunctionExecutionCount|Aantal uitvoeringen van functie|Count|Totaal|Aantal uitvoeringen van functie|Exemplaar|
|AppConnections|Verbindingen|Count|Gemiddeld|Verbindingen|Exemplaar|
|Ingangen|Aantal ingangen|Count|Gemiddeld|Aantal ingangen|Exemplaar|
|Threads|Aantal threads|Count|Gemiddeld|Aantal threads|Exemplaar|
|IoReadBytesPerSecond|I/o gelezen Bytes Per seconde|BytesPerSecond|Totaal|I/o gelezen Bytes Per seconde|Exemplaar|
|IoWriteBytesPerSecond|I/o geschreven Bytes Per seconde|BytesPerSecond|Totaal|I/o geschreven Bytes Per seconde|Exemplaar|
|IoOtherBytesPerSecond|I/o andere Bytes Per seconde|BytesPerSecond|Totaal|I/o andere Bytes Per seconde|Exemplaar|
|IoReadOperationsPerSecond|I/o-leesbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-leesbewerkingen Per seconde|Exemplaar|
|IoWriteOperationsPerSecond|I/o-schrijfbewerkingen Per seconde|BytesPerSecond|Totaal|I/o-schrijfbewerkingen Per seconde|Exemplaar|
|IoOtherOperationsPerSecond|I/o andere bewerkingen Per seconde|BytesPerSecond|Totaal|I/o andere bewerkingen Per seconde|Exemplaar|
|RequestsInApplicationQueue|Aanvragen In toepassingswachtrij voor de|Count|Gemiddeld|Aanvragen In toepassingswachtrij voor de|Exemplaar|
|CurrentAssemblies|Huidige assembly's|Count|Gemiddeld|Huidige assembly's|Exemplaar|
|TotalAppDomains|Totaal aantal AppDomains|Count|Gemiddeld|Totaal aantal AppDomains|Exemplaar|
|TotalAppDomainsUnloaded|Totaal aantal AppDomains verwijderd|Count|Gemiddeld|Totaal aantal AppDomains verwijderd|Exemplaar|
|Gen0Collections|Garbagecollections van generatie 0|Count|Totaal|Garbagecollections van generatie 0|Exemplaar|
|Gen1Collections|Garbagecollections gen 1|Count|Totaal|Garbagecollections gen 1|Exemplaar|
|Gen2Collections|Garbagecollections gen 2|Count|Totaal|Garbagecollections gen 2|Exemplaar|

## <a name="microsoftwebhostingenvironmentsmultirolepools"></a>Microsoft.Web/hostingEnvironments/multiRolePools

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|Aanvragen|Aanvragen|Count|Totaal|Aanvragen|Exemplaar|
|BytesReceived|Inkomende gegevens|Bytes|Totaal|Inkomende gegevens|Exemplaar|
|BytesSent|Uitgaande gegevens|Bytes|Totaal|Uitgaande gegevens|Exemplaar|
|Http101|HTTP-fout 101|Count|Totaal|HTTP-fout 101|Exemplaar|
|Http2xx|HTTP 2xx|Count|Totaal|HTTP 2xx|Exemplaar|
|Http3xx|HTTP 3xx|Count|Totaal|HTTP 3xx|Exemplaar|
|Http401|HTTP 401|Count|Totaal|HTTP 401|Exemplaar|
|Http403|HTTP-fout 403|Count|Totaal|HTTP-fout 403|Exemplaar|
|Http404|HTTP-fout 404|Count|Totaal|HTTP-fout 404|Exemplaar|
|Http406|HTTP-fout 406|Count|Totaal|HTTP-fout 406|Exemplaar|
|Http4xx|Http 4xx|Count|Totaal|Http 4xx|Exemplaar|
|Http5xx|HTTP-serverfouten|Count|Totaal|HTTP-serverfouten|Exemplaar|
|AverageResponseTime|Gemiddelde reactietijd|Seconden|Gemiddeld|Gemiddelde reactietijd|Exemplaar|
|CpuPercentage|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Exemplaar|
|MemoryPercentage|Geheugenpercentage|Procent|Gemiddeld|Geheugenpercentage|Exemplaar|
|DiskQueueLength|Lengte van de wachtrij voor de schijf|Count|Gemiddeld|Lengte van de wachtrij voor de schijf|Exemplaar|
|HttpQueueLength|Lengte van de HTTP-wachtrij|Count|Gemiddeld|Lengte van de HTTP-wachtrij|Exemplaar|
|ActiveRequests|Actieve aanvragen|Count|Totaal|Actieve aanvragen|Exemplaar|
|TotalFrontEnds|Totaalaantal front-ends|Count|Gemiddeld|Totaalaantal front-ends|Er zijn geen dimensies|
|SmallAppServicePlanInstances|Werkrollen kleine App Plan Service-plan|Count|Gemiddeld|Werkrollen kleine App Plan Service-plan|Er zijn geen dimensies|
|MediumAppServicePlanInstances|Werkrollen middelgrote App Service-plan|Count|Gemiddeld|Werkrollen middelgrote App Service-plan|Er zijn geen dimensies|
|LargeAppServicePlanInstances|Werkrollen grote App Service-plan|Count|Gemiddeld|Werkrollen grote App Service-plan|Er zijn geen dimensies|

## <a name="microsoftwebhostingenvironmentsworkerpools"></a>Microsoft.Web/hostingEnvironments/workerPools

|Gegevens|Metrische weergavenaam|Eenheid|Samenvoegingstype|Beschrijving|Dimensies|
|---|---|---|---|---|---|
|WorkersTotal|Totaalaantal werkrollen|Count|Gemiddeld|Totaalaantal werkrollen|Er zijn geen dimensies|
|WorkersAvailable|Beschikbare werkrollen|Count|Gemiddeld|Beschikbare werkrollen|Er zijn geen dimensies|
|WorkersUsed|Gebruikte werkrollen|Count|Gemiddeld|Gebruikte werkrollen|Er zijn geen dimensies|
|CpuPercentage|CPU-percentage|Procent|Gemiddeld|CPU-percentage|Exemplaar|
|MemoryPercentage|Geheugenpercentage|Procent|Gemiddeld|Geheugenpercentage|Exemplaar|

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over metrische gegevens in Azure-Monitor](monitoring-overview-metrics.md)
* [Waarschuwingen maken op de metrische gegevens](insights-receive-alert-notifications.md)
* [Metrische gegevens exporteren naar opslag, Event Hub of Log Analytics](monitoring-overview-of-diagnostic-logs.md)

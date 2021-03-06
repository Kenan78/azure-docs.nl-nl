---
title: Hybrid Runbook Worker voor Azure Automation in Windows
description: In dit artikel bevat informatie over het installeren van een Azure Automation Hybrid Runbook Worker waarmee u runbooks worden uitgevoerd op Windows gebaseerde computers in uw lokale datacentrum of cloudomgeving.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 04/25/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 30eda7683a1e8c27eb117b92744bf90eae3fd5d9
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/16/2018
---
# <a name="how-to-deploy-a-windows-hybrid-runbook-worker"></a>Het implementeren van een Windows hybride Runbook Worker

De Hybrid Runbook Worker-functie van Azure Automation kunt u direct op de computer die als host fungeert voor de rol en op basis van bronnen in de omgeving voor het beheren van de lokale bronnen runbooks worden uitgevoerd. Runbooks zijn opgeslagen en beheerd in Azure Automation en vervolgens aan een of meer specifieke computers geleverd. Dit artikel decribes de hybride Runbook Worker installeren op een Windows-machine.

## <a name="installing-the-windows-hybrid-runbook-worker"></a>De Windows hybride Runbook Worker installeren

Als u wilt installeren en configureren van een hybride Runbook Worker van Windows, zijn er twee methoden beschikbaar. De aanbevolen methode gebruikt een Automation-runbook om het proces dat is vereist voor het configureren van een Windows-computer volledig te automatiseren. De tweede methode volgt een stapsgewijze procedure om handmatig te installeren en configureren van de rol.

> [!NOTE]
> Voor het beheren van de configuratie van uw servers die ondersteuning bieden de hybride Runbook Worker-rol met Desired State Configuration (DSC), moet u hen toevoegen als DSC-knooppunten.

Hier volgen de minimale vereisten voor een Windows hybride Runbook Worker.

* WindowsServer 2012 of later.
* Windows PowerShell 4.0 of hoger is vereist ([WMF 4.0 downloaden](https://www.microsoft.com/download/details.aspx?id=40855)). Windows PowerShell 5.1 ([downloaden WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616)) wordt aanbevolen voor een hogere mate van betrouwbaarheid.
* .NET framework 4.6.2 of hoger.
* Minimaal twee kernen.
* Een minimum van 4 GB RAM-geheugen.
* Poort 443 (uitgaand)

Zie voor aanvullende netwerkvereisten voor de hybride Runbook Worker [configureren van uw netwerk](automation-hybrid-runbook-worker.md#network-planning).

Voor meer informatie over het voorbereiden voor beheer met DSC, Zie [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md).
Als u inschakelt de [Update beheeroplossing](../operations-management-suite/oms-solution-update-management.md), elke Windows-computer die is verbonden met uw werkruimte voor logboekanalyse is automatisch geconfigureerd als een hybride Runbook Worker ter ondersteuning van runbooks die zijn opgenomen in deze oplossing. Het is echter niet geregistreerd bij de Hybrid Worker-groepen in uw Automation-account al gedefinieerd. De computer kan worden toegevoegd aan een hybride Runbook Worker-groep in uw Automation-account voor de ondersteuning van Automation-runbooks, zolang u hetzelfde account voor de oplossing en de hybride Runbook Worker-groepslidmaatschap gebruikt. Deze functionaliteit is toegevoegd aan versie 7.2.12024.0 van de Hybrid Runbook Worker.

Nadat u hebt een runbook worker is geïmplementeerd, controleren [runbooks worden uitgevoerd op een hybride Runbook Worker](automation-hrw-run-runbooks.md) voor informatie over het configureren van uw runbooks voor het automatiseren van processen in uw on-premises datacentrum of andere cloudomgeving.

### <a name="automated-deployment"></a>Geautomatiseerde implementatie

Voer de volgende stappen uit voor het automatiseren van de installatie en configuratie van de Windows Hybrid Worker-rol.

1. Download de *nieuw OnPremiseHybridWorker.ps1* script van de [PowerShell Gallery](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/DisplayScript) rechtstreeks van de computer waarop de hybride Runbook Worker-rol of vanaf een andere computer in uw omgeving en Kopieer het naar de werknemer.

   De *nieuw OnPremiseHybridWorker.ps1* vereist dat de volgende parameters tijdens het uitvoeren van script:

   * *AutomationAccountName* (verplicht) - de naam van uw Automation-account.
   * *AAResourceGroupName* (verplicht) - de naam van de resourcegroep die zijn gekoppeld aan uw Automation-account
   * *OMSResourceGroupName* (optioneel): de naam van de resourcegroep voor de OMS-werkruimte. Als niet wordt opgegeven, wordt de AAResourceGroupName gebruikt.
   * *HybridGroupName* (verplicht) - de naam van een hybride Runbook Worker-groep die u opgeeft als doel voor de runbooks die dit scenario te ondersteunen.
   * *SubscriptionID* (verplicht) - de ID van de Azure-abonnement dat uw Automation-account in.
   * *WorkspaceName* (optioneel): de naam van de werkruimte de logboekanalyse. Als u een werkruimte voor logboekanalyse niet hebt, wordt het script maakt en configureert u een.

     > [!NOTE]
     > De enige Automation-regio's ondersteund voor de integratie met logboekanalyse zijn momenteel - **Australië-Zuidoost**, **VS-Oost 2**, **Zuidoost-Azië**, en  **West-Europa**. Als uw Automation-account zich niet in een van deze regio's, wordt het script maakt een werkruimte voor logboekanalyse maar wordt er een waarschuwingsbericht weergegeven dat er kan geen koppeling ze samen.

1. Start op uw computer **Windows PowerShell** van de **Start** scherm in de beheerdersmodus.
1. Ga naar de map waarin het script dat u hebt gedownload en het wijzigen van de waarden voor parameters worden uitgevoerd vanuit de PowerShell opdrachtregel-shell, *- AutomationAccountName*, *- AAResourceGroupName*, *- OMSResourceGroupName*, *- HybridGroupName*, *- SubscriptionId*, en *- WorkspaceName*.

     > [!NOTE]
     > U wordt gevraagd om te verifiëren met Azure nadat u het script hebt uitgevoerd. U **moet** aanmelden met een account dat lid is van de rol Abonnementsbeheerders en CO-beheerder van het abonnement.

   ```powershell-interactive
   .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> -AAResourceGroupName <NameofResourceGroup>`
   -OMSResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
   -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfLogAnalyticsWorkspace>
   ```

1. U wordt gevraagd om akkoord te installeren te **NuGet** en wordt u gevraagd om te verifiëren met uw Azure-referenties.

1. Nadat het script voltooid is, ziet de Hybrid Worker-groepen pagina de nieuwe groep en het aantal leden of als een bestaande groep, het aantal leden wordt verhoogd. U kunt de groep in de lijst selecteren op de **Hybrid Worker-groepen** pagina en selecteer de **Hybrid Workers** tegel. Op de **Hybrid Workers** pagina ziet u elk lid van de groep die wordt vermeld.

### <a name="manual-deployment"></a>Handmatige implementatie

De eerste twee stappen eenmaal uitvoeren voor uw Automation-omgeving en vervolgens de resterende stappen herhalen voor elke worker-computer.

#### <a name="1-create-log-analytics-workspace"></a>1. Een Log Analytics-werkruimte maken

Als u nog geen een werkruimte voor logboekanalyse, maakt u een met instructies voor [beheren van uw werkruimte](../log-analytics/log-analytics-manage-access.md). Als u al hebt, kunt u een bestaande werkruimte gebruiken.

#### <a name="2-add-automation-solution-to-log-analytics-workspace"></a>2. Automation-oplossing naar de werkruimte voor logboekanalyse toevoegen

Oplossingen voegen functionaliteit toe aan Log Analytics. De Automation-oplossing voegt u functionaliteit voor Azure Automation biedt ook ondersteuning voor hybride Runbook Worker. Wanneer u de oplossing voor uw werkruimte toevoegt, duwt wordt automatisch omlaag worker-onderdelen voor de agentcomputer die u in de volgende stap installeren wilt.

Volg de instructies voor [toevoegen van een oplossing met behulp van de galerie met oplossingen](../log-analytics/log-analytics-add-solutions.md) toevoegen de **Automation** oplossing voor uw werkruimte voor logboekanalyse.

#### <a name="3-install-the-microsoft-monitoring-agent"></a>3. Microsoft Monitoring Agent installeren

Microsoft Monitoring Agent verbonden computers met logboekanalyse. Wanneer u de agent op uw on-premises computer installeren en met uw werkruimte verbinden, worden de onderdelen die vereist zijn voor hybride Runbook Worker automatisch gedownload.

Volg de instructies voor [verbinding maken met Windows-computers met logboekanalyse](../log-analytics/log-analytics-windows-agent.md) voor het installeren van de agent op de lokale computer. U kunt dit proces voor meerdere computers meerdere werknemers toevoegen aan uw omgeving herhalen.

De agent verbonden is met Log Analytics, wordt weergegeven op de **verbonden bronnen** tabblad van de logboekanalyse **instellingen** pagina. U kunt controleren of de agent correct de Automation-oplossing heeft gedownload wanneer er een map met de naam **AzureAutomationFiles** in C:\Program Files\Microsoft Monitoring Agent\Agent. Als u wilt controleren welke versie van de hybride Runbook Worker, u kunt navigeren naar C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\ en noteer de \\ *versie* submap.

#### <a name="4-install-the-runbook-environment-and-connect-to-azure-automation"></a>4. De runbook-omgeving installeren en verbinding maken met Azure Automation

Wanneer u een agent met logboekanalyse toevoegt, wordt de Automation-oplossing pushes omlaag de **HybridRegistration** PowerShell-module bevat de **Add-HybridRunbookWorker** cmdlet. Met deze cmdlet kunt u de runbook-omgeving op de computer installeren en registreren met Azure Automation.

Open een PowerShell-sessie in de beheerdersmodus en voer de volgende opdrachten in de module te importeren.

```powershell-interactive
cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
Import-Module HybridRegistration.psd1
```

Voer vervolgens de **Add-HybridRunbookWorker** cmdlet met de volgende syntaxis:

```powershell-interactive
Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>
```

U kunt de vereiste informatie voor deze cmdlet uit de **sleutels beheren** pagina in de Azure-portal. Deze pagina openen door te selecteren de **sleutels** optie van de **instellingen** pagina in uw Automation-account.

![Overzicht van hybride Runbook Worker](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** is de naam van de Hybrid Runbook Worker-groep. Als deze groep al in het automation-account bestaat, is klikt u vervolgens de huidige computer toegevoegd. Als deze niet bestaat nog, wordt deze toegevoegd.
* **Eindpunt** is de **URL** veld in de **sleutels beheren** pagina.
* **Token** is de **primaire toegangssleutel** in de **sleutels beheren** pagina.

Gebruik de **-uitgebreide** overschakelen met **Add-HybridRunbookWorker** voor het ontvangen van gedetailleerde informatie over de installatie.

#### <a name="5-install-powershell-modules"></a>5. PowerShell-modules installeren

Runbooks kunt u elk van de activiteiten en de cmdlets die zijn gedefinieerd in de modules die zijn geïnstalleerd in uw Azure Automation-omgeving. Deze modules worden niet automatisch geïmplementeerd op lokale computers, zodat u ze handmatig moet installeren. De uitzondering is de Azure-module, dat standaard toegang tot de cmdlets voor alle Azure-services en activiteiten bieden voor Azure Automation is geïnstalleerd.

Omdat het voornaamste doel van de Hybrid Runbook Worker-functie voor het beheren van lokale bronnen, moet u waarschijnlijk de modules die ondersteuning bieden voor deze resources te installeren. U kunt verwijzen naar [Modules installeren](http://msdn.microsoft.com/library/dd878350.aspx) voor informatie over het installeren van Windows PowerShell-modules. Modules die zijn geïnstalleerd, moeten zich in een locatie waarnaar wordt verwezen door de omgevingsvariabele PSModulePath zodat ze automatisch worden geïmporteerd door de hybride worker. Zie voor meer informatie [wijzigen van het installatiepad PSModulePath](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx).

## <a name="troubleshooting"></a>Problemen oplossen

De hybride Runbook Worker is afhankelijk van de Microsoft Monitoring Agent te communiceren met uw Automation-account voor het registreren van de werknemer, ontvangen van runbooktaken en status rapporteren. Als de registratie van de werknemer is mislukt, volgen hier enkele mogelijke oorzaken voor de fout:

### <a name="the-microsoft-monitoring-agent-is-not-running"></a>Microsoft Monitoring Agent wordt niet uitgevoerd.

Als de Microsoft Monitoring Agent Windows-service niet wordt uitgevoerd, dit voorkomt dat de hybride Runbook Worker communicatie met Azure Automation. Controleer of de agent wordt uitgevoerd met de volgende opdracht in PowerShell: `Get-Service healthservice`. Als de service wordt gestopt, voert u de volgende opdracht in PowerShell om de service te starten: `Start-Service healthservice`.

### <a name="event-4502-in-operations-manager-log"></a>Gebeurtenis 4502 in Operations Manager-logboek

In de **toepassingen en Services Logs\Operations Manager** gebeurtenislogboek, ziet u gebeurtenis 4502 en EventMessage met **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**met de volgende beschrijving: *het certificaat dat is doorgegeven door de service \<wsid\>. oms.opinsights.azure.com is niet uitgegeven door een certificeringsinstantie die wordt gebruikt voor Microsoft-services. Neem contact op met de netwerkbeheerder om te controleren of er een proxy die TLS/SSL-communicatie wordt onderschept worden uitgevoerd. Artikel KB3126513 bevat extra informatie over probleemoplossing voor problemen met de netwerkverbinding.*

Dit kan worden veroorzaakt door uw proxy- of -firewall blokkeert communicatie met Microsoft Azure. Controleer of dat de computer heeft uitgaande toegang tot de *.azure automation.net op poort 443.

Logboeken worden lokaal opgeslagen op elke worker hybride op C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes. U kunt controleren of er zijn waarschuwingen of fouten die zijn geschreven naar de **toepassingen en Services Logs\Microsoft-SMA\Operations** en **toepassingen en Services Logs\Operations Manager** in het gebeurtenislogboek die duidt dit op een verbindings- of andere probleem met betrekking tot de voorbereiding van de rol aan Azure Automation of probleem tijdens het normale bewerkingen uitvoeren.

Zie voor aanvullende stappen over het oplossen van problemen met updatebeheer [updatebeheer - probleemoplossing](automation-update-management.md#troubleshooting)

## <a name="next-steps"></a>Volgende stappen

* Bekijk [runbooks worden uitgevoerd op een hybride Runbook Worker](automation-hrw-run-runbooks.md) voor informatie over het configureren van uw runbooks voor het automatiseren van processen in uw on-premises datacentrum of andere cloudomgeving.
* Zie voor instructies over het verwijderen van Hybrid Runbook Workers [verwijderen Azure Automation Hybrid Runbook Workers](automation-hybrid-runbook-worker.md#removing-hybrid-runbook-worker)
---
title: De werkruimten in Azure Log Analytics en de OMS-portal beheren | Microsoft Docs
description: U kunt de toegang tot werkruimten in Azure Log Analytics en de OMS-portal beheren met behulp van verschillende beheertaken voor gebruikers, accounts, werkruimten en Azure-accounts.
services: log-analytics
documentationcenter: ''
author: MGoedtel
manager: carmonm
editor: ''
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2018
ms.author: magoedte
ms.openlocfilehash: d2480936ed54ec58ba289eae1ba605a16e27f0b3
ms.sourcegitcommit: 96089449d17548263691d40e4f1e8f9557561197
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/17/2018
ms.locfileid: "34271667"
---
# <a name="manage-workspaces"></a>Werkruimten beheren

Voor het beheren van toegang tot Log Analytics, voert u verschillende beheertaken uit voor werkruimten. In dit artikel worden adviezen en aanbevolen procedures beschreven voor het beheren van werkruimten. Een werkruimte is in wezen een container met accountgegevens en eenvoudige configuratiegegevens voor het account. U of andere leden van uw organisatie kunnen meerdere werkruimten gebruiken om verschillende gegevenssets te beheren die worden verzameld uit de gehele of delen van uw IT-infrastructuur.

Het volgende is nodig om een werkruimte te maken:

1. U dient een Azure-abonnement te hebben.
2. U dient een naam voor de werkruimte te kiezen.
3. U dient de werkruimte aan uw abonnement te koppelen.
4. U dient een geografische locatie te kiezen.

## <a name="determine-the-number-of-workspaces-you-need"></a>Vaststellen hoeveel werkruimten u nodig hebt
Een werkruimte is een Azure-resource die bestaat uit een container waarin gegevens worden verzameld, samengevoegd, geanalyseerd en gepresenteerd in Azure Portal.

U kunt per Azure-abonnement meerdere werkruimten hebben en toegang hebben tot meer dan één werkruimte, met de mogelijkheid om op verschillende werkruimten tegelijk een query uit te voeren. In deze sectie wordt beschreven wanneer het handig kan zijn om meer dan één werkruimte te maken.

Een werkruimte biedt momenteel het volgende:

* Een geografische locatie voor de opslag van gegevens
* Details voor facturering
* Gegevensisolatie
* Bereik voor configuratie

Op basis van de voorgaande kenmerken kunt u in de volgende gevallen meerdere werkruimten maken:

* U vertegenwoordigt een mondiaal bedrijf en moet de gegevens opslaan in specifieke regio’s ten behoeve van de onafhankelijkheid van de gegevens of om nalevingsredenen.
* U gebruikt Azure en wilt kosten voor de overdracht van uitgaande gegevens voorkomen door een werkruimte in dezelfde regio te hebben als de Azure-resource die deze beheert.
* U wilt kosten toewijzen aan verschillende afdelingen of bedrijfsonderdelen op basis van hun gebruik. Wanneer u voor elke afdeling of bedrijfsgroep een eigen werkruimte maakt, worden op uw factuur- en gebruiksoverzicht van Azure de kosten voor elke werkruimte afzonderlijk weergegeven.
* U bent aanbieder van beheerde services en moet de Log Analytics-gegevens voor elke klant geïsoleerd van de gegevens van andere klanten bewaren.
* U beheert meerdere klanten en wilt dat elke klant, afdeling of bedrijfsgroep de eigen gegevens kan bekijken, maar niet de gegevens van anderen.

Wanneer u Windows-agents gebruikt om gegevens te verzamelen, kunt u [elke agent configureren om te rapporteren aan een of meer werkruimten](log-analytics-windows-agents.md).

Als u System Center Operations Manager gebruikt, kan elke beheergroep uit Operations Manager worden verbonden met slechts één werkruimte. U kunt Microsoft Monitoring Agent installeren op computers die worden beheerd door Operations Manager en de agent laten rapporteren over zowel Operations Manager als een andere Log Analytics-werkruimte.

### <a name="workspace-information"></a>Werkruimtegegevens

U kunt gegevens van uw werkruimte in Azure Portal bekijken. U kunt de gegevens ook bekijken in de OMS-portal.

#### <a name="view-workspace-information-in-the-azure-portal"></a>Werkruimtegegevens weergeven in Azure Portal

1. Meld u met uw Azure-abonnement aan bij [Azure Portal](https://portal.azure.com) als u dit nog niet hebt gedaan.
2. Klik in het menu **Hub** op **Meer services** en typ in de lijst met resources op **Log Analytics**. Als u begint te typen, wordt de lijst gefilterd op basis van uw invoer. Klik op **Log Analytics**.  
    ![Azure-hub](./media/log-analytics-manage-access/hub.png)  
3. Selecteer een werkruimte op de blade Abonnementen in Log Analytics.
4. De blade van de werkruimte geeft gegevens over de werkruimte en koppelingen voor meer informatie weer.  
    ![details van de werkruimte](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Accounts en gebruikers beheren
Aan elke werkruimte kunnen meerdere accounts worden gekoppeld en elk account (Microsoft-account of organisatieaccount) kan toegang hebben tot meerdere werkruimten.

Standaard wordt het Microsoft-account of organisatieaccount dat wordt gebruikt voor het maken van de werkruimte, de beheerder van de werkruimte.

Er zijn twee machtigingsmodellen die de toegang tot een Log Analytics-werkruimte beheren:

1. Verouderde Log Analytics-gebruikersrollen
2. [Toegang op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md)

In de volgende tabel ziet u de toegang die met elk machtigingsmodel kan worden ingesteld:

|                          | Log Analytics-portal | Azure Portal | API (inclusief PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Log Analytics-gebruikersrollen | Ja                  | Nee           | Nee                         |
| Toegang op basis van rollen in Azure  | Ja                  | Ja          | Ja                        |

> [!NOTE]
> Log Analytics zal in plaats van Log Analytics-gebruikersrollen toegang op basis van rollen in Azure gaan gebruiken als machtigingsmodel.
>
>

De oude Log Analytics-gebruikersrollen beheren alleen de toegang tot activiteiten die worden uitgevoerd in de [Log Analytics-portal](https://mms.microsoft.com).

Voor de volgende activiteiten zijn ook Azure-machtigingen vereist:

| Bewerking                                                          | Azure-machtigingen nodig | Opmerkingen |
|-----------------------------------------------------------------|--------------------------|-------|
| Beheeroplossingen toevoegen en verwijderen                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| De prijscategorie wijzigen                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Gegevens weergeven op de tegels *Back-up* en *Site Recovery* | Beheerder/medebeheerder | Heeft toegang tot resources die zijn geïmplementeerd met behulp van het klassieke implementatiemodel |
| Een werkruimte maken in Azure Portal                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-to-log-analytics-using-azure-permissions"></a>Toegang tot Log Analytics beheren met behulp van Azure-machtigingen
Volg de stappen in [Roltoewijzingen gebruiken voor het beheer van de toegang tot de resources van uw Azure-abonnement](../active-directory/role-based-access-control-configure.md) om toegang te verlenen tot de Log Analytics-werkruimte met behulp van Azure-machtigingen.

Azure heeft twee ingebouwde gebruikersrollen voor Log Analytics:
- Lezer van Log Analytics
- Inzender van Log Analytics

Leden van de rol *Lezer van Log Analytics* kunnen:
- Alle controlegegevens weergeven en doorzoeken 
- Controlegegevens weergeven, inclusief de configuratie van Azure Diagnostics voor alle Azure-resources.

| Type    | Machtiging | Beschrijving |
| ------- | ---------- | ----------- |
| Bewerking | `*/read`   | De mogelijkheid om alle resources en de resourceconfiguratie weer te geven. Omvat: <br> Status van de VM-extensie <br> Configuratie van Azure Diagnostics voor resources <br> Alle eigenschappen en instellingen van alle resources |
| Bewerking | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Mogelijkheid om Zoeken in logboeken v2-query's uit te voeren |
| Bewerking | `Microsoft.OperationalInsights/workspaces/search/action` | Mogelijkheid om Zoeken in logboeken v1-query's uit te voeren |
| Bewerking | `Microsoft.Support/*` | Mogelijkheid ondersteuningsaanvragen te openen |
|Geen bewerking | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Zorgt ervoor dat de werkruimtesleutel die is vereist om de gegevensverzameling-API te gebruiken en agents te installeren, niet kan worden gelezen |


Leden van de rol *Inzender van Log Analytics* kunnen:
- Alle controlegegevens lezen 
- Automation-accounts maken en configureren
- Beheeroplossingen toevoegen en verwijderen
- Opslagaccountsleutels lezen 
- Verzameling met logboeken uit Azure Storage configureren
- De controle-instellingen voor Azure-resources bewerken, inclusief
  - De VM-extensie toevoegen aan virtuele machines
  - Azure Diagnostics configureren op alle Azure-resources

> [!NOTE] 
> U kunt de mogelijkheid om een VM-extensie toe te voegen aan een virtuele machine, gebruiken om volledige controle over een virtuele machine te krijgen.

| Machtiging | Beschrijving |
| ---------- | ----------- |
| `*/read`     | De mogelijkheid om alle resources en de resourceconfiguratie weer te geven. Omvat: <br> Status van de VM-extensie <br> Configuratie van Azure Diagnostics voor resources <br> Alle eigenschappen en instellingen van alle resources |
| `Microsoft.Automation/automationAccounts/*` | De mogelijkheid om Azure Automation-accounts te maken en te configureren, inclusief het toevoegen en bewerken van runbooks |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | VM-extensies toevoegen, bijwerken en verwijderen, met inbegrip van de Microsoft Monitoring Agent-extensie en de OMS Agent for Linux-extensie |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Geef de opslagaccountsleutel weer. Vereist om Log Analytics te configureren om logboeken uit Azure-opslagaccounts te lezen |
| `Microsoft.Insights/alertRules/*` | Waarschuwingsregels toevoegen, bijwerken en verwijderen |
| `Microsoft.Insights/diagnosticSettings/*` | Diagnostische instellingen bij Azure-resources toevoegen, bijwerken en verwijderen |
| `Microsoft.OperationalInsights/*` | Configuratie voor Log Analytics-werkruimten toevoegen, bijwerken en verwijderen |
| `Microsoft.OperationsManagement/*` | Beheeroplossingen toevoegen en verwijderen |
| `Microsoft.Resources/deployments/*` | Maak en verwijder implementaties. Vereist voor het toevoegen en verwijderen van oplossingen, werkruimten en Automation-accounts |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Maak en verwijder implementaties. Vereist voor het toevoegen en verwijderen van oplossingen, werkruimten en Automation-accounts |

Als u gebruikers wilt toevoegen aan en verwijderen uit een gebruikersrol, moet u beschikken over machtigingen voor `Microsoft.Authorization/*/Delete` en `Microsoft.Authorization/*/Write`.

Gebruik deze rollen om gebruikers toegang te geven op verschillende niveaus:
- Abonnement: toegang tot alle werkruimten in het abonnement
- Resourcegroep: toegang tot alle werkruimten in de resourcegroep
- Resource: alleen toegang tot de opgegeven werkruimte

Gebruik [aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md) om rollen te maken met de specifieke machtigingen die nodig zijn.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Gebruikersrollen in Azure en in Log Analytics-portal
Als u minimaal Azure-leesmachtiging hebt in de Log Analytics-werkruimte, kunt u de Log Analytics-portal openen door op de taak **OMS-portal** te klikken wanneer de Log Analytics-werkruimte wordt weergegeven.

Bij het openen van de Log Analytics-portal schakelt u over op het gebruik van de verouderde Log Analytics-gebruikersrollen. Als u niet beschikt over een roltoewijzing in de Log Analytics-portal, [worden de Azure-machtigingen waarover u beschikt, in de werkruimte gecontroleerd](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
De roltoewijzing in de Log Analytics-portal wordt als volgt bepaald:

| Voorwaarden                                                   | Toegewezen Log Analytics-gebruikersrol | Opmerkingen |
|--------------------------------------------------------------|----------------------------------|-------|
| Uw account behoort tot een verouderde Log Analytics-gebruikersrol     | De opgegeven Log Analytics-gebruikersrol | |
| Uw account behoort niet tot een verouderde Log Analytics-gebruikersrol <br> Volledige Azure-machtigingen voor de werkruimte (`*` machtiging <sup>1</sup>) | Beheerder ||
| Uw account behoort niet tot een verouderde Log Analytics-gebruikersrol <br> Volledige Azure-machtigingen voor de werkruimte (`*` machtiging <sup>1</sup>) <br> *geen acties* van `Microsoft.Authorization/*/Delete` en `Microsoft.Authorization/*/Write` | Inzender ||
| Uw account behoort niet tot een verouderde Log Analytics-gebruikersrol <br> Azure-leesmachtiging | Alleen-lezen ||
| Uw account behoort niet tot een verouderde Log Analytics-gebruikersrol <br> Azure-machtigingen zijn niet begrepen | Alleen-lezen ||
| Voor door Cloud Solution Provider (CSP) beheerde abonnementen <br> Het account waarbij u bent aangemeld, bevindt zich in de Azure Active Directory die aan de werkruimte is gekoppeld | Beheerder | Doorgaans de klant van een CSP |
| Voor door Cloud Solution Provider (CSP) beheerde abonnementen <br> Het account waarbij u bent aangemeld, bevindt zich niet in de Azure Active Directory die aan de werkruimte is gekoppeld | Inzender | Doorgaans de CSP |

<sup>1</sup> Raadpleeg [Azure-machtigingen](../active-directory/role-based-access-control-custom-roles.md) voor meer informatie over roldefinities. Bij het evalueren van rollen is een actie van `*` niet equivalent aan `Microsoft.OperationalInsights/workspaces/*`.

Een aantal punten met betrekking tot de Azure Portal waarmee u rekening moet houden:

* Als u zich bij de OMS-portal aanmeldt via http://mms.microsoft.com, wordt de lijst **Een werkruimte selecteren** weergegeven. Deze lijst bevat alleen werkruimten waarin u een Log Analytics-gebruikersrol hebt. Als u de werkruimten wilt zien waartoe u toegang hebt met Azure-abonnementen, moet u een tenant als onderdeel van de URL opgeven. Bijvoorbeeld `mms.microsoft.com/?tenant=contoso.com`. De tenant-id is vaak het laatste deel van het e-mailadres waarmee u zich aanmeldt.
* Als u rechtstreeks wilt navigeren naar een portal waartoe u toegang hebt via Azure-machtigingen, moet u de resource als onderdeel van de URL opgeven. Het is mogelijk om deze URL op te halen met behulp van PowerShell.

  Bijvoorbeeld `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  De URL ziet er als volgt uit: `https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-the-oms-portal"></a>Gebruikers beheren in de OMS-portal
U beheert gebruikers en groepen op het tabblad **Gebruikers beheren** onder het tabblad **Accounts** op de pagina Instellingen.   

![gebruikers beheren](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-to-an-existing-workspace"></a>Een gebruiker toevoegen aan een bestaande werkruimte
Voer de volgende stappen uit om een gebruiker of groep toe te voegen aan een werkruimte.

1. Klik in de OMS-portal op de tegel **Instellingen**.
2. Klik op het tabblad **Accounts** en vervolgens op het tabblad **Gebruikers beheren**.
3. Kies in de sectie **Gebruikers beheren** het accounttype dat u wilt toevoegen: **Organisatieaccount**, **Microsoft-account** of **Microsoft-ondersteuning**.

   * Als u Microsoft-account kiest, typt u het e-mailadres in van de gebruiker die is gekoppeld aan het Microsoft-account.
   * Als u Organisatieaccount kiest, geeft u een deel van de naam of e-mailalias van de gebruiker/groep op. Er wordt dan een lijst met overeenkomende gebruikers en groepen weergegeven in een vervolgkeuzevak. Selecteer een gebruiker of groep.
   * Gebruik Microsoft-ondersteuning om een medewerker van Microsoft-ondersteuning of andere medewerker van Microsoft tijdelijk toegang te verlenen tot uw werkruimte om u te helpen bij het oplossen van problemen.

     > [!NOTE]
     > Voor optimale prestaties kunt u het aantal Active Directory-groepen dat aan één OMS-account is gekoppeld, het beste tot drie beperken: één voor beheerders, één voor bijdragers en één voor gebruikers met alleen-lezentoegang. Gebruik van meer groepen kan de prestaties van Log Analytics beïnvloeden.
     >
     >
4. Kies het type gebruiker of groep dat u wilt toevoegen: **Beheerder**, **Bijdrager** of **Gebruiker met alleen-lezentoegang**.  
5. Klik op **Add**.

   Als u een Microsoft-account toevoegt, wordt er een uitnodiging om lid te worden van de werkruimte verzonden naar het e-mailadres dat u hebt opgegeven. Nadat de gebruiker de instructies in de uitnodiging voor OMS heeft gevolgd, heeft de gebruiker toegang tot deze werkruimte.
   Als u een organisatieaccount toevoegt, heeft de gebruiker onmiddellijk toegang tot Log Analytics.  

#### <a name="edit-an-existing-user-type"></a>Een bestaand gebruikerstype bewerken
U kunt de accountrol van een gebruiker die aan uw OMS-account is gekoppeld, wijzigen. De volgende rollen zijn beschikbaar:

* *Beheerder*: kan gebruikers beheren, alle waarschuwingen weergeven en er actie voor ondernemen, en servers toevoegen en verwijderen
* *Bijdrager*: kan alle waarschuwingen weergeven en er actie voor ondernemen, en servers toevoegen en verwijderen
* *Gebruiker met alleen-lezentoegang*: gebruikers die zijn gemarkeerd als alleen-lezen kunnen het volgende niet:

  1. Oplossingen toevoegen/verwijderen. De oplossingengalerie is verborgen.
  2. Tegels toevoegen/wijzigen/verwijderen in **Mijn dashboard**.
  3. De pagina’s met **instellingen** bekijken. De pagina's zijn verborgen.
  4. In de zoekweergave zijn taken voor Power BI-configuratie, opgeslagen zoekopdrachten en waarschuwingen verborgen.

#### <a name="to-edit-an-account"></a>Een account bewerken
1. Klik in de OMS-portal op de tegel **Instellingen**.
2. Klik op het tabblad **Accounts** en vervolgens op het tabblad **Gebruikers beheren**.
3. Selecteer de rol van de gebruiker die u wilt wijzigen.
4. Klik in het bevestigingsdialoogvenster op **Ja**.

### <a name="remove-a-user-from-a-workspace"></a>Een gebruiker uit een werkruimte verwijderen
Voer de volgende stappen uit om een gebruiker te verwijderen uit een werkruimte. Met het verwijderen van de gebruiker wordt de werkruimte niet gesloten. In plaats daarvan wordt de koppeling tussen die gebruiker en de werkruimte verwijderd. Als een gebruiker is gekoppeld aan meerdere werkruimten, kan die gebruiker zich nog wel aanmelden bij OMS en de andere werkruimten zien.

1. Klik in de OMS-portal op de tegel **Instellingen**.
2. Klik op het tabblad **Accounts** en vervolgens op het tabblad **Gebruikers beheren**.
3. Klik op **Verwijderen** naast de naam van de gebruiker die u wilt verwijderen.
4. Klik in het bevestigingsdialoogvenster op **Ja**.

### <a name="add-a-group-to-an-existing-workspace"></a>Een groep toevoegen aan een bestaande werkruimte
1. Volg stap 1-4 in het gedeelte 'Een gebruiker toevoegen aan een bestaande werkruimte' hierboven.
2. Selecteer onder **Gebruiker/groep kiezen** de optie **Groep**.  
   ![een groep toevoegen aan een bestaande werkruimte](./media/log-analytics-manage-access/add-group.png)
3. Voer de weergavenaam of het e-mailadres in voor de groep die u wilt toevoegen.
4. Selecteer de groep in de lijst met resultaten en klik op **Toevoegen**.

## <a name="link-an-existing-workspace-to-an-azure-subscription"></a>Een bestaande werkruimte koppelen aan een Azure-abonnement
Alle werkruimten die zijn gemaakt na 26 september 2016 moeten op het moment van maken zijn gekoppeld aan een Azure-abonnement. Werkruimten die vóór deze datum zijn gemaakt, moeten bij aanmelding worden gekoppeld aan een werkruimte. Wanneer u de werkruimte maakt via Azure Portal of uw werkruimte koppelt aan een Azure-abonnement, wordt uw Azure Active Directory als uw organisatieaccount gekoppeld.

### <a name="to-link-a-workspace-to-an-azure-subscription-in-the-oms-portal"></a>Een werkruimte koppelen aan een Azure-abonnement in de OMS-portal

- Wanneer u zich aanmeldt bij de OMS-portal, wordt u gevraagd om een Azure-abonnement te selecteren. Selecteer het abonnement dat u aan uw werkruimte wilt koppelen en klik vervolgens op **Koppelen**.  
    ![Azure-abonnement koppelen](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > U kunt een werkruimte alleen koppelen als uw Azure-account al toegang heeft tot deze werkruimte.  Met andere woorden: het account dat u gebruikt voor toegang tot Azure Portal, moet **hetzelfde** zijn als het account dat u gebruikt voor toegang tot de werkruimte. Zie [Een gebruiker toevoegen aan een bestaande werkruimte](#add-a-user-to-an-existing-workspace) als dit niet het geval is.

### <a name="to-link-a-workspace-to-an-azure-subscription-in-the-azure-portal"></a>Een werkruimte in de Azure Portal koppelen aan een Azure-abonnement
1. Meld u aan bij de [Azure Portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Klik op **Add**.  
   ![lijst met werkruimten](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. Klik onder **OMS-werkruimte** op **Of bestaande koppelen**.  
   ![bestaande koppelen](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Klik op **Vereiste instellingen configureren**.  
   ![vereiste instellingen configureren](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Hier ziet u de lijst met werkruimten die nog niet zijn gekoppeld aan uw Azure-account. Selecteer een werkruimte.  
   ![werkruimten selecteren](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Indien nodig kunt u de waarden van de volgende items wijzigen:
   * Abonnement
   * Resourcegroep
   * Locatie
   * Prijscategorie  
     ![waarden wijzigen](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Klik op **OK**. De werkruimte is nu gekoppeld aan uw Azure-account.

> [!NOTE]
> Als u de te koppelen werkruimte niet ziet, heeft uw Azure-abonnement geen toegang tot de werkruimte die u hebt gemaakt met behulp van de OMS-portal.  Zie [Een gebruiker toevoegen aan een bestaande werkruimte](#add-a-user-to-an-existing-workspace) om dit account toegang te verlenen vanuit de OMS-portal.
>
>

## <a name="upgrade-a-workspace-to-a-paid-plan"></a>Een werkruimte upgraden naar een betaald abonnement
Er zijn drie typen werkruimteabonnementen voor OMS: **Gratis**, **Zelfstandig** en **OMS**.  Als u het *gratis* abonnement hebt, geldt een limiet van 500 MB aan gegevens dat per dag naar Log Analytics wordt verzonden.  Als u deze hoeveelheid overschrijdt, moet u uw werkruimte wijzigen naar een betaald abonnement om te voorkomen dat gegevens buiten deze limiet niet worden verzameld. U kunt op elk gewenst moment uw type abonnement wijzigen.  Zie [Prijsgegevens](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing) voor meer informatie over de tarieven voor OMS.

### <a name="using-entitlements-from-an-oms-subscription"></a>Rechten van een OMS-abonnement gebruiken
Als u de rechten wilt gebruiken die horen bij de aanschaf van OMS E1, OMS E2 OMS of de OMS-invoegtoepassing voor System Center, kiest u het *OMS*-abonnement van OMS Log Analytics.

Wanneer u een OMS-abonnement koopt, worden de rechten toegevoegd aan uw Enterprise-overeenkomst. Elk Azure-abonnement dat onder deze overeenkomst wordt gemaakt, kan gebruikmaken van deze rechten. Alle werkruimten in deze abonnementen gebruiken de OMS-rechten.

Doe het volgende om ervoor te zorgen dat gebruik van een werkruimte wordt toegepast op uw rechten voor het OMS-abonnement:

1. Maak uw werkruimte in een Azure-abonnement dat deel uitmaakt van de Enterprise-overeenkomst die het OMS-abonnement omvat
2. Selecteer het *OMS*-abonnement voor de werkruimte

> [!NOTE]
> Als uw werkruimte is gemaakt vóór 26 september 2016 en uw Log Analytics-abonnement *Premium* is, maakt deze werkruimte gebruik van de rechten van de OMS-invoegtoepassing voor System Center. U kunt uw rechten ook gebruiken door over te schakelen naar de *OMS*-prijscategorie.
>
>

De rechten van het OMS-abonnement zijn niet zichtbaar in de Azure Portal of OMS-portal. U kunt de rechten en het gebruik wel in de Enterprise Portal zien.  

Als u het Azure-abonnement waaraan uw werkruimte is gekoppeld, wilt wijzigen, kunt u de Azure PowerShell-cmdlet [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) gebruiken.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Azure Commitment gebruiken via een Enterprise-overeenkomst
Als u geen OMS-abonnement hebt, betaalt u voor elk onderdeel van OMS afzonderlijk en wordt het gebruik weergegeven op uw Azure-factuur.

Als u een Azure-betalingsverplichting hebt voor de Enterprise-inschrijving waaraan uw Azure-abonnementen zijn gekoppeld, wordt gebruik van Log Analytics automatisch verrekend met de resterende betalingsverplichting.

Als u het Azure-abonnement waaraan de werkruimte is gekoppeld, wilt wijzigen, kunt u de Azure PowerShell-cmdlet [Move-AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) gebruiken.  

### <a name="change-a-workspace-to-a-paid-pricing-tier-in-the-azure-portal"></a>Een werkruimte wijzigen in een betaalde prijscategorie in Azure Portal
1. Meld u aan bij de [Azure Portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Selecteer een werkruimte.  
4. Klik op de blade van de werkruimte onder **Algemeen** op **Prijscategorie**.  
5. Selecteer onder **Prijscategorie** een prijscategorie en klik vervolgens op **Selecteren**.  
    ![abonnement selecteren](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Wanneer u de weergave in Azure Portal vernieuwt, ziet u dat **Prijscategorie** is bijgewerkt met de categorie dat u hebt geselecteerd.  
    ![bijgewerkt abonnement](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Als de werkruimte is gekoppeld aan een Automation-account, moet u vóórdat u de prijscategorie *Zelfstandig (per GB)* kunt selecteren eerst alle oplossingen **Automation and Control** verwijderen en het Automation-account loskoppelen. Klik op de blade van de werkruimte onder **Algemeen** op **Oplossingen** om oplossingen te bekijken en te verwijderen. Klik op de blade **Prijscategorie** op de naam van het Automation-account om het Automation-account los te koppelen.
>
>

### <a name="change-a-workspace-to-a-paid-pricing-tier-in-the-oms-portal"></a>Een werkruimte wijzigen in een betaalde prijscategorie in de OMS-portal

Als u de prijscategorie wilt wijzigen via de OMS-portal, moet u een Azure-abonnement hebben.

1. Klik in de OMS-portal op de tegel **Instellingen**.
2. Klik op het tabblad **Accounts** en vervolgens op het tabblad **Azure-abonnement en data-abonnement**.
3. Klik op de prijscategorie die u wilt gebruiken.
4. Klik op **Opslaan**.  
   ![abonnement en data-abonnementen](./media/log-analytics-manage-access/subscription-tab.png)

Uw nieuwe data-abonnement wordt weergegeven in het lint van de OMS-portal boven aan de webpagina.

![OMS-lint](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Wijzigen hoelang gegevens worden opgeslagen in Log Analytics

In de prijscategorie Gratis blijven de gegevens van de afgelopen zeven dagen beschikbaar in Log Analytics.
In de prijscategorie Standard blijven de gegevens van de afgelopen dertig dagen beschikbaar in Log Analytics.
In de prijscategorie Premium blijven de gegevens van de afgelopen 365 dagen beschikbaar in Log Analytics.
In de prijscategorieën Standalone en OMS blijven de gegevens van de afgelopen 31 dagen standaard beschikbaar in Log Analytics.

Wanneer u de prijscategorieën Standalone en OMS gebruikt, kunt u de gegevens van maximaal 2 jaar (730 dagen) bewaren. Als gegevens langer dan 31 dagen (de standaardtermijn) zijn opgeslagen, worden er kosten voor gegevensretentie in rekening gebracht. Zie [Overschrijdingskosten](https://azure.microsoft.com/pricing/details/log-analytics/) voor meer informatie.

Zie [Kosten beheren door gegevensvolume en retentie in te stellen in Log Analytics](log-analytics-manage-cost-storage.md) om de duur van gegevensretentie te wijzigen.

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Een Azure Active Directory-organisatie wijzigen voor een werkruimte

U kunt de Azure Active Directory-organisatie van een werkruimte wijzigen. Door de Azure Active Directory-organisatie te wijzigen, kunt u gebruikers en groepen uit die map toevoegen aan de werkruimte.

### <a name="to-change-the-azure-active-directory-organization-for-a-workspace"></a>De Azure Active Directory-organisatie wijzigen voor een werkruimte

1. Klik op de pagina Instellingen in de OMS-portal op **Accounts** en klik vervolgens op het tabblad **Gebruikers beheren**.  
2. Controleer de informatie over organisatieaccounts en klik vervolgens op **Organisatie wijzigen**.  
    ![organisatie wijzigen](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Voer de identiteitsgegevens in van de beheerder van uw Azure Active Directory-domein. Vervolgens wordt er een bevestiging weergegeven waarin staat dat uw werkruimte is gekoppeld aan uw Azure Active Directory-domein.  
    ![bevestiging van gekoppelde werkruimte](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Een Log Analytics-werkruimte verwijderen
Wanneer u een OMS-werkruimte verwijdert, worden alle gegevens die betrekking hebben op uw werkruimte binnen 30 dagen uit Log Analytics verwijderd.

Als u een beheerder bent en er aan de werkruimte meerdere gebruikers zijn gekoppeld, wordt de koppeling tussen gebruikers en de werkruimte verbroken. Als de gebruikers zijn gekoppeld aan andere werkruimten, kunnen ze Log Analytics blijven gebruiken met die andere werkruimten. Als ze echter niet zijn gekoppeld aan andere werkruimten, moeten ze een werkruimte maken voor het gebruik van de service. Zie [Een Azure Log Analytics-werkruimte verwijderen](log-analytics-manage-del-workspace.md) voor informatie over het verwijderen van een werkruimte.

## <a name="next-steps"></a>Volgende stappen
* Zie [Gegevens van computers in uw omgeving verzamelen met Log Analytics](log-analytics-concept-hybrid.md) voor het verzamelen van gegevens van computers in uw datacenter of andere cloudomgeving.
* Zie [Gegevens verzamelen over Azure Virtual Machines](log-analytics-quick-collect-azurevm.md) voor het configureren van het verzamelen van gegevens van Azure VM's.  
* [Log Analytics-oplossingen uit de galerie met oplossingen toevoegen](log-analytics-add-solutions.md) om functionaliteit toe te voegen en gegevens te verzamelen.


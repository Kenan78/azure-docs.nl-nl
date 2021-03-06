---
title: Configureer uw API Management-service met Git - Azure | Microsoft Docs
description: Informatie over het opslaan en het configureren van de configuratie van uw API Management-service met Git.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: mattfarm
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2018
ms.author: apimpm
ms.openlocfilehash: 57d14b6aa6caca0cc9b075723d4c350b0a50c9f8
ms.sourcegitcommit: 059dae3d8a0e716adc95ad2296843a45745a415d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/09/2018
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a>Het opslaan en het configureren van de configuratie van uw API Management-service met Git

Elk exemplaar van API Management-service houdt een configuratiedatabase die informatie over de configuratie en metagegevens voor het service-exemplaar bevat. Door een instelling in de Azure portal te wijzigen, gebruikt een PowerShell-cmdlet of REST API-aanroep, kunnen u wijzigingen aangebracht in het service-exemplaar. Naast deze methoden kunt u ook de serviceconfiguratie-exemplaar met behulp van Git, zoals het inschakelen van scenario's voor het beheer van service beheren:

* Configuratie versioning - downloaden en opslaan van verschillende versies van de serviceconfiguratie
* Bulksgewijs configuratiewijzigingen - wijzigingen aanbrengen in meerdere delen van uw serviceconfiguratie in uw lokale opslagplaats en de wijzigingen naar de server integreren met een enkele bewerking
* Werkstroom- en bekend Git toolchain de Git tooling en werkstromen die u al bekend met bent gebruiken

Het volgende diagram toont een overzicht van de verschillende manieren voor het configureren van uw API Management-service-exemplaar.

![GIT configureren][api-management-git-configure]

Wanneer u wijzigingen aan uw service met de Azure-portal, PowerShell-cmdlets of de REST-API aanbrengt, u beheert uw service configuration database met de `https://{name}.management.azure-api.net` eindpunt, zoals wordt weergegeven aan de rechterkant van het diagram. Aan de linkerkant van het diagram ziet u hoe u de configuratie van uw service met Git kunt beheren en Git-opslagplaats voor uw service zich bevindt op `https://{name}.scm.azure-api.net`.

De volgende stappen geven een overzicht van het beheer van uw API Management-service-exemplaar met Git.

1. Toegang tot de configuratie van Git in uw service
2. Sla de configuratiedatabase voor uw service op de Git-opslagplaats
3. Kloon de Git-opslagplaats op uw lokale computer
4. Trek de meest recente opslagplaats naar beneden op uw lokale computer en wijzigingen doorvoeren en push terug naar uw opslagplaats
5. De wijzigingen van uw opslagplaats implementeren in uw service-configuratiedatabase

Dit artikel wordt beschreven hoe u inschakelen en Git gebruiken voor het beheren van de serviceconfiguratie en bevat een verwijzing voor de bestanden en mappen in de Git-opslagplaats.

## <a name="access-git-configuration-in-your-service"></a>Toegang tot de configuratie van Git in uw service

Als u wilt weergeven en configureren van de Git-configuratie-instellingen, klikt u op de **beveiliging** menu en navigeer naar de **configuratie opslagplaats** tabblad.

![GIT inschakelen][api-management-enable-git]

> [!IMPORTANT]
> Geen geheimen die niet zijn gedefinieerd zoals eigenschappen worden opgeslagen in de opslagplaats en in de geschiedenis totdat u blijven uitschakelen en opnieuw inschakelen Git. Eigenschappen van bieden een veilige plaats voor het beheren van de constante string-waarden, inclusief geheimen, voor alle configuratie-API en beleidsregels, zodat u niet hoeft op te slaan ze rechtstreeks in uw beleidsverklaringen. Zie voor meer informatie [het gebruik van eigenschappen in Azure API Management-beleidsregels](api-management-howto-properties.md).
> 
> 

Zie voor meer informatie over het inschakelen of uitschakelen via de REST-API toegang tot een Git [in- of uitschakelen via de REST-API toegang tot een Git](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="to-save-the-service-configuration-to-the-git-repository"></a>Configuratie van de service om op te slaan de Git-opslagplaats

De eerste stap voordat u de opslagplaats klonen is de huidige status van de serviceconfiguratie opslaan in de opslagplaats. Klik op **opslaan in de opslagplaats**.

Breng de gewenste wijzigingen in het bevestigingsvenster en klik op **Ok** om op te slaan.

Na enkele ogenblikken de configuratie wordt opgeslagen en de status van de configuratie van de opslagplaats wordt weergegeven, inclusief de datum en tijd van de laatste wijziging in de configuratie en de laatste synchronisatie tussen de configuration-service en de opslagplaats.

Zodra de configuratie is opgeslagen in de opslagplaats, kunnen worden gekloond.

Zie voor informatie over het uitvoeren van deze bewerking met de REST API, [doorvoeren configuratie momentopname over met de REST-API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="to-clone-the-repository-to-your-local-machine"></a>Voor het klonen van de opslagplaats op uw lokale computer

Als u wilt een opslagplaats klonen, moet u de URL van uw opslagplaats, een gebruikersnaam en een wachtwoord. Als u de gebruikersnaam en andere referenties, klikt u op **toegang tot de referenties** bovenaan op de pagina.  
 
Als een wachtwoord worden gegenereerd, eerst voor zorgen dat de **verstrijken** is ingesteld op de gewenste vervaldatum en -tijd en klik vervolgens op **genereren**.

> [!IMPORTANT]
> Noteer dit wachtwoord. Zodra u deze pagina verlaat het wachtwoord niet opnieuw weergegeven.
> 

De volgende voorbeelden gebruikt het hulpprogramma Git Bash van [Git voor Windows](http://www.git-scm.com/downloads) , maar u kunt een Git-hulpmiddel dat u bekend met bent.

Open uw Git-hulpprogramma in de gewenste map en voer de volgende opdracht voor het klonen van de git-opslagplaats op uw lokale computer, met de opdracht die is geleverd door de Azure-portal.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Geef de gebruikersnaam en wachtwoord wanneer u wordt gevraagd.

Als u eventuele fouten ontvangt, probeert u het wijzigen van uw `git clone` opdracht om op te nemen van de gebruikersnaam en wachtwoord, zoals wordt weergegeven in het volgende voorbeeld.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Als dit een fout biedt, kunt u URL-codering van het gedeelte van het wachtwoord van de opdracht. Een snelle manier om dit te doen is Visual Studio openen, en voert u de volgende opdracht in de **venster direct**. Openen van de **venster direct**, opent u een oplossing of project in Visual Studio (of maak een nieuwe lege console-toepassing), en kies **Windows**, **direct** van de **fouten opsporen in** menu.

```
?System.NetWebUtility.UrlEncode("password from the Azure portal")
```

Gebruik het gecodeerde wachtwoord samen met de naam en opslagplaats locatie om samen te stellen de git-opdracht.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Zodra de opslagplaats wordt gekloond kunt u deze kunt bekijken en bewerken in het lokale bestandssysteem. Zie voor meer informatie [structuur verwijzing van lokale Git-opslagplaats, bestanden en mappen](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a>Bijwerken van uw lokale opslagplaats met de meest recente configuratie van de service-exemplaar

Als u wijzigingen in uw API Management-service-exemplaar in de Azure portal of met de REST API aanbrengen, moet u deze wijzigingen opslaan in de opslagplaats voordat u uw lokale opslagplaats met de meest recente wijzigingen bijwerken kunt. Om dit te doen, klikt u op **configuratie opslaan naar opslagplaats** op de **configuratie opslagplaats** tabblad in de Azure portal en voert u de volgende opdracht in uw lokale opslagplaats.

```
git pull
```

Voordat u `git pull` Zorg ervoor dat u in de map voor uw lokale opslagplaats. Als u hebt zojuist de `git clone` opdracht, en vervolgens moet u de map op uw opslagplaats door een opdracht als volgt uit te voeren.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a>Naar wijzigingen uit uw lokale opslagplaats naar de server-opslagplaats forceren
Voor het wijzigingen van uw lokale opslagplaats pushen naar de opslagplaats van de server, moet u uw wijzigingen en vervolgens toepassen op de server-opslagplaats. Open uw opdracht Git hulpprogramma, overschakelen naar de map van uw lokale opslagplaats en uitgeven van de volgende opdrachten om uw wijzigingen.

```
git add --all
git commit -m "Description of your changes"
```

Voor het pushen alle van de doorvoeracties naar de server, moet u de volgende opdracht uitvoeren.

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a>Eventuele wijzigingen in de serviceconfiguratie implementeren op service-exemplaar van API Management

Als uw lokale wijzigingen zijn doorgevoerd en naar de opslagplaats server gepusht, kunt u ze kunt implementeren in uw API Management-service-exemplaar.

Zie voor informatie over het uitvoeren van deze bewerking met de REST API, [Git implementeren wijzigingen in de REST-API-configuratiedatabase](https://docs.microsoft.com/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Verwijzing in de bestanden en mappen de structuur van de lokale Git-opslagplaats

De bestanden en mappen in de lokale git-opslagplaats bevatten de configuratie-informatie over het service-exemplaar.

| Item | Beschrijving |
| --- | --- |
| Hoofdmap voor de api-management |Op het hoogste niveau van de configuratie voor de service-exemplaar bevat |
| map van de API 's |Bevat de configuratie voor de API's in het service-exemplaar |
| map groepen |Bevat de configuratie voor de groepen in het service-exemplaar |
| map beleid |Bevat de beleidsregels in het service-exemplaar |
| portalStyles map |Bevat de configuratie voor de developer portal aanpassingen in het service-exemplaar |
| map Products |Bevat de configuratie voor de producten in het service-exemplaar |
| sjablonenmap |Bevat de configuratie voor de e-mailsjablonen in het service-exemplaar |

Elke map kan een of meer bestanden bevatten en in sommige gevallen een of meer mappen, bijvoorbeeld een map voor elke API, product of groep. De bestanden in elke map zijn specifieke voor het entiteitstype beschreven door de naam van de map.

| Bestandstype | Doel |
| --- | --- |
| json |Configuratie-informatie over de respectieve entiteit |
| html |Beschrijvingen van de entiteit, vaak worden weergegeven in de portal voor ontwikkelaars |
| xml |Beleidsinstructies |
| CSS |Opmaakmodellen voor developer portal aanpassen |

Deze bestanden kunnen worden gemaakt, verwijderd, bewerkt en beheerd op het lokale bestandssysteem en de wijzigingen die zijn geïmplementeerd weer met de uw API Management-service-exemplaar.

> [!NOTE]
> De volgende entiteiten worden niet opgenomen in de Git-opslagplaats en kunnen niet worden geconfigureerd met Git.
> 
> * Gebruikers
> * Abonnementen
> * Eigenschappen
> * Developer portal entiteiten dan stijlen
> 

### <a name="root-api-management-folder"></a>Hoofdmap voor de api-management
De hoofdmap `api-management` map bevat een `configuration.json` bestand dat op het hoogste niveau informatie over de service-exemplaar in de volgende indeling bevat.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

De eerste vier instellingen (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, en `UserRegistrationTermsConsentRequired`) toewijzen aan de volgende instellingen op de **identiteiten** tabblad de **beveiliging** sectie.

| Identiteit | Toegewezen aan |
| --- | --- |
| RegistrationEnabled |**Anonieme gebruikers omleiden naar de aanmeldingspagina** selectievakje |
| UserRegistrationTerms |**Gebruiksvoorwaarden op aanmelding gebruiker** tekstvak |
| UserRegistrationTermsEnabled |**Gebruiksvoorwaarden weergeven op de aanmeldingspagina** selectievakje |
| UserRegistrationTermsConsentRequired |**Toestemming vereist** selectievakje |

De volgende vier instellingen (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, en `DelegationValidationKey`) toewijzen aan de volgende instellingen op de **delegering** tabblad de **beveiliging** sectie.

| Delegatie-instelling | Toegewezen aan |
| --- | --- |
| DelegationEnabled |**Gemachtigde aanmelden & registratie** selectievakje |
| DelegationUrl |**De eindpunt-URL voor overdracht** tekstvak |
| DelegatedSubscriptionEnabled |**Product abonnement delegeren** selectievakje |
| DelegationValidationKey |**Validatiesleutel delegeren** tekstvak |

De laatste instelling `$ref-policy`, toegewezen aan het bestand globaal beleid instructies voor het service-exemplaar.

### <a name="apis-folder"></a>map van de API 's
De `apis` een map voor elke API in het service-exemplaar waarin de volgende items bevat.

* `apis\<api name>\configuration.json`-Dit is de configuratie voor de API en bevat informatie over de URL van de back-service en de bewerkingen. Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen [ophalen van een specifieke API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) met `export=true` in `application/json` indeling.
* `apis\<api name>\api.description.html`-Dit is de beschrijving van de API en komt overeen met de `description` eigenschap van de [API entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Deze map bevat `<operation name>.description.html` bestanden die zijn toegewezen aan de bewerkingen in de API. Elk bestand bevat de beschrijving van één bewerking in de API die wordt toegewezen aan de `description` eigenschap van de [bewerking entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in de REST-API.

### <a name="groups-folder"></a>map groepen
De `groups` een map voor elke groep die is gedefinieerd in het service-exemplaar bevat.

* `groups\<group name>\configuration.json`-Dit is de configuratie voor de groep. Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen de [ophalen van een specifieke groep](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) bewerking.
* `groups\<group name>\description.html`-Dit is de beschrijving van de groep en komt overeen met de `description` eigenschap van de [groep entiteit](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>map beleid
De `policies` map bevat de instructies van het beleid voor uw service-exemplaar.

* `policies\global.xml`-beleid is gedefinieerd op globaal bereik voor uw service-exemplaar bevat.
* `policies\apis\<api name>\`-Als er beleid is gedefinieerd op API-scope, zijn opgenomen in deze map.
* `policies\apis\<api name>\<operation name>\`map - als er beleid is gedefinieerd op bewerkingsbereik, zijn opgenomen in deze map in `<operation name>.xml` bestanden die zijn toegewezen aan de beleidsverklaringen voor elke bewerking.
* `policies\products\`-Als er beleid is gedefinieerd op de product-scope, zijn opgenomen in deze map bevat `<product name>.xml` bestanden die zijn toegewezen aan de instructies van het beleid voor elk product.

### <a name="portalstyles-folder"></a>portalStyles map
De `portalStyles` map bevat configuratie- en opmaakmodellen developer portal aanpassingen voor service-exemplaar.

* `portalStyles\configuration.json`-de namen bevat van de opmaakmodellen die wordt gebruikt door de portal voor ontwikkelaars
* `portalStyles\<style name>.css`-elke `<style name>.css` bestand bevat stijlen voor de portal voor ontwikkelaars (`Preview.css` en `Production.css` standaard).

### <a name="products-folder"></a>map Products
De `products` een map voor elk product dat is gedefinieerd in het service-exemplaar bevat.

* `products\<product name>\configuration.json`-Dit is de configuratie voor het product. Dit is dezelfde informatie die wordt geretourneerd als u aan te roepen de [ophalen van een specifiek product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) bewerking.
* `products\<product name>\product.description.html`-Dit is de beschrijving van het product en komt overeen met de `description` eigenschap van de [product entiteit](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in de REST-API.

### <a name="templates"></a>sjablonen
De `templates` map bevat de configuratie voor de [e-mailsjablonen](api-management-howto-configure-notifications.md) van het service-exemplaar.

* `<template name>\configuration.json`-Dit is de configuratie voor de e-mailsjabloon.
* `<template name>\body.html`-Dit is de hoofdtekst van het e-mailsjabloon.

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over andere manieren voor het beheren van uw service-exemplaar:

* Beheren van uw service-exemplaar met de volgende PowerShell-cmdlets
  * [Naslaginformatie over PowerShell-cmdlets voor service-implementatie](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Service management PowerShell-cmdlet-verwijzing](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Beheren van uw service-exemplaar met de REST API
  * [Naslaginformatie over API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)


[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png





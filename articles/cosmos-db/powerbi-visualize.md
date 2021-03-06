---
title: Power BI-zelfstudie voor Azure DB die Cosmos-connector | Microsoft Docs
description: Gebruik deze zelfstudie Power BI importeren JSON, begrijpelijke manier mee rapporten maken en gegevens visualiseren met behulp van de Azure DB die Cosmos en Power BI-connector.
keywords: Power bi zelfstudie, visualiseren van gegevens, power bi-connector
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 04/19/2018
ms.author: sngun
ms.openlocfilehash: 67ea7a9ea1a1be4fd0780f8b8ce22f1a133615e0
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/01/2018
ms.locfileid: "34615866"
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-the-power-bi-connector"></a>Power BI-zelfstudie voor Azure Cosmos DB: gegevens visualiseren met behulp van de Power BI-connector
[PowerBI.com](https://powerbi.microsoft.com/) is een onlineservice waar u kunt maken en delen van dashboards en rapporten met gegevens die belangrijk voor u en uw organisatie.  Power BI Desktop is een speciale rapport ontwerpgereedschap waarmee u gegevens ophalen uit verschillende gegevensbronnen, samen te voegen en de gegevens transformeren krachtige rapporten en visualisaties maken en publiceren van de rapporten naar Power BI.  Met de meest recente versie van Power BI Desktop, kunt u nu verbinding met uw Azure DB die Cosmos-account via de Azure DB die Cosmos-connector voor Power BI.   

In deze zelfstudie Power BI bekijken we de stappen voor het verbinding maken met een Azure DB die Cosmos-account in Power BI Desktop, gaat u naar een verzameling waar we wilt ophalen van de gegevens met behulp van de Navigator, transformeren JSON-gegevens in tabelvorm met Power BI Desktop Query-Editor , en maken en publiceren van een rapport op PowerBI.com.

Na het voltooien van deze zelfstudie Power BI, hebt u mogelijk de volgende vragen beantwoorden:  

* Hoe kan ik rapporten maken met gegevens uit Azure Cosmos DB met Power BI Desktop?
* Hoe kan ik verbinding maken met een Azure DB die Cosmos-account in Power BI Desktop?
* Hoe kan ik gegevens ophalen uit een verzameling in Power BI Desktop?
* Hoe kan ik geneste JSON-gegevens in Power BI Desktop transformeren?
* Hoe kan ik publiceren en delen van mijn rapporten op PowerBI.com?

> [!NOTE]
> De Power BI-connector voor Azure Cosmos DB maakt verbinding met Power BI Desktop voor extractie en transformatie van gegevens. Rapporten die zijn gemaakt in Power BI Desktop kunnen vervolgens worden gepubliceerd bij PowerBI.com. Directe uitpakken en transformatie van Azure DB die Cosmos-gegevens kunnen niet worden uitgevoerd op PowerBI.com. 

> [!NOTE]
> Voor Azure Cosmos DB verbinding met Power BI met de MongoDB-API, moet u de [Simba MongoDB ODBC-stuurprogramma](http://www.simba.com/drivers/mongodb-odbc-jdbc/).

## <a name="prerequisites"></a>Vereisten
Voordat u de instructies in deze zelfstudie Power BI, zorg ervoor dat u toegang tot de volgende bronnen hebben:

* [De nieuwste versie van Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Toegang tot onze demo-account of de gegevens in uw Azure DB die Cosmos-account.
  * De demo-account is gevuld met de Vulkaan gegevens weergegeven in deze zelfstudie. Dit account demo niet afhankelijk is van een SLA's en is bedoeld voor demonstratiedoeleinden alleen.  We de voorbehouden wijzigingen aanbrengen in deze demo voor het inclusief maar niet beperkt tot beëindiging van het account, het wijzigen van de sleutel, beperken van toegang, wijzigen, en verwijderen van de gegevens op elk moment zonder voorafgaande kennisgeving of reden.
    * URL: https://analytics.documents.azure.com
    * Read-only key: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * Of Zie maken van uw eigen account [een Azure Cosmos DB database-account maken met de Azure-portal](https://azure.microsoft.com/documentation/articles/create-account/). Vervolgens voorbeeld Vulkaan ophalen gegevens die is vergelijkbaar met wat in deze zelfstudie wordt gebruikt (maar bevat niet de GeoJSON-blokken), Zie de [NOAA site](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) en importeer de gegevens met de [hulpprogramma voor gegevensmigratie Azure Cosmos DB](import-data.md).

Als u wilt uw rapporten op PowerBI.com delen, hebt u een account op PowerBI.com.  Voor meer informatie over Power BI voor vrije en Power BI Pro, gaat u naar [ https://powerbi.microsoft.com/pricing ](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Aan de slag
In deze zelfstudie gaan we stelt u zich dat u een geologist bestudeert vulkanen over de hele wereld.  De Vulkaan gegevens worden opgeslagen in een Azure DB die Cosmos-account en de JSON-documenten eruitzien als het volgende voorbeelddocument.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

U wilt de Vulkaan-gegevens ophalen uit het account voor Azure Cosmos DB en visualiseren van gegevens in een interactieve Power BI-rapport, zoals het volgende rapport.

![Door het voltooien van deze zelfstudie Power BI met de Power BI-connector, hebt u mogelijk gegevens visualiseren met het Power BI Desktop Vulkaan rapport](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Wilt u het proberen? Aan de slag.

1. Power BI Desktop worden uitgevoerd op uw werkstation.
2. Als Power BI Desktop wordt gestart, een *Welkom* scherm wordt weergegeven.
   
    ![Power BI Desktop welkomstscherm - Power BI-connector](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. U kunt **gegevens ophalen**, Zie **recente bronnen**, of **Open andere rapporten** rechtstreeks vanuit de *Welkom* scherm.  Klik op de X in de rechterbovenhoek om te sluiten van het scherm. De **rapport** weergave van Power BI Desktop.
   
    ![Power BI Desktop rapportweergave - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Selecteer de **Start** lint en klik vervolgens op **gegevens ophalen**.  De **gegevens ophalen** venster moet worden weergegeven.
5. Klik op **Azure**, selecteer **Azure Cosmos-DB (bèta)**, en klik vervolgens op **Connect**. 

    ![Power BI Desktop ophalen van gegevens - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Op de **Preview Connector** pagina, klikt u op **doorgaan**. De **Azure Cosmos DB** venster wordt weergegeven.
7. Geef de URL Azure Cosmos DB account eindpunt u wilt de gegevens ophalen, zoals hieronder wordt weergegeven, en klik vervolgens op **OK**. Uw eigen account wil gebruiken, kunt u de URL ophalen uit het vak URI in de **[sleutels](manage-account.md#keys)** blade van de Azure-portal. Als u wilt de demo-account gebruikt, voer `https://analytics.documents.azure.com` voor de URL. 
   
    Laat de databasenaam, de naam van verzameling en de SQL-instructie leeg als u deze velden zijn optioneel.  We gebruiken in plaats daarvan de Navigator selecteren van de Database en verzameling om te bepalen waar de gegevens opgehaald.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, bureaublad-venster verbinding maken](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Als u naar dit eindpunt voor de eerste keer verbindt, wordt u gevraagd de accountsleutel op te geven. Voor uw eigen account ophalen van de sleutel van de **primaire sleutel** vak de **[alleen-lezen sleutels](manage-account.md#keys)** blade van de Azure-portal. Voor de demo-account, de sleutel is `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Voer de juiste sleutel in en klik vervolgens op **Connect**.
   
    Het is raadzaam dat u de sleutel alleen-lezen bij het maken van rapporten.  Dit voorkomt dat onnodige blootstelling van de hoofdsleutel voor potentiële beveiligingsrisico's. De sleutel alleen-lezen is beschikbaar via de [sleutels](manage-account.md#keys) blade van de Azure portal of u kunt de bovenstaande demo-accountgegevens.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, Accountsleutel](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Als u krijgt een foutbericht 'de opgegeven database is niet gevonden.' Zie de oplossing in deze stappen [Power BI probleem](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Wanneer het account met succes is verbonden, de **Navigator** deelvenster wordt weergegeven.  De **Navigator** bevat een lijst met databases die onder het account.
10. Klik op en vouw op de database waarin de gegevens voor het rapport is afkomstig uit, als u de demo-account selecteren **volcanodb**.   
11. Selecteer nu een verzameling waartoe de gegevens moeten worden opgehaald. Als u de demo-account gebruikt, selecteert u **volcano1**.
    
    Het voorbeeldvenster bevat een overzicht van **Record** items.  Een Document wordt weergegeven als een **Record** type in Power BI. Een geneste JSON-blok in het document is op deze manier ook een **Record**.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, Navigator-venster](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Klik op **bewerken** starten van de Query-Editor in een nieuw venster voor het transformeren van de gegevens.

## <a name="flattening-and-transforming-json-documents"></a>Plat en transformeren JSON-documenten
1. Overschakelen naar de editor voor Power BI Query waarin de **Document** kolom in het middelste deelvenster.
   ![Power BI Desktop Query-Editor](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Klik op de uitbreidingsmodule aan de rechterkant van de **Document** kolomkop.  Het snelmenu dat verschijnt een lijst met velden worden weergegeven.  Selecteer de velden die u nodig hebt voor uw rapport bijvoorbeeld Vulkaan naam, land, regio, locatie, uitbreiding van bevoegdheden, Type, Status en laatste uitbreken weten. Schakel de **oorspronkelijke kolomnaam gebruiken als voorvoegsel** vak en klik vervolgens op **OK**.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector - documenten uitvouwen](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Het middelste deelvenster ziet een voorbeeld van het resultaat met de velden die zijn geselecteerd.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector - plat resultaten](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. In ons voorbeeld is de locatie-eigenschap een blok GeoJSON in een document.  Zoals u zien kunt, de locatie wordt weergegeven als een **Record** type in Power BI Desktop.  
5. Klik op de uitbreidingsmodule aan de rechterkant van de kolomkop Document.Location.  Het snelmenu met type en coördinaten velden worden weergegeven.  Laten we het veld coördinaten Selecteer, controleert u **oorspronkelijke kolomnaam gebruiken als voorvoegsel** niet is ingeschakeld en klik op **OK**.
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, locatie-record](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Het middelste deelvenster ziet u nu een kolom coördinaten van **lijst** type.  Zoals wordt weergegeven aan het begin van de zelfstudie, wordt de status van de GeoJSON-gegevens in deze zelfstudie is van het type met breedtegraad en lengtegraad waarden worden vastgelegd in de matrix coördinaten.
   
    Het element coördinaten [0] geeft lengtegraad terwijl coördinaten [1] breedtegraad vertegenwoordigt.
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, coördinaten lijst](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Als u wilt de matrix coördinaten afvlakken, maakt u een **aangepaste kolom** LatLong aangeroepen.  Selecteer de **kolom toevoegen** lint en klik op **aangepaste kolom**.  De **aangepaste kolom** venster wordt weergegeven.
8. Geef een naam voor de nieuwe kolom, bijvoorbeeld LatLong.
9. Geef vervolgens de aangepaste formule voor de nieuwe kolom.  In ons voorbeeld wordt we samenvoegen van de breedtegraad en lengtegraad waarden, gescheiden door komma's, zoals hieronder met de volgende formule weergegeven: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Klik op **OK**.
   
    Ga voor meer informatie over gegevens Analysis expressies (DAX) waaronder DAX-functies [Basic DAX in Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, aangepaste kolom toevoegen](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)

10. Het middelste deelvenster ziet nu de nieuwe LatLong kolommen gevuld met de waarden.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, aangepaste LatLong kolom](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Als u een foutbericht in de nieuwe kolom ontvangt, zorg ervoor dat de toegepaste stappen onder Query-instellingen overeenkomen met de volgende afbeelding:
    
    ![Toegepaste stappen moet bron, navigatie, uitgebreid Document, uitgebreid Document.Location, aangepaste toegevoegd](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Als uw stappen verschillen, de extra stappen te verwijderen en probeer opnieuw de aangepaste kolom toe te voegen. 

11. Klik op **sluiten en toepassen** om op te slaan van het gegevensmodel.
    
    ![Power BI-zelfstudie voor Azure Cosmos DB Power BI-connector, sluit & toepassen](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-the-reports"></a>De rapporten maken
Power BI Desktop rapportweergave is waar u kunt gaan maken van rapporten om gegevens te visualiseren.  U kunt rapporten maken met slepen en neerzetten van velden in de **rapport** canvas.

![Power BI Desktop rapportweergave - Power BI-connector](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

U moet in de rapportweergave vinden:

1. De **velden** deelvenster dit is waar u een lijst met gegevensmodellen met velden die u voor uw rapporten gebruiken kunt kunt zien.
2. De **visualisaties** deelvenster. Een rapport kan één of meerdere visualisaties bevatten.  Kies de visuele typen aanpassen van uw behoeften van de **visualisaties** deelvenster.
3. De **rapport** canvas, dit is waar u de visuele elementen maken voor uw rapport.
4. De **rapport** pagina. U kunt meerdere pagina's het rapport in Power BI Desktop toevoegen.

Hieronder ziet u de basisstappen voor het maken van een eenvoudige interactieve kaart view-rapport.

1. We gaan een overzichtsweergave van de locatie van elke Vulkaan maken in ons voorbeeld.  In de **visualisaties** deelvenster, klik op de kaart visuele element als gemarkeerd in de bovenstaande schermafbeelding.  U ziet de kaart visuele element getekend op de **rapport** canvas.  De **visualisatie** deelvenster moet ook een set eigenschappen die betrekking hebben op de kaart visuele element worden weergegeven.
2. Nu slepen en neerzetten van het veld LatLong uit de **velden** deelvenster naar de **locatie** eigenschap in **visualisaties** deelvenster.
3. Vervolgens slepen en neerzetten van het veld Naam Vulkaan de **legenda** eigenschap.  
4. Vervolgens slepen en neerzetten van het veld uitbreiding van bevoegdheden voor de **grootte** eigenschap.  
5. U ziet nu de kaart visual met een set van die wijzen op de locatie van elke Vulkaan met de grootte van de belgrootte correleren van de onrechtmatige uitbreiding van Vulkaan bellen.
6. U hebt nu een eenvoudig rapport gemaakt.  Verder kunt u het rapport aanpassen door meer visualisaties toe te voegen.  In ons geval hebben we een slicer Vulkaan Type zodat het rapport interactieve toegevoegd.  
   
    ![Schermopname van het laatste rapport Power BI Desktop na voltooiing van de Power BI-zelfstudie voor Azure Cosmos-DB](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)
7. Klik in het menu bestand **opslaan** en sla het bestand als PowerBITutorial.pbix.

## <a name="publish-and-share-your-report"></a>Publiceren en delen van uw rapport
Als u wilt delen van uw rapport, hebt u een account op PowerBI.com.

1. Klik in de Power BI Desktop op de **Start** lint.
2. Klik op **Publish**.  U wordt gevraagd de gebruikersnaam en wachtwoord invoeren voor uw account PowerBI.com.
3. Zodra de referentie is geverifieerd, wordt het rapport is gepubliceerd naar uw bestemming die u hebt geselecteerd.
4. Klik op **Open 'PowerBITutorial.pbix' in Power BI** om te bekijken en delen van uw rapport op PowerBI.com.
   
    ![Publiceren om Power BI geslaagd! Open zelfstudie in Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Een dashboard maken in PowerBI.com
Nu dat u een rapport hebt, kunnen delen op PowerBI.com

Wanneer u uw rapport uit Power BI Desktop bij PowerBI.com publiceert, genereert een **rapport** en een **gegevensset** in uw tenant PowerBI.com. Bijvoorbeeld: nadat u een rapport genaamd gepubliceerd **PowerBITutorial** bij PowerBI.com, ziet u PowerBITutorial in zowel de **rapporten** en **gegevenssets** secties op PowerBI.com.

   ![Schermopname van het nieuwe rapport en gegevensset in PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

Voor het maken van een deelbare dashboard, klikt u op de **pincode Live pagina** knop op uw rapport PowerBI.com.

   ![Schermopname van het nieuwe rapport en gegevensset in PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Volg de instructies in [een tegel uit een rapport vastmaken](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) voor het maken van een nieuw dashboard. 

U kunt ook ad-hoc wijzigingen in het rapport doen voordat u een dashboard. Het wordt echter aanbevolen dat u Power BI Desktop uitvoeren van de wijzigingen en het rapport naar PowerBI.com te publiceren.

<!-- ## Refresh data in PowerBI.com
There are two ways to refresh data, ad hoc and scheduled.

For an ad hoc refresh, simply click on the eclipses (…) by the **Dataset**, e.g. PowerBITutorial. You should see a list of actions including **Refresh Now**. Click **Refresh Now** to refresh the data.

![Screenshot of Refresh Now in PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

For a scheduled refresh, do the following.

1. Click **Schedule Refresh** in the action list. 

    ![Screenshot of the Schedule Refresh in PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. In the **Settings** page, expand **Data source credentials**. 
3. Click on **Edit credentials**. 
   
    The Configure popup appears. 
4. Enter the key to connect to the Azure Cosmos DB account for that data set, then click **Sign in**. 
5. Expand **Schedule Refresh** and set up the schedule you want to refresh the dataset. 
6. Click **Apply** and you are done setting up the scheduled refresh.
-->
## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over Power BI, [aan de slag met Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* Zie voor meer informatie over Azure Cosmos DB, de [startpagina van Azure DB die Cosmos documentatie](https://azure.microsoft.com/documentation/services/cosmos-db/).


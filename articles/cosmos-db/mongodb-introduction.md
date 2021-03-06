---
title: 'Inleiding tot Azure Cosmos DB: MongoDB API | Microsoft Docs'
description: Meer informatie over hoe u Azure Cosmos DB kunt gebruiken om op te slaan en query grote hoeveelheden JSON-documenten met een lage latentie met behulp van de populaire OSS MongoDB APIs.
keywords: Wat is MongoDB
services: cosmos-db
author: AndrewHoh
manager: kfile
documentationcenter: ''
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2018
ms.author: anhoh
ms.openlocfilehash: bebf8b8830255277b5ea492f06e130ee667affa5
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/18/2018
---
# <a name="introduction-to-azure-cosmos-db-mongodb-api"></a>Inleiding tot Azure Cosmos DB: MongoDB-API

[Azure Cosmos DB](../cosmos-db/introduction.md) is de wereldwijd gedistribueerde databaseservice met meerdere modellen van Microsoft voor essentiële toepassingen. Biedt Azure Cosmos DB [directe globale distributie](distribute-data-globally.md), [elastisch schalen van doorvoer en opslag](partition-data.md) overal ter wereld, één cijfer milliseconde latenties bij de 99th percentiel en gegarandeerde hoog beschikbaarheid van alle back-ups door [toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Met Azure Cosmos DB worden [gegevens automatisch geïndexeerd](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf), zonder dat u te maken krijgt met schema- en indexbeheer. Azure Cosmos DB beschikt over meerdere modellen en ondersteunt modellen voor document-, sleutelwaarde-, grafiek- en kolomgegevens. 

![Azure Cosmos DB: MongoDB API](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Azure DB Cosmos-databases kunnen worden gebruikt als gegevensopslag voor apps die zijn geschreven voor [MongoDB](https://docs.mongodb.com/manual/introduction/). Deze functionaliteit betekent dat met behulp van de bestaande [stuurprogramma's](https://docs.mongodb.org/ecosystem/drivers/), uw toepassing geschreven voor MongoDB kan nu met Azure Cosmos DB communiceren en gebruiken van Azure DB die Cosmos-databases in plaats van MongoDB-databases. In veel gevallen kunt u overschakelen van het gebruik van MongoDB bij Azure Cosmos DB door eenvoudigweg een verbindingsreeks. Met deze functionaliteit kunt u gemakkelijk maken en in de MongoDB globaal gedistribueerd databasetoepassingen uitvoeren in Azure met Azure Cosmos DB en de cloud [uitgebreide toonaangevende Sla's](https://azure.microsoft.com/support/legal/sla/cosmos-db), maar blijft bekend gebruiken vaardigheden en hulpprogramma's voor MongoDB.

**Compatibiliteit met MongoDB**: U kunt uw bestaande MongoDB-expertise toepassingscode en tooling gebruiken zoals Azure Cosmos DB via het protocol MongoDB 3.4 (versie 5) implementeert en ondersteunt de [MongoDB aggregatie pijplijn](mongodb-feature-support.md#aggregation-pipeline). U kunt ontwikkelen met behulp van MongoDB en deze implementeren in productieomgevingen met een volledig beheerde en globaal gedistribueerde Azure DB die Cosmos-service.

## <a name="what-is-the-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Wat is het voordeel van het gebruik van Azure DB die Cosmos voor MongoDB toepassingen?

**Elastische schaalbare doorvoer en opslag:** voldoen aan uw toepassingen moeten door te schalen eenvoudig omhoog of omlaag de MongoDB-database. Uw gegevens worden opgeslagen op SSD-schijven (Solid State Disks) voor lage voorspelbare latenties. Azure Cosmos DB ondersteunt MongoDB-verzamelingen die kunnen worden geschaald naar vrijwel onbeperkte opslaggrootte en ingerichte doorvoer. Naarmate uw toepassing groeit, kunt u Azure Cosmos DB probleemloos elastisch schalen met voorspelbare prestaties. 

**Meerdere landen/regio-replicatie:** Azure Cosmos DB transparant uw gegevens worden gerepliceerd naar alle regio's die je hebt gekoppeld aan je account MongoDB, zodat u voor het ontwikkelen van toepassingen waarvoor globale toegang tot gegevens en tegelijkertijd de wisselwerking tussen consistentie, beschikbaarheid en prestaties, met bijbehorende garanties. Azure Cosmos DB biedt transparante regionale failover met multihoming-API's en de mogelijkheid om doorvoer en opslag wereldwijd elastisch te schalen. Meer informatie [Distribueer gegevens globaal](distribute-data-globally.md).

**Er is geen Serverbeheer**: U hoeft te beheren en schalen van uw MongoDB-databases. Azure Cosmos-database is een volledig beheerde service, waardoor u niet beschikt over een infrastructuur of virtuele Machines om zelf te beheren. Azure Cosmos DB is beschikbaar in 30 + [Azure-gebieden](https://azure.microsoft.com/regions/services/).

**Instelbare consistentieniveaus:** Azure Cosmos DB momenteel MongoDB versie 3.4 die twee consistentie instellingen sterk en uiteindelijk heeft wordt geïmplementeerd. Omdat Azure Cosmos DB multi-api, de instellingen van de consistentie van toepassing zijn op het niveau van het account en afdwingen van de consistentie wordt beheerd door elke API. Pas 3.6 MongoDB, er is geen concept van een sessieconsistentie, dus als u een MongoDB-API-account moet worden gebruikt met sessieconsistentie instelt, de consistentiecontrole is verlaagd tot de uiteindelijke bij gebruik van MongoDB APIs. Als u een garantie-your-eigenaar-lezen voor een account met MongoDB-API moet, wordt het standaardniveau voor consistentie voor het account moet worden ingesteld op strong of gebonden veroudering. Zie [Consistentieniveaus gebruiken om de beschikbaarheid en prestaties te maximaliseren](consistency-levels.md) voor meer informatie.

| Azure Cosmos DB standaardniveau consistentie |   Mongo-API (3.4) |
|---|---|
|Mogelijk| Mogelijk |
|Consistent prefix| Uiteindelijke met consistente volgorde |
|Sessie| Uiteindelijke met consistente volgorde |
|Gebonden veroudering| Sterk |
| Sterk | Sterk |

**Automatische indexering**: standaard Azure Cosmos DB indexeert automatisch alle de documenten in uw MongoDB-eigenschappen van de database en niet verwacht of vereist een schema of het maken van secundaire indexen. De unieke index mogelijkheid kunt bovendien een UNIQUE-beperking voor alle documentvelden die al automatisch geïndexeerd in Azure Cosmos DB zijn.

**Enterprise hoogwaardige**: Azure Cosmos DB ondersteunt meerdere lokale replica's voor het leveren van 99,99% beschikbaarheid en gegevensbescherming, met betrekking tot lokale en regionale fouten. Azure Cosmos DB heeft enterprise hoogwaardige [naleving certificeringen](https://www.microsoft.com/trustcenter) en beveiligingsfuncties. 

Meer informatie in deze video met Azure Cosmos DB Senior Program Manager, Aleksey Savateyev.

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T136/player]
> 

## <a name="how-to-get-started"></a>Hoe gaat u aan de slag

Ga als volgt de MongoDB-snelstartgidsen voor het maken van een Cosmos-DB Azure-account en uw bestaande MongoDB-toepassing voor het gebruik van Azure DB die Cosmos migreren of een nieuwe wilt bouwen:

* [Migreren van een bestaande Node.js MongoDB-web-app](create-mongodb-nodejs.md).
* [Een web-App voor MongoDB-API met .NET- en de Azure-portal](create-mongodb-dotnet.md)
* [Maken van een console-app van de MongoDB-API met Java en de Azure-portal](create-mongodb-java.md)

## <a name="next-steps"></a>Volgende stappen

Informatie over de Azure-API voor MongoDB Cosmos DB is geïntegreerd in de algehele Azure DB die Cosmos-documentatie, maar hier zijn enkele verwijzingen naar u op weg:

* Ga als volgt de [verbinding maken met een account MongoDB](connect-mongodb-account.md) zelfstudie voor informatie over het ophalen van de verbindingsinformatie voor uw account.
* Ga als volgt de [gebruik Studio 3T (MongoChef) met Azure Cosmos DB](mongodb-mongochef.md) zelfstudie voor informatie over het maken van een verbinding tussen uw Azure DB die Cosmos-database en de MongoDB-app in Studio 3 T.
* Ga als volgt de [gegevens voor het migreren naar Azure Cosmos DB met het protocol ondersteunen voor MongoDB](mongodb-migrate.md) zelfstudie voor het importeren van uw gegevens naar een API voor MongoDB-database.
* Verbinding maken met een API voor het gebruik van MongoDB-account [Robomongo](mongodb-robomongo.md).
* Meer informatie over hoeveel RUs van uw bewerkingen met gebruikmaakt de [GetLastRequestStatistics opdracht en de Azure portal metrische gegevens](set-throughput.md#GetLastRequestStatistics).
* Meer informatie over hoe [lezen voorkeuren voor globaal gedistribueerde apps configureren](../cosmos-db/tutorial-global-distribution-mongodb.md).

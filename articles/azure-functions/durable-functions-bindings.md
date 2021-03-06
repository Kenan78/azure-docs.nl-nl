---
title: Bindingen voor duurzame functies - Azure
description: Het gebruik van triggers en bindingen voor de extensie voor duurzame Functons voor Azure Functions.
services: functions
author: cgillum
manager: cfowler
editor: ''
tags: ''
keywords: ''
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/29/2017
ms.author: azfuncdf
ms.openlocfilehash: 370e6e2c569aaf6d9289bddccde2174b4dd2ee97
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2018
---
# <a name="bindings-for-durable-functions-azure-functions"></a>Bindingen voor duurzame functies (Azure-functies)

De [duurzame functies](durable-functions-overview.md) extensie introduceert twee nieuwe trigger bindingen waarmee de uitvoering van de functies orchestrator en activiteit. Er kleven ook een uitvoer-binding die als een client voor de runtime duurzame functies fungeert.

## <a name="orchestration-triggers"></a>Orchestration-triggers

De orchestration-trigger kunt u auteur duurzame orchestrator-functies. Deze trigger biedt ondersteuning voor nieuwe exemplaren van orchestrator-functie wordt gestart en bestaande exemplaren van orchestrator-functie die in afwachting zijn 'van' een taak wordt hervat.

Wanneer u de Visual Studio-hulpprogramma's voor Azure Functions, de orchestration-trigger is geconfigureerd met behulp van de [OrchestrationTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationTriggerAttribute.html) .NET-kenmerk.

Bij het schrijven van orchestrator-functies in scripttalen (bijvoorbeeld in de Azure-portal), de orchestration-trigger wordt gedefinieerd door de volgende JSON-object in de `bindings` matrix van de *function.json* bestand:

```json
{
    "name": "<Name of input parameter in function signature>",
    "orchestration": "<Optional - name of the orchestration>",
    "type": "orchestrationTrigger",
    "direction": "in"
}
```

* `orchestration` de naam van de orchestration is. Dit is de waarde die clients gebruiken moeten wanneer ze willen nieuwe exemplaren van deze functie orchestrator te starten. Deze eigenschap is optioneel. Als niet wordt opgegeven, wordt de naam van de functie gebruikt.

Deze binding trigger opgevraagd intern een reeks van wachtrijen in het standaardopslagaccount voor de functie-app. Deze wachtrijen zijn interne implementatiegegevens van de extensie, dat is waarom ze niet expliciet worden geconfigureerd in de bindingeigenschappen.

### <a name="trigger-behavior"></a>Gedrag van de trigger

Hieronder vindt u informatie over de orchestration-trigger:

* **Single-threading** -een enkele dispatcher-thread wordt gebruikt voor alle orchestrator-functie uitvoeren op een exemplaar van één host. Daarom is het belangrijk om ervoor te zorgen dat de functiecode orchestrator efficiënte en alle i/o niet uitvoeren. Het is ook belangrijk om ervoor te zorgen dat deze thread geen asynchrone werk, behalve wanneer in afwachting voor duurzame functies-specifieke taaktypen.
* **Afhandeling van poison-bericht** -er is geen ondersteuning voor verontreinigd bericht in de orchestration-triggers.
* **Bericht zichtbaarheid** -Orchestration triggerberichten worden uit wachtrij geplaatst en onzichtbaar voor een configureerbare duur behouden. De zichtbaarheid van deze berichten wordt automatisch vernieuwd, zolang de functie-app uitgevoerd en goed wordt.
* **Retourwaarden** -waarden worden geserialiseerd naar JSON en opgeslagen in de geschiedenistabel orchestration in Azure Table storage worden geretourneerd. Deze waarden geretourneerd, kunnen worden opgevraagd met de orchestration-client binding, die verderop worden beschreven.

> [!WARNING]
> Orchestrator-functies moeten nooit gebruik geen invoer of uitvoer bindingen dan de orchestration binding activeren. In dat geval heeft problemen met de extensie duurzame taak veroorzaken omdat deze bindingen kunnen zich niet aan de één-threading en i/o-regels.

### <a name="trigger-usage"></a>Gebruik van de trigger

De orchestration-trigger binding ondersteunt zowel invoer en uitvoer. Hier volgen enkele dingen die u moet weten over invoer en uitvoer van de verwerking van:

* **invoer** -Orchestration-functies ondersteunen alleen [DurableOrchestrationContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html) als een parametertype. Deserialisatie van invoer rechtstreeks in de functiehandtekening wordt niet ondersteund. Code moet gebruiken de [GetInput\<T >](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_GetInput__1) methode voor het ophalen van orchestrator-functie invoer. Deze invoer moet JSON-serialiseerbaar typen.
* **levert** -Orchestration triggers ondersteunen zowel uitvoerwaarden als invoer. De retourwaarde van de functie wordt gebruikt voor het toewijzen van de uitvoerwaarde en moet een JSON-serialiseerbaar. Als een functie retourneert `Task` of `void`, een `null` waarde wordt opgeslagen als de uitvoer.

### <a name="trigger-sample"></a>Voorbeeld van de trigger

Hier volgt een voorbeeld van wat de meest eenvoudige 'Hallo wereld' orchestrator-functie als volgt uitzien:

#### <a name="c"></a>C#

```csharp
[FunctionName("HelloWorld")]
public static string Run([OrchestrationTrigger] DurableOrchestrationContext context)
{
    string name = context.GetInput<string>();
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a>JavaScript (alleen functies v2)

```javascript
const df = require("durable-functions");

module.exports = df(function*(context) {
    const name = context.df.getInput();
    return `Hello ${name}!`;
});
```

> [!NOTE]
> JavaScript orchestrators moeten gebruiken `return`. De `durable-functions` bibliotheek zorgt voor aanroepen de `context.done` methode.

De meeste orchestrator-functies aanroepen activiteit functies, dus hier is een voorbeeld van een 'Hallo wereld' die laat zien hoe u een functie van de activiteit:

#### <a name="c"></a>C#

```csharp
[FunctionName("HelloWorld")]
public static async Task<string> Run(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    string name = context.GetInput<string>();
    string result = await context.CallActivityAsync<string>("SayHello", name);
    return result;
}
```

#### <a name="javascript-functions-v2-only"></a>JavaScript (alleen functies v2)

```javascript
const df = require("durable-functions");

module.exports = df(function*(context) {
    const name = context.df.getInput();
    const result = yield context.df.callActivityAsync("SayHello", name);
    return result;
});
```

## <a name="activity-triggers"></a>Activiteit-triggers

De trigger activiteit kunt u schrijven van functies die door de orchestrator-functies worden aangeroepen.

Als u Visual Studio, de activiteit trigger is geconfigureerd met behulp van de [ActvityTriggerAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.ActivityTriggerAttribute.html) .NET-kenmerk. 

Als u de Azure-portal voor ontwikkeling, de activiteit trigger wordt gedefinieerd door de volgende JSON-object in de `bindings` matrix van *function.json*:

```json
{
    "name": "<Name of input parameter in function signature>",
    "activity": "<Optional - name of the activity>",
    "type": "activityTrigger",
    "direction": "in"
}
```

* `activity` is de naam van de activiteit. Dit is de waarde die het orchestrator-functies gebruiken om aan deze activiteit functie aanroepen. Deze eigenschap is optioneel. Als niet wordt opgegeven, wordt de naam van de functie gebruikt.

Deze binding trigger opgevraagd intern een wachtrij in het standaardopslagaccount voor de functie-app. Deze wachtrij is een interne implementatie details van de extensie, dat is waarom deze niet expliciet is geconfigureerd in de bindingeigenschappen.

### <a name="trigger-behavior"></a>Gedrag van de trigger

Hieronder vindt u informatie over de trigger activiteit:

* **Threading** -activiteit triggers geen in tegenstelling tot de orchestration-trigger beperkingen rond threading of i/o. Ze kunnen worden behandeld als reguliere functies.
* **Afhandeling van poising berichten** -er is geen ondersteuning voor verontreinigd bericht in de activiteit triggers.
* **Bericht zichtbaarheid** -activiteit triggerberichten worden uit wachtrij geplaatst en onzichtbaar voor een configureerbare duur behouden. De zichtbaarheid van deze berichten wordt automatisch vernieuwd, zolang de functie-app uitgevoerd en goed wordt.
* **Retourwaarden** -waarden worden geserialiseerd naar JSON en opgeslagen in de geschiedenistabel orchestration in Azure Table storage worden geretourneerd.

> [!WARNING]
> De opslag back-end voor functies van de activiteit is de details van een implementatie en gebruikerscode mag geen interactie hebben met deze entiteiten opslag rechtstreeks.

### <a name="trigger-usage"></a>Gebruik van de trigger

De activiteit trigger binding ondersteunt zowel invoer en uitvoer, net als de orchestration-trigger. Hier volgen enkele dingen die u moet weten over invoer en uitvoer van de verwerking van:

* **invoer** -activiteit functies systeemeigen gebruiken [DurableActivityContext](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html) als een parametertype. Een functie van de activiteit kan ook worden gedeclareerd met de parametertype dat JSON-serialiseerbaar. Als u werkt met `DurableActivityContext`, u kunt aanroepen [GetInput\<T >](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableActivityContext.html#Microsoft_Azure_WebJobs_DurableActivityContext_GetInput__1) invoer voor het ophalen en deserialiseren van de functie van de activiteit.
* **levert** -activiteit werkt ondersteuning uitvoerwaarden als invoer. De retourwaarde van de functie wordt gebruikt voor het toewijzen van de uitvoerwaarde en moet een JSON-serialiseerbaar. Als een functie retourneert `Task` of `void`, een `null` waarde wordt opgeslagen als de uitvoer.
* **metagegevens** -functies van de activiteit kunnen worden verbonden met een `string instanceId` -parameter voor de exemplaar-ID van de bovenliggende orchestration niet ophalen.

### <a name="trigger-sample"></a>Voorbeeld van de trigger

Hier volgt een voorbeeld van wat een eenvoudige 'Hallo wereld' activiteit functie als volgt uitzien:

#### <a name="c"></a>C#

```csharp
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] DurableActivityContext helloContext)
{
    string name = helloContext.GetInput<string>();
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a>JavaScript (alleen functies v2)

```javascript
module.exports = function(context) {
    context.done(null, `Hello ${context.bindings.name}!`);
};
```

Het parametertype voor de `ActivityTriggerAttribute` -binding is `DurableActivityContext`. Echter, activiteit triggers ook ondersteuning voor het binden van rechtstreeks aan JSON serializeable typen (met inbegrip van primitieve typen), zodat dezelfde functie kan worden vereenvoudigd als volgt:

#### <a name="c"></a>C#

```csharp
[FunctionName("SayHello")]
public static string SayHello([ActivityTrigger] string name)
{
    return $"Hello {name}!";
}
```

#### <a name="javascript-functions-v2-only"></a>JavaScript (alleen functies v2)

```javascript
module.exports = function(context, name) {
    context.done(null, `Hello ${name}!`);
};
```

### <a name="passing-multiple-parameters"></a>Meerdere parameters doorgeven 

Het is niet mogelijk meerdere parameters rechtstreeks doorgeven aan een functie van de activiteit. Om door te geven in een matrix met objecten of voor het gebruik van de aanbeveling is in dit geval [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) objecten.

Het volgende voorbeeld met behulp van nieuwe functies van [ValueTuples](https://docs.microsoft.com/dotnet/csharp/tuples) toegevoegd met [C# 7](https://docs.microsoft.com/dotnet/csharp/whats-new/csharp-7#tuples):

```csharp
[FunctionName("GetCourseRecommendations")]
public static async Task<dynamic> RunOrchestrator(
    [OrchestrationTrigger] DurableOrchestrationContext context)
{
    string major = "ComputerScience";
    int universityYear = context.GetInput<int>();

    dynamic courseRecommendations = await context.CallActivityAsync<dynamic>("CourseRecommendations", (major, universityYear));
    return courseRecommendations;
}

[FunctionName("CourseRecommendations")]
public static async Task<dynamic> Mapper([ActivityTrigger] DurableActivityContext inputs)
{
    // parse input for student's major and year in university 
    (string Major, int UniversityYear) studentInfo = inputs.GetInput<(string, int)>();

    // retrieve and return course recommendations by major and university year
    return new {
        major = studentInfo.Major,
        universityYear = studentInfo.UniversityYear,
        recommendedCourses = new []
        {
            "Introduction to .NET Programming",
            "Introduction to Linux",
            "Becoming an Entrepreneur"
        }
    };
}
```

## <a name="orchestration-client"></a>Orchestration-client

De orchestration-client binding kunt u het schrijven van functies die communiceren met orchestrator-functies. U kunt bijvoorbeeld fungeren voor orchestration-exemplaren in de volgende manieren:
* Ze worden gestart.
* Query uitvoeren op hun status.
* Ze worden beëindigd.
* Gebeurtenissen verzenden naar deze terwijl ze uitvoert.

Als u Visual Studio gebruikt, kunt u binden aan de orchestration-client met behulp van de [OrchestrationClientAttribute](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.OrchestrationClientAttribute.html) .NET-kenmerk.

Als u scripttalen (bijvoorbeeld *.csx* bestanden) voor ontwikkeling, de orchestration-trigger wordt gedefinieerd door de volgende JSON-object in de `bindings` matrix van *function.json*:

```json
{
    "name": "<Name of input parameter in function signature>",
    "taskHub": "<Optional - name of the task hub>",
    "connectionName": "<Optional - name of the connection string app setting>",
    "type": "orchestrationClient",
    "direction": "out"
}
```

* `taskHub` : Wordt gebruikt in scenario's waarbij meerdere functie apps delen hetzelfde opslagaccount maar moeten worden van elkaar geïsoleerd. Als niet wordt opgegeven, de standaardwaarde van `host.json` wordt gebruikt. Deze waarde moet overeenkomen met de waarde die wordt gebruikt door de doel-orchestrator-functies.
* `connectionName` -De naam van een app-instelling met een verbindingsreeks voor opslag-account. Het opslagaccount dat wordt vertegenwoordigd door deze verbindingsreeks moet hetzelfde account dat door de doel-orchestrator-functies gebruikt. Als niet wordt opgegeven, wordt de verbindingsreeks standaard storage-account voor de functie-app gebruikt.

> [!NOTE]
> In de meeste gevallen wordt aangeraden dat u deze eigenschappen weglaten en zijn afhankelijk van het standaardgedrag.

### <a name="client-usage"></a>Gebruik door clients

In C# functies, bindt u doorgaans aan `DurableOrchestrationClient`, u hebt volledige toegang aan alle client-API's die worden ondersteund door duurzame functies. API's op de clientobject zijn onder andere:

* [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_)
* [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_)
* [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_)
* [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_)

U kunt ook koppelen aan `IAsyncCollector<T>` waar `T` is [StartOrchestrationArgs](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.StartOrchestrationArgs.html) of `JObject`.

Zie de [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html) API-documentatie voor meer informatie over deze bewerkingen.

### <a name="client-sample-visual-studio-development"></a>Clientvoorbeeld (Visual Studio-ontwikkeling)

Hier volgt een voorbeeld van de wachtrij geactiveerd functie die een orchestration "Hallo wereld" begint.

```csharp
[FunctionName("QueueStart")]
public static Task Run(
    [QueueTrigger("durable-function-trigger")] string input,
    [OrchestrationClient] DurableOrchestrationClient starter)
{
    // Orchestration input comes from the queue message content.
    return starter.StartNewAsync("HelloWorld", input);
}
```

### <a name="client-sample-not-visual-studio"></a>Clientvoorbeeld (geen Visual Studio)

Als u Visual Studio niet voor ontwikkeling gebruikt, kunt u de volgende *function.json* bestand. In dit voorbeeld ziet u hoe een wachtrij geactiveerd functie die gebruikmaakt van de binding duurzame orchestration-client configureren:

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "queueTrigger",
      "queueName": "durable-function-trigger",
      "direction": "in"
    },
    {
      "name": "starter",
      "type": "orchestrationClient",
      "direction": "out"
    }
  ],
  "disabled": false
} 
```

Hieronder vindt u taalspecifieke voorbeelden die nieuwe exemplaren van orchestrator-functie te starten.

#### <a name="c-sample"></a>C#-voorbeeld

Het volgende voorbeeld laat zien hoe de duurzame orchestration client binden aan een nieuw exemplaar van de functie starten vanuit een functie C#-script gebruiken:

```csharp
#r "Microsoft.Azure.WebJobs.Extensions.DurableTask"

public static Task<string> Run(string input, DurableOrchestrationClient starter)
{
    return starter.StartNewAsync("HelloWorld", input);
}
```

#### <a name="javascript-sample"></a>JavaScript-voorbeeld

Het volgende voorbeeld laat zien hoe de duurzame orchestration client binden aan een nieuw exemplaar van de functie starten vanuit een JavaScript-functie gebruiken:

```js
module.exports = function (context, input) {
    var id = generateSomeUniqueId();
    context.bindings.starter = [{
        FunctionName: "HelloWorld",
        Input: input,
        InstanceId: id
    }];

    context.done(null, id);
};
```

Meer informatie over het starten van de exemplaren vindt u in [management-instantie](durable-functions-instance-management.md).

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Meer informatie over het plaatsen van controlepunten en replay-gedrag](durable-functions-checkpointing-and-replay.md)


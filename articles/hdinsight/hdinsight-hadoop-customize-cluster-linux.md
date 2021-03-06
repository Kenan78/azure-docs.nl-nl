---
title: Met behulp van scriptacties - Azure HDInsight-clusters aanpassen | Microsoft Docs
description: Aangepaste onderdelen toevoegen op Linux gebaseerde HDInsight-clusters met behulp van scriptacties. Scriptacties zijn Bash-scripts die kunnen worden gebruikt voor het aanpassen van de configuratie van het cluster of Voeg extra services en hulpprogramma's zoals Hue, Solr of R.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: cgronlun
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: larryfr
ms.openlocfilehash: 856a94b0cf64a20fbe9267b76422c47d88d21f43
ms.sourcegitcommit: ca05dd10784c0651da12c4d58fb9ad40fdcd9b10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/03/2018
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-actions"></a>Linux gebaseerde HDInsight-clusters met behulp van scriptacties aanpassen

HDInsight biedt een configuratiemethode aangeroepen **acties script** die aangepaste scripts voor het aanpassen van het cluster wordt aangeroepen. Deze scripts worden gebruikt voor het installeren van extra onderdelen en configuratie-instellingen wijzigen. Scriptacties kunnen worden gebruikt tijdens of na het maken van het cluster.

> [!IMPORTANT]
> De mogelijkheid om met scriptacties op een cluster al actief is alleen beschikbaar voor Linux gebaseerde HDInsight-clusters.
>
> Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

Scriptacties kunnen ook worden gepubliceerd naar Azure Marketplace als een HDInsight-toepassing. Zie voor meer informatie over HDInsight-toepassingen [publiceren HDInsight-toepassingen in Azure Marketplace](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Machtigingen

Als u van een domein HDInsight-cluster gebruikmaakt, zijn er twee Ambari-machtigingen die vereist zijn bij het gebruik van scriptacties met het cluster:

* **AMBARI. Voer\_aangepaste\_opdracht**: de Ambari-beheerdersrol beschikt over deze machtiging standaard.
* **HET CLUSTER. Voer\_aangepaste\_opdracht**: zowel de HDInsight-Clusterbeheer en Ambari beheerder hebben deze machtiging standaard.

Zie voor meer informatie over het werken met machtigingen met HDInsight domein [domein HDInsight-clusters beheren](./domain-joined/apache-domain-joined-manage.md).

## <a name="access-control"></a>Toegangsbeheer

Als u niet de beheerder of de eigenaar van uw Azure-abonnement, uw account moet er ten minste **Inzender** toegang tot de resourcegroep die het HDInsight-cluster bevat.

Bovendien, als u een HDInsight-cluster iemand met ten minste maakt **Inzender** toegang tot het Azure-abonnement moet hebben eerder geregistreerd de provider voor HDInsight. Registratie van een provider vindt plaats wanneer een gebruiker met toegang tot het abonnement op het niveau van Inzender, voor het eerst een resource maakt onder het abonnement. Dit kan ook worden bereikt zonder dat er een resource wordt gemaakt door [een provider te registreren met behulp van REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Zie de volgende documenten voor meer informatie over werken met toegangsbeheer:

* [Aan de slag met toegangsbeheer in Azure Portal](../role-based-access-control/overview.md)
* [Roltoewijzingen gebruiken voor het beheer van de toegang tot de resources van uw Azure-abonnement](../role-based-access-control/role-assignments-portal.md)

## <a name="understanding-script-actions"></a>Understanding scriptacties

Een scriptactie is Bash-script dat wordt uitgevoerd op de knooppunten in een HDInsight-cluster. Hieronder vindt u kenmerken en functies van scriptacties.

* Moet worden opgeslagen op een URI die toegankelijk is vanaf het HDInsight-cluster. Hier volgen de mogelijke opslaglocaties:

    * Een **Azure Data Lake Store** account die toegankelijk is voor het HDInsight-cluster. Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Wanneer u een script dat is opgeslagen in Data Lake Store, de indeling van de URI is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > De service-principal die hdinsight gebruikt voor toegang tot Data Lake Store moet leestoegang hebben tot het script.

    * Een blob in een **Azure Storage-account** die beide het primaire of extra storage-account voor het HDInsight-cluster. HDInsight is toegang verleend tot beide typen opslagaccounts tijdens het maken van het cluster.

    * Bestand met een openbare sharing-service zoals Azure Blob, GitHub, OneDrive, Dropbox, enz.

        Bijvoorbeeld URI's, Zie de [voorbeeldscripts script actie](#example-script-action-scripts) sectie.

        > [!WARNING]
        > HDInsight biedt alleen ondersteuning voor __algemeen__ Azure Storage-accounts. Het momenteel geen ondersteunt de __Blob storage__ accounttype.

* Kan worden beperkt tot **uitvoeren op alleen bepaalde knooppunttypen**voor voorbeeld hoofdknooppunten of worker-knooppunten.

* Kan **persistent** of **ad hoc**.

    **Persistent** scripts worden gebruikt voor het aanpassen van de nieuwe worker-knooppunten toegevoegd aan het cluster via het schalen van bewerkingen. Een persistent script mogelijk ook wijzigingen toepassen op een ander knooppunttype, zoals een hoofdknooppunt wanneer schalen bewerkingen plaatsvinden.

  > [!IMPORTANT]
  > Persistente scriptacties moeten een unieke naam hebben.

    **Ad hoc** scripts blijven niet bestaan. Ze worden niet toegepast op de worker-knooppunten aan het cluster worden toegevoegd nadat het script is uitgevoerd. U kunt vervolgens promoveren van een ad-hoc script een persistent script of degraderen van een persistent script naar een ad-hoc-script.

  > [!IMPORTANT]
  > Scriptacties gebruikt tijdens het maken van het cluster worden automatisch doorgevoerd.
  >
  > Scripts die mislukken niet persistent hebt gemaakt, zelfs als u specifiek aangeeft dat ze moeten worden.

* Kan accepteren **parameters** die door het script worden gebruikt tijdens de uitvoering.

* Voer met **root bevoegdheden** op de clusterknooppunten.

* Kan worden gebruikt via de **Azure-portal**, **Azure PowerShell**, **Azure CLI v1.0**, of **HDInsight .NET SDK**

Het cluster houdt een geschiedenis van alle scripts die hebben is uitgevoerd. De geschiedenis is handig als u moet de ID van een script voor promotie of degradatie bewerkingen vinden.

> [!IMPORTANT]
> Er is geen automatische manier om de wijzigingen die door een scriptactie ongedaan te maken. Handmatig de wijzigingen ongedaan maken of een script dat wordt teruggedraaid ze bieden.

### <a name="script-action-in-the-cluster-creation-process"></a>Scriptactie in het proces voor het cluster maken

Scriptacties gebruikt tijdens het maken van het cluster zijn enigszins afwijken van het script acties worden uitgevoerd op een bestaand cluster:

* Het script is **automatisch persistente**.

* Een **fout** in het script kan ertoe leiden dat het maakproces cluster mislukken.

Het volgende diagram illustreert wanneer het script wordt uitgevoerd tijdens het maken:

![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]

Het script wordt uitgevoerd terwijl HDInsight wordt geconfigureerd. Het script wordt parallel uitgevoerd op de opgegeven knooppunten in het cluster en uitgevoerd met basis-bevoegdheden op de knooppunten.

> [!NOTE]
> U kunt bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services uitvoeren. Als u services stoppen, moet u ervoor zorgen dat de Ambari-service en andere Hadoop-gerelateerde services die worden uitgevoerd voordat het script is voltooid. Deze services zijn vereist om te bepalen is de status en de status van het cluster terwijl deze wordt gemaakt.


U kunt meerdere scriptacties tegelijk gebruiken tijdens het maken van het cluster. Deze scripts worden aangeroepen in de volgorde waarin ze zijn opgegeven.

> [!IMPORTANT]
> Scriptacties moeten binnen 60 minuten of time-out voltooien. Het script wordt uitgevoerd tijdens de clusterinrichting, samen met andere processen installatie en configuratie. Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte kan ertoe leiden dat het script duurt langer dan in uw ontwikkelomgeving te voltooien.
>
> Als u wilt de tijd minimaliseren nodig die is om te voorkomen dat taken zoals het downloaden en toepassingen van bron compileren uit te voeren van het script. Toepassingen vooraf gecompileerd en het binaire bestand opslaan in Azure Storage.


### <a name="script-action-on-a-running-cluster"></a>Scriptactie op een actief cluster

Een fout in een script uitgevoerd op een al actief cluster automatisch niet leidt tot het cluster te wijzigen in een mislukte status. Zodra een script is voltooid, moet het cluster naar een status 'actief' retourneren.

> [!IMPORTANT]
> Zelfs als het cluster heeft een status 'actief', bevatten het mislukte script verbroken dingen. Een script kan bijvoorbeeld bestanden die nodig zijn door het cluster te verwijderen.
>
> Scripts acties worden uitgevoerd met machtigingen van de hoofdmap. Zorg ervoor dat u wat een script doet begrijpt voordat u deze toepast op uw cluster.

Bij het toepassen van een script naar een cluster wordt de clusterstatus van verandert **met** naar **geaccepteerde**, vervolgens **HDInsight configuratie**, en ten slotte terug naar  **Met** voor geslaagde scripts. De scriptstatus wordt geregistreerd in de geschiedenis van de scriptactie en u kunt deze informatie gebruiken om te bepalen of het script is geslaagd of mislukt. Bijvoorbeeld, de `Get-AzureRmHDInsightScriptActionHistory` PowerShell-cmdlet kan worden gebruikt om de status van een script. Gegevens worden geretourneerd vergelijkbaar met de volgende tekst:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!IMPORTANT]
> Als u kunt het wachtwoord van de cluster-gebruiker (admin) zijn gewijzigd nadat het cluster is gemaakt, mislukken script acties uitgevoerd op dit cluster. Als u een persistente scriptacties die doel worker-knooppunten hebt, mislukken deze scripts wanneer u de schaal van het cluster.

## <a name="example-script-action-scripts"></a>Voorbeeldscripts script actie

Script actie scripts kunnen worden gebruikt door de volgende hulpprogramma's:

* Azure Portal
* Azure PowerShell
* Azure CLI v1.0
* HDInsight .NET-SDK

HDInsight biedt scripts voor het installeren van de volgende onderdelen op HDInsight-clusters:

| Naam | Script |
| --- | --- |
| **Een Azure Storage-account toevoegen** |https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Zie [extra opslag toevoegen aan een HDInsight-cluster](hdinsight-hadoop-add-storage.md). |
| **Hue installeren** |https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Zie [installeert en gebruikt Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md). |
| **Functie installeren** |https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Zie [installeert en gebruikt de functie op HDInsight-clusters](hdinsight-hadoop-install-presto.md). |
| **Solr installeren** |https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md). |
| **Giraph installeren** |https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md). |
| **Vooraf laden Hive-bibliotheken** |https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md). |
| **Mono installeren of bijwerken** | https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash. Zie [installeren of update Mono op HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Gebruik de scriptactie van een tijdens het maken van het cluster

Deze sectie vindt u voorbeelden van de verschillende manieren waarop die u scriptacties gebruiken kunt bij het maken van een HDInsight-cluster.

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a>Gebruik de scriptactie van een tijdens het maken van de Azure-portal

1. Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Stoppen wanneer u bereikt de __Cluster samenvatting__ sectie.

2. Van de __Cluster samenvatting__ sectie, selecteer de __bewerken__ koppelen voor __geavanceerde instellingen__.

    ![Koppeling van de geavanceerde instellingen](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Van de __geavanceerde instellingen__ sectie __acties Script__. Van de __acties Script__ sectie __+ nieuw verzenden__

    ![Een nieuwe scriptactie verzenden](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Gebruik de __selecteert u een script__ item naar een vooraf gemaakte script te selecteren. Selecteer voor het gebruik van een aangepast script __aangepaste__ en geef vervolgens de __naam__ en __Bash script URI__ voor uw script.

    ![Een script in de vorm Selecteer script toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    De volgende tabel beschrijft de elementen in het formulier:

    | Eigenschap | Waarde |
    | --- | --- |
    | Een script selecteren | Selecteer voor het gebruik van uw eigen script __aangepaste__. Anders selecteert u een van de opgegeven scripts. |
    | Naam |Geef een naam voor de scriptactie. |
    | Bash-script-URI |Geef de URI van het script. |
    | Worker-HEAD/Zookeeper |Geef de knooppunten (**Head**, **Worker**, of **ZooKeeper**) op waarmee het script wordt uitgevoerd. |
    | Parameters |Geef de parameters op, indien vereist door het script. |

    Gebruik de __deze scriptactie__ vermelding om ervoor te zorgen dat het script wordt toegepast tijdens het schalen van bewerkingen.

5. Selecteer __maken__ om op te slaan van het script. Vervolgens kunt u __+ indienen nieuwe__ toevoegen van een ander script.

    ![Meerdere scriptacties](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Wanneer u klaar bent met het toe te voegen scripts gebruiken de __Selecteer__ knop, en vervolgens de __volgende__ terug te keren naar de __Cluster samenvatting__ sectie.

3. Voor het maken van het cluster selecteert __maken__ van de __Cluster samenvatting__ selectie.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Gebruik de scriptactie van een van Azure Resource Manager-sjablonen

Scriptacties kunnen worden gebruikt met Azure Resource Manager-sjablonen. Zie voor een voorbeeld [ https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/ ](https://azure.microsoft.com/resources/templates/hdinsight-linux-run-script-action/).

In dit voorbeeld is de scriptactie toegevoegd met de volgende code:

```json
"scriptActions": [
    {
        "name": "setenvironmentvariable",
        "uri": "[parameters('scriptActionUri')]",
        "parameters": "headnode"
    }
]
```

Zie de volgende documenten voor meer informatie over het implementeren van een sjabloon:

* [Resources met sjablonen en Azure PowerShell implementeren](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)

* [Resources met sjablonen en Azure CLI implementeren](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Een scriptactie tijdens het maken van Azure PowerShell gebruiken

In deze sectie gebruikt u de [toevoegen AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet aan te roepen scripts voor het aanpassen van een cluster. Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell. Zie voor meer informatie over het configureren van een werkstation als HDInsight PowerShell-cmdlets wilt uitvoeren, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

Het volgende script laat zien hoe een scriptactie toepassen bij het maken van een cluster met behulp van PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Het kan enkele minuten duren voordat het cluster is gemaakt.

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a>Gebruik de scriptactie van een tijdens het maken van de HDInsight-SDK voor .NET

De HDInsight-SDK voor .NET biedt clientbibliotheken waarmee eenvoudiger te laten werken met HDInsight vanuit een .NET-toepassing. Zie voor een voorbeeld van code [maken Linux gebaseerde clusters in HDInsight met behulp van de .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-to-a-running-cluster"></a>De scriptactie toepassen op een actief cluster

Informatie over het toepassen van scriptacties met een actief cluster in deze sectie.

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a>Scriptactie toepassen op een cluster uitgevoerd vanuit de Azure-portal

1. Van de [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.

2. Selecteer in het overzicht van HDInsight-cluster, de **scriptacties** tegel.

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** in het gedeelte instellingen.

3. Selecteer vanaf de bovenkant van het script acties gedeelte **indienen nieuwe**.

    ![Een script toevoegen aan een actieve cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Gebruik de __selecteert u een script__ item naar een vooraf gemaakte script te selecteren. Selecteer voor het gebruik van een aangepast script __aangepaste__ en geef vervolgens de __naam__ en __Bash script URI__ voor uw script.

    ![Een script in de vorm Selecteer script toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    De volgende tabel beschrijft de elementen in het formulier:

    | Eigenschap | Waarde |
    | --- | --- |
    | Een script selecteren | Selecteer voor het gebruik van uw eigen script __aangepaste__. Anders selecteert u een geleverde script. |
    | Naam |Geef een naam voor de scriptactie. |
    | Bash-script-URI |Geef de URI van het script. |
    | Worker-HEAD/Zookeeper |Geef de knooppunten (**Head**, **Worker**, of **ZooKeeper**) op waarmee het script wordt uitgevoerd. |
    | Parameters |Geef de parameters op, indien vereist door het script. |

    Gebruik de __deze scriptactie__ vermelding om ervoor te zorgen dat het script wordt toegepast tijdens het schalen van bewerkingen.

5. Gebruik tot slot de **maken** knop om toe te passen van het script voor het cluster.

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a>Scriptactie toepassen op een actief cluster van Azure PowerShell

Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell. Zie voor meer informatie over het configureren van een werkstation als HDInsight PowerShell-cmdlets wilt uitvoeren, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).

Het volgende voorbeeld laat zien hoe een scriptactie toepassen op een actief cluster:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Nadat de bewerking is voltooid, wordt de informatie is vergelijkbaar met de volgende tekst:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a>Scriptactie toepassen op een actief cluster van de Azure CLI

Zorg ervoor dat u hebt geïnstalleerd en de Azure CLI geconfigureerd voordat u verdergaat. Zie voor meer informatie [installeren van de Azure CLI 1.0](../cli-install-nodejs.md).

> [!IMPORTANT]
> HDInsight vereist Azure CLI 1.0. Azure CLI 2.0 bieden momenteel geen opdrachten werken met HDInsight.

1. Als u wilt overschakelen naar de modus Azure Resource Manager, gebruik de volgende opdracht bij de opdrachtprompt:

    ```bash
    azure config mode arm
    ```

2. Gebruik de volgende om uw Azure-abonnement te verifiëren.

    ```bash
    azure login
    ```

3. Gebruik de volgende opdracht toe te passen van een scriptactie naar een actief cluster

    ```bash
    azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>
    ```

    Als u de parameters voor deze opdracht weglaat, wordt u gevraagd deze. Als het script dat u met opgeeft `-u` accepteert parameters, kunt u deze opgeven met behulp van de `-p` parameter.

    Geldige knooppunt-typen zijn `headnode`, `workernode`, en `zookeeper`. Als het script moet worden toegepast op typen met meerdere knooppunten, geeft u de typen gescheiden door een ';'. Bijvoorbeeld `-n headnode;workernode`.

    Om te blijven behouden het script, voeg de `--persistOnSuccess`. U kunt ook het script later behouden met behulp van `azure hdinsight script-action persisted set`.

    Zodra de taak is voltooid, wordt de uitvoer is vergelijkbaar met de volgende tekst:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a>De scriptactie toepassen op een actief cluster met behulp van REST-API

Zie [scriptacties uitvoeren op een actief cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a>Scriptactie toepassen op een actief cluster van de HDInsight-SDK voor .NET

Zie voor een voorbeeld van het gebruik van de .NET SDK scripts toepassen op een cluster [ https://github.com/Azure-Samples/hdinsight-dotnet-script-action ](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Geschiedenis weergeven en degraderen scriptacties promoveren

### <a name="using-the-azure-portal"></a>Azure Portal gebruiken

1. Van de [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.

2. Selecteer in het overzicht van HDInsight-cluster, de **scriptacties** tegel.

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** in het gedeelte instellingen.

4. Een geschiedenis van scripts voor dit cluster wordt weergegeven op de sectie script acties. Deze informatie omvat een lijst met persistente scripts. In de onderstaande schermafbeelding ziet u dat de Solr script is uitgevoerd op dit cluster. De permanente scripts niet wordt weergegeven in de schermafbeelding.

    ![De sectie Acties script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. De sectie met eigenschappen voor dit script te selecteren van een script in de geschiedenis worden weergegeven. U kunt het script opnieuw uitvoeren of promoveer deze vanaf de bovenkant van het scherm.

    ![Eigenschappen van de script-acties](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. U kunt ook de **...**  rechts van items in de sectie script acties acties uit te voeren.

    ![Acties... script gebruik](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Azure PowerShell gebruiken

| Gebruik de volgende... | Aan... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Informatie over persistente scriptacties ophalen |
| Get-AzureRmHDInsightScriptActionHistory |Een geschiedenis van scriptacties toegepast op het cluster of de details voor een specifiek script ophalen |
| Set-AzureRmHDInsightPersistedScriptAction |Bijdraagt aan een ad-hoc scriptactie naar een persistent script-actie |
| Remove-AzureRmHDInsightPersistedScriptAction |Selecteert, wordt een actie persistent script aan een ad-hoc actie |

> [!IMPORTANT]
> Met behulp van `Remove-AzureRmHDInsightPersistedScriptAction` die de acties die worden uitgevoerd door een script wordt niet ongedaan gemaakt. Deze cmdlet worden alleen de persistente vlag verwijderd.

Het volgende voorbeeldscript wordt gedemonstreerd met behulp van de cmdlets verhogen, en vervolgens degraderen van een script.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-the-azure-cli"></a>Azure CLI gebruiken

| Gebruik de volgende... | Aan... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Een lijst met persistente scriptacties ophalen |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Ophalen van gegevens op een specifieke persistente scriptacties actie |
| `azure hdinsight script-action history list <clustername>` |Ophalen van een geschiedenis van scriptacties toegepast op het cluster |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Ophalen van informatie over een specifiek script-actie |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Bijdraagt aan een ad-hoc scriptactie naar een persistent script-actie |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Selecteert, wordt een actie persistent script aan een ad-hoc actie |

> [!IMPORTANT]
> Met behulp van `azure hdinsight script-action persisted delete` die de acties die worden uitgevoerd door een script wordt niet ongedaan gemaakt. Deze cmdlet worden alleen de persistente vlag verwijderd.

### <a name="using-the-hdinsight-net-sdk"></a>Met behulp van de HDInsight-SDK voor .NET

Voor een voorbeeld van het gebruik van de .NET SDK script geschiedenis ophalen uit een cluster promoten of degraderen van scripts, Zie [ https://github.com/Azure-Samples/hdinsight-dotnet-script-action ](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> In dit voorbeeld demonstreert ook hoe u een HDInsight-toepassing met de .NET SDK te installeren.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Ondersteuning voor open-source software gebruikt op HDInsight-clusters

De Microsoft Azure HDInsight-service gebruikt een ecosysteem van open-source technologieën gevormd rond Hadoop. Microsoft Azure biedt een algemeen niveau van ondersteuning voor de open source-technologieën. Zie voor meer informatie de **ondersteuning bereik** sectie van de [ondersteuning Veelgestelde vragen over Azure-website](https://azure.microsoft.com/support/faq/). De HDInsight-service biedt een extra verificatieniveau van ondersteuning voor ingebouwde-onderdelen.

Er zijn twee soorten open source-onderdelen die beschikbaar in de HDInsight-service zijn:

* **Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van het cluster. Bijvoorbeeld: YARN ResourceManager, de Hive-query language (HiveQL) en de bibliotheek Mahout behoren tot deze categorie. Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in de Hadoop-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).
* **Aangepaste onderdelen** -u, als een gebruiker van het cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in de community of door u gemaakte.

> [!WARNING]
> Onderdelen van het HDInsight-cluster worden volledig ondersteund. Microsoft Support kunt opsporen en oplossen van problemen met betrekking tot deze onderdelen.
>
> Aangepaste onderdelen ontvangt binnen commercieel redelijke ondersteuning u helpen het probleem verder op te lossen. Microsoft ondersteuning mogelijk het probleem op te lossen of ze gevraagd om te benaderen beschikbare kanalen voor de open-source technologieën waar grondige kennis van deze technologie kan worden gevonden. Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [ http://stackoverflow.com ](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [ http://apache.org ](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).

De HDInsight-service biedt verschillende manieren om te gebruiken van aangepaste onderdelen. Hetzelfde niveau van de ondersteuning van toepassing is, ongeacht hoe een onderdeel gebruikt of is geïnstalleerd op het cluster. De volgende lijst bevat de meest voorkomende manieren dat aangepaste onderdelen op HDInsight-clusters kunnen worden gebruikt:

1. Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden naar het cluster.

2. Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die zijn geïnstalleerd op de clusterknooppunten opgeven.

3. Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op de HDInsight-clusters bieden. Deze voorbeelden worden geleverd zonder ondersteuning.

## <a name="troubleshooting"></a>Problemen oplossen

Ambari-webgebruikersinterface kunt u informatie die zijn vastgelegd door scriptacties weergeven. Als het script is mislukt tijdens maken van het cluster, zijn de logboeken ook beschikbaar in het standaardopslagaccount die is gekoppeld aan het cluster. Deze sectie bevat informatie over het ophalen van de logboeken met behulp van deze beide opties.

### <a name="using-the-ambari-web-ui"></a>Met behulp van de Ambari-webgebruikersinterface

1. Ga in de browser naar https://CLUSTERNAME.azurehdinsight.net. CLUSTERNAAM vervangen door de naam van uw HDInsight-cluster.

    Wanneer u wordt gevraagd, typt u de accountnaam van de beheerder (admin) en het wachtwoord voor het cluster. U moet de beheerdersreferenties in een webformulier invoeren.

2. Selecteer in de balk aan de bovenkant van de pagina de **ops** vermelding. Een lijst met huidige en vorige bewerkingen die worden uitgevoerd op het cluster door Ambari wordt weergegeven.

    ![Ambari web UI-balk met ops geselecteerd](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. De items waarvoor vindt **uitvoeren\_customscriptaction** in de **Operations** kolom. Deze vermeldingen worden gemaakt wanneer de script-bewerkingen worden uitgevoerd.

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    Als u wilt weergeven in de uitvoer STDOUT en STDERR, selecteer de vermelding run\customscriptaction en inzoomen via de koppelingen. Deze uitvoer wordt gegenereerd wanneer het script wordt uitgevoerd, en mogelijk bevatten nuttige informatie.

### <a name="access-logs-from-the-default-storage-account"></a>Toegang tot logboeken van het standaardopslagaccount

Als het maken van het cluster is mislukt vanwege een fout in het script, worden de logboeken in het cluster opslagaccount bewaard.

* De logboeken van de opslag zijn beschikbaar op `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    De logboeken zijn in deze map afzonderlijk ingedeeld voor headnode, workernode en zookeeper-knooppunten. Een aantal voorbeelden:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Werkrolknooppunt** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper-knooppunt** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Alle stdout en stderr van de bijbehorende host is geüpload naar het opslagaccount. Er is een **uitvoer -\*.txt** en **fouten -\*.txt** voor elke scriptactie. De uitvoer-txt-bestand bevat informatie over de URI van het script dat is uitgevoerd op de host. De volgende tekst is een voorbeeld van deze informatie:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Het is mogelijk dat u een script actie cluster herhaaldelijk met dezelfde naam maken. In dat geval kunt u de relevante logboekbestanden op basis van de naam van de datum-map onderscheiden. Bijvoorbeeld, lijkt de mapstructuur voor een cluster (mijncluster) gemaakt op verschillende datums op de volgende logboekvermeldingen:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Als u een script actie cluster met dezelfde naam op dezelfde dag maakt, kunt u het voorvoegsel uniek te identificeren van de relevante logboekbestanden.

* Als u een cluster in de buurt van 12:00 AM (middernacht) maakt, is het mogelijk dat de logboekbestanden twee dagen overbruggen. In dergelijke gevallen ziet u twee andere datum mappen voor hetzelfde cluster.

* Logboekbestanden uploaden naar de standaardcontainer kan maximaal 5 minuten, met name voor grote clusters duren. Dus als u toegang wilt tot de logboeken, verwijdert niet onmiddellijk u het cluster als een scriptactie is mislukt.

### <a name="ambari-watchdog"></a>Ambari watchdog

> [!WARNING]
> Wijzig het wachtwoord niet voor de Ambari-Watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster. Wijzigen van het wachtwoord voor dit account, verbreekt de mogelijkheid nieuwe scriptacties uitvoeren op het HDInsight-cluster.

### <a name="cant-import-name-blobservice"></a>Naam BlobService kan niet worden geïmporteerd.

__Symptomen__: het script actie mislukt. Tekst die vergelijkbaar is met de volgende fout wordt weergegeven wanneer u de bewerking in Ambari weergeven:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Oorzaak__: deze fout treedt op als u de Python Azure Storage client bijwerkt die is opgenomen in het HDInsight-cluster. HDInsight verwacht Azure Storage client 0.20.0.

__Resolutie__: los deze fout, handmatig verbinding maken met elk cluster knooppunt gebruikt `ssh` en gebruik de volgende opdracht om opnieuw te installeren de juiste opslag clientversie:

```bash
sudo pip install azure-storage==0.20.0
```

Zie voor informatie over de verbinding met het cluster met SSH, [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Geschiedenis van niet wordt scripts die worden gebruikt tijdens het maken van het cluster weergegeven

Als uw cluster is gemaakt voordat 15 maart 2016, ziet u mogelijk niet een vermelding in de geschiedenis van de scriptactie. Het cluster vergroten of verkleinen zorgt ervoor dat de scripts die worden weergegeven in de geschiedenis van de scriptactie.

Er zijn twee uitzonderingen:

* Als uw cluster is gemaakt vóór 1 September 2015. Deze datum is wanneer scriptacties zijn geïntroduceerd. Een cluster is gemaakt voor deze datum kan niet hebben gebruikt scriptacties voor maken van het cluster.

* Als u meerdere scriptacties tijdens het maken van het cluster gebruikt en dezelfde naam voor meerdere scripts of de dezelfde naam, dezelfde URI, maar verschillende parameters voor meerdere scripts gebruikt. In deze gevallen is foutbericht het volgende:

    Op dit cluster vanwege conflicterende scriptnamen in bestaande scripts worden geen nieuwe script acties kunnen worden uitgevoerd. Scriptnamen die zijn opgegeven bij het cluster moet maken allemaal uniek zijn. Bestaande scripts worden uitgevoerd op formaat.

## <a name="next-steps"></a>Volgende stappen

* [Script actie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Installeren en gebruiken van Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md)
* [Installeren en gebruiken van Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md)
* [Extra opslag toevoegen aan een HDInsight-cluster](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"

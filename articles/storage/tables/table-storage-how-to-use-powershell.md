---
title: Azure Table storage bewerkingen uitvoeren met PowerShell | Microsoft Docs
description: Azure Table storage bewerkingen uitvoeren met PowerShell.
services: cosmos-db
documentationcenter: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2018
ms.author: robinsh
ms.openlocfilehash: de8bd78451e12f758397d84459c6740779426d8a
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/01/2018
ms.locfileid: "34660819"
---
# <a name="perform-azure-table-storage-operations-with-azure-powershell"></a>Azure Table storage bewerkingen uitvoeren met Azure PowerShell 
[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Azure Table storage is een NoSQL-gegevensarchief die u gebruiken kunt voor het opslaan en grote sets gestructureerde, niet-relationele gegevens opvragen. De belangrijkste onderdelen van de service zijn tabellen, entiteiten en eigenschappen. Een tabel is een verzameling entiteiten. Een entiteit is een set eigenschappen. Elke entiteit kan maximaal 252 eigenschappen die alle naam / waarde-paren hebben. In dit artikel wordt ervan uitgegaan dat u al bekend met de concepten met Azure Table Storage-Service bent. Zie voor gedetailleerde informatie [inzicht in de tabel Service Data Model](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model) en [aan de slag met Azure Table storage met .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).

Dit artikel bevat informatie over algemene bewerkingen voor Azure Table-opslag. In deze zelfstudie leert u procedures om het volgende te doen: 

> [!div class="checklist"]
> * Een tabel maken
> * Ophalen van een tabel
> * Tabelentiteiten toevoegen
> * Een tabel
> * Tabelentiteiten verwijderen
> * Een tabel verwijderen

Dit artikel laat zien hoe een nieuw Azure Storage-account in een nieuwe resourcegroep maken zodat u het eenvoudig verwijderen kunt wanneer u klaar bent. Als u liever een bestaand opslagaccount, kunt u dat in plaats daarvan doen.

De voorbeelden moet Azure PowerShell-moduleversie 4.4.0 of hoger. Voer in een PowerShell-venster `Get-Module -ListAvailable AzureRM` de versie te vinden. Als niets wordt weergegeven of dat u wilt bijwerken, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). 

Nadat u Azure PowerShell is geïnstalleerd of bijgewerkt, moet u de module installeren **AzureRmStorageTable**, die de opdrachten voor het beheren van de entiteiten heeft. Installeert deze module voeren PowerShell als beheerder en gebruik de **Install-Module** opdracht.

```powershell
Install-Module AzureRmStorageTable
```

## <a name="sign-in-to-azure"></a>Aanmelden bij Azure

Meld u aan bij uw Azure-abonnement met de opdracht `Connect-AzureRmAccount` en volg de instructies op het scherm.

```powershell
Connect-AzureRmAccount
```

## <a name="retrieve-list-of-locations"></a>Lijst met locaties ophalen

Als u niet weet welke locatie u kunt gebruiken, kunt u een lijst met de beschikbare locaties weergeven. Selecteer de gewenste locatie in de lijst. Deze voorbeelden gebruikt **eastus**. Deze waarde wordt opgeslagen in de variabele **locatie** voor toekomstig gebruik.

```powershell
Get-AzureRmLocation | select Location 
$location = "eastus"
```

## <a name="create-resource-group"></a>Een resourcegroep maken

Maak een resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/New-AzureRmResourceGroup). 

Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. Naam van de resourcegroep opgeslagen in een variabele voor toekomstig gebruik. In dit voorbeeld wordt een resourcegroep met de naam *pshtablesrg* wordt gemaakt in de *eastus* regio.

```powershell
$resourceGroup = "pshtablesrg"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

## <a name="create-storage-account"></a>Een opslagaccount maken

Maken van een standaard algemeen opslagaccount met lokaal redundante opslag (LRS) met behulp van [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/New-AzureRmStorageAccount). Haal de context van het opslagaccount waarin de storage-account moet worden gebruikt. Als u werkt met een opslagaccount, verwijst u naar de context in plaats van herhaaldelijk de referenties op te geven.

```powershell
$storageAccountName = "pshtablestorage"
$storageAccount = New-AzureRmStorageAccount -ResourceGroupName $resourceGroup `
  -Name $storageAccountName `
  -Location $location `
  -SkuName Standard_LRS `
  -Kind Storage

$ctx = $storageAccount.Context
```

## <a name="create-a-new-table"></a>Een nieuwe tabel maken

Een tabel te maken, gebruikt u de [nieuw AzureStorageTable](/powershell/module/azure.storage/New-AzureStorageTable) cmdlet. In dit voorbeeld wordt de tabel wordt genoemd `pshtesttable`.

```powershell
$tableName = "pshtesttable"
New-AzureStorageTable –Name $tableName –Context $ctx
```

## <a name="retrieve-a-list-of-tables-in-the-storage-account"></a>Een lijst met tabellen in de storage-account ophalen

Ophalen van een lijst met tabellen in het storage-account met [Get-AzureStorageTable](/powershell/module/azure.storage/Get-AzureStorageTable).

```powershell
Get-AzureStorageTable –Context $ctx | select Name
```

## <a name="retrieve-a-reference-to-a-specific-table"></a>Een verwijzing naar een specifieke tabel ophalen

Voor het uitvoeren van bewerkingen in een tabel, moet u een verwijzing naar de specifieke tabel. Ophalen van een referentie met [Get-AzureStorageTable](/powershell/module/azure.storage/Get-AzureStorageTable). 

```powershell
$storageTable = Get-AzureStorageTable –Name $tableName –Context $ctx
```

[!INCLUDE [storage-table-entities-powershell-include](../../../includes/storage-table-entities-powershell-include.md)]

## <a name="delete-a-table"></a>Een tabel verwijderen

Als u wilt verwijderen van een tabel, gebruikt u [verwijderen AzureStorageTable](/powershell/module/azure.storage/Remove-AzureStorageTable). Deze cmdlet wordt de tabel, inclusief alle gegevens verwijderd.

```powershell
Remove-AzureStorageTable –Name $tableName –Context $ctx

# Retrieve the list of tables to verify the table has been removed.
Get-AzureStorageTable –Context $Ctx | select Name
```

## <a name="clean-up-resources"></a>Resources opschonen

Als u een nieuwe resource groep en storage-account aan het begin van deze instructies hebt gemaakt, kunt u alle van de activa die u in deze oefening hebt gemaakt door het verwijderen van de resourcegroep verwijderen. Deze opdracht verwijdert u alle resources die zich in de groep, evenals de resourcegroep zelf.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In dit artikel how-to, hebt u geleerd over algemene bewerkingen van Azure Table storage met PowerShell, inclusief hoe: 

> [!div class="checklist"]
> * Een tabel maken
> * Ophalen van een tabel
> * Tabelentiteiten toevoegen
> * Een tabel
> * Tabelentiteiten verwijderen
> * Een tabel verwijderen

Zie de volgende artikelen voor meer informatie.

* [PowerShell Storage-cmdlets](/powershell/module/azurerm.storage#storage)

* [Werken met Azure Storage-tabellen vanuit PowerShell](https://blogs.technet.microsoft.com/paulomarques/2017/01/17/working-with-azure-storage-tables-from-powershell/)

* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.

## <a name="overview"></a>Overzicht
Wanneer u een nieuwe virtuele machine (VM) maakt in een resourcegroep met de implementatie van een installatiekopie van [Azure Marketplace](https://azure.microsoft.com/marketplace/), de standaard OS-station is vaak 127 GB (enkele afbeeldingen hebben kleinere voor OS-schijf standaard). Hoewel het mogelijk is om gegevensschijven toe te voegen aan de VM (het aantal is afhankelijk van de SKU die u hebt gekozen) en het bovendien wordt aangeraden om toepassingen en CPU-intensieve werkbelastingen te installeren op deze aanvullende schijven, moeten klanten vaak ook de besturingssysteemschijf uitbreiden om bepaalde scenario's te ondersteunen, zoals de volgende:

1. Ondersteuning voor oudere toepassingen die onderdelen op de besturingssysteemschijf installeren.
2. Een fysieke computer of virtuele machine migreren van on-premises met een grotere besturingssysteemschijf.

> [!IMPORTANT]
> In Azure zijn twee verschillende implementatiemodellen beschikbaar voor het maken van en werken met resources: Resource Manager en het klassieke model. In dit artikel wordt het Resource Manager-model beschreven. U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.
> 
> 
> [!WARNING]
> Formaat van de OS-schijf van een virtuele Machine van Azure, wordt deze opnieuw op te starten.
>

## <a name="resize-the-os-drive"></a>Besturingssysteemschijf uitbreiden
In dit artikel gaan we de grootte van de besturingssysteemschijf aanpassen met behulp van Resource Manager-modules van [Azure Powershell](/powershell/azureps-cmdlets-docs). We tonen grootte wijzigen van het station OS voor zowel beheerde als Unamanged schijven omdat de aanpak voor het vergroten of verkleinen schijven verschilt voor beide schijftypen.

### <a name="for-resizing-unmanaged-disks"></a>Grootte van niet-beheerde schijven:

Open de Powershell ISE of het Powershell-venster in de beheerdersmodus en voer de volgende stappen uit:

1. Meld u in de modus voor resourcebeheer aan bij uw Microsoft Azure-account en selecteer uw abonnement als volgt:
   
   ```Powershell
   Connect-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Stel de naam van de resourcegroep en de VM als volgt in:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Vraag als volgt een verwijzing op naar uw VM:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Ga als volgt te werk om de VM te stoppen voordat u de grootte van de schijf aanpast:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. En dan nu het moment waarop we allemaal gewacht hebben! De grootte van de niet-beheerde besturingssysteemschijf ingesteld op de gewenste waarde en de virtuele machine als volgt bijwerken:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > De nieuwe grootte moet groter zijn dan de bestaande schijfgrootte. Het toegestane maximum is 2048 GB voor OS-schijven. (Het is mogelijk uit te breiden de VHD-blob afgezien van deze grootte, maar het besturingssysteem is alleen mogelijk voor gebruik met de eerste 2048 GB aan ruimte.)
   > 
   > 
6. Het bijwerken van de VM kan een paar seconden duren. Zodra de opdracht is voltooid, start u de VM als volgt opnieuw op:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

### <a name="for-resizing-managed-disks"></a>Voor de schijfgrootte beheerd:

Open de Powershell ISE of het Powershell-venster in de beheerdersmodus en voer de volgende stappen uit:

1. Meld u in de modus voor resourcebeheer aan bij uw Microsoft Azure-account en selecteer uw abonnement als volgt:
   
   ```Powershell
   Connect-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Stel de naam van de resourcegroep en de VM als volgt in:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Vraag als volgt een verwijzing op naar uw VM:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Ga als volgt te werk om de VM te stoppen voordat u de grootte van de schijf aanpast:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Verkrijg een verwijzing naar de schijf met het besturingssysteem worden beheerd. De grootte van de beheerde besturingssysteemschijf ingesteld op de gewenste waarde en bijwerken van de schijf als volgt:
   
   ```Powershell
   $disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.OsDisk.Name
   $disk.DiskSizeGB = 1023
   Update-AzureRmDisk -ResourceGroupName $rgName -Disk $disk -DiskName $disk.Name
   ```   
   > [!WARNING]
   > De nieuwe grootte moet groter zijn dan de bestaande schijfgrootte. Het toegestane maximum is 2048 GB voor OS-schijven. (Het is mogelijk uit te breiden de VHD-blob afgezien van deze grootte, maar het besturingssysteem is alleen mogelijk voor gebruik met de eerste 2048 GB aan ruimte.)
   > 
   > 
6. Het bijwerken van de VM kan een paar seconden duren. Zodra de opdracht is voltooid, start u de VM als volgt opnieuw op:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Dat is alles. Ga nu met RDP naar de VM, open Computerbeheer (of Schijfbeheer) en vouw het station met de zojuist toegewezen ruimte uit.

## <a name="summary"></a>Samenvatting
In dit artikel hebben we Azure Resource Manager-modules van Powershell gebruikt om de besturingssysteemschijf van een virtuele IaaS-machine uit te breiden. Hieronder wordt het volledige script voor de referentie voor zowel niet-beheerd als beheerde schijven:

Unamanged schijven:

```Powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```
Beheerde schijven:

```Powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRMVM -ResourceGroupName $rgName -Name $vmName
$disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.OsDisk.Name
$disk.DiskSizeGB = 1023
Update-AzureRmDisk -ResourceGroupName $rgName -Disk $disk -DiskName $disk.Name
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Volgende stappen
Hoewel in dit artikel wordt primair gericht op het uitbreiden van de Unamanged/beheerde OS-schijf van de virtuele machine, kan het script ontwikkelde ook worden gebruikt voor het uitbreiden van de gegevensschijven gekoppeld aan de virtuele machine. Als u bijvoorbeeld de eerste gegevensschijf die is gekoppeld aan de VM wilt uitbreiden, vervangt u het object ```OSDisk``` van ```StorageProfile``` door de matrix ```DataDisks``` en gebruikt u een numerieke index om een verwijzing naar de eerste gekoppelde schijf te verkrijgen, zoals hieronder wordt weergegeven:

Unamanged schijf:
```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Beheerde schijf:
```Powershell
$disk= Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $vm.StorageProfile.DataDisks[0].Name
$disk.DiskSizeGB = 1023
```

Op dezelfde manier kunt u verwijzen naar andere gegevensschijven die aan de VM zijn gekoppeld. Dit kan met behulp van een index, zoals hierboven, of met de eigenschap ```Name``` van de schijf, zoals hieronder wordt weergegeven:

Unamanged schijf:
```Powershell
($vm.StorageProfile.DataDisks | Where ({$_.Name -eq 'my-second-data-disk'}).DiskSizeGB = 1023
```
Beheerd schijf:
```Powershell
(Get-AzureRmDisk -ResourceGroupName $rgName -DiskName ($vm.StorageProfile.DataDisks | Where ({$_.Name -eq 'my-second-data-disk'})).Name).DiskSizeGB = 1023
```

Als u wilt weten hoe u schijven koppelt aan een Azure Resource Manager-VM, raadpleegt u dit [artikel](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


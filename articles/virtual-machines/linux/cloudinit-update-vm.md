---
title: Cloud-init gebruiken om te werken en pakketten installeren op een Linux-VM op Azure | Microsoft Docs
description: Het gebruik van cloud-init om bij te werken en pakketten worden geïnstalleerd op een Linux-VM tijdens het maken van met de Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: rickstercdn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 04/20/2018
ms.author: rclaus
ms.openlocfilehash: 8d5835b5d1b0c2f77bdf5e1a2b808478b8f4de22
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2018
---
# <a name="use-cloud-init-to-update-and-install-packages-in-a-linux-vm-in-azure"></a>Cloud-init gebruiken om te werken en pakketten installeren op een Linux-VM in Azure
Dit artikel laat zien hoe u [cloud init](https://cloudinit.readthedocs.io) om bij te werken van pakketten op een Linux virtuele machine (VM) of virtuele-machineschaalset ingesteld (VMSS) bij het inrichten van de tijd in Azure. Deze cloud init-scripts worden uitgevoerd op de eerste keer wordt opgestart nadat de resources zijn ingericht met Azure. Zie voor meer informatie over hoe cloud init systeemeigen in Azure en de ondersteunde Linux-distributies werkt [cloud init-overzicht](using-cloud-init.md)

## <a name="update-a-vm-with-cloud-init"></a>Bijwerken van een virtuele machine met cloud-init
Om veiligheidsredenen wilt u mogelijk een VM voor het toepassen van de meest recente updates op de eerste keer opstarten configureren. Als u cloud-init voor verschillende Linux-distributies werkt, is niet nodig om op te geven `apt` of `yum` voor de package manager. In plaats daarvan u definiëren `package_upgrade` en laat het cloud-init-proces bepalen van het juiste mechanisme voor het distro in gebruik. Deze werkstroom kunt u de dezelfde cloud init-scripts gebruiken via distributies.

Om het upgradeproces in actie zien, kunt u een bestand maken in uw huidige shell met de naam *cloud_init_upgrade.txt* en plak de volgende configuratie. Bijvoorbeeld, het bestand te maken in de Cloud-Shell niet op uw lokale machine. U kunt elke editor die u wilt gebruiken. Voer `sensible-editor cloud_init_upgrade.txt` in voor het maken van het bestand en om een overzicht van beschikbare editors te zien. Kies #1 gebruiken de **nano** editor. Controleer of het hele cloud-init-bestand correct is gekopieerd met name de eerste regel.  

```yaml
#cloud-config
package_upgrade: true
packages:
- httpd
```

Voordat u deze installatiekopie implementeert, moet u maken van een resourcegroep met de [az groep maken](/cli/azure/group#az_group_create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS Oost*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

Maak nu een virtuele machine met [az vm maken](/cli/azure/vm#az_vm_create) en geef het cloud-init-bestand met `--custom-data cloud_init_upgrade.txt` als volgt:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_upgrade.txt \
  --generate-ssh-keys 
```

SSH kunt uitvoeren naar het openbare IP-adres van uw virtuele machine wordt weergegeven in de uitvoer van de voorgaande opdracht. Voer uw eigen **publicIpAddress** als volgt:

```bash
ssh <publicIpAddress>
```

De pakket-beheerprogramma en controleren op updates uitvoeren.

```bash
sudo yum update
```

Omdat cloud init gecontroleerd en updates geïnstalleerd op opstarten, moet er geen aanvullende updates worden toegepast.  U ziet het updateproces kan controleren, aantal gewijzigde pakketten, evenals de installatie van `httpd` door het uitvoeren van `yum history` en bekijk de uitvoer ziet er als hieronder.

```bash
Loaded plugins: fastestmirror, langpacks
ID     | Command line             | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
     3 | -t -y install httpd      | 2018-04-20 22:42 | Install        |    5
     2 | -t -y upgrade            | 2018-04-20 22:38 | I, U           |   65
     1 |                          | 2017-12-12 20:32 | Install        |  522
```

## <a name="next-steps"></a>Volgende stappen
Zie voor meer cloud-init voorbeelden van wijzigingen in de configuratie, de volgende:
 
- [Een extra Linux-gebruiker toevoegen aan een virtuele machine](cloudinit-add-user.md)
- [Voer een Pakketbeheer voor het bijwerken van bestaande pakketten op de eerste keer opstarten](cloudinit-update-vm.md)
- [Wijzigen van de lokale hostnaam VM](cloudinit-update-vm-hostname.md) 
- [Installeren van een toepassingspakket, het bijwerken van de configuratiebestanden en het invoeren van sleutels](tutorial-automate-vm-deployment.md)
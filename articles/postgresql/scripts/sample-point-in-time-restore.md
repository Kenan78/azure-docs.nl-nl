---
title: 'Azure CLI-script: een Azure Database for PostgreSQL-server herstellen'
description: Dit Azure CLI-voorbeeldscript laat zien hoe u een Azure Database for PostgreSQL-server en de databases ervan kunt herstellen naar een eerder tijdstip.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 02/28/2018
ms.openlocfilehash: 14e365d90942a09db8bbd2f3eeb4c72a8be3819b
ms.sourcegitcommit: 8c3267c34fc46c681ea476fee87f5fb0bf858f9e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/09/2018
---
# <a name="restore-an-azure-database-for-postgresql-server-using-azure-cli"></a>Een Azure Database voor PostgreSQL-server herstellen met behulp van Azure CLI
Met dit CLI-voorbeeldscript wordt één Azure Database for PostgreSQL-server hersteld naar een eerder tijdstip.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om de CLI lokaal uit te voeren, moet u voor dit artikel gebruikmaken van Azure CLI-versie 2.0 of hoger. Controleer de versie door `az --version` uit te voeren. Zie [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli) voor het installeren of upgraden van uw versie van Azure CLI.

## <a name="sample-script"></a>Voorbeeldscript
Bewerk in dit voorbeeldscript de gemarkeerde regels om de gebruikersnaam en het wachtwoord van de beheerder naar uw eigen bij te werken. Vervang de abonnement-ID die wordt gebruikt in de `az monitor`-opdrachten door uw eigen abonnement-ID.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/backup-restore/backup-restore.sh?highlight=18-19 "Restore Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Opschonen van implementatie
Gebruik de volgende opdracht om de resourcegroep en alle resources die er aan zijn gekoppeld te verwijderen nadat het script is uitgevoerd. 
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/backup-restore/delete-postgresql.sh  "Delete the resource group.")]

## <a name="script-explanation"></a>Uitleg van het script
Dit script maakt gebruik van de opdrachten die in de volgende tabel worden weergegeven:

| **Opdracht** | **Opmerkingen** |
|---|---|
| [az group create](/cli/azure/group#az_group_create) | Hiermee wordt een resourcegroep gemaakt waarin alle resources worden opgeslagen. |
| [az postgresql server create](/cli/azure/postgresql/server#az_msql_server_create) | Hiermee wordt een PostgreSQL-server gemaakt waar de SQL-database wordt gehost. |
| [az postgresql server restore](/cli/azure/postgresql/server#az_msql_server_restore) | Een server herstellen uit een back-up. |
| [az group delete](/cli/azure/group#az_group_delete) | Hiermee verwijdert u een resourcegroep met inbegrip van alle geneste resources. |

## <a name="next-steps"></a>Volgende stappen
- Lees de [documentatie van Azure CLI](/cli/azure) voor meer informatie over de Azure CLI.
- Meer scripts om te proberen: [Azure CLI-voorbeelden voor Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)
- [Back-up maken en herstellen van een server in Azure Database voor PostgreSQL met behulp van de Azure portal](../howto-restore-server-portal.md)

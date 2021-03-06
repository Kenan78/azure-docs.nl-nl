---
title: Verbinding maken met Azure Analysis Services-servers | Microsoft Docs
description: Informatie over het verbinding maken met en gegevens ophalen uit een Analysis Services-server in Azure.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: ce95337c042d6acbdf6e7cff300eb643146e3d87
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/01/2018
ms.locfileid: "34597365"
---
# <a name="connecting-to-servers"></a>Verbinding maken met servers

Dit artikel wordt beschreven verbinding maken met een server met behulp van gegevens modelleren en toepassingen zoals SQL Server Management Studio (SSMS) of SQL Server Data Tools (SSDT). Of met client reporting toepassingen zoals Microsoft Excel, Power BI Desktop of aangepaste toepassingen. HTTPS gebruikt voor verbindingen met Azure Analysis Services.

## <a name="client-libraries"></a>Clientbibliotheken
[De meest recente clientbibliotheken ophalen](analysis-services-data-providers.md)

Alle verbindingen met een server, ongeacht het type, bijgewerkte AMO ADOMD.NET en OLEDB-clientbibliotheken verbinding maken met en contact kunnen maken met een Analysis Services-server is vereist. Voor SSMS, SSDT, Excel 2016 en Power BI, worden de meest recente clientbibliotheken geïnstalleerd of bijgewerkt met maandelijkse releases. In sommige gevallen is het echter mogelijk dat een toepassing heeft mogelijk niet de nieuwste versie. Bijvoorbeeld, zijn als beleid vertraging worden bijgewerkt of Office 365-updates op het kanaal uitgesteld.

## <a name="server-name"></a>Servernaam

Wanneer u een Analysis Services-server in Azure maakt, geeft u een unieke naam en de regio waar de server wordt gemaakt. Wanneer u de servernaam opgeeft in een verbinding, is de schematische naam server:

```
<protocol>://<region>/<servername>
```
 Protocol is waar tekenreeks **asazure**, regio is de Uri waar de server is gemaakt (bijvoorbeeld westus.asazure.windows.net) en servername is de naam van uw unieke server binnen de regio.

### <a name="get-the-server-name"></a>Naam van de server ophalen
In **Azure-portal** > server > **overzicht** > **servernaam**, de naam van de hele server kopiëren. Als andere gebruikers in uw organisatie verbinding met deze server te maakt, kunt u de naam van deze server met hen kunt delen. Wanneer u een servernaam opgeeft, moet het volledige pad worden gebruikt.

![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>Verbindingsreeks

Bij het verbinden met Azure Analysis Services met behulp van het Model in tabelvorm Object, gebruikt u de volgende indelingen voor verbinding tekenreeks:

###### <a name="integrated-azure-active-directory-authentication"></a>Geïntegreerde Azure Active Directory-verificatie
Geïntegreerde verificatie neemt over de Azure Active Directory-referentiecache indien beschikbaar. Als dat niet het geval is, moet u het venster Azure-aanmelding wordt weergegeven.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>Azure Active Directory-verificatie met gebruikersnaam en wachtwoord

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows-verificatie (geïntegreerde beveiliging)
Gebruik het Windows-account met het huidige proces.

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>Verbinding maken met behulp van een ODC-bestand
Gebruikers kunnen met oudere versies van Excel verbinding met een Azure Analysis Services-server met behulp van een bestand Office Data Connection (.odc). Zie voor meer informatie, [maakt u een bestand Office Data Connection (.odc)](analysis-services-odc.md).


## <a name="next-steps"></a>Volgende stappen
[Verbinding maken met Excel](analysis-services-connect-excel.md)    
[Verbinding maken met Power BI](analysis-services-connect-pbi.md)   
[Beheren van uw server](analysis-services-manage.md)   


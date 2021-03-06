---
title: Azure Active Directory-toepassingsproxy en Tableau | Microsoft Docs
description: Informatie over het gebruik van toepassingsproxy van Azure Active Directory (Azure AD) voor externe toegang voor uw implementatie Tableau.  .
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 88da943224ce9df22a3d3befcb8fae6113986862
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/01/2018
ms.locfileid: "34588570"
---
# <a name="azure-active-directory-application-proxy-and-tableau"></a>Azure Active Directory-toepassingsproxy en Tableau 

Azure Active Directory-toepassingsproxy en Tableau hebben hun zodat u zich eenvoudig kunt toepassingsproxy gebruiken voor externe toegang voor uw implementatie Tableau. Dit artikel wordt uitgelegd hoe u dit scenario configureert.  

## <a name="prerequisites"></a>Vereisten 

Het scenario in dit artikel wordt ervan uitgegaan dat u hebt:

- [Tableau](https://onlinehelp.tableau.com/current/server/en-us/proxy.htm#azure) geconfigureerd. 

- Een [Application Proxy connector](manage-apps/application-proxy-enable.md) geïnstalleerd. 

 

## <a name="enabling-application-proxy-for-tableau"></a>Toepassingsproxy voor Tableau inschakelen 

Als u wilt de toepassingsproxy gebruiken voor Tableau, moet u een e-mail sturen naar [ aadapfeedback@microsoft.com ](mailto:aadapfeedback@microsoft.com) ophalen van dit scenario is ingeschakeld.
In uw e-mailadres:

-   Toepassingsproxy inschakelen voor Tableau gebruiken als onderwerp
-   Het opnemen van uw tenant-ID in de hoofdtekst    

U krijgt een bevestiging wanneer u klaar bent voor het gebruik van de toepassing. U kunt de configuraties voltooien tijdens het wachten op voor de bevestiging.


 

## <a name="publish-your-applications-in-azure"></a>Uw toepassingen publiceren in Azure 

Als u wilt publiceren Tableau, moet u een toepassing publiceren in de Azure Portal.

Voor:

- Gedetailleerde instructies van de stappen 1-8, Zie [toepassingen publiceren met Azure AD-toepassingsproxy](manage-apps/application-proxy-publish-azure-portal.md). 
- Informatie over het zoeken naar Tableau waarden voor de velden toepassingsproxy Raadpleeg de documentatie van Tableau.  

**Voor het publiceren van uw app**: 


1. Meld u aan bij de [Azure Portal](https://portal.azure.com) als globale beheerder. 

2. Selecteer **Azure Active Directory > bedrijfstoepassingen**. 

3. Selecteer **toevoegen** boven aan de blade. 

4. Selecteer **On-premises toepassing**. 

5. Vul de vereiste velden met informatie over uw nieuwe app. Gebruik de volgende richtlijnen voor de instellingen: 

    - **Interne URL**: deze toepassing moet een interne URL de URL van de Tableau is. Bijvoorbeeld `https://adventure-works.tableau.com`. 

    - **Methode voor verificatie vooraf**: Azure Active Directory (aanbevolen maar niet vereist). 

6. Selecteer **toevoegen** boven aan de blade. Uw toepassing wordt toegevoegd en het menu Snel starten wordt geopend. 

7. Selecteer in het menu Snel starten **een gebruiker toewijzen voor het testen van**, en ten minste één gebruiker toevoegen aan de toepassing. Zorg ervoor dat deze testaccount toegang heeft tot de on-premises toepassing. 

8. Selecteer **toewijzen** om op te slaan van de toewijzing van de gebruiker test. 

9. (Optioneel) Selecteer op de pagina app-beheer **eenmalige aanmelding**. Kies **geïntegreerde Windows-verificatie** uit de vervolgkeuzelijst en vul de vereiste velden op basis van uw configuratie Tableau. Selecteer **Opslaan**. 

 

## <a name="testing"></a>Testen 

Uw toepassing is nu gereed om te testen. Toegang tot de externe URL die u gebruikt voor het publiceren van Tableau, en meld u aan als een gebruiker die is toegewezen aan beide toepassingen.



## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Azure AD-toepassingsproxy [het verstrekken van veilige externe toegang tot on-premises toepassingen](manage-apps/application-proxy.md).


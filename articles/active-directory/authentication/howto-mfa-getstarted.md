---
title: Aan de slag met Azure MFA in de cloud | Microsoft Docs
description: Dit is de pagina Azure Multi-Factor Authentication waarop wordt beschreven hoe u aan de slag kunt met Azure MFA in de cloud.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.openlocfilehash: 0a822d55e8d7bd0d503eb7d77f96dc9e60e1a4ba
ms.sourcegitcommit: 870d372785ffa8ca46346f4dfe215f245931dae1
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/08/2018
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a>Aan de slag met Azure Multi-Factor Authentication in de cloud
In het volgende artikel staat beschreven hoe u aan de slag gaat met Azure Multi-Factor Authentication in de cloud.

> [!NOTE]
> De volgende documentatie bevat informatie over hoe u gebruikers de mogelijkheid geeft om de **Azure-portal** te gebruiken. Ga naar [Multi-Factor Authentication instellen voor Office 365](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US) als u op zoek bent naar informatie over het instellen van Azure Multi-Factor Authentication voor O365-gebruikers.

![MFA in de Cloud](./media/howto-mfa-getstarted/mfa_in_cloud.png)

## <a name="prerequisite"></a>Vereiste
[U moet u aanmelden voor een Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/): als u nog geen Azure-abonnement hebt, moet u er een nemen. Als u net begint en Azure MFA gebruikt, kunt u een proefabonnement nemen

## <a name="enable-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication inschakelen
Als uw gebruikers licenties hebben die Azure Multi-Factor Authentication bevatten, hoeft u niets te doen om Azure MFA in te schakelen. U kunt starten met het vereisen van verificatie in twee stappen voor afzonderlijke gebruikers. De licenties die Azure MFA inschakelen zijn:
- Azure Multi-Factor Authentication
- Azure Active Directory Premium
- Enterprise Mobility + Security

Als u niet een van deze drie licenties hebt, of onvoldoende licenties hebt voor alle gebruikers, is dat ook geen probleem. U hoeft dan alleen een extra stap uit te voeren en [een Multi-Factor Authentication-provider te maken](concept-mfa-authprovider.md) in uw directory.

## <a name="turn-on-two-step-verification-for-users"></a>Verificatie in twee stappen inschakelen voor gebruikers

Gebruik een van de procedures in de sectie [Verificatie in twee stappen vereisen voor een gebruiker of groep](howto-mfa-userstates.md) om aan de slag te gaan met Azure MFA. U kunt ervoor kiezen om verificatie in twee stappen af te dwingen voor alle aanmeldingen of u kunt een beleid voor voorwaardelijke toegang maken om verificatie in twee stappen alleen te vereisen wanneer dit voor u belangrijk is.

## <a name="next-steps"></a>Volgende stappen
Nu dat u Multi-Factor Authentication in de cloud hebt ingesteld, kunt u uw implementatie configureren en instellen. Zie [Azure Multi-Factor Authentication configureren](howto-mfa-mfasettings.md) voor meer informatie.


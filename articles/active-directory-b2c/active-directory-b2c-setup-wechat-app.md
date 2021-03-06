---
title: WeChat configuratie in Azure Active Directory B2C | Microsoft Docs
description: Registreren en aanmelden gebruikers met een account in uw toepassingen die zijn beveiligd met Azure Active Directory B2C WeChat bieden.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.date: 3/26/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: bbdeccbdd0d6786fdf32fc2f547344b379bd0d7c
ms.sourcegitcommit: 59fffec8043c3da2fcf31ca5036a55bbd62e519c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2018
ms.locfileid: "34712484"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-wechat-accounts"></a>Azure Active Directory B2C: Zich kunnen registreren en aanmelden gebruikers bieden met WeChat-accounts

> [!NOTE]
> Deze functie is beschikbaar als preview-versie.
> 

## <a name="create-a-wechat-application"></a>Een toepassing WeChat maken

Als u wilt gebruiken als een id-provider in Azure Active Directory (Azure AD) B2C WeChat gebruikt, moet u een WeChat-toepassing maken en geeft deze met de juiste parameters. U moet een account WeChat om dit te doen. Als u niet hebt, kunt u een aanmelden via een van hun mobiele apps of via het nummer van uw q krijgen. Hierna is uw account is geregistreerd bij de Ontwikkelaarsprogramma WeChat worden opgehaald. U vindt meer informatie [hier](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Een toepassing WeChat registreren

1. Ga naar [https://open.weixin.qq.com/](https://open.weixin.qq.com/) en meld u aan.
2. Klik op**管理中心**(center management).
3. De benodigde stappen voor het registreren van een nieuwe toepassing.
4. Voor**授权回调域**(callback URL), voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Bijvoorbeeld, als uw `tenant_name` is contoso.onmicrosoft.com, de URL moet worden ingesteld `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Vindt en kopieert de **APP-ID** en **APP-sleutel**. U moet deze later.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>WeChat configureren als een id-provider in uw tenant
1. Volg deze stappen voor [gaat u naar de blade B2C-functies](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in de Azure portal.
2. Klik op de blade B2C-functies op **identiteitsproviders**.
3. Klik op **+Toevoegen** boven aan de blade.
4. Geef een beschrijvende **naam** voor de configuratie van de id-provider. Voer bijvoorbeeld 'WeChat'.
5. Klik op **identiteit providertype**, selecteer **WeChat**, en klik op **OK**.
6. Klik op **instellen van deze id-provider**
7. Voer de **App-sleutel** die u eerder hebt gekopieerd als het **Client-ID**.
8. Voer de **App geheim** die u eerder hebt gekopieerd als het **Clientgeheim**.
9. Klik op **OK** en klik vervolgens op **maken** naar uw WeChat-configuratie op te slaan.


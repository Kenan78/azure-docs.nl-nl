---
title: Het oplossen van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Oplossingen voor bekende problemen met Azure Active Directory B2B-samenwerking
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 05/25/2017
ms.author: twooley
author: twooley
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 4347b846b0ff91f606615abc2c94253c0ae70587
ms.sourcegitcommit: 96089449d17548263691d40e4f1e8f9557561197
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/17/2018
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Het oplossen van Azure Active Directory B2B-samenwerking

Hier volgen een aantal oplossingen voor bekende problemen met Azure Active Directory (Azure AD) B2B-samenwerking.


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a>Ik een externe gebruiker hebt toegevoegd, maar ze niet zien in mijn algemene adresboek of in de personen selecteren

In gevallen waarbij externe gebruikers niet worden ingevuld in de lijst, kan het object enkele minuten duren.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Een gastgebruiker B2B, wordt niet weergegeven in SharePoint Online/OneDrive personen selecteren 
 
De mogelijkheid om te zoeken naar bestaande gastgebruikers in de kiezer voor SharePoint Online (gesimuleerde Productieorder) mensen is uitgeschakeld standaard overeenkomen met de verouderde gedrag.

U kunt deze functie inschakelen met behulp van de instelling 'ShowPeoplePickerSuggestionsForGuestUsers' op het niveau van de verzameling tenant en de site. U kunt de functie met de Set SPOTenant en Set-SPOSite-cmdlets waarmee leden toe aan alle bestaande gastgebruikers zoeken in de map instellen. Wijzigingen in het tenantbereik is niet van invloed op al ingerichte gesimuleerde Productieorder sites.

## <a name="invitations-have-been-disabled-for-directory"></a>Uitnodigingen zijn uitgeschakeld voor de directory

Als er een bericht dat u bent niet gemachtigd om uit te nodigen gebruikers, moet u controleren of uw gebruikersaccount is geautoriseerd om uit te nodigen externe gebruikers onder gebruikersinstellingen:

![](media/troubleshoot/external-user-settings.png)

Als u deze instellingen onlangs hebt gewijzigd of de uitnodiging antwoorden Gast-rol wordt toegewezen aan een gebruiker, kan er een vertraging 15 tot 60 minuten voordat de wijzigingen van kracht.

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a>De gebruiker die ik uitgenodigd ontvangt een fout opgetreden tijdens de inwisselcode

Veelvoorkomende fouten zijn onder andere:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Genodigden Admin is EmailVerified gebruikers worden gemaakt in de tenant toegestaan

Wanneer gebruikers uitnodigen waarvan organisatie gebruikmaakt van Azure Active Directory, maar waarin de specifieke gebruikersaccount bestaat niet (bijvoorbeeld: de gebruiker bestaat niet in Azure AD contoso.com). De beheerder van contoso.com kan beschikken over een beleid te voorkomen dat gebruikers worden gemaakt. De gebruiker moet contact op met de beheerder om te bepalen of de externe gebruikers zijn toegestaan. De beheerder van de externe gebruiker wilt toestaan dat gebruikers e-mailadres gecontroleerd in het domein (dit [artikel](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) op e-mailadres gecontroleerd gebruikers in staat).

![](media/troubleshoot/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Externe gebruiker bestaat niet al in een federatieve domein

Als u van federatieve authenticatie gebruikmaakt en de gebruiker al niet in Azure Active Directory bestaat, kan de gebruiker kan niet worden uitgenodigd.

U lost dit probleem, moet de beheerder van de externe gebruiker het gebruikersaccount met Azure Active Directory synchroniseren.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Hoe biedt\#', die niet is normaal gesproken een ongeldig teken, synchroniseren met Azure AD?

"\#' is een gereserveerd teken in de UPN's voor Azure AD B2B-samenwerking of externe gebruikers, omdat de uitgenodigde account user@contoso.com user_contoso.com#EXT# wordt@fabrikam.onmicrosoft.com. Daarom \# in afkomstig van on-premises UPN's zijn niet toegestaan aan te melden bij de Azure-portal. 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a>Een foutbericht wanneer externe gebruikers toevoegen aan een gesynchroniseerde groep

Externe gebruikers kunnen worden toegevoegd, uitsluitend voor 'toegewezen' of '-' beveiligingsgroepen en niet voor groepen die Gemastered on-premises.

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a>Mijn externe gebruiker heeft geen ontvangen een e-mailbericht te gebruiken

De genodigden moet controleren met hun ISP of spam filter om ervoor te zorgen dat het volgende adres is toegestaan: Invites@microsoft.com

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Ik zoals u ziet dat het aangepaste bericht geen deel uit van de Uitnodigingsberichten op tijdstippen krijgt

Om te voldoen aan de privacywetten onze API's bevatten geen aangepaste berichten in de uitnodiging e-mailbericht wanneer:

- De uitnodiging antwoorden geen een e-mailadres in de uitnodiging tenant
- Wanneer een App service-principal verzendt de uitnodiging

Als dit scenario voor u belangrijk is, kunt u onze API uitnodigingsmail onderdrukken en versturen via het mechanisme voor e-mailadres van uw keuze. Raadpleeg uw juridische afdeling om te controleren of een e-mailbericht verzenden van dat deze manier ook privacywetten naleeft.

## <a name="next-steps"></a>Volgende stappen

- [Ondersteuning krijgen voor B2B-samenwerking](get-support.md)
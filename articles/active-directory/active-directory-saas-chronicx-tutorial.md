---
title: 'Zelfstudie: Azure Active Directory-integratie met ChronicX® | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ChronicX®.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f3f19be6-6ee8-413c-919c-4884ffe685ca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2018
ms.author: jeedes
ms.openlocfilehash: 7a4d5654cb1d771c2e7ce093926e38df18184be2
ms.sourcegitcommit: 59fffec8043c3da2fcf31ca5036a55bbd62e519c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2018
ms.locfileid: "34698608"
---
# <a name="tutorial-azure-active-directory-integration-with-chronicx"></a>Zelfstudie: Azure Active Directory-integratie met ChronicX®

In deze zelfstudie leert u hoe ChronicX® integreren met Azure Active Directory (Azure AD).

Integrating ChronicX® met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot ChronicX® heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij ChronicX® (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met ChronicX®, moet u de volgende items:

- Een Azure AD-abonnement
- Eenmalige aanmelding A ChronicX® ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Adding ChronicX® uit de galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-chronicx-from-the-gallery"></a>Adding ChronicX® uit de galerie
Voor het configureren van de integratie van ChronicX® in Azure AD, moet u ChronicX® uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen ChronicX® uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop Nieuw toepassing][3]

4. Typ in het zoekvak **ChronicX®**, selecteer **ChronicX®** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![ChronicX® in de lijst met resultaten](./media/active-directory-saas-chronicx-tutorial/tutorial_chronicx_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met ChronicX® op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ChronicX® is voor een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ChronicX® tot stand worden gebracht.

Om te configureren en testen van Azure AD eenmalige aanmelding met ChronicX®, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker ChronicX®](#create-a-chronicx®-test-user)**  - ChronicX® die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing ChronicX® configureren.

**Voor het configureren van Azure AD eenmalige aanmelding met ChronicX®, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **ChronicX®** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-chronicx-tutorial/tutorial_chronicx_samlbase.png)

3. Op de **ChronicX®-domein en URL's** sectie, voert u de volgende stappen uit:

    ![ChronicX®-domein en URL's van eenmalige aanmelding informatie](./media/active-directory-saas-chronicx-tutorial/tutorial_chronicx_url.png)

    a. In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen: `https://<subdomain>.chronicx.com/ups/processlogonSSO.jsp`

    b. In de **id** textbox, typ een URL: `ups.chronicx.com`

    > [!NOTE] 
    > De waarde van de aanmeldings-URL is geen echte. Werk de waarde met de werkelijke URL voor eenmalige aanmelding. Neem contact op met [ChronicX® Client ondersteuningsteam](https://www.casebank.com/contact-us/) de waarde op te halen. 
 
4. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-chronicx-tutorial/tutorial_chronicx_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-chronicx-tutorial/tutorial_general_400.png)

6. Eenmalige aanmelding configureren op **ChronicX®** zijde, moet u de gedownloade verzenden **Metadata XML** naar [ChronicX® ondersteuningsteam](https://www.casebank.com/contact-us/). Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/active-directory-saas-chronicx-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-chronicx-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/active-directory-saas-chronicx-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-chronicx-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-chronicx-test-user"></a>Een testgebruiker ChronicX® maken

Het doel van deze sectie is het maken van een gebruiker Britta Simon in ChronicX® genoemd. ChronicX® ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot ChronicX® als deze nog niet bestaat.

>[!Note]
>Als u maken van een gebruiker handmatig wilt, neem dan contact op met [ChronicX® ondersteuningsteam](https://www.casebank.com/contact-us/).

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan ChronicX®.

![Toewijzen van de gebruikersrol][200] 

**Britta Simon om aan te wijzen ChronicX®, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **ChronicX®**.

    ![The ChronicX® koppeling in de lijst met toepassingen](./media/active-directory-saas-chronicx-tutorial/tutorial_chronicx_app.png)  

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel ChronicX® in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ChronicX®.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chronicx-tutorial/tutorial_general_203.png


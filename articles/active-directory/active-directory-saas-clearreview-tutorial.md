---
title: 'Zelfstudie: Azure Active Directory-integratie met duidelijke revisie | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en schakel controleren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8264159a-11a2-4a8c-8285-4efea0adac8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2018
ms.author: jeedes
ms.openlocfilehash: aae5504e593902768ba6e9576a09f3cff1911eb6
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-clear-review"></a>Zelfstudie: Azure Active Directory-integratie met duidelijke revisie

In deze zelfstudie leert u hoe wissen revisie integreren met Azure Active Directory (Azure AD).

Schakel controleren integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot wissen controleren heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij wissen revisie (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met duidelijke controleren, moet u de volgende items:

- Een Azure AD-abonnement
- Een duidelijke revisie eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Schakel controleren uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-clear-review-from-the-gallery"></a>Schakel controleren uit de galerie toevoegen
Voor het configureren van de integratie van duidelijke Lees in Azure AD, moet u Schakel controleren uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt wissen revisie uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop Nieuw toepassing][3]

4. Typ in het zoekvak **wissen revisie**, selecteer **wissen revisie** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Controleer in de lijst met resultaten wissen](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met duidelijke controleren op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in wissen controleren in Azure AD voor een gebruiker is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker wissen gecontroleerd tot stand worden gebracht.

Wijs in wissen Controleer de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met duidelijke revisie, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker wissen revisie](#create-a-clear-review-test-user)**  - hebben een equivalent van Britta Simon wissen gecontroleerd die is gekoppeld aan de Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing wissen controleren.

**Voor het configureren van Azure AD eenmalige aanmelding met duidelijke controleren, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **wissen revisie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_samlbase.png)

3. Op de **wissen revisie domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IdP geïnitieerd** modus:

    ![Schakel controleren domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_url.png)

    a. In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<customer name>.clearreview.com/sso/metadata/`

    b. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen: `https://<customer name>.clearreview.com/sso/acs/`

4. Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:

    ![Schakel controleren domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_url_sp.png)

    In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<customer name>.clearreview.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met de werkelijke aanmeldings-URL, de id en de antwoord-URL. Neem contact op met [wissen revisie ondersteuningsteam](https://clearreview.com/contact/) ophalen van deze waarden.

5. Schakel controleren toepassing verwachten dat de unieke gebruikers-id-waarde in de claim-naam-id. U moet de gebruiker-id-waarde moet worden toegewezen **user.mail**.

    ![De kenmerk-sectie](./media/active-directory-saas-clearreview-tutorial/attribute.png)


6. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_certificate.png)

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clearreview-tutorial/tutorial_general_400.png)

8. Op de **configuratie wissen controleren** sectie, klikt u op **wissen revisie configureren** openen **eenmalige aanmelding configureren** venster. Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**

    ![Wissen van de configuratie controleren](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_configure.png) 

9. Eenmalige aanmelding configureren op **wissen revisie** aan clientzijde, open de **wissen revisie** portal met beheerdersreferenties.

10. Selecteer **Admin** van de linkernavigatiebalk.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin1.png)

11. Selecteer **wijziging** aan de onderkant van de pagina.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin2.png)

12. Voert u de volgende stappen uit op **instellingen voor eenmalige aanmelding** pagina

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app_admin3.png)

    a. In de **URL-verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    b. In de **SAML-eindpunt** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.    

    c. In de **SLO-eindpunt** textbox, plak de waarde van **Service-URL aanmelding** die u hebt gekopieerd vanuit Azure-portal. 

    d. Het gedownloade certificaat openen in Kladblok en plak de inhoud in de **X.509-certificaat** textbox.   

13. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/active-directory-saas-clearreview-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-clearreview-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/active-directory-saas-clearreview-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-clearreview-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
  
### <a name="create-a-clear-review-test-user"></a>Maak een testgebruiker wissen controleren

In deze sectie maakt u Britta Simon aangeroepen in wissen revisie van een gebruiker. Neem contact op met [wissen revisie ondersteuningsteam](https://clearreview.com/contact/) om toe te voegen de gebruikers van het platform wissen controleren.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan wissen controleren.

![Toewijzen van de gebruikersrol][200] 

**Als u wilt toewijzen Britta Simon te wissen controleren, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **wissen revisie**.

    ![De koppeling wissen controleren in de lijst met toepassingen](./media/active-directory-saas-clearreview-tutorial/tutorial_clearreview_app.png)  

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel wissen controleren in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing wissen controleren.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clearreview-tutorial/tutorial_general_203.png

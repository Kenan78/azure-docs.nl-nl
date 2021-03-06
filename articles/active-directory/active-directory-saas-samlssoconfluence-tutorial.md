---
title: 'Zelfstudie: Azure Active Directory-integratie met SAML SSO voor samenloop door resolutie GmbH | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SAML SSO voor samenloop door resolutie GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 6593a53cc05771b6001aed1316233b5d17fe0f24
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Zelfstudie: Azure Active Directory-integratie met SAML SSO voor samenloop door resolutie GmbH

In deze zelfstudie leert u het integreren van SAML SSO voor samenloop door resolutie GmbH met Azure Active Directory (Azure AD).

Integratie van SAML SSO voor samenloop door resolutie GmbH met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot SAML SSO voor samenloop door resolutie GmbH heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij SAML SSO voor samenloop door resolutie GmbH (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met SAML SSO voor samenloop door resolutie GmbH, moet u de volgende items:

- Een Azure AD-abonnement
- Een SAML SSO voor samenloop door resolutie GmbH eenmalige aanmelding voor ingeschakelde abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. SAML SSO voor samenloop door resolutie GmbH uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a>SAML SSO voor samenloop door resolutie GmbH uit de galerie toevoegen

Voor het configureren van de integratie van SAML SSO voor samenloop door resolutie GmbH in Azure AD, moet u SAML SSO voor samenloop door resolutie GmbH uit de galerie toevoegt aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen SAML SSO voor samenloop resolutie GmbH uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak **SAML SSO voor samenloop door resolutie GmbH**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. Selecteer in het deelvenster resultaten **SAML SSO voor samenloop door resolutie GmbH**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding

In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAML SSO voor samenloop door resolutie die GmbH op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de equivalente gebruiker in SAML SSO voor samenloop door resolutie GmbH aan een gebruiker in Azure AD is. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SAML SSO voor samenloop door resolutie GmbH moet tot stand worden gebracht.

Wijs in SAML SSO voor samenloop door resolutie GmbH, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met SAML SSO voor samenloop door resolutie GmbH, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SAML SSO voor samenloop door resolutie GmbH testgebruiker](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  - bevatten een equivalent van Britta Simon SAML SSO voor samenloop door resolutie GmbH die is gekoppeld aan de Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en configureer eenmalige aanmelding in uw SAML SSO voor samenloop resolutie GmbH toepassing.

**Voor het configureren van Azure AD eenmalige aanmelding met SAML SSO voor samenloop door resolutie GmbH, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **SAML SSO voor samenloop door resolutie GmbH** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. Op de **SAML SSO voor samenloop door resolutie GmbH domein en URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    a. In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<server-base-url>/plugins/servlet/samlsso`

    b. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen: `https://<server-base-url>/plugins/servlet/samlsso`

4. Controleer **weergeven geavanceerde instellingen voor URL**. Als u wilt configureren van de toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen: `https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met de werkelijke id, antwoord-URL en aanmeldings-URL. Neem contact op met [SAML SSO voor samenloop door resolutie GmbH Client ondersteuningsteam](https://www.resolution.de/go/support) ophalen van deze waarden. 

5. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. In een ander browservenster geopend, moet u zich aanmelden bij uw **SAML SSO voor samenloop door resolutie GmbH beheerportal** als beheerder.

8. Beweeg de muisaanwijzer op het tandwiel en klik op de **invoegtoepassingen**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. U omgeleid naar de pagina toegang als beheerder. Voer het wachtwoord en klikt u op **bevestigen** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. Onder **ATLASSIAN MARKETPLACE** tabblad **vinden van nieuwe invoegtoepassingen**. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Search **SAML eenmalige aanmelding op (SSO) voor samenloop** en klik op **installeren** knop voor het installeren van de nieuwe SAML-invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. De installatie van de invoegtoepassing wordt gestart. Klik op **Sluiten**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Klik op **Beheren**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Klik op **configureren** voor het configureren van de nieuwe invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Deze nieuwe invoegtoepassing kunt u vinden onder **gebruikers & beveiliging** tabblad.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. Op **SAML-configuratie voor invoegtoepassing van SingleSignOn** pagina, klikt u op **toevoegen van nieuwe IdP** knop voor het configureren van de instellingen van de id-Provider.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. Op **Kies uw SAML-identiteitsprovider** pagina, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon5a.png)
 
    a. Stel **Azure AD** als de IdP-type.
    
    b. Voeg **naam** van de id-Provider (bijvoorbeeld Azure AD).
    
    c. Voeg **beschrijving** van de id-Provider (bijvoorbeeld Azure AD).
    
    d. Klik op **Volgende**.
    
18. Op **identiteit providerconfiguratie** pagina, klikt u op **volgende** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon5b.png)

19. Op **SAML IdP-metagegevens importeren** pagina, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon5c.png)

    a. Klik op **bestand laden** knop en kies Metadata XML-bestand die u in stap 5 hebt gedownload.

    b. Klik op **importeren** knop.
    
    c. Wacht even tot importeren is gelukt.
    
    d. Klik op **volgende** knop.
    
20. Op **gebruikers-ID-kenmerk en transformatie** pagina, klikt u op **volgende** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon5d.png)
    
21. Op **gebruiker gemaakt en update** pagina, klikt u op **opslaan & volgende** instellingen op te slaan.   
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon6a.png)
    
22. Op **testen van uw instellingen** pagina, klikt u op **test overslaan & handmatig configureren** test van de gebruiker nu overslaan. Dit wordt uitgevoerd in de volgende sectie en sommige instellingen in Azure-portal vereist. 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon6b.png)
    
23. In het dialoogvenster apprearing lezen **overslaan van de test betekent...** , klikt u op **OK**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/addon6c.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **BrittaSimon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Maken van een SAML SSO voor samenloop door resolutie GmbH testgebruiker

Om Azure AD-gebruikers aan te melden bij SAML SSO voor samenloop door resolutie GmbH, moeten ze in SAML SSO voor samenloop worden ingericht met behulp van de resolutie GmbH.  
In SAML SSO voor samenloop door resolutie GmbH is inrichting een handmatige taak.

**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**

1. Aanmelden bij uw SAML SSO voor samenloop door resolutie GmbH bedrijf site als beheerder.

2. Beweeg de muisaanwijzer op het tandwiel en klik op de **Gebruikersbeheer**.

    ![Werknemer toevoegen](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. Klik onder de sectie gebruikers op **gebruikers toevoegen** tabblad. Op de **'Gebruiker toevoegen'** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Werknemer toevoegen](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    a. In de **gebruikersnaam** textbox, typt u het e-mailadres van de gebruiker zoals Britta Simon.

    b. In de **volledige naam** textbox, typ de volledige naam van gebruiker zoals Britta Simon.

    c. In de **e** textbox, typ het e-mailadres van gebruiker, zoals Brittasimon@contoso.com.

    d. In de **wachtwoord** textbox, typt u het wachtwoord voor Britta Simon.

    e. Klik op **wachtwoord bevestigen** het wachtwoord opnieuw invoeren.
    
    f. Klik op **toevoegen** knop.    

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie maakt inschakelen u Britta Simon SAML SSO voor samenloop toegang verlenen door resolutie GmbH gebruikt Azure eenmalige aanmelding.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen SAML SSO voor samenloop door resolutie GmbH, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **SAML SSO voor samenloop door resolutie GmbH**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op het SAML SSO voor samenloop door resolutie GmbH tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw SAML SSO voor samenloop door resolutie GmbH toepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png


---
title: 'Zelfstudie: Azure Active Directory-integratie met Manabi Pocket | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Manabi Pocket.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8e521099-bf7d-43ab-a0e0-86aa1c9e577e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/30/2018
ms.author: jeedes
ms.openlocfilehash: 3c4b3f32ce2a66a3b0fccea1f9d73ce685750bb2
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-manabi-pocket"></a>Zelfstudie: Azure Active Directory-integratie met Manabi Pocket

In deze zelfstudie leert u hoe Manabi Pocket integreren met Azure Active Directory (Azure AD).

Manabi Pocket integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Manabi Pocket heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij Manabi Pocket (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Manabi Pocket, moet u de volgende items:

- Een Azure AD-abonnement
- Een Manabi Pocket eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Manabi Pocket uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-manabi-pocket-from-the-gallery"></a>Manabi Pocket uit de galerie toevoegen
Voor het configureren van de integratie van Manabi Pocket in Azure AD, moet u Manabi Pocket uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Manabi Pocket uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop Nieuw toepassing][3]

4. Typ in het zoekvak **Manabi Pocket**, selecteer **Manabi Pocket** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Manabi Pocket in de lijst met resultaten](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Manabi Pocket op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Manabi Pocket is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Manabi Pocket tot stand worden gebracht.

Om te configureren en testen van Azure AD eenmalige aanmelding met Manabi Pocket, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Manabi Pocket](#create-a-manabi-pocket-test-user)**  - Manabi Pocket die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Manabi Pocket configureren.

**Voor het configureren van Azure AD eenmalige aanmelding met Manabi Pocket, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Manabi Pocket** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_samlbase.png)

3. Op de **Manabi Pocket domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:

    ![URL's en Manabi Pocket domein eenmalige aanmelding informatie](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_url.png)

    a. In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<SERVER-NAME>.ed-cl.com/<TENANT-ID>/idp/provider`
    
    b. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen: `https://<SERVER-NAME>.ed-cl.com/<TENANT-ID>/idp/assertion_post`

    > [!NOTE]
    > Deze waarden zijn niet echt. Deze waarden bijwerken met de werkelijke id en de antwoord-URL. Neem contact op met [Manabi Pocket Client ondersteuningsteam](mailto:info-ed-cl@ntt.com) ophalen van deze waarden.

4. Controleer **weergeven geavanceerde instellingen voor URL** en voer de volgende stap als u wilt configureren van de toepassing in **SP** modus gestart:

    ![URL's en Manabi Pocket domein eenmalige aanmelding informatie](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_url1.png)

    In de **aanmeldings-URL** textbox, typ de URL: `https://ed-cl.com/`

5. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_certificate.png) 

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-manabipocket-tutorial/tutorial_general_400.png)

7. Eenmalige aanmelding configureren op **Manabi Pocket** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Manabi Pocket ondersteuningsteam](mailto:info-ed-cl@ntt.com). Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/active-directory-saas-manabipocket-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-manabipocket-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/active-directory-saas-manabipocket-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-manabipocket-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-manabi-pocket-test-user"></a>Een testgebruiker Manabi Pocket maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Manabi Pocket maken. Werken met [Manabi Pocket ondersteuningsteam](mailto:info-ed-cl@ntt.com) de gebruikers van het platform Manabi Pocket toevoegen. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Manabi Pocket.

![Toewijzen van de gebruikersrol][200] 

**Britta Simon om aan te wijzen Manabi Pocket, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Manabi Pocket**.

    ![De koppeling Manabi Pocket in de lijst met toepassingen](./media/active-directory-saas-manabipocket-tutorial/tutorial_manabipocket_app.png)  

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel Manabi Pocket in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Manabi Pocket.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-manabipocket-tutorial/tutorial_general_203.png


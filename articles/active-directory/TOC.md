# Overzicht
## [Wat is Azure Active Directory?](active-directory-whatis.md)
## [Over Azure-identiteitsbeheer](identity-fundamentals.md)
## [Inzicht krijgen in Azure-identiteitsoplossingen](understand-azure-identity-solutions.md)
## [Een hybride identiteitsoplossing kiezen](choose-hybrid-identity-solution.md)
## [Azure-abonnementen koppelen](active-directory-how-subscriptions-associated-directory.md)
## [Overwegingen met betrekking tot vestigingsplaats en gegevens](active-directory-data-storage-eu.md)
## [Veelgestelde vragen](active-directory-faq.md)
## [Nieuwe functies](whats-new.md)


# Aan de slag
## [Aan de slag met Azure AD](get-started-azure-ad.md)
## [Meld u aan voor Azure AD Premium](active-directory-get-started-premium.md)
## [Een aangepaste domeinnaam toevoegen](add-custom-domain.md)
## [Een bedrijfshuisstijl toevoegen](customize-branding.md)
## [Gebruikers toevoegen aan Azure AD](add-users-azure-active-directory.md)
## [Licenties toewijzen aan een gebruikers](license-users-groups.md)
## [Self-service voor wachtwoord opnieuw instellen configureren](authentication/quickstart-sspr.md)
## [Privacy-informatie van uw organisatie toevoegen in Azure AD](active-directory-properties-area.md)


# Procedures
## Plannen en ontwerpen
### [Inzicht in de Azure AD-architectuur](active-directory-architecture.md)
### [Claimtoewijzing in Azure Active Directory](active-directory-claims-mapping.md)
### [Een hybride identiteitsoplossing implementeren](active-directory-hybrid-identity-design-considerations-overview.md)
#### Vereisten bepalen
##### [Identity](active-directory-hybrid-identity-design-considerations-business-needs.md)
##### [Directory-synchronisatie](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
##### [Multi-Factor Authentication](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)
##### [Levenscyclus van identiteit plannen](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)
#### [Plan voor gegevensbeveiliging](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)
##### [Gegevensbeveiliging](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
##### [Inhoudsbeheer](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
##### [Toegangsbeheer](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
##### [Reageren op incidenten](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)
#### Levenscyclus van identiteit plannen
##### [Taken](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)
##### [Acceptatiestrategie](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)
#### [Volgende stappen](active-directory-hybrid-identity-design-considerations-nextsteps.md)
#### [Hulpprogramma's vergelijken](active-directory-hybrid-identity-design-considerations-tools-comparison.md)

## Gebruikers beheren
### [Nieuwe gebruikers toevoegen aan Azure AD](add-users-azure-active-directory.md)
### [Gebruikersprofielen beheren](active-directory-users-profile-azure-portal.md)
### [Accounts delen](active-directory-sharing-accounts.md)
### [Gebruikers aan beheerdersrollen toewijzen](active-directory-users-assign-role-azure-portal.md)
### [Gastgebruikers toevoegen van een andere directory (B2B)](b2b/what-is-b2b.md)
#### [Beheerders die B2B-gebruikers toevoegen](b2b/add-users-administrator.md)
#### [Informatiewerkers die B2B-gebruikers toevoegen](b2b/add-users-information-worker.md)
#### [API en aanpassingen](b2b/customize-invitation-api.md)
#### [Code- en Azure PowerShell-voorbeelden](b2b/code-samples.md)
#### [Voorbeeld self-service-aanmelding portal](b2b/self-service-portal.md)
#### [Uitnodigingse-mail](b2b/invitation-email-elements.md)
#### [Uitnodiging inwisselen](b2b/redemption-experience.md)
#### [B2B-gebruikers zonder uitnodiging toevoegen](b2b/add-user-without-invite.md)
#### [Uitnodigingen toestaan of blokkeren](b2b/allow-deny-list.md)
#### [Voorwaardelijke toegang voor B2B](b2b/conditional-access.md)
#### [Beleid voor B2B-deling](b2b/delegate-invitations.md)
#### [Een B2B-gebruiker toevoegen aan een rol](b2b/add-guest-to-role.md)
#### [Dynamische groepen en B2B-gebruikers](b2b/use-dynamic-groups.md)
#### [Een organisatie verlaten](b2b/leave-the-organization.md)
#### [Controle en rapportage](b2b/auditing-and-reporting.md)
#### [B2B voor hybride organisaties](b2b/hybrid-organizations.md)
##### [B2B-gebruikers toegang geven tot lokale apps](b2b/hybrid-cloud-to-on-premises.md)
##### [Lokale gebruikers toegang geven tot cloud-apps](b2b/hybrid-on-premises-to-cloud.md)
#### [Extern delen B2B en Office 365](b2b/o365-external-user.md)
#### [B2B-licentieverlening](b2b/licensing-guidance.md)
#### [Huidige beperkingen](b2b/current-limitations.md)
#### [Veelgestelde vragen](b2b/faq.md)
#### [Problemen oplossen voor B2B](b2b/troubleshoot.md)
#### [Informatie over de B2B-gebruiker](b2b/user-properties.md)
#### [B2B-gebruikerstoken](b2b/user-token.md)
#### [B2B voor in Azure AD geïntegreerde apps](b2b/configure-saas-apps.md)
#### [B2B-gebruikersclaims toewijzen](b2b/claims-mapping.md)
#### [B2B-samenwerking vergelijken met B2C](b2b/compare-with-b2c.md)
#### [Ondersteuning krijgen voor B2B](b2b/get-support.md)

## [Groepen en leden beheren](active-directory-manage-groups.md)
### Groepen beheren
#### [Azure Portal](active-directory-groups-create-azure-portal.md)
#### [Azure PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
### [Groepsleden beheren](active-directory-groups-members-azure-portal.md)
### [Eigenaren van groepen beheren](active-directory-accessmanagement-managing-group-owners.md)
### [Groepslidmaatschap beheren](active-directory-groups-membership-azure-portal.md)
### [Licenties toewijzen met behulp van groepen](active-directory-licensing-whatis-azure-portal.md)
#### [Licenties toewijzen aan een groep](active-directory-licensing-group-assignment-azure-portal.md)
#### [Licentieproblemen in een groep vaststellen en oplossen](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [Gebruikers met een afzonderlijke licentie migreren naar een groepslicentie](active-directory-licensing-group-migration-azure-portal.md)
#### [Overige scenario's voor groepslicenties](active-directory-licensing-group-advanced.md)
#### [Azure PowerShell-voorbeelden voor groepslicenties](active-directory-licensing-ps-examples.md)
#### [Naslaginformatie voor producten en serviceabonnementen in Azure AD](active-directory-licensing-product-and-service-plan-reference.md)
### [Vervaldatum instellen voor Office 365-groepen](active-directory-groups-lifecycle-azure-portal.md)
### [Alle groepen weergeven](active-directory-groups-view-azure-portal.md)
### [Groepstoegang tot SaaS-apps toevoegen](active-directory-accessmanagement-group-saasapps.md)
### [Herstellen van een verwijderde Office 365-groep](active-directory-groups-restore-azure-portal.md)
### Groepsinstellingen beheren
#### [Azure Portal](active-directory-groups-settings-azure-portal.md)
#### [Cmdlets](active-directory-accessmanagement-groups-settings-cmdlets.md)
### Geavanceerde regels maken
#### [Azure Portal](active-directory-groups-dynamic-membership-azure-portal.md)
### [Selfservicegroepen instellen](active-directory-accessmanagement-self-service-group-management.md)
### [Problemen oplossen](active-directory-accessmanagement-troubleshooting.md)

## [Rapporten beheren](active-directory-reporting-azure-portal.md)
### [Aanmeldingsactiviteit](active-directory-reporting-activity-sign-ins.md)
### [Activiteit controleren](active-directory-reporting-activity-audit-logs.md)
### [Gebruikers die risico lopen](active-directory-reporting-security-user-at-risk.md)
### [Riskante aanmeldingen](active-directory-reporting-security-risky-sign-ins.md)
### [Risicogebeurtenissen](active-directory-reporting-risk-events.md)
### [Veelgestelde vragen](active-directory-reporting-faq.md)
### Taken
#### [Benoemde locaties configureren](active-directory-named-locations.md)
#### [Activiteitenrapporten vinden](active-directory-reporting-migration.md)
#### [Het Power BI-inhoudspakket van Azure Active Directory gebruiken](active-directory-reporting-power-bi-content-pack-how-to.md)
### Naslaginformatie
#### [Retentie](active-directory-reporting-retention.md)
#### [Wachttijden](active-directory-reporting-latencies-azure-portal.md)
#### [Meldingen](active-directory-reporting-notifications.md)
#### [Activiteitsverwijzing controleren](active-directory-reporting-activity-audit-reference.md)
#### [Foutcodes voor aanmeldingsactiviteit](active-directory-reporting-activity-sign-ins-errors.md)
#### [Multi-factor authentication](active-directory-reporting-activity-sign-ins-mfa.md)
### Problemen oplossen
#### [Ontbrekende controlegegevens](active-directory-reporting-troubleshoot-missing-audit-data.md)
#### [Ontbrekende gegevens in downloads](active-directory-reporting-troubleshoot-missing-data-download.md)
#### [Azure Active Directory-activiteitenlogboek registreert inhoudspakketfouten](active-directory-reporting-troubleshoot-content-pack.md)
### [Toegang op programmeerniveau](active-directory-reporting-api-getting-started-azure-portal.md)
#### [Controleverwijzing](active-directory-reporting-api-audit-reference.md)
#### [Verwijzing voor aanmelden](active-directory-reporting-api-sign-in-activity-reference.md)
#### [Vereisten](active-directory-reporting-api-prerequisites-azure-portal.md)
#### [Controlevoorbeelden](active-directory-reporting-api-audit-samples.md)
#### [Voorbeelden van aanmelden](active-directory-reporting-api-sign-in-activity-samples.md)
#### [Certificaten gebruiken](active-directory-reporting-api-with-certificates.md)

## Wachtwoorden beheren
### [Overzicht met betrekking tot wachtwoorden](authentication/active-directory-passwords-overview.md)
### Gebruikersdocumenten
#### [Uw wachtwoord opnieuw instellen of wijzigen](active-directory-passwords-update-your-own-password.md)
#### [Aanbevolen procedures voor wachtwoorden](active-directory-secure-passwords.md)
#### [Registreren voor de selfservice voor wachtwoordherstel](active-directory-passwords-reset-register.md)
### [Hoe SSPR werkt](authentication/concept-sspr-howitworks.md)
### [SSPR-implementatiegids](authentication/howto-sspr-deployment.md)
### [SSPR en Windows 10](authentication/tutorial-sspr-windows.md)
### [Beleidsregels voor SSPR](authentication/concept-sspr-policy.md)
### [SSPR aanpassen](authentication/concept-sspr-customization.md)
### [Gegevensvereisten voor SSPR](authentication/howto-sspr-authenticationdata.md)
### [Rapportage voor SSPR](authentication/howto-sspr-reporting.md)
### IT-beheerders: wachtwoorden opnieuw instellen
#### [Azure Portal](active-directory-users-reset-password-azure-portal.md)
### [SSPR licentiëren](authentication/concept-sspr-licensing.md)
### [Wachtwoord terugschrijven](authentication/howto-sspr-writeback.md)
### [Problemen oplossen](authentication/active-directory-passwords-troubleshoot.md)
### [Veelgestelde vragen](authentication/active-directory-passwords-faq.md)


## Apparaten beheren
### [Inleiding](device-management-introduction.md)
### [Azure Portal gebruiken](device-management-azure-portal.md)
### [Azure AD Join plannen](active-directory-azureadjoin-deployment-aadjoindirect.md)
### [Veelgestelde vragen](device-management-faq.md)
### Taken
#### [Bij Azure AD ingeschreven Windows 10-apparaten instellen](device-management-azuread-registered-devices-windows10-setup.md)
#### [In Azure AD gekoppelde apparaten instellen](device-management-azuread-joined-devices-setup.md)
#### [Hybride, in Azure AD gekoppelde apparaten instellen](device-management-hybrid-azuread-joined-devices-setup.md)
#### [On-premises implementeren](active-directory-device-registration-on-premises-setup.md)
#### [Koppelen aan Azure AD tijdens eerste sessie in Windows 10](device-management-azuread-joined-devices-frx.md)
### Problemen oplossen
#### [Hybride, in Azure AD gekoppelde Windows 10- en Windows Server 2016-apparaten](device-management-troubleshoot-hybrid-join-windows-current.md)
#### [Hybride, in Azure AD gekoppelde oudere Windows-apparaten](device-management-troubleshoot-hybrid-join-windows-legacy.md)

## Apps beheren
### [Overzicht](manage-apps/what-is-application-management.md)
### [Aan de slag](manage-apps/plan-an-application-integration.md)
### [Zelfstudies voor SaaS-app-integratie](active-directory-saas-tutorial-list.md)
### [Cloud App Discovery](manage-apps/cloud-app-discovery.md)
#### [Momentopnamerapporten maken](manage-apps/cloud-app-discovery-create-snapshot-reports.md)
#### [Continue rapportage configureren](https://docs.microsoft.com/cloud-app-security/discovery-docker)
#### [Een aangepaste logboekparser gebruiken](https://docs.microsoft.com/cloud-app-security/custom-log-parser)


### [Toegang tot apps op afstand via App Proxy](manage-apps/application-proxy.md)
#### Aan de slag
##### [App-Proxy inschakelen](manage-apps/application-proxy-enable.md)
##### [Apps publiceren](manage-apps/application-proxy-publish-azure-portal.md)
##### [Aangepaste domeinen](manage-apps/application-proxy-configure-custom-domain.md)
#### [Eenmalige aanmelding](manage-apps/application-proxy-single-sign-on.md)
##### [Eenmalige aanmelding met KCD](manage-apps/application-proxy-configure-single-sign-on-with-kcd.md)
##### [Eenmalige aanmelding met koppen](manage-apps/application-proxy-configure-single-sign-on-with-ping-access.md)
##### [Eenmalige aanmelding met wachtwoordkluis](manage-apps/application-proxy-configure-single-sign-on-password-vaulting.md)
#### Concepten
##### [Connectors](manage-apps/application-proxy-connectors.md)
##### [Beveiliging](manage-apps/application-proxy-security.md)
##### [Netwerken](manage-apps/application-proxy-network-topology.md)


##### [Upgraden van TMG of UAG](manage-apps/application-proxy-migration.md)

#### Geavanceerd configuratie
##### [Publiceren op afzonderlijke netwerken](manage-apps/application-proxy-connector-groups.md)
##### [Proxyservers](manage-apps/application-proxy-configure-connectors-with-proxy-servers.md)
##### [Claimbewuste apps](manage-apps/application-proxy-configure-for-claims-aware-applications.md)
##### [Systeemeigen client-apps](manage-apps/application-proxy-configure-native-client-application.md)
##### [Stille installatie](manage-apps/application-proxy-register-connector-powershell.md)
##### [Aangepaste startpagina](manage-apps/application-proxy-configure-custom-home-page.md)
##### [Inlinelinks vertalen](manage-apps/application-proxy-configure-hard-coded-link-translation.md)
##### [Jokertekens](active-directory-application-proxy-wildcard.md)
##### [Persoonlijke gegevens verwijderen](manage-apps/application-proxy-remove-personal-data.md)


#### Publicatie-overzicht
##### [Extern bureaublad](manage-apps/application-proxy-integrate-with-remote-desktop-services.md)
##### [SharePoint](manage-apps/application-proxy-integrate-with-sharepoint-server.md)
##### [Microsoft Teams](application-proxy-teams.md)
##### [Tableau](active-directory-application-proxy-tableau.md)
##### [Qlik](active-directory-application-proxy-qlik.md)


#### [Problemen oplossen](active-directory-application-proxy-troubleshoot.md)

### Enterprise-apps beheren
#### [Gebruikers toewijzen](active-directory-coreapps-assign-user-azure-portal.md)
#### [Huisstijl aanpassen](active-directory-coreapps-change-app-logo-user-azure-portal.md)
#### [Gebruikersaanmeldingen uitschakelen](active-directory-coreapps-disable-app-azure-portal.md)
#### [Gebruikers verwijderen](active-directory-coreapps-remove-assignment-azure-portal.md)
#### [Al mijn apps weergeven](active-directory-coreapps-view-azure-portal.md)
#### [Inrichting van gebruikersaccount beheren](active-directory-enterprise-apps-manage-provisioning.md)
#### [Eenmalige aanmelding voor zakelijke apps beheren](active-directory-enterprise-apps-manage-sso.md)
#### [Geavanceerde certificaatondertekening voor SAML-apps](active-directory-enterprise-apps-advance-certificate-options.md)
#### [Een app van een externe partij verbergen voor een gebruiker](active-directory-coreapps-hide-third-party-app.md)
### [Automatisch versnellen van aanmelding configureren met behulp van HRD-beleid](active-directory-auto-acceleration-using-hrd.md)

### [Toegang tot apps beheren](active-directory-managing-access-to-apps.md)
#### [Toegang via eenmalige aanmelding](manage-apps/what-is-single-sign-on.md)
#### [Certificaten voor SSO](active-directory-sso-certs.md)
#### [Beperkingen voor tenants](active-directory-tenant-restrictions.md)
#### [SCIM gebruiken voor het inrichten van gebruikers](active-directory-scim-provisioning.md)

### [Problemen oplossen](active-directory-application-troubleshoot-content-map.md)
#### [Ontwikkeling van toepassingen](active-directory-application-dev-troubleshoot-content-map.md)
##### [Configuratie en registratie](active-directory-application-dev-config-content-map.md)
##### [Ontwikkeling](active-directory-application-dev-development-content-map.md)
#### [Beheer van toepassingen](active-directory-application-management-troubleshoot-content-map.md)
##### [Configuratie](active-directory-application-config-content-map.md)
##### [Aanmelden](active-directory-application-sign-in-content-map.md)
##### [Inrichten](active-directory-application-provisioning-content-map.md)
##### [Toegang beheren](active-directory-application-access-content-map.md)
##### [Toegangsvenster](active-directory-application-access-panel-content-map.md)
##### [Toepassingsproxy](active-directory-application-proxy-content-map.md)
##### [Voorwaardelijke toegang](active-directory-application-conditional-access-content-map.md)
### [Apps ontwikkelen](active-directory-applications-guiding-developers-for-lob-applications.md)
### [Documentbibliotheek](active-directory-apps-index.md)

## Uw directory beheren
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### Aangepaste domeinnamen
#### [Snelstartgids](add-custom-domain.md)
#### [Aangepaste domeinnamen toevoegen](active-directory-domains-manage-azure-portal.md)
### [Uw directory beheren](active-directory-administer.md)
### [Meerdere directory’s beheren](active-directory-licensing-directory-independence.md)
### [Selfservice registreren](active-directory-self-service-signup.md)
### [Een niet-beheerde directory overnemen](domains-admin-takeover.md)
### [Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
#### [Inschakelen](active-directory-windows-enterprise-state-roaming-enable.md)
#### [Instellingen voor groepsbeleid](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
#### [Windows 10-instellingen](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
#### [Veelgestelde vragen](active-directory-windows-enterprise-state-roaming-faqs.md)
#### [Problemen oplossen](active-directory-windows-enterprise-state-roaming-troubleshooting.md)


### [On-premises identiteiten integreren met Azure AD Connect](./connect/active-directory-aadconnect.md)

## [Toegang tot Azure beheren](../role-based-access-control/toc.yml)

## Toegang tot resources delegeren
### [Beheerdersrollen](active-directory-assign-admin-roles-azure-portal.md)
#### [Beheerdersrollen toewijzen](active-directory-users-assign-role-azure-portal.md)
#### [Standaard gebruikersmachtigingen](users-default-permissions.md)
### [Beheereenheden](active-directory-administrative-units-management.md)
### [De levensduur van tokens configureren](active-directory-configurable-token-lifetimes.md)
### [Beheerdersaccounts voor noodtoegang beheren](active-directory-admin-manage-emergency-access-accounts.md)
### [Bevoorrechte rollen beveiligen](admin-roles-best-practices.md)

## Toegangsbeoordelingen
### [Overzicht toegangsbeoordelingen](active-directory-azure-ad-controls-access-reviews-overview.md)
### [Complete an access review](active-directory-azure-ad-controls-complete-access-review.md) (Een toegangscontrole voltooien)
### [Create an access review](active-directory-azure-ad-controls-create-access-review.md) (Een toegangscontrole maken)
### [How to perform an access review](active-directory-azure-ad-controls-perform-access-review.md) (Een toegangscontrole uitvoeren)
### [Uw toegang controleren](active-directory-azure-ad-controls-how-to-review-your-access.md)
### [Toegang voor gasten met toegangsbeoordelingen](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md)
### [Gebruikerstoegang met beoordelingen beheren](active-directory-azure-ad-controls-manage-user-access-with-access-reviews.md)
### [Programma's en besturingselementen beheren](active-directory-azure-ad-controls-manage-programs-controls.md)
### [Resultaten van de toegangsbeoordeling ophalen](active-directory-azure-ad-controls-retrieve-access-review.md)

## Uw identiteiten beveiligen
### [Voorwaardelijke toegang](active-directory-conditional-access-azure-portal.md)
#### [Voorwaarden](active-directory-conditional-access-conditions.md)
#### [Locatievoorwaarden](active-directory-conditional-access-locations.md)
#### [Besturingselementen](active-directory-conditional-access-controls.md)
#### [Aan de slag](active-directory-conditional-access-azure-portal-get-started.md)
#### [Aanbevolen procedures](active-directory-conditional-access-best-practices.md)
#### [Inzicht in apparaatbeleidsregels voor Office 365-services](active-directory-conditional-access-device-policies.md)
#### [Klassieke beleidsregels migreren](active-directory-conditional-access-migration.md)
#### [Hulpprogramma What-If](active-directory-conditional-access-whatif.md)
#### Snelstartgids
##### [MFA per cloud-app configureren](active-directory-conditional-access-app-based-mfa.md)
#### Taken
##### [Klassiek MFA-beleid migreren](active-directory-conditional-access-migration-mfa.md)
##### [Voorwaardelijke toegang op basis van apparaten instellen](active-directory-conditional-access-policy-connected-applications.md)
##### [Voorwaardelijke toegang op basis van apps instellen](active-directory-conditional-access-mam.md)
##### [Gebruiksvoorwaarden bieden voor gebruikers en apps](active-directory-tou.md)
##### [VPN-connectiviteit instellen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)
##### [SharePoint en Exchange Online instellen](active-directory-conditional-access-no-modern-authentication.md)
##### [Herstel](active-directory-conditional-access-device-remediation.md)
#### [Technische naslaginformatie](active-directory-conditional-access-technical-reference.md)
#### [Veelgestelde vragen](active-directory-conditional-faqs.md)

### Windows Hello
#### [Verifiëren zonder wachtwoorden](active-directory-azureadjoin-passport.md)
#### [Windows Hello voor Bedrijven inschakelen](active-directory-azureadjoin-passport-deployment.md)
### Verificatie op basis van certificaat
#### [Android](active-directory-certificate-based-authentication-android.md)
#### [iOS](active-directory-certificate-based-authentication-ios.md)
#### [Aan de slag](active-directory-certificate-based-authentication-get-started.md)

### [Azure AD Identity Protection](active-directory-identityprotection.md)
#### [Inschakelen](active-directory-identityprotection-enable.md)
#### [Beveiligingslekken detecteren](active-directory-identityprotection-vulnerabilities.md)
#### [Risicogebeurtenissen](active-directory-identity-protection-risk-events.md)
#### [Meldingen](active-directory-identityprotection-notifications.md)
#### [Aanmeldingservaring](active-directory-identityprotection-flows.md)
#### [Risicogebeurtenissen simuleren](active-directory-identityprotection-playbook.md)
#### [Gebruikers deblokkeren](active-directory-identityprotection-unblock-howto.md)
#### [Veelgestelde vragen](active-directory-identity-protection-faqs.md)
#### [Woordenlijst](active-directory-identityprotection-glossary.md)
#### [Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
### [Privileged Identity Management](active-directory-privileged-identity-management-configure.md)

## [Andere services integreren met Azure AD]()
### [LinkedIn-integratie inschakelen](linkedin-integration.md)

## [AD FS in Azure implementeren](active-directory-aadconnect-azure-adfs.md)
### [Hoge beschikbaarheid](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
### [Hash-algoritme van de handtekening wijzigen](active-directory-federation-sha256-guidance.md)

## [Problemen oplossen](active-directory-troubleshooting-support-howto.md)

## Azure AD Proof of Concept (PoC) implementeren
### [PoC Playbook: inleiding](active-directory-playbook-intro.md)
### [PoC Playbook: onderdelen](active-directory-playbook-ingredients.md)
### [PoC Playbook: implementatie](active-directory-playbook-implementation.md)
### [PoC Playbook: bouwstenen](active-directory-playbook-building-blocks.md)


# Naslaginformatie
## [Codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory)
## [Azure PowerShell-cmdlets](/powershell/azure/overview)
## [Naslaginformatie over de Java-API](/java/api)
## [.NET API](/active-directory/adal/microsoft.identitymodel.clients.activedirectory)
## [Servicelimieten en -beperkingen](active-directory-service-limits-restrictions.md)

# Verwant
## [Multi-Factor Authentication](/azure/multi-factor-authentication/)
## [Azure AD Connect](./connect/active-directory-aadconnect.md)
## [Azure AD Connect Health (Engelstalig)](./connect-health/active-directory-aadconnect-health.md)
## [Azure AD for Developers](./develop/active-directory-how-to-integrate.md)
## [Azure AD Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

# Resources
## [Azure-feedbackforum](https://feedback.azure.com/forums/169401-azure-active-directory)
## [Azure-roadmap](https://azure.microsoft.com/roadmap/?category=security-identity)
## [MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)
## [Prijzen](https://azure.microsoft.com/pricing/details/active-directory/)
## [Prijscalculator](https://azure.microsoft.com/pricing/calculator/)
## [Service-updates](https://azure.microsoft.com/updates/?product=active-directory)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
## [Video's](https://azure.microsoft.com/documentation/videos/index/?services=active-directory)

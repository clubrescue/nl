# IT Suite for non profits

## Introduction

- Doel van deze sectie
    - Een overzicht geven van de functionaliteiten, architectuur en roadmap van de IT Suite voor non profits en Club.Redders.
    - Informeren van gebruikers, beheerders en ontwikkelaars over hoe de verschillende componenten samenhangen.
    - Bewustzijn creëren over de afhankelijkheden en impact van bepaalde acties door betrokkenen op de componenten.
    - Duidelijk maken voor welke periode bepaalde wensen bij de ontwikkelaars bekend moeten zijn voor de volgende release.
- Doelgroep
    - Gebruikers en beheerders van de IT Suite
        - Office 365, MachForm, Club.Redders, C.R WordPress plugin
    - Ontwikkelaars van Club.Redders
        - Core, modules en CMS plugins

## The Suite

- Organisatie wensen:
    - Een volledige online beschikbare IT omgeving.
    - Zo’n professioneel mogelijke kwaliteit tegen zo’n laag mogelijke kosten.
    - Bestaande vrij beschikbare tooling over low- cost tooling over bouwen.
    - IT componenten moeten los van elkaar kunnen functioneren of individueel vervangen kunnen worden door een alternatief product met dezelfde functionaliteiten.
- IT Suite voor non profits:
    - Maakt gebruik van open source of via TechSoup gratis verkrijgbare software.
    - Gebruikt Office 365 als oplossing voor mail, gegevens opslag, chat en social platform.
        - Azure AD wordt ingezet voor Single Sign On en wachtwoordresetfunctionaliteit binnen de IT Suite.
    - Gebruikt MachForm (betaald) als WYSIWYG formulieren tool.
        - SSO is mogelijk met Okta (MachForm <> LDAP <> OKTA <> SAML <> O365).
    - Gebruikt WordPress als website content management oplossing met SSO via O365.
- Club.Redders:
    - Zet voor vereniging specifieke wensen een zelfbouw tool in gebaseerd op PHP.
    - Modulair opgebouwd zodat modules door verschillende ontwikkelaars kunnen worden ontwikkeld en worden toegevoegd en verwijderd zonder impact op andere modules.
    - Open Source zodat de software en documentatie voor alle betrokkenen vrij beschikbaar is en blijft.
        - Software is vrij beschikbaar onder de GPL en/of MIT licentie.
        - Documentatie is vrij beschikbaar onder de CC BY-SA 4.0 licentie.
# Ledenadministratie

## Factsheet

| | |
| --- | --- |
| Functionaliteiten | - Ledenadministratie beheren van leden (incl. pasfotos) |
| Afhankelijkheden | - Core |
| Ontwikkelaars | Core developer(s) |

- Deze module biedt de volgende mogelijkheden;
    - **Uitbreiden met ledenadmin module info**
    - Uploaden van pasfoto voor leden door kaderleden.
    - Uploaden van eigen pasfoto door leden.
    - Zowel intern als t.z.t. via Microsoft Graph.
- Afhankelijkheden;
    - Core

## Leden beheren

Voor het leden beheer dient ervanuit uit gegaan te worden dat mutaties als volgt
plaatsvinden;

| **Mutatie**             | **Eerst doorvoeren in** | **Daarna doorvoeren in**                    | **Controle d.m.v.**                              |
|-------------------------|-------------------------|---------------------------------------------|--------------------------------------------------|
| Aanmaken van een lid    | Ledenadministratie bond | Club.Redders                                | Differentiatie lijst                             |
| Wijzigen van een lid    | Club.Redders            | Ledenadministratie bond                     | Differentiatie lijst                             |
|                         |                         | (indien van toepassing)                     | (indien basis gegevens, bij jaarlijkse controle) |
| Verwijderen van een lid | Volgens eigen procedure | Differentiatie lijst                        |                                                  |
|                         |                         | (advies controle 1 week voor peildata bond) |                                                  |

### Aanmaken

Voor het aanmaken van het lid dient de werkwijze van het bond systeem gevolgd te
worden waarbij na toevoegen van het lid aan de ledenadministratie van de bond de basis
gegevens opgevoerd/ingesteld worden. Let erop dat een lid bij een
inschrijving andere gegevens kan hebben ingevuld dan in de ledenadministratie van de bond staan geregistreerd
mocht het betreffende lid ook elders lid zijn.

Na deze controle dient het lid verder opgevoerd te worden in Club.Redders
waarbij het lid nummer uit de ledenadministratie van de bond als lid nummer dient te worden opgevoerd. Vandaar
dat een lid eerst in de ledenadministratie van de bond wordt opgevoerd. Dit is tevens de grondslag voor
de controle commissie van de bond dat wij leden altijd in de ledenadministratie van de bond hebben staan
(of i.i.g een gelijk of groter aantal dan in Club.Redders).

### Wijzigen

Leden kunnen via Club.Redders / Club.Forms wijzigingen indienen. Andere
verenigingen, het rayon en de bond kunnen wijzigingen doorvoeren  in de ledenadministratie van de bond.
Het is daarom verstandig de wijzigingen van leden automatisch door te laten
voeren in Club.Redders waarna deze via een melding bij de secretaris of
ledenadministrateur ook worden doorgevoerd  in de ledenadministratie van de bond.
Voor wat betreft de wijziging gegevens betreft die daar worden opgeslagen en wij dienen door te geven aan de bond.

### Verwijderen

Het verwijderen van leden dient te gebeuren in beide systemen. Via Club.Redders
/ Club.Forms meld een lid zich af. Indien het lid geen betalingsachterstand
heeft kan de secretaris de opzegging in het systeem accorderen en daarna
handmatig in de ledenadministratie van de bond verwerken. Indien het lid toestemming heeft gegeven zijn
gegevens te bewaren wordt deze in Club.Redders geregistreerd als oud lid.
In de ledenadministratie van de bond is het echter mogelijk gegevens van alle oud leden in te zien. Ook als
hier geen toestemming voor is gegeven! Wederom een belangrijk argument daar zo min mogelijk gegevens in te verwerken.

### Ledenbestand vergelijken

Toelichten op vergelijken ledenbestand en automatisch doorvoeren wijzigen in CR of handmatig in de ledenadministratie van de bond. Wijs er op dat bij de 1e je vertrouwd op gegevens die 3de kunnen wijzigen en bij
de 2e op je eigen administratie en wat leden jouw vertellen!

### Bijlage: Op welke plaatsen dienen rechten ingeregeld te worden?

Uitgaande van onderstaande tooling is toegang noodzakelijk voor;

| **Tooling**           | **Accout**            | **Toegang nodig voor** | **Rechten krijg je door**         |
|-----------------------|-----------------------|------------------------|-----------------------------------|
| Office 365 / Azure AD | Intern account        | Alle leden             | Work in progress                  |
| Club.Redders (ResQ)   | O365-account (SSO)    | \-                     | Work in progress                  |
| WordPress             | O365-account (SSO)    | \-                     | Automatisch                       |
| MachForm              | Intern account        | Kader leden            | Work in progress                  |
| Akounting             | Intern account        | Bestuur + Kascommissie | Work in progress                  |
| *Systeem van de bond* | Intern account        | Bestuur                | Handmatig via bestuur             |
| KeeWeb                | Geen account          | Vrij toegankelijk      | n.v.t.                            |
| Webhosting            | Div. interne accounts | Functionaris IT        | Handmatig via andere functionaris |
| Domeinregistratie     | Intern account        | Bestuur                | LastPass/KeePass van het bestuur  |

Momenteel wordt er gewerkt om alle rechten automatisch toe te laten kennen. Dit
geld straks voor al onze systemen m.u.v. het systeem van de bond, webhosting,
domeinregistratie en LastPass. De overige systemen werken straks met één account
en zodra je lid bent wordt je account dan automatisch aangemaakt. Een bestuurder
kan vervolgens zelf aangeven welke rechten nodig zijn.

Tot die tijd dienen voor deze systemen rechten aangevraagd te worden bij de
functionaris IT, m.u.v. het het systeem van de bond. Die rechten dienen door het
bestuur te worden toegekend en toegang is dan ook enkel nodig binnen het bestuur
zelf.
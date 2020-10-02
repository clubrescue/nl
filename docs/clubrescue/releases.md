# Releases

## Actuele wijzigingen

- Inkomende gegevens
    - Leden gegevens van overschrijven naar vergelijken. Hierdoor hebben wijzigingen in de structuur van de bondsledenadministratie geen impact meer op de tool. Met name met de wijziging van Java Web Start app naar Web app.
- Uitgaande gegevens
    - Van VBA IE koppeling naar CSV bestanden. Hierdoor kunnen ontwikkelingen van de tool doorgaan zonder dat deze koppeling stuk kan gaan.
- Uitfaseren van de Excel bewakingstool
    - Hierdoor wordt het gebruik van de data buiten de tool (CSV/Excel) beperkt tot een select aantal gebruikers binnen het bestuur en CSz.
    - Omhelst het bouwen van een competentie beheer en toekenningssysteem (70%)
    - Omhelst een eenmalige ‘migratie’ van een deel van de reeds in de bondsledenadministratie verlengde competenties door deze in de tool nogmaals te verlengen.
- Na bovenstaande wijzigingen volgt het technisch herschikken van de tool naar afgekaderde modules.
    - Hierna kan onderhoud per module door een aparte ontwikkelaar plaats vinden.

## Release schema

| Generatie | Primaire focus/verbeteringen | Periode | Maand |
| --- | --- | --- | --- |
| Gen 1 – fase 1 | Concept met Excel front- & back-end | Pre-seizoen | Juni 2015 |
| Gen 1 – fase 2 | PHP back-end met Excel front-end | Pre-seizoen | Juni 2016 |
| Gen 2 – fase 1 | DB back-end met PHP & Excel front-end | Pre-seizoen | Februari 2017 |
| | Implementatie Office 365 | Gehele jaar | 2018 |
| Gen 2 – fase 2 | Geïntegreerde IT suite met 1ID/SSO | Post-seizoen | December 2019 |
| Gen 3 – fase 1 | Tool zonder externe afhankelijkheden | Pre-seizoen | Februari 2020 |
| Gen 3 – fase 2 | Modulaire tool met P-A-O releases | Post-seizoen | December 2020 |
| | | | |
| Proces | Proces verbeteringen & features release | Pre-seizoen | Jan-Apr 2021 |
| Architectuur | Architectuur wijzigingen release | Seizoen | Mei-Aug 2021 |
| Optimalisatie | Optimalisatie release | Post-seizoen | Sep-Dec 2021 |
| | Jaarlijks 1 P-A-O cyclus |||

## Ontstaan en doorontwikkeling van de IT Suite en Club.Redders

- Ontstaan IT Suite
    - Geleidelijk aan ontstaan op basis van best-practice bij de ontwikkeling van Club.Redders
    - Bestaande gratistoolingover low-cost tooling over bouwen
- Ontwikkeling Club.Redders tot en met 2020  
    - 2015 start ontwikkelingentool in Excel  
    - 2016 tool omgebouwd naar PHP  
    - 2017 toevoeging vanMachForm  
    - 2018 toevoeging van Office 365  
    - 2019 integratie vande diverse componenten tot één geïntegreerde omgeving  
    - 2020 pre-seizoen koppelingen tussen componenten ombouwen/omgebouwd zodat deze zelfstandig van elkaar blijven werken  
    - 2020 post-seizoen ombouwen van de tool naar een modulaire inrichting t.b.v. betere code en doorontwikkeling (future-proofing)  
- Ontwikkeling Club.Redders vanaf 2021 en verder
    - Ontwikkeling volgens Proces-Architectuur-Optimalisatie principe
        - Pre-seizoen worden proces (functionaliteiten) toegevoegd in de diverse modules
        - Tijdens het seizoen worden (op de achtergrond in OTA) technische verbeteringen doorgevoerd
        - Na het seizoen worden de functionele en technische wijzigingen geoptimaliseerd
            - Functioneel door input vanuit het seizoen door te voeren in de modules
            - Technisch door de technische verbeteringen in decoreuit te lijnen met de modules en de IT suite

## Proces-Architectuur-Optimalisatie cyclus

- Proces cyclus
    - Januari t/m april (pre-seizoen)
    - Doel: toevoegen functionaliteiten aan diverse modules, geen wijzigingen in de core.
    - Deadline wijzigingsverzoeken: 1 november.
        - Om verzoeken goed voor te bereiden dienen deze 2 maanden vooraf bekend te zijn.
- Architectuur cyclus
    - Mei t/m augustus (tijdens seizoen)
    - Doel: doorvoeren van technische verbeteringen aan decore, geen nieuwe functionaliteiten.
    - Deadline wijzigingsverzoeken: 1 maart.
        - Om verzoeken goed voor te bereiden dienen deze 2 maanden vooraf bekend te zijn.
- Optimalisatie cyclus
    - September t/m december (post seizoen)
    - Doel: verbeteren van bestaande functionaliteiten en technische uitlijning tussen de diverse modules en de core.
        - Indien van toepassing ook het optimaliseren van de componenten binnen de IT Suite.
    - Deadline wijzigingsverzoekentechnisch: 1september.
        - Deze verzoeken ontstaan vanuit de wijzigingen in de architectuur cyclus en zijn z.s.m. bekend bij de module ontwikkelaars.
    - Deadline wijzigingsverzoeken functioneel: 15 september.
        - Deze verzoeken ontstaan vanuit de ervaringen in het seizoen en dienen uiterlijk 2 weken hierna bekend te zijn bij de module ontwikkelaars.
		
## Supported Browsers:
Chrome 80+, Edge 80+, Firefox 74+, Safari 13+

## Changelog

Bolded styling surrounded by emojis indicates the major release focus.

- CRV	 Status		 Date		Release series	Released by
- v0.8.6 RC (6)		(t.b.d.)	Beluga 600		Core team
    - **Online portal op basis van CSS design framework for mobile apps**
    - Materialize CSS Framework v0.100.1 implemented as new front-end for Club.Redders.
    - Updated .htaccess for web-authentication only with restrictive deny.
    - My C.R envoironment is now also available inside C.R (previously only when included to your website).
- v0.8.5 RC (5)		(3/28/2017)	Beluga 600		Core team
    - **Product modulaire opbouw**
    - Online portal is modulair opgezet ipv een enkele php file voor meer flexibiliteit.
- v0.8.4 RC (4)		(3/13/2017)	Beluga 600		Core team
    - **Product breede web-authenticatie**
    - Authenticatie tegen WP ipv .htaccess/.htpasswd bestanden
- v0.8.3 RC (3)		(6/23/2016)	Beluga 600		Ruud Borghouts
    - **Weekindeling**
    - EBT kan nu weekindelingen printen voor de ASC en 809.
    - Alle output bestanden hebben een vergelijkbare layout.
    - Excel authenticatie tegen online portal en backup procedure verbeterd.
    - Print opdrachten worden nu allemaal voorzien van een standaard naamgeving.
    - Eerste set van de nieuwe proces/werkinstructies toegevoegd aan de release package.
- v0.8.1 RC (2)		(6/14/2016)	Beluga 600		Ruud Borghouts
    - **Online portal**
    - EBT op basis van data import en automatische online EBT import.
    - Gebruikershandleiding is naar een eigen set documenten verplaatst.
    - Versie nummering is uitgebreid naar 3 posities.
- v0.8.0 RC (1)		(6/2/2016)	Beluga 600		Ruud Borghouts
    - **Bron data gemigreerd naar bondsledenadministratie én competentiekaarten module**
    - EBT op basis van bondsledenadministratie data via een handmatige .csv export en automatische EBT import.
    - Interne data (uit de vorige versies op basis van ST-RBM) is verwijderd, inclusief bijbehorende tabbladen.
    - Berekening van interne rollen en diploma's vind nu plaats op de achtergrond i.p.v. bij de postindeling.
    - Competentiekaarten module toegevoegd welke voor alle bewakers een competentiekaart genereerd.
    - Macro knop toegevoegd waarmee de competentiekaarten worden geprint.
- v0.7.0 Beta		(8/7/2015)	Tonijn			Ruud Borghouts
    - **Gebruik postindeling verbeterd**
    - Posities gelijk gemaakt aan de post, het volgnummer word nu op de achtergrond geregeld.
    - Sorterings issue opgelost bij gelijke ervaring én leeftijd (of ontbreken van deze data).
    - Macro knop toegevoegd waarmee de externe data word vernieuwd en alles word herberekend.
    - Macro knop toegevoegd waarmee de planning als PDF word opgeslagen.
    - Macro knop toegevoegd waarmee de verzendlijst voor de enquete van die week word aangemaakt.
    - Macro knop toegevoegd waarmee de indeling en enquete verzonden worden naar de SL beheerders.
    - Macro knop toegevoegd om de applicatie modus te testen (in ontwikkeling).
    - Macro toegevoegd die bij openen en afsluiten het document optimaliseerd.
    - SplashScreen toegevoegd tijdens de voorberekeningen van het document bij openen.
    - Release data om tabblad Info verbeterd en uitgebreid met geplande features.
- v0.6.0 Pre-Beta	(7/22/2015)	Development		Ruud Borghouts
    - **Postindeling automatisch gesorteerd**
    - Posities worden gevuld op basis van meest naar minste weken ervaring.
    - Op het tabblad Bron-Commissie ook een hulpkolom voor leeftijd in dagen toegevoegd om bij gelijke ervaring te sorteren op leeftijd.
    - Indien iemand bewaakt en (geen) pasfoto heeft word de achtergrond grijs gekleurd.
    - Toelichting toegevoegd op het tabblad info.
- v0.5.0 A-Bug-fix	(7/14/2015)	Development		Ruud Borghouts
    - **Bug-fixes doorgevoerd t.a.v gebruik**
    - Controle op dubbele postposities toegevoegd.
    - Macroscript aangepast zodat ook de positie 28.7 in de nieuwe layout van een pasfoto word voorzien.
- v0.4.0 Alpha		(7/11/2015)	Development		Ruud Borghouts
    - **Nieuwe layout**
    - Nieuwe layout (nieuw tabblad Postindeling/PIv1) doorgevoerd i.v.m. de leesbaarheid van de postindelingen.
- v0.3.0 Pre-Alpha	(7/1/2015)	Development		Ruud Borghouts
    - **Erv. afronden technisch verbeterd**
    - Gemiddelde ervaring per post word nu afgerond weergegeven in de postindeling.
- v0.2.0 Init VBA	(6/27/2015)	Development		Ruud Borghouts
    - **Data website aangepast op script**
    - Namen van de pasfoto's gecorrigeerd op de webserver zodat deze juist ingeladen worden door het script.
    - De celindeling van het rooster is veranderd tussen de demo en versie 0.1, deze is nu doorgevoerd in het macroscript voor de pasfotos. Bewakers week 27 aangepast in de bron data.
- v0.1.0 Init rel.	(6/26/2015)	Development		Ruud Borghouts
    - **Initiele EBT voor het maken en printen van de bewakingsroosters op basis van Excel met oude (Access) DB data**
    - Postindeling invullen incl. foto op basis van beschikbare pasfotos.
    - bondsledenadministratie-EBT vergelijking maken, wie zit in bondsledenadministratie en niet in de EBT data en vica versa.
    - Ervaring word geteld t/m seisoen 2014 (formule moet (nog) elke week worden aangepast voor actuele erv.).
    - Deze tool is de basis voor een database registratie in de bondsledenadministratie die de roosters en competentiekaarten uitprint via een csv export in/met Excel.
- Demo Concept		(5/29/2015)	Development		Ruud Borghouts
    - **Mock-up indeling/compkaart systeem**
    - Demonstratie geven van de mogelijkheden van een rooster/competentiekaart generator op basis van Excel.

## Planned feature releases

Bolded styling surrounded by emojis indicates the major release focus.

| CRV | Status | Date | Release series | Release focus | Released by |
| --- | --- | --- | --- | --- | --- |
| v0.8.7 | RC (7) | (t.b.d.) | Beluga 600 | Online portal uitbreiding met installatie/update script | Core team |
| v0.8.8 | RC (8) | (t.b.d.) | Beluga 600 | Alle waardes zijn variabel, te configureren in online configuratie bestanden | Core team |
| v0.8.9 | RC (9) | (t.b.d.) | Beluga 600 | Bux-fixes uit voorgaande release candidates | Core team |
| v0.9.0 | RTM | (t.b.d.) | Leng | Volledig online configureerbare release welke automatisch kan updaten | Core team |
| v1.0.0 | GA | (t.b.d.) | Zalm	| Bug-fixes uit de RTM, update zou automatisch moeten kunnen uitrollen | Core team |

## Sitemap

```
   clubredders/
   |--css/
   |  |--style.css
   |  |--materialize.css
   |  |--materialize.min.css
   |
   |--fonts/
   |  |--roboto/
   |
   |--images/							Map met SVG images.
   |  |--crm-photo-notavailable.svg
   |  |--imageloader.html
   |  |--logo.svg
   |  |--logo-custom.svg
   |  |--logo-square.svg
   |  |--squareimageloader .html
   |
   |--js/
   |  |--init.js
   |  |--materialize.js
   |  |--materialize.min.js
   |
   |--modules/							Map met functie code.
   |  |--accounting/
   |  |--contribution/
   |  |--core/
   |  |--customscheduling/
   |  |  |--/
   |  |--diplomamanagement/
   |  |  |--/
   |  |--import/						Module voor het inlezen van csv bestanden uit externe systemen.
   |  |--mailinglists/
   |  |--membermanagement/				Module voor het uploaden en bijsnijden van een pasfoto door het lid zelf. / Module voor het uploaden van meerdere pasfotos van leden door het kader.
   |  |  |--/
   |  |--mycr/
   |  |--pdfmerger/
   |  |  |--/
   |  |--sdem/							ExterneDataConnector, leest de ingelezen csv data uit de C.R database en maakt deze beschikbaar voor de C.R ExcelDataModule.
   |
   |--util/								Map met functie code.
   |  |--msgraph/
   |  |  |--composer.json
   |  |  |--composer.lock
   |  |  |--index.php
   |  |  |--mailtemplate.html
   |  |  |--msgraph.class.php
   |  |  |--user.class.php  
   |  |--clubrescue.sql
   |  |--database.class.php
   |  |--dbupdate.php
   |  |--env.example.ini
   |  |--utility.class.php
   |
   |--LICENSE
   |--style.css
   |--.htaccess
   |--README.md							Dit document met basis informatie en versie historie.
   |--auth.php
   |--error.php
   |--footer.php
   |--gitlab-pull.php
   |--header.php
   |--index.php							Club.Redders core waarvandaan de modules gepresenteerd worden op basis van de ingelogde gebruiker.   
   |--wp-authenticate.php				Security module voor WordPress authenticatie.   
   |--favicon.ico
   |--.gitignore
   
   crbin/                       		Map met binaire bestanden die buiten de public_html folder moet worden geplaatst.
   |--backup/							Map voor backups van vorige Excel tools, CSV imports en pasfotos.
   |--excel/							Map voor Excel tools.
   |--import/							Map voor CSV uploads.
   |--pasfotos/							Map voor pasfotos uploads.
   |--uploads/							Map voor documenten uploads.
   
   crapp/                      			Map voor het toekomstige framework.
```
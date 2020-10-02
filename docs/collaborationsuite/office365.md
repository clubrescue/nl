# Werkinstructie Office 365 beheer

## Uitgangspunten

Dit document wordt nog uitgewerkt met de toelichting vanuit het onderzoek naar de optimale inrichting van Office 365 voor de vereniging. Uit deze toelichting blijkt namelijk waarom bepaalde inrichting keuzes zijn gemaakt en bepaalde waarde in specifieke attributen (dienen te) worden overgenomen.

In dit document is uitgegaan van het volgende (resultaat van het onderzoek);

- De Office 365 omgeving vervangt;
    - Dropbox door SharePoint (via Teams).
    - E-mail forwards door Exchange 365 met een nieuw mail adres format voornaam.achternaam@mydomain.org. Dit format is eenvoudig met de gegevens in Club.Redders te genereren bij automatische user provisioning.
    - Teams als het centrale ingangspunt voor kader, functionarissen, de ledenraad en VCP&#39;s. Teams _kan_ daarnaast ook de WhatsApp groepen vervangen en voorzien in een online video conferencing tool.
- Office 365 moet (uiteindelijk) een volledig geautomatiseerde user provisioning (_kunnen_) ondersteunen vanuit Club.Redders. Hierbij worden leden opgevoerd of van een kader/ledenraad/etc. functie voorzien in Club.Redders waarna deze informatie wordt doorgezet naar Club.Redders. Vanuit Club.Redders kunnen gebruikers vervolgens worden gesynchroniseerd met de Office 365 omgeving. Leden die verwijderd zijn worden in Office 365 gedisabled waarna een verzoek naar de secretaris wordt gestuurd om de gebruiker daadwerkelijk te verwijderen. Automatisch verwijderen kan ook maar dit kan bij een foutieve sync ongewenste situaties opleveren.
    - Met kunnen wordt beoogd dat alles wat handmatig wordt ingericht/beheert ook automatisch moet kunnen functioneren zonder extra licentie kosten (noot, veel functionaliteiten bleken tijdens het onderzoek extra P1/2 licentie kosten met zich mee te brengen). Door de stappen te volgen in dit document kan t.z.t. alles geautomatiseerd worden zonder dat verdere aanpassingen of kosten nodig zijn.
- De kader laptop (en waar mogelijk overige appraten) worden beheert door onze Office 365 omgeving waardoor alle kaderleden met hun O365 account kunnen inloggen op de laptop.
- Het inlog id is LIDID@mydomain.org dit zal tevens het inlog id zijn van alle overige accounts die je als lid nodig hebt voor de vereniging.
    - Office 365 zelf, maar ook indien SSO mogelijk is voor overige systemen die tegen onze O365 omgeving authentiseren.
        - WordPress en daarmee Club.Redders kunnen tegen O365 gaan authentiseren.
    - Forms (kan authentiseren tegen LDAP maar het is nog niet zeker of de AAD daaronder valt).
    - Accounts bij derden (worden aangemaakt als [LIDID@mydomain.org](mailto:LIDID@mydomain.org)). Hiermee hoeven leden i.i.g. maar een inlog ID te onthouden en wijzigt dit ID niet indien SSO later alsnog mogelijk wordt.
- Alle leden worden (t.z.t.) opgevoerd in Office 365 als lid waarbij hun account **niet** wordt weergegeven in de GAL.
    - Alle leden worden (t.z.t.) ook opgevoerd in Office 365 als contact. Deze contacten kunnen automatisch in maillijsten worden gezet vanuit Club.Redders.
- Kaderleden, functionarissen, ledenraad en VCP-ers krijgen extra rechten in Office 365. Daarnaast wordt hun account wel weergegeven in de GAL totdat deze extra rechten worden ingetrokken.
- Alle gebruikers zijn onderworpen aan een verplichting tot MFA en SSPR.
    - Enkel de 2 NPA&#39;s voor scripted beheer en SASL zijn hiervan uitgezonderd.
- Alle gebruikers worden als gebruiker opgevoerd in O365, zonder beheer toegang.
- Naast gewone gebruikers bestaan er 1+n Global Administrator accounts voor O365.
    - Hoofdbeheerders hebben één kale E1 licentie zonder sublicenties (apps). Voor niet beheer functionaliteiten moeten beheerders hun reguliere account gebruiken.
    - Deze accounts gebruiken ook het lid nummer van de betreffende beheerder máár de eerste letter &quot;D&quot; is vervangen door &quot;G&quot; van globale beheerder. (Voor niet brigades is het advies indien de eerste letter een &quot;G&quot; is uit te wijken naar de &quot;H&quot; van hoofdbeheerder).
 Verder is het login domein van beheer accounts @myfulldomain.onmicrosoft.com
    - Naast de gebruiker gebonden beheer accounts bezit de vereniging een kluis account waarbij het relatie nummer van de vereniging (bij de bond) wordt gebruikt (waarbij ook de &quot;D&quot; is vervangen door &quot;G&quot;). Aan dit account is ook een Azure abonnement gekoppeld voor eventuele script jobs die moeten lopen voor de automatische syncs indien geen gebruik kan worden gemaakt van de Microsoft Graph API.

- Binnen de O365 omgeving wordt enkel gebruik gemaakt van Office 365 groepen.
    - Deze groepen kunnen vanuit verschillende plekken in O365 worden aangemaakt door elke gebruiker. De gentlemen agreement is gemaakt dat niemand dit doet behalve bestuur/webmasters. Zodoende worden groepen altijd juist aangemaakt omdat de plek waar een groep wordt aangemaakt voor en nadelen met zich meebrengt.
    - Groepen worden aangemaakt vanuit;
        - Het beheercentrum – groepen;
            - Met een naam die begint met een hoofdletter en zonder @mydomain.org.
Indien de groep ook wordt opgevoerd als team door in Teams daarna de groep te promoten tot een team.
             - Met een naam bestaande uit volledig kleine letters en met @mydomain.org indien de groep niet gepromoot wordt als team en enkel gebruikt wordt als extra mailgroep (we maken geen gebruik van gedeelde postvakken omdat enkel O365 groepen worden ingezet in lijn met de visie van Microsoft).
        - Outlook – groepen;
            - Met een naam bestaande uit volledig kleine letters en met @mydomain.org indien de groep niet gepromoot wordt als team en enkel gebruikt wordt als extra mailgroep **én** daarnaast ook voorzien moet kunnen worden van submappen. Een O365 groep die is aangemaakt vanuit het beheercentrum kan geen mappen bevatten in de gedeelde mailbox terwijl een O365 groep aangemaakt vanuit Outlook dat wel kan.
        - Teams;
            - Wordt vooralsnog niet ingezet om groepen aan te maken. Groepen in teams genereren wel een mailadres maar deze is niet benaderbaar vanuit Outlook/GAL. Dit levert een ongewenste situatie op.
    - Naast O365 groepen is er één uitzondering en is er wél een gedeelde mailbox [noreply@mydomain.org](mailto:noreply@mydomain.org) aangemaakt om als SASL adres ingezet te worden.

## Gebruikersbeheer

Binnen de vereniging gebruiken we ten aanzien van het gebruikersbeheer binnen Office 365 de termen;

- Lid, is een lid van de vereniging, al dan niet bewakend.
    - Deze leden krijgen een Office 365 account met een beperkte E1 licentie, zonder rechten en zonder e-mail adres.
    - Alle reguliere leden hebben (uiteindelijk) een gebruikersaccount nodig binnen de Office 365 omgeving. Dit account zal gebruikt worden voor (SSO) toegang tot de website, Club.Redders en alle overige tooling die binnen de vereniging in gebruik is.
    - Initieel krijgen alleen leden met een actieve functie een account. Zodra dit voor iedereen werkt kan WordPress aangepast worden om SSO via Office 365 te ondersteunen en kunnen alle overige leden ook worden voorzien van een account.
    - We spreken bij wijzigingen bij deze leden/gebruikers over;
        - Nieuw lid (instroom);  
          Dit is een (nieuw) lid van de vereniging welke nog geen Office 365 account heeft en deze dient te krijgen.
        - Oud lid (uitstroom);  
          Dit is een lid van de vereniging welke zijn lidmaatschap heeft opgezegd en waarvoor het bestuur de opzegging heeft goedgekeurd (lees het lid heeft geen contributie achterstand) met een Office 365 account welke dient te worden opgeheven.
- Lid met actieve functie, is een lid van de vereniging welke zich inzet in de functie als kaderlid, functionaris, vertrouwenscontactpersoon of in de ledenraad zit.
    - Voor deze leden wordt hun Office 365 account voorzien van extra opties binnen de E1 licentie, een e-mail adres en extra rechten op mailgroepen/teams.
    - We spreken bij wijzigingen in deze functies over;
        - Lid krijgt actieve functie (doorstroom);  
          Een lid (reguliere gebruiker in Office 365) welke nog geen actieve functie heeft gaat deze beoefenen. Daarvoor dient hun Office 365 account voorzien te worden van extra opties binnen de E1 licentie, een e-mail adres en extra rechten op mailgroepen/teams.
        - Lid wijzigt van actieve functie (doorstroom);  
          Een lid met actieve functie wijzigt van functie. Daarvoor dienen de rechten op mailgroepen/teams te worden aangepast van hun de oude functie naar de nieuwe functie.
        - Lid stopt met actieve functie (doorstroom);  
          Een lid met actieve functie stopt met het vervullen van actieve functies. Daarvoor dient de E1 licentie weer beperkt te worden, het e-mail adres opgeheven en de rechten voor mailgroepen/teams te worden verwijderd.
    - Voor alle wijzigingen van lid naar lid met actieve functie of wijzigingen bij leden met een actieve functie dienen ook de attributen geupdate te worden omdat op basis daarvan rechten worden toegekend binnen de website.

De volgende situaties zijn mogelijk bij het beheer van gebruikers;

- Instroom
    - Nieuw lid.
    - Nieuw lid welke direct start met een actieve functie.  
      (instroom direct gevolgd met doorstroom).
- Doorstroom
    - Lid krijgt actieve functie.
        - Indien het lid de functie webmaster krijgt zie de opmerking hieronder.
    - Lid wijzigt van actieve functie.
        - Wordt een lid (met actieve functie) webmaster?
 Dan wordt zijn reguliere account aangepast naar lid met actieve functie webmaster, maar net als alle andere gebruikers krijgt dit account géén beheer rechten. In plaats daarvan krijgen webmasters een extra account welke alleen beheer rechten krijgt en geen andere rechten. Hiermee wordt voorkomen dat voor alle activiteiten met hoge bevoegdheden dient te worden ingelogd.
    - Lid stopt met actieve functie.
        - Stopt een lid met actieve functie als webmaster?  
          Dan dient naast de aanpassingen van zijn reguliere account, ook zijn of haar beheer account te worden verwijderd.
- Uitstroom
    - Lid meld zich af.
    - Lid met actieve functie meld zich af.  
      (doorstroom direct gevolgd met uitstroom).

Een nieuw lid welke een actieve functie heeft (per 1-1-2019) is bij de initiële inrichting van Office 365 aangemaakt. Een nieuw lid welke vanaf heden een actieve functie krijgt dient dus eerst als gebruiker te worden aangemaakt volgens het instroom proces en daarna via het doorstroom proces te worden voorzien van de benodigde rechten etc. Een oud lid welke bij het opzeggen van zijn lidmaatschap een actieve functie had dient eerst als actief lid terug gezet te worden naar regulier lid via het doorstroom proces en daarna via het uitstroom proces verwijderd te worden als gebruiker binnen Office 365.

Zorg dat voor alle wijzigingen de secretaris de gegevens uit het externe ledenadministratie systeem heeft gesyncroniseerd met Club.Redders en genereer de O365 meta data door daarna deze pagina aan te roepen:  
[https://mydomain.org/clubredders/edp-aad1id.php](https://mydomain.org/clubredders/edp-aad1id.php)

Office 365 wordt actief voorzien van nieuwe functies, wijzigingen van het licentiemodel en gebruikers interfaces.
Het heeft daarom geen meerwaarde veel screenshots op te nemen van Office 365. Dit wordt om deze reden zoveel mogelijk voorkomen.

### Instroom

#### Nieuw lid

Log in als beheerder in het beheercentrum en ga naar Gebruikers &gt; Actieve gebruikers &gt; Gebruiker toevoegen. Neem de gegevens als volgt over vanuit C.R [https://mydomain.org/clubredders/aadusers.php](https://mydomain.org/clubredders/aadusers.php);

- Login gegevens;
    - Voornaam Source\_GivenName
    - Achternaam Source\_Surname
    - Weergavenaam Source\_DisplayName
    - Gebruikersnaam Source\_UserPrincipalName
    - Domein mydomain.org voor gebruiker accounts
    - Locatie Source\_Country\*
- Contactgegevens
    - Functie Source\_JobTitle
    - Afdeling Source\_Department
    - Kantoor n.v.t.
    - Telefoon (werk) n.v.t. / Placeholder\_TelephoneNumber
    - Mobiele telefoon Source\_Mobile
    - Faxnummer n.v.t./ Placeholder\_FacsimileTelephoneNumber
    - Adres Source\_StreetAddress
    - Plaats Source\_City
    - Provincie n.v.t.
    - Postcode Source\_PostalCode
    - Land of regio Source\_Country\*
- Wachtwoord
    - [X] Wachtwoord automatisch genereren
    - [X] Deze gebruiker het wachtwoord laten wijzigen bij de eerste keer aanmelden
- Rollen
    - [X] Gebruiker (geen beheerderstoegang)
    - Alternatief e-mailadres Source\_OtherMails
- Productlicenties
 LET OP: Zet alleen Office 365 Enterprise E1 aan **én** vink alle sublicenties uit;
    - [X] Office 365 Enterprise E1
        - [ ] MyAnalytics
        - [ ] Office Mobile-apps voor Office 365
        - [ ] Taken (abonnement 1)
        - [ ] Microsoft Forms (Abonnement E1)
        - [ ] Microsoft Stream for O365 E1 SKU
        - [ ] Microsoft StaffHub
        - [ ] Flow for Office 365
        - [ ] PowerApps for Office 365
        - [ ] Microsoft Teams
        - [ ] Office Online
        - [ ] Microsoft Planner
        - [ ] Sway
        - [X] Mobile Device Management voor Office 365
Deze app wordt toegewezen op organisatieniveau.
        - [ ] Yammer Enterprise
        - [ ] Skype voor Bedrijven Online (Abonnement 2)
        - [ ] SharePoint Online (Abonnement 1)
        - [ ] Exchange Online (Abonnement 1)
    - [ ] Microsoft Flow Free
    - [ ] Power BI (gratis)
- Klik nu op toevoegen en vink op de volgende pagina [X] Wachtwoord verzenden per e-mail aan en vul daarna bij het veld &quot;Nieuw wachtwoord per e-mail verzenden naar de volgende geadresseerden \*&quot; het Source\_OtherMails adres in.
- Ga nu in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangemaakte gebruiker naar de MFA instellingen onder Account &gt; Meervoudige verificatie &gt; Meervoudige verificatie beheren. Selecteer de betreffende gebruiker en selecteer inschakelen in het rechter menu onder quick steps en bevestig MFA in de pop-up via de knop multi-factor auth inschakelen en klik op sluiten.
- Ga tenslotte in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangemaakte gebruiker naar de E-mail instellingen onder E-mail &gt; Weergeven in algemene adreslijst &gt; Zichtbaarheid van algemene adreslijst beheren. Zet Weergeven in de adreslijst van mijn organisatie **uit** en sluit de gebruiker.
    - ~~Optie niet beschikbaar? Ga dan in het beheercentrum onder Beheercentrums naar Exchange.~~
    - Mogelijk kan dit vervallen omdat de gebruiker zonder Exchange Online licentie geen mail adres heeft.

De standaard gebruiker is nu aangemaakt.

#### Nieuw lid welke direct start met een actieve functie

Volg eerst de stappen uit 2.1.1 en ga daarna verder met de stappen in 2.2.1

### Doorstroom

#### Lid krijgt actieve functie

Log in als beheerder in het beheercentrum en ga onder Gebruikers &gt; Actieve gebruikers naar de gebruiker die de extra rechten dient te krijgen t.b.v. een actieve functie binnen de vereniging.

- Pas onder Account &gt; Contactgegevens &gt; Contactgegevens beheren &gt; Contactgegevens de volgende 2 attributen aan vanuit C.R [https://mydomain.org/clubredders/aadusers.php](https://mydomain.org/clubredders/aadusers.php);
    - Functie Source\_JobTitle
    - Afdeling Source\_Department
- Voeg onder Licenties en apps &gt; Licenties de volgende licenties toe;
    - [X] Microsoft Flow Free
    - [X] Power BI (gratis)
- Voeg onder Licenties en apps &gt; Apps alle apps toe onder de Office 365 Enterprise E1 licentie m.u.v. MS Forms en Yammer.
    - [X] Office 365 Enterprise E1
        - [X] Exchange Online (Abonnement 1)
        - [X] Flow for Office 365
        - [ ] Microsoft Forms (Abonnement E1)
 i.p.v. Microsoft Forms gebruikt de vereniging Club.Forms
        - [X] Microsoft Planner
        - [X] Microsoft StaffHub
        - [X] Microsoft Stream for O365 E1 SKU
        - [X] Microsoft Teams
        - [ ] Mobile Device Management voor Office 365
 Deze app wordt toegewezen op organisatieniveau.
        - [X] MyAnalytics
        - [X] Office Mobile-apps voor Office 365
        - [X] Office Online
        - [X] PowerApps for Office 365
        - [X] SharePoint Online (Abonnement 1)
        - [X] Skype voor Bedrijven Online (Abonnement 2)
        - [X] Sway
        - [X] Taken (abonnement 1)
        - [ ] Yammer Enterprise
 Yammer wordt vooralsnog niet ingezet binnen de vereniging.
    - [X] Microsoft Flow Free
        - [X] Common Data Service
        - [X] Flow Free
    - [X] Power BI (gratis)
        - [X] Power BI (gratis)

Bevestig de wijzigingen met de knop opslaan de √ knop.

- Ga nu in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangepaste gebruiker naar de E-mail instellingen onder E-mail &gt; Weergeven in algemene adreslijst &gt; Zichtbaarheid van algemene adreslijst beheren. Zet Weergeven in de adreslijst van mijn organisatie **aan** en sluit de gebruiker.
- Ga tenslotte in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangemaakte gebruiker naar de E-mail instellingen onder E-mail &gt; Meer acties &gt; Eigenschappen van Exchange bewerken. De specifieke Exchange instellingen van deze gebruiker worden nu geopend. Ga hier naar e-mailadres en pas de e-mail instellingen als volgt aan;
    - Wijzig;
        - SMTP – LIDID@mydomain.org
    - Naar;
        - smtp – LIDID@mydomain.org
    - Door;
        - Op het + icoon te klikken en een nieuw SMTP adres aan te maken.  
          Vul onder E-mailadres het Source\_EmailAddresses in en vink tenslote de optie Hiervan het antwoordadres maken aan. Hiermee wordt het mailadres gezet op het vereniging format en blijft het LIDID@mydomain.org de inlognaam van de gebruiker.
Verder zie je bij een reeds ingelogde gebruiker mogelijk nog een of meer van de volgende opties aan welke genegeerd kunnen worden;
        - SIP – LIDID@mydomain.org
        - SPO – SPO\_cc2-28-a-ac6f-641@SPO\_b5-da22-48ff-9f9c-613b24bfc673

De gebruiker is nu geupgrade naar een gebruiker voor actieve leden.  
Gaat dit lid de functie van webmaster uitoefenen? Volg dan ook de stappen voor het aanmaken van een beheer account in 2.2.4.

#### Lid wijzigt van actieve functie

Log in als beheerder in het beheercentrum en ga onder Gebruikers &gt; Actieve gebruikers naar de gebruiker die van actieve functie wijzigt.

- Pas onder Account &gt; Contactgegevens &gt; Contactgegevens beheren &gt; Contactgegevens de volgende 2 attributen aan vanuit C.R [https://mydomain.org/clubredders/aadusers.php](https://mydomain.org/clubredders/aadusers.php);
    - Functie Source\_JobTitle
    - Afdeling Source\_Department

Gaat dit lid de functie van webmaster uitoefenen? Volg dan ook de stappen voor het aanmaken van een beheer account in 2.2.4

Verder zijn de eigenaren van de Office 365 groepen zelf verantwoordelijk voor het op en afvoeren van gewijzigde actieve leden.

#### Lid stopt met actieve functie

Log in als beheerder in het beheercentrum en ga onder Gebruikers &gt; Actieve gebruikers naar de gebruiker die minder rechten dient te krijgen t.b.v. het stoppen met een actieve functie binnen de vereniging.

- Ga nu in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangepaste gebruiker naar de E-mail instellingen onder E-mail &gt; Weergeven in algemene adreslijst &gt; Zichtbaarheid van algemene adreslijst beheren. Zet Weergeven in de adreslijst van mijn organisatie **uit** en sluit de gebruiker.
- Pas onder Account &gt; Contactgegevens &gt; Contactgegevens beheren &gt; Contactgegevens de volgende 2 attributen aan vanuit C.R [https://mydomain.org/clubredders/aadusers.php](https://mydomain.org/clubredders/aadusers.php);
    - Functie Source\_JobTitle
    - Afdeling Source\_Department
- Verwijder onder Licenties en apps &gt; Licenties de volgende licenties;
    - [X] Office 365 Enterprise E1
        - [ ] MyAnalytics
        - [ ] Office Mobile-apps voor Office 365
        - [ ] Taken (abonnement 1)
        - [ ] Microsoft Forms (Abonnement E1)
        - [ ] Microsoft Stream for O365 E1 SKU
        - [ ] Microsoft StaffHub
        - [ ] Flow for Office 365
        - [ ] PowerApps for Office 365
        - [ ] Microsoft Teams
        - [ ] Office Online
        - [ ] Microsoft Planner
        - [ ] Sway
        - [X] Mobile Device Management voor Office 365
Deze app wordt toegewezen op organisatieniveau.
        - [ ] Yammer Enterprise
        - [ ] Skype voor Bedrijven Online (Abonnement 2)
        - [ ] SharePoint Online (Abonnement 1)
        - [ ] Exchange Online (Abonnement 1)
        - [ ] Yammer Enterprise
 Yammer wordt vooralsnog niet ingezet binnen de vereniging.
    - [ ] Microsoft Flow Free
        - [ ] Common Data Service
        - [ ] Flow Free
    - [ ] Power BI (gratis)
        - [ ] Power BI (gratis)  
Bevestig de wijzigingen met de knop opslaan de √ knop.
- De E-mail instellingen in het beheercentrum onder Gebruikers &gt; Actieve gebruikers &gt; E-mail instellingen onder E-mail &gt; Meer acties &gt; Eigenschappen van Exchange met de SMTP/SIP/SPO gegevens hoeven niet te worden aangepast. Deze instellingen mogen behouden blijven. Door het verbergen het mail adres in de GAL is het adres al niet meer zichtbaar. Indien dit lid in de toekomst weer een actieve functie gaat beoefenen hoeft deze niet nogmaals opnieuw ingesteld te worden.

De gebruiker is nu gedowngrade naar een gebruiker voor reguliere/niet actieve leden.  
Stopt dit lid met de functie van webmaster? Volg dan ook de stappen voor het verwijderen van een beheer account in 2.2.4

#### Aanmaken en verwijderen van beheer accounts

Log in als beheerder in het beheercentrum en ga naar Gebruikers &gt; Actieve gebruikers &gt; Gebruiker toevoegen. Neem de gegevens als volgt over vanuit C.R [https://mydomain.org/clubredders/aadusers.php](https://mydomain.org/clubredders/aadusers.php);

- Login gegevens;
    - Voornaam Source\_GivenName
    - Achternaam Source\_Surname
    - Weergavenaam Source\_DisplayName + (Admin) vb Julia Doe (Admin)
    - Gebruikersnaam Source\_UserPrincipalName &gt; de &quot;D&quot; vooraan vervangen door &quot;G&quot;.
    - Domein @myfulldomain.onmicrosoft.com voor beheer accounts
    - Locatie Nederland (altijd Nederland kiezen voor beheer accounts)
- Contactgegevens
    - Functie PA voor persoonlijke accounts en NPA voor niet persoonlijke accounts
    - Afdeling Webmaster-GA (of Bestuur-GA voor de NPA van het bestuur)
    - Mobiele telefoon Source\_Mobile
- Wachtwoord
    - [X] Wachtwoord automatisch genereren
    - [X] Deze gebruiker het wachtwoord laten wijzigen bij de eerste keer aanmelden
- Rollen
    - [X] Globale beheerder
    - Alternatief e-mailadres Source\_OtherMails
- Productlicenties (enkel beheerderstoegang)
 LET OP: Zet alleen Office 365 Enterprise E1 aan **én** vink alle sublicenties uit;
    - [X] Office 365 Enterprise E1
        - [ ] MyAnalytics
        - [ ] Office Mobile-apps voor Office 365
        - [ ] Taken (abonnement 1)
        - [ ] Microsoft Forms (Abonnement E1)
        - [ ] Microsoft Stream for O365 E1 SKU
        - [ ] Microsoft StaffHub
        - [ ] Flow for Office 365
        - [ ] PowerApps for Office 365
        - [ ] Microsoft Teams
        - [ ] Office Online
        - [ ] Microsoft Planner
        - [ ] Sway
        - [X] Mobile Device Management voor Office 365
Deze app wordt toegewezen op organisatieniveau.
        - [ ] Yammer Enterprise
        - [ ] Skype voor Bedrijven Online (Abonnement 2)
        - [ ] SharePoint Online (Abonnement 1)
        - [ ] Exchange Online (Abonnement 1)
    - [ ] Microsoft Flow Free
    - [ ] Power BI (gratis)
- Klik nu op toevoegen en vink op de volgende pagina [X] Wachtwoord verzenden per e-mail aan en vul daarna bij het veld &quot;Nieuw wachtwoord per e-mail verzenden naar de volgende geadresseerden \*&quot; het Source\_OtherMails adres in.
- Ga nu in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangemaakte gebruiker naar de MFA instellingen onder Account &gt; Meervoudige verificatie &gt; Meervoudige verificatie beheren. Selecteer de betreffende gebruiker en selecteer inschakelen in het rechter menu onder quick steps en bevestig MFA in de pop-up via de knop multi-factor auth inschakelen en klik op sluiten.
- Ga tenslotte in het beheercentrum onder Gebruikers &gt; Actieve gebruikers naar de zojuist aangemaakte beheerder naar de E-mail instellingen onder E-mail &gt; Weergeven in algemene adreslijst &gt; Zichtbaarheid van algemene adreslijst beheren. Zet Weergeven in de adreslijst van mijn organisatie **uit** en sluit de gebruiker.
    - ~~Optie niet beschikbaar? Ga dan in het beheercentrum onder Beheercentrums naar Exchange.~~
    - Mogelijk kan dit vervallen omdat de gebruiker zonder Exchange Online licentie geen mail adres heeft.

Het globale beheerders account is nu aangemaakt.  
**Volg voor het verwijderen van een globale beheerders account de stappen in 2.3.1.**  
Verwijder echter nooit het NPA beheerders account van de vereniging (G123ABC).

### Uitstroom

#### Lid meld zich af

Log in als beheerder in het beheercentrum en ga onder Gebruikers &gt; Actieve gebruikers naar de gebruiker van het lid dat zich afmeld.

  - Kies onder het menu (3 verticale punten) achter de gebruiker voor de optie Gebruiker verwijderen. Alternatief kan men ook de gebruiker selecteren en dan in het menu (3 horizontale punten) bovenaan bij actieve gebruikers de optie Gebruiker verwijderen kiezen.

#### Lid met actieve functie meld zich af

Volg eerst de stappen uit 2.2.3 en ga daarna verder met de stappen in 2.3.1.

## Bijzondere beheer activiteiten

### Wijzigen mailadres Office 365 groep

Het wijzigen van een mailadres van een Office 365 groep is (in tegenstelling tot die van een gebruiker) niet mogelijk van uit het Office 365 beheercentrum, Exchange-beheercentrum of het Azure portal.

Het is uiteraard mogelijk een nieuwe groep aan te maken en de oude groep te verwijderen maar hiermee worden instellingen, gekoppelde rechten en gebruikers teniet gedaan. Ook wordt eventuele e-mail in de mailbox van de groep verwijderd.

Om deze te behouden kan het mailadres eenvoudig worden gewijzigd via PowerShell.

Instelleer in PowerShell de Exchange Online PowerShell V2 module indien je deze nog niet eerder hebt gebruikt.

Start hiervoor je PowerShell (ISE) prompt met beheerrechten en voer de volgende commando&#39;s uit;

``` powershell
Install-Module PowershellGet -Force
Update-Module PowershellGet
Set-ExecutionPolicy RemoteSigned
Install-Module -Name ExchangeOnlineManagement
Import-Module ExchangeOnlineManagement; Get-Module ExchangeOnlineManagement
Update-Module -Name ExchangeOnlineManagement
Import-Module ExchangeOnlineManagement; Get-Module ExchangeOnlineManagement
```

Maak nu connetie met Exchange Online met het volgende commando;

&gt; Connect-ExchangeOnline -UserPrincipalName \&lt;UPN&gt; -ShowProgress $true

Vervang hier &lt;UPN&gt; met jouw beheeraccount als user principal name formaat (bijvoorbeeld, GUPN@myfulldomain.onmicrosoft.com).

Je krijgt nu een pop-up waar je vervolgens dient in te loggen met je wachtwoord en vervolgens je MFA token.

Zodra je bent verbonden kun je de gegevens van de betreffende groep opvragen;

&gt; Get-UnifiedGroup -Identity &lt;naam van de groep&gt; (bijvoorbeeld &gt; Get-UnifiedGroup -Identity example-old).

Je krijgt dan de groep te zien;

Name DisplayName GroupType PrimarySmtpAddress

---- ----------- --------- ------------------

example-old\_6cf2afb2-44c7-88da-12x9-e969ff3cbbcf example-old@mydomain.org Universal example-old@mydomain.org

We gaan hier het PrimarySmtpAddress aanpassen. De DisplayName kan ook worden aangepast maar dat kan vanuit het Azure portal en staat in de volgende paragraaf uitgelegd;

&gt; Set-UnifiedGroup -Identity &lt;naam van de groep&gt; -PrimarySmtpAddress &lt;nieuw mailadres van de groep&gt; (bijvoorbeeld &gt; Set-UnifiedGroup -Identity example-old -PrimarySmtpAddress example-new@mydomain.org).

Vraag nu nogmaals de groepsinformatie op;

&gt; Get-UnifiedGroup -Identity example-old

Name DisplayName GroupType PrimarySmtpAddress

---- ----------- --------- ------------------

example-old\_6cf2afb2-44c7-88da-12x9-e969ff3cbbcf example-old@mydomain.org Universal example-new@mydomain.org

Je ziet nu dat het mailadres is gewijzigd. Het oude mailadres is nu als alias toegevoegd aan de groep. De groep blijft daar dus op bereikbaar.

Na het aanpassen van de DisplayName in de volgende paragraaf zal de groepsinformatie er zo uit kunnen komen te zien;

&gt; Get-UnifiedGroup -Identity example-old

Name DisplayName GroupType PrimarySmtpAddress

---- ----------- --------- ------------------

example-old\_6cf2afb2-44c7-88da-12x9-e969ff3cbbcf example-new@mydomain.org Universal example-new@mydomain.org

### Wijzigen naam Office 365 groep

De groepsnaam zelf kan gewijzigd worden vanuit het Azure portal op portal.azure.com.

Ga hier naar de Azure Active Directory en dan naar groepen. Klik op de groep die je wilt wijzigen en vervolgens op eigenschappen.

Wijzig de groepsnaam en de groepsbeschrijving indien van toepassing en klik op opslaan.

### Toestemming aan SAAS oplossingen van derden

Sommige SAAS oplossingen van derden ondersteunen SSO via je Office 365 account.

Een beheerder van de Office 365 omgeving kan hiervoor toestemming geven of deze intrekken.

Standaard ondersteund Office 365 SAML, SCIM of koppelingen op basis van eenmalige aanmelding met een wachtwoord.

#### Toekennen

Nader uit te werken.

#### Intrekken

Toestemming voor bedrijfstoepassingen kan gewijzigd of ingetrokken worden vanuit het Azure portal op portal.azure.com.

Ga hier naar Azure-services en dan naar Meer services. Hier vind je onder de categorie Identiteit de service Bedrijfstoepassingen.

Klik op de toepassing die je wilt wijzigen/intrekken en vervolgens op eigenschappen.

Wijzig de gewenste instellingen indien van toepassing en klik op opslaan of klik bovenin op Verwijderen om de toepassingsrechten in te trekken.
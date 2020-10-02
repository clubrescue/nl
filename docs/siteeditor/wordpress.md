# Werkinstructie WordPress beheer

## Uitgangspunten

Binnen de IT Suite voor non profits is voor [WordPress](https://wordpress.org/download/) gekozen als website/CMS. WordPress kan geheel naar eigen inzicht worden ingericht maar gebruikt als onderdeel van de suite 2 plugins;

- [SSO with AAD (for WordPress)](https://github.com/psignoret/aad-sso-wordpress) voor het opzetten van SSO vanuit Office 365.
- [Club.Redders-WP](https://github.com/clubrescue/clubrescue-wp) voor het integreren van de Mijn omgeving uit Club.Redders in WordPress.
 Deze plugin is alleen nodig indien je niet alle eindgebruikers wilt doorverwijzen naar de tool.

In dit document is uitgegaan van het volgende;

- De Office 365 omgeving is ingericht volgens de werkinstructie Office 365 beheer.
- WordPress is geïnstalleerd en up to date.
- Beide plugins zijn geïnstalleerd en up to date.
- De SSO with AAD plugin is geconfigureerd volgens dit document.
- Binnen Office 365 zijn de applicatie groepen aangemaakt volgens dit document.
    - In tegenstelling tot de werkinstructie Office 365 beheer worden voor externe applicaties wél andere groepen aangemaakt dan z.g.n. Office 365 groepen, namelijk security groups. Deze worden aangemaakt vanuit;
        - Het beheercentrum – groepen;
            - Met een naam volgens de volgende naamconventie;
                - App\_ als indicatie voor externe rechten groepen.
                - &lt;NaamApplicatie&gt;\_ naam van de externe applicatie.
                - &lt;NaamApplicatieRol&gt;\_ naam van de rol in de applicatie.
        - Bijvoorbeeld: App\_WordPress\_Administrator voor de applicatie WordPress en de rol Administrator in die applicatie.
        - Als beschrijving kan worden gekozen om de officiële beschrijving van de rechtengroep toe te voegen uit de documentatie van de betreffende applicatie.
     - Na het aanmaken van de groep kan deze worden voorzien van eigenaren en leden. Zoals gesteld in de werkinstructie Office 365 beheer zijn Verder zijn de eigenaren van de Office 365 groepen zelf verantwoordelijk voor het op en afvoeren van gewijzigde (actieve) leden.
         - Voor de App\_ groepen wordt het beheer vooralsnog uitgevoerd door de IT functionarissen. Zij worden tot op heden ingesteld als eigenaar.
         - De leden worden toegevoegd en verwijderd op verzoek van het bestuur. Zie hiervoor ook de standaard toekenning onder gebruikersbeheer.

- _Het SASL adres uit O365 kan indien_ _gewenst worden ingesteld voor het verzenden van E-mail berichten vanuit WordPress (_[_noreply@mydomain.org_](mailto:noreply@mydomain.org)_)._

## Gebruikersbeheer

Dit document houd de termen aan zoals gebruikt in de werkinstructie Office 365 beheer.

De volgende situaties zijn mogelijk bij het beheer van gebruikers;

- Instroom / nieuw lid.
    - Standaard krijgt een lid geen rechten binnen WordPress.
- Doorstroom / lid krijgt, wijzigt of stopt met actieve functie.
    - Lid krijgt actieve functie.
 Het lid wordt toegevoegd of verwijderd uit de gewenste App\_ groep(en).
 Standaard wordt hiervoor nu gehanteerd;
        - X: App\_WordPress\_Editor
        - Y: App\_WordPress\_Contributor
        - Z: App\_WordPress\_Contributor
        - IT: App\_WordPress\_Administrator

Deze wijzigingen worden niet standaard doorgevoerd in WordPress (niet gestest…). Log na de aanpassingen in O365 in op WordPress en _ **of** _ verwijder de betreffende
 gebruiker. Deze wordt bij de eerstvolgende aanmelding in WordPress opnieuw
 aangemaakt met de juiste rechten. _ **Of** _ zoek de gebruiker op en pas de
 rechtenwijzigingen ook door in WordPress zelf.

- Uitstroom / lid meld zich af.
      - Na het disabelen of verwijderen van het account in O365 kan een lid zich niet meer aanmelden in WordPress. Het account blijft (niet getest) wel in WordPress bestaan met de laatst toegekende rechten. Het advies is om de IT functionarissen te verzoeken een WordPress account dat niet meer nodig is te laten verwijderen. Indien een gebruiker content heeft toegevoegd/bewerkt dient het eigenaarschap hiervan toegekend te worden aan een andere gebruiker. Kies hierbij bij voor de voorzitter van dezelfde eenheid (werkgroep/commissie/bestuur). Indien niet mogelijk kies dan de secretaris. Indien dat ook niet mogelijk is, kies dan de voorzitter van het bestuur.

### Attribute mapping vanuit Office 365.

De volgende attributen worden vanuit Office 365 overgenomen in WordPress;

- Login gegevens;
    - GivenName First Name
    - Surname Last Name
    - DisplayName Display name publicly as
    - UserPrincipalName Username/Nickname/Email
- Rollen
    - Alle rollen van de App\_WordPress\_ groepen waarvan de gebruiker lid is.

## SSO with AAD (for WordPress) configuratie

### Algemeen

|||
| --- | --- |
| Display name | My Organisation Name |
| Domain hint | mydomain.org |
| Client ID | 115e93b9-98f9-4732-82bf-0cf79c0ed437 |
| Client secret | \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* |
| Redirect URL | https://mydomain.org/wp-login.php |
| Logout redirect URL | https://mydomain.org/ |
| Enable full logout | [X] |
| Field to match to UPN | Login Name |
| Match on alias of the UPN | [ ]  do not enable this option!\* |
| Enable auto-provisioning | [X] |
| Enable auto-forward to Azure AD | [X] |
| Enable Azure AD group to WP role association | [X] |
| Default WordPress role if not in Azure AD group | (None, deny access) |
\*) enabling matching on alias of the UPN will remove the domain name from the username. This will prevent apps based on WordPress authentication from matching usernames.

### WordPress role to Azure AD group map

| WordPress Role O365 Group Name | Azure AD Group Object ID |
| --- | --- |
| App\_WordPress\_Administrator | a8d7d44a-bacd-5caf-x841-d5421770453d |
| App\_WordPress\_Editor | 9cd102ds-c2d1-88c2-21d5-9ccf554bd054 |
| App\_WordPress\_Author | b88031dd-ccaa-45db-22ca-d44dd64d25d9 |
| App\_WordPress\_Contributor | 3addf9d9-b254-4a52-da44-201c4cc591bb |
| App\_WordPress\_Subscriber | 47dc8433-dc88-44cb-a1d6-545f1886c253 |

### Advanced

OpenID Connect configuration endpoint :
 https://login.microsoftonline.com/common/.well-known/openid-configuration

### Configuratie in Azure

Volg voor de configuratie van deze plugin aan de Azure zijde de plugin handleiding:

[https://github.com/psignoret/aad-sso-wordpress/blob/master/README.md](https://github.com/psignoret/aad-sso-wordpress/blob/master/README.md)

## Club.Rescue-WP configuratie

### Algemeen

|||
| --- | --- |
| My Club.Rescue pages | mijn-domain.org |
| Whitelabel (OTAP) | clubredders |
| Default source | label activities |
| Default variable | label activiteitenTable |
| Error message | Mijn MyDomain.org is tijdelijk niet beschikbaar i.v.m.<br />onderhoud. Probeer het later nog een keer. |

### Club.Rescue role to Azure AD group map

| Club.Rescue Role O365 Group Name | Azure AD Group Object ID |
| --- | --- |
| App\_ClubRedders\_Administrator | 429cb9a2-4925-48a4-a1c7-d146850dc1bb |
| App\_ClubRedders\_WP\_Editor | 88df8c75-f5ed-3b6e-8c85-ba8e66bb1ad6 |
| App\_ClubRedders\_WP\_Contributor | c881b850-c135-4948-c4e4-6fa28c226c3f |
| App\_ClubRedders\_Member | 707bca88-825d-5ab1-97c5-7ea8b7f5cd77 |

### Advanced

|||
| --- | --- |
| Club.Rescue link | [X] |
| Branch | (X) Master (default).<br />( ) Development (only for test environments). |

### Shortcodes

De actuele uitleg van de beschikbare shortcodes is beschikbaar op de configuratie pagina:

[https://mydomain.org/wp-admin/options-general.php?page=cr-wp](https://mydomain.org/wp-admin/options-general.php?page=cr-wp)

De volgende shortcodes zijn (enkel) beschikbaar binnen de pagina&#39;s welke zijn toegevoegd onder de configuratie &#39;My Club.Rescue pages&#39;; [crwp\_mycr] geeft de standard submodule en dataset weer uit Mijn Club.Redders zoals geconfigureerd in de configuratie &#39;Default source&#39; en &#39;Default variable&#39;. Deze shortcode heeft drie attributen die kunnen worden gebruikt om de opgevraagde data te wijzigen:

[crwp\_mycr otap=&quot;clubredders&quot; source=&quot;mycr-attributes&quot; table=&quot;lidTable&quot;] otap bepaalt de folder van de Club.Redders installatie die gebruikt wordt. Handig om de installatie te White labelen of data uit een test installatie op te vragen. source bepaalt de Mijn C.R submodule die wordt ingevoegd. table bepaalt de dataset uit de submodule die teruggegeven wordt.
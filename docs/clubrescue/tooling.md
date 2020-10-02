# Club.Redders & externe systemen

## App.Core

| | |
| --- | --- |
| Functionaliteiten | - Alle functionaliteiten die niet worden ondersteund door reeds beschikbare software. |
| Afhankelijkheden | - Office 365<br />- MachForm<br />- WordPress (indien gebruik wordt gemaakt van de plugin) |
| Architectuur | Core developer(s) |

- Core componenten
    - Generieke technische functionaliteiten
    - Bruikbaar in alle modules
    - Gedeeltes van modules kunnen t.z.t. overgaan naar de core
- Modules
    - Bevatten één enkele functionaliteit
    - Kunnen los van elkaar en de core ontwikkeld worden
    - Maken geen gebruik van andere modules
        - M.u.v. de jaarrooster module (afhankelijk van competenties module)

## Club.Redders

| ![Logo C.R](../assets/images/logo/logo_CR.png) ||
| --- | --- |
| Werkt - getest | - Vimexx. |
| Werkt - niet getest | - TransIP.<br />- Hostnet. |
| Werkt niet - getest | - PCextreme. |

- Software eisen;
    - SSL-certificaten (met auto renewal), SFTP, SSH, MariaDB, .htaccess, PHP 7.4 of hoger.
- Taken/kennis eisen IT functionaris;
    - Git, PHP, SQL, HTML, JS, Apache, MariaDB, phpMyAdmin, MVC principes, SSH, Microsoft Graph.
    - Couldhaves; ervaring met WordPress Plugin Development.

## Externe systemen

| ![Logo TechSoup](../assets/images/logo/logo_techsoup.png) ||
| --- | --- |
| Werkt - getest | - Sportlink.<br />- Rabobank CSV. |
| Werkt - niet getest | - Rabobank MT940. |
| Werkt niet - getest | - Geen producten bekend. |

- Software eisen extern ledenadministratie pakket;
    - CSV export van leden met attributen.
    - CSV export van bondsfuncties met attributen.
    - CSV export van bondsdiploma’s met attributen.
- Software eisen internetbankieren;
    - CSV export vantransactiesmetattributen.
    - MT940 export vantransactiesmetattributen.
- Taken/kennis eisen IT functionaris;
    - Het beheer van externe systemen valt buiten de scope t.a.v. het takenpakket en kennis vereiste van IT functionarissen.
- Advies: houd domeinregistratie en webhosting gescheiden tussen bestuur en IT functionarissen.
    - Zorg dat toegang van MFA is voorzien en bij voorkeur ook van persoonlijke accounts.

# App.Modules

```mermaid
graph LR;
    A(App.Core);
    B(C.R Core);
    C(C.R Modules);
    Q(DB Connections);
    R(Environment vars);
    S(SMTP);
    T(MS Graph);
    D(Mijn C.R);
    E(Ledenadministratie);
    F(Competenties);
    G(Weekroosters);
    H(Maillijsten);
    I(Contributie);
    J(Boekhouding);
    K(PDF-merger);
    L(Data imports);
    M(SDEM - modules);
    N(Core - Beheer);
    O(Club.Rescue-WP);
    P(Jaarrooster - onderzoek extra ITS4NP pakket);
    U(Logging);
    A --- B;
    A --- C;
    B --- Q;
    B --- R;
    B --- S;
    B --- T;
    C --- D;
    C --- E;
    C --- F;
    C --- G;
    C --- H;
    C --- I;
    C --- J;
    C --- K;
    C --- L;
    C --- M;
    C --- N;
    D --- O;
    G --- P;
    N --- U;
```

# Procesflow

```mermaid
graph TD;
    subgraph legend;
    id1([Begin/einde proces]);
    id2[Proces];
    id3[[Subproces]];
    id4{Beslissing};
    end;

    df1{Is iemand lid?};
    df1 --- Nee --> mm1;
    df1 --- Ja --> ae1;
    mm3 --> ae1;
    ae6 --> as1;

    subgraph membermanagement;
    mm1([Leden Administratie]);
    mm2[Inschrijf formulier - nieuwe leden];
    mm3[Toelating nieuwe leden];
    mm4[Wijzigen leden gegevens];
    mm5[Beëindiging lidmaatschap];
    mm1 --> mm2 --> mm3 --> mm4 --> mm5;
    end;

    subgraph activitiesenrollment;
    ae1([Inschrijving activiteiten]);
    ae2[Inschrijf formulier - activiteiten];
    ae3[Roosteren activiteiten];
    ae4[Bevestigen inschrijving/indeling];
    ae5[Indeling kader activiteit];
    ae6[Verzenden informatie naar kader];
    ae1 --> ae2 --> ae3 --> ae4 --> ae5 --> ae6;
    end;

    subgraph activitiesscheduling;
    as1([Administratie activiteiten]);
    as2[Roosteren activiteiten - incl. competenties & examens];
    as3[Rooster verwerken in C.R];
    as4[Versturen week enquête];
    as5[Opmerkingen n.a.v. activiteiten verwerken];
    as6[Competenties opvoeren];
    as1 --> as2 --> as3 --> as4 --> as5 --> as6;
    end;

    subgraph datasynchronization;
    ds1([Synchroniseren data bronnen]);
    ds2[Exporteren data uit bron];
    ds3[Importeren data in C.R];
    ds4[[Vergelijken data bron en C.R]];
    ds1 --> ds2 --> ds3 --> ds4;
    end;
```
# IT Suite for non profits

## High level view

| | | Product |
| --- | --- | --- |
| ![Logo Okta](../../assets/images/logo/icon_npst.png) | NONPROFIT SUPPORT TOOLING<br />Modulaire open source app voor maatwerk functionaliteiten | ![Logo C.R](../assets/images/logo/logo_CR.png) |
| ![Logo Okta](../../assets/images/logo/icon_idpvw.png) | COLLABORATION SUITE & SSO IdP<br />Één account voor toegang tot interne en externe diensten | ![Logo O365](../assets/images/logo/logo_O365.png) |
| ![Logo Okta](../../assets/images/logo/icon_wysiwygform.png) | FORM (WYSIWYG) EDITOR<br />Bouw eenvoudig veilige en versleutelde formulieren met procesflows | ![Logo MachForm](../assets/images/logo/logo_MachForm.png) |
| ![Logo Okta](../../assets/images/logo/icon_wysiwygsite.png) | SITE (WYSIWYG) EDITOR<br />Bouw en beheer eenvoudig je website en haar content | ![Logo WordPress](../assets/images/logo/logo_WP.png) |
| | | ![Logo TechSoup](../assets/images/logo/logo_techsoup.png) |

## IT Suite | IT services

```mermaid
graph BT;
    A((Club.Redders));
    C((WordPress));
    B((Office 365));
    D((MachForm));
    E((CSV-exports));
    F((Overige apps));
    A --- C;
    A --- B;
    A --- D;
    A --- F;
    A --- E;
```

```mermaid
graph LR;
    A(IT diensten);
    B(Domein gebonden);
    C(3rd party);
    D(Self-hosted);
    E(Cloud);
    F(WordPress);
    G(Club.Redders);
    H(MachForm);
    I(Office 365);
    A --- B;
    A --- C;
    B --- D;
    B --- E;
    D --- F;
    D --- G;
    D --- H;
    E --- I;
```

## Internal and external IT components

```mermaid
graph LR;
    A(Architectuur);
    B(Domein gebonden - registrar);
    C(IT diensten derden - 1ID/SSO of KeeWeb);
    D(Webhosting - self-hosted);
    E(Office 365 - cloud);
    F(WordPress);
    G(MachForm);
    H(Club.Redders);
    I(Overige apps?);
    J(Mail - Exchange);
    K(Data - Teams);
    L(Chat - Teams);
    M(Social - Yammer);
    N(Extern ledenadministratie systeem);
    O(RIB);
    P(RHR);
    Q(KeeWeb);
    R(Bonds-diplomas & functies);
    S(Internet-bankieren);
    T(WHV & licentie administratie);
    U(IT diensten derden);
    A --- B;
    A --- C;
    B --- D;
    B --- E;
    D --- F;
    D --- G;
    D --- H;
    D --- I;
    E --- J;
    E --- K;
    E --- L;
    E --- M;
    C --- N;
    C --- O;
    C --- P;
    C --- Q;
    N --- R;
    O --- S;
    P --- T;
    Q --- U;
```

## IT services third parties | through KeeWeb

```mermaid
graph LR;
    A(IT diensten derden - via KeeWeb);
    B(Wettelijk);
    C(Financieel);
	D(Social media);
	E(Overig);
    F(eHerkenning);
    G(TechSoup);
    H(Geef.nl);
    I(iZettle);
    J(Samsung - POS);
    K(Twitter);
    L(Facebook);
    M(YouTube);
    N(Overige systeem X);
    O(RVR-Dropbox);
    P(KvK);
    Q(VOG);
    A --- B;
    A --- C;
	A --- D;
	A --- E;
    B --- F;
    C --- G;
    C --- H;
    C --- I;
    C --- J;
    D --- K;
    D --- L;
    D --- M;
    E --- N;
    E --- O;
    F --- P;
    F --- Q;
```
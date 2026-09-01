# Kapittel 9 – Et helt nettsted

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - planlegge et nettsted med et sidekart før du koder
> - bygge flere sider som deler samme struktur og meny
> - markere hvilken side brukeren er på
> - kontrollere hele nettstedet ditt systematisk før innlevering

Dette er siste kapittel i del 1. Etter dette er HTML-en på plass, og vi går løs på utseendet.

---

## 9.1 Fra løse sider til et nettsted

Du har nå en håndfull sider: `index.html`, `om-meg.html`, `bilder.html`, `oppskrift.html`,
`timeplan.html`, `ordliste.html`. De er laget én etter én, etter hvert som kapitlene krevde det.

Det er ikke et nettsted ennå. Det er en bunke sider som tilfeldigvis ligger i samme mappe.

Et **nettsted** er noe mer:

- sidene har en **felles struktur** — brukeren kjenner seg igjen fra side til side
- de deler **samme meny**, på samme sted
- de har en **tydelig forside** som binder det hele sammen
- brukeren vet **hvor hen er** og **hvor hen kan gå videre**

I dette kapitlet gjør vi de løse sidene om til en helhet.

---

## 9.2 Sidekartet

Før du koder: tegn. Et **sidekart** er en enkel oversikt over hvilke sider nettstedet har og hvordan
de henger sammen.

```
Forsiden (index.html)
├── Om meg (om-meg.html)
├── Bilder (bilder.html)
├── Oppskrift (oppskrift.html)
├── Timeplan (timeplan.html)
└── Ordliste (ordliste.html)
```

Dette er et **flatt** nettsted: alle sidene ligger på samme nivå under forsiden. For seks sider er det
akkurat passe.

Blir nettstedet større, grupperer du i stedet:

```
Forsiden (index.html)
├── Om meg (om-meg.html)
├── Turer
│   ├── Oversikt (turer/index.html)
│   ├── Besseggen (turer/besseggen.html)
│   └── Galdhøpiggen (turer/galdhopiggen.html)
└── Kontakt (kontakt.html)
```

**Tommelfingerregel:** har du tre eller flere sider som hører til samme tema, lag en undermappe med en
egen `index.html` som oversiktsside.

**Regelen om tre klikk:** brukeren bør nå hvilken som helst side på nettstedet innen tre klikk fra
forsiden. Blir det flere, er strukturen for dyp.

**Oppgave 9.1 – Tegn sidekartet ditt**

Tegn sidekartet for ditt eget nettsted, slik det ser ut nå. Vurder så:

- Er det noen sider som egentlig hører sammen og burde vært gruppert?
- Mangler det en side for at helheten skal gi mening?
- Er det noen side som ikke har noe der å gjøre?

Tegn deretter kartet slik du *vil* at det skal være. Det er den versjonen du bygger resten av
kapitlet.

---

## 9.3 Forsiden har en egen jobb

`index.html` er ikke bare «enda en side». Det er den siden folk kommer til først, og den skal svare på
tre spørsmål på under fem sekunder:

1. **Hva er dette?**
2. **Hvem står bak?**
3. **Hvor kan jeg gå videre?**

En forside som bare sier «Velkommen til nettsiden min» svarer ikke på noen av dem.

En god forside inneholder som regel:

- en tydelig `<h1>` som sier hva nettstedet er
- en kort ingress som forklarer det litt nærmere
- lenker videre til de viktigste sidene — gjerne med en setning om hva som venter
- menyen, som på alle andre sider

**Oppgave 9.2 – Skriv om forsiden**

Bygg om `index.html` slik at den faktisk introduserer nettstedet ditt. Ta med:

- `<h1>` som sier hva dette er
- ett avsnitt som forklarer hva en besøkende finner her
- en liste med lenker til minst tre av sidene dine, der hver lenke har en kort setning ved siden av
  seg om hva siden inneholder
- et bilde som passer

---

## 9.4 Sidemalen

Alle sidene dine skal nå ha samme skjelett. Det er dette skjelettet du kopierer når du lager en ny
side:

```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="utf-8">
    <title>Sidens navn – Nettstedets navn</title>
</head>
<body>

    <header>
        <p>Navnet på nettstedet</p>
        <nav>
            <ul>
                <li><a href="index.html">Forsiden</a></li>
                <li><a href="om-meg.html">Om meg</a></li>
                <li><a href="bilder.html">Bilder</a></li>
                <li><a href="oppskrift.html">Oppskrift</a></li>
                <li><a href="timeplan.html">Timeplan</a></li>
                <li><a href="ordliste.html">Ordliste</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <h1>Overskriften på denne siden</h1>

        <!-- Innholdet på siden -->

    </main>

    <footer>
        <p>Laget av [navn], Vg1 IM, Elvebakken vgs — 2026</p>
    </footer>

</body>
</html>
```

Legg merke til `<title>`: **den skal være ulik på hver side.** Mønsteret
«Sidens navn – Nettstedets navn» er standard på nettsteder, og gjør at fanene er til å skille fra
hverandre når brukeren har flere åpne.

### Vanlige feil når du kopierer

Å kopiere malen er praktisk, men det er akkurat her feilene sniker seg inn:

| Feil | Følge |
|---|---|
| Glemt å endre `<title>` | Alle faner heter det samme |
| Glemt å endre `<h1>` | To sider ser identiske ut i søkeresultater |
| Glemt å oppdatere menyen etter at du la til en side | Én side mangler i menyen på tre andre sider |
| Feil sti fra en side i undermappe | Menyen virker på forsiden, men ikke i `turer/` |

**Oppgave 9.3 – Samme skjelett på alle sider**

Gå gjennom hver eneste side og sørg for at de har nøyaktig samme `<header>`, `<nav>` og `<footer>`,
og at hver side har sin egen `<title>` og `<h1>`.

Ligger noen av sidene dine i en undermappe, husk at menyen der må ha `../` foran stiene.

---

## 9.5 Hvor er jeg?

Menyen forteller brukeren hvor hen *kan* gå. Den bør også fortelle hvor hen **er**.

På den siden du står på, markerer du menypunktet slik:

```html
<li><a href="om-meg.html" aria-current="page" class="aktiv">Om meg</a></li>
```

To ting skjer her:

- `aria-current="page"` er en opplysning til skjermlesere: «dette er siden du er på nå». Den leses opp.
- `class="aktiv"` er en krok vi styler i del 2 — der gir vi den for eksempel en farge eller en
  understrek, slik at også de som ser siden, oppdager det.

Akkurat nå ser du ingen forskjell. Det er greit. Du legger inn kroken nå, og henger utseendet på den
i kapittel 11.

> **Merk:** noen fjerner lenken helt på den aktive siden, siden det er litt rart å lenke til den man
> allerede er på. Begge deler er vanlig. Vi beholder lenken — det gjør malen enklere å kopiere.

**Oppgave 9.4 – Marker aktiv side**

Legg inn `aria-current="page"` og `class="aktiv"` på riktig menypunkt på hver enkelt side. Husk at
det er **et annet punkt** på hver side.

---

## 9.6 Bunnteksten

`<footer>` er stedet for det som hører hjemme nederst på alle sider:

- hvem som har laget nettstedet
- årstall
- kontaktinformasjon
- kildehenvisninger for bilder du har lånt
- eventuelt en lenke tilbake til toppen

```html
<footer>
    <p>Laget av Nora Hansen, Vg1 IM, Elvebakken vgs — 2026</p>
    <p>Foto: Unsplash. <a href="#top">Til toppen</a></p>
</footer>
```

Den skal være lik på alle sider, akkurat som menyen.

---

## 9.7 Kontroll av hele nettstedet

Nå skal du gjøre noe utviklere gjør hele tiden: **teste systematisk**, ikke bare klikke litt rundt og
håpe.

**Oppgave 9.5 – Full gjennomgang**

Gå gjennom nettstedet ditt punkt for punkt. Noter alt du finner, og rett det.

**1. Alle lenker**
Start på forsiden. Klikk deg til hver eneste side, og fra hver side videre til alle de andre. Bruk
aldri tilbakeknappen underveis. Fant du en side du ikke kom deg til?

**2. Alle bilder**
Vises alle bildene på alle sidene? Også fra sider i undermapper?

**3. Titlene**
Åpne alle sidene i hver sin fane. Kan du se på fanene hvilken side som er hvilken?

**4. Overskriftene**
Har hver side nøyaktig én `<h1>`? Hopper noen av dem over overskriftsnivåer?

**5. Alt-tekstene**
Har alle bildene `alt`? Sier alt-teksten faktisk hva bildet viser?

**6. Innrykkene**
Kjør `Shift + Alt + F` på hver fil. Ser strukturen fornuftig ut etterpå?

**7. Validatoren**
Gå til [validator.w3.org](https://validator.w3.org), velg **Validate by Direct Input**, lim inn koden
fra én side om gangen og trykk Check.

Validatoren er et program som leser HTML-en din og sier fra om alt som er galt — manglende sluttager,
feil nøsting, elementer på feil sted. Dette er den eneste gangen HTML faktisk gir deg feilmeldinger,
og de er verdt å lese.

Noter hvor mange feil du hadde til å begynne med, og rett alle sammen.

---

## 9.8 Sjekkpunkt 1 — HTML

Dette er første innlevering av selve nettstedet. Merk deg at det skal leveres **uten CSS**.

Det er med vilje. Et nettsted som er riktig bygget skal fungere og gi mening også uten utseende — all
struktur, alle overskrifter, all navigasjon skal være på plass i HTML-en alene. Er strukturen rotete
nå, blir den bare vanskeligere å rydde opp i når det ligger farger og layout oppå.

### Krav til innleveringen

Nettstedet skal ha:

- [ ] minst seks sider, alle med gyldig grunnstruktur
- [ ] `index.html` som forside, med tydelig innledning og lenker videre
- [ ] samme `<header>`, `<nav>` og `<footer>` på alle sider
- [ ] menyen bygget som en `<ul>` med lenker
- [ ] aktiv side markert med `aria-current="page"` og `class="aktiv"`
- [ ] unik `<title>` og én `<h1>` på hver side
- [ ] semantiske elementer i bruk — ikke bare `<div>`
- [ ] minst fem bilder, alle med god `alt`, riktig skalert, i `bilder/`-mappen
- [ ] minst én punktliste, én nummerert liste og én nøstet liste
- [ ] minst én tabell med `<caption>` og `<th>`
- [ ] én `<dl>` med minst åtte begreper
- [ ] ingen brutte lenker og ingen manglende bilder
- [ ] null feil i validatoren
- [ ] ryddige innrykk og minst én forklarende kommentar per side

### Levering

1. Hele `webkurs`-mappen, pakket som zip
2. Skjermbilde av hver side
3. Sidekartet fra oppgave 9.1
4. Kort refleksjon (tre–fem setninger): hva var vanskeligst i del 1, og hva sitter best?

---

## 9.9 Oppsummering av hele del 1

Du kan nå:

| Kapittel | Det du sitter igjen med |
|---|---|
| 1 | Hva en nettside er, og hva som skjer fra adresse til ferdig side |
| 2 | VS Code, Live Server, prosjektmapper og filnavn som virker |
| 3 | Grunnstrukturen, og ordene tag, element, attributt og verdi |
| 4 | Overskriftshierarki, avsnitt og utheving med mening |
| 5 | Lenker, og filstier som faktisk peker riktig |
| 6 | Bilder, alt-tekst, filformater og opphavsrett |
| 7 | Lister og tabeller — og menyen som en ekte liste |
| 8 | Semantiske elementer som gir siden mening |
| 9 | Et sammenhengende nettsted du har testet systematisk |

Det du har nå er **innhold og struktur**. Alt er der, det er riktig bygget, og det er stygt.

Det er nøyaktig slik det skal være. Nå begynner del 2.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Nettsted | En samling sider som hører sammen og deler struktur og navigasjon |
| Sidekart | Oversikt over hvilke sider nettstedet har og hvordan de henger sammen |
| Flat struktur | Alle sider på samme nivå under forsiden |
| Sidemal | Det felles skjelettet alle sidene bygger på |
| Konsekvent navigasjon | Samme meny, samme sted, på alle sider |
| `aria-current="page"` | Opplysning til skjermlesere om hvilken side brukeren er på |
| Validator | Program som sjekker om HTML-en din er riktig skrevet |

---

## Innlevering – kapittel 9

Sjekkpunkt 1, slik det står i avsnitt 9.8, er innleveringen for dette kapitlet.

I tillegg leverer du i læringsloggen:

1. Sidekartet fra oppgave 9.1 — begge versjoner, slik det var og slik du gjorde det.
2. Notatene fra gjennomgangen i oppgave 9.5: hva du fant, og hva du rettet.
3. Antall feil validatoren fant første gang.

---

**Neste kapittel:** CSS. Vi kobler på et stilark, og for første gang bestemmer du selv hvordan
siden skal se ut.

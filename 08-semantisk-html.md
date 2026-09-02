# Kapittel 8 – Semantisk HTML

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - forklare hva semantikk betyr, og hvorfor det har praktiske konsekvenser
> - dele en side inn i `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>` og `<footer>`
> - se forskjellen på når `<div>` er riktig og når det er latskap
> - gi deler av siden navn med `class` og `id`

---

## 8.1 To sider som ser helt like ut

Se på disse to kodesnuttene. På skjermen er de **identiske** — helt like, piksel for piksel.

**Versjon A**

```html
<div>
    <div>Nora sin nettside</div>
    <div>
        <div><a href="index.html">Forsiden</a></div>
        <div><a href="om-meg.html">Om meg</a></div>
    </div>
</div>
<div>
    <div>Om meg</div>
    <div>Jeg går på Elvebakken.</div>
</div>
<div>Laget av Nora, 2026</div>
```

**Versjon B**

```html
<header>
    <p>Nora sin nettside</p>
    <nav>
        <ul>
            <li><a href="index.html">Forsiden</a></li>
            <li><a href="om-meg.html">Om meg</a></li>
        </ul>
    </nav>
</header>

<main>
    <h1>Om meg</h1>
    <p>Jeg går på Elvebakken.</p>
</main>

<footer>
    <p>Laget av Nora, 2026</p>
</footer>
```

Versjon A sier ingenting om hva delene **er**. Det er ni bokser. Versjon B sier: her er toppen, her er
menyen, her er hovedinnholdet, her er bunnen.

For øyet ditt er de like. For alle andre som leser siden — og det er flere enn du tror — er de vidt
forskjellige.

---

## 8.2 Hva semantikk betyr

**Semantikk** betyr *betydning*. Semantisk HTML er å velge elementer ut fra hva innholdet **er**, ikke
ut fra hvordan det skal se ut.

Du har egentlig gjort dette hele veien:

- `<h1>` sier «dette er hovedoverskriften» — ikke «gjør teksten stor og fet»
- `<ul>` sier «dette er en liste» — ikke «sett kuler foran»
- `<strong>` sier «dette er viktig» — ikke «gjør det fett»
- `<table>` sier «dette er data i rader og kolonner» — ikke «still opp i rutenett»

Nå utvider vi det samme prinsippet fra enkeltelementer til **hele seksjoner av siden**.

---

## 8.3 `<div>` — boksen uten mening

`<div>` er et element som ikke betyr noe som helst. Det er en nøytral boks du kan legge ting i.

```html
<div>
    <h2>Været i dag</h2>
    <p>Sol og 21 grader.</p>
</div>
```

Den gjør ingenting i seg selv — ingen farge, ingen ramme, ingen avstand. Den bare **grupperer**
innhold, slik at du kan behandle det som én enhet i CSS senere.

`<div>` er ikke forbudt. Den er nyttig, og du kommer til å bruke den mye i del 2 når du trenger en
boks å style. Problemet oppstår når `<div>` brukes til *alt* — også der det finnes et element som
faktisk sier hva innholdet er.

Det kalles **div-suppe**: hundrevis av identiske bokser der ingenting forteller hva noe er. Åpne
kildekoden på et vilkårlig moderne nettsted, så finner du garantert noen.

> **Regelen:** finnes det et element som beskriver innholdet, bruk det. Finnes det ikke, bruk `<div>`.

---

## 8.4 De semantiske seksjonene

Her er elementene som deler siden i deler.

### `<header>`

Toppen av siden eller av en seksjon. Typisk logo, nettstedets navn og menyen.

```html
<header>
    <p>Nora sin nettside</p>
    <nav>...</nav>
</header>
```

En side kan ha flere `<header>` — én for hele siden, og gjerne én øverst i hver artikkel.

### `<nav>`

Navigasjon: en samling lenker som fører videre i nettstedet.

```html
<nav>
    <ul>
        <li><a href="index.html">Forsiden</a></li>
        <li><a href="om-meg.html">Om meg</a></li>
    </ul>
</nav>
```

Merk: **ikke alle lenker skal ligge i `<nav>`.** Elementet er for hovednavigasjonen — menyer,
innholdsfortegnelser, brødsmulestier. En lenke midt inne i et avsnitt hører ikke hjemme der.

### `<main>`

Hovedinnholdet på **akkurat denne siden** — det som er unikt for den, og som ikke gjentas på de andre.

```html
<main>
    <h1>Om meg</h1>
    <p>...</p>
</main>
```

To viktige regler: det skal være **nøyaktig én `<main>` per side**, og menyen og bunnteksten skal
ligge *utenfor* den, siden de er like overalt.

`<main>` er kanskje det mest nyttige semantiske elementet som finnes. Nettlesere og skjermlesere lar
brukeren hoppe rett dit — forbi menyen — med én tast. Uten `<main>` må en skjermleserbruker høre hele
menyen lest opp på hver eneste side.

### `<section>`

En tematisk avgrenset del av innholdet. En seksjon bør ha en overskrift.

```html
<section>
    <h2>Interesser</h2>
    <p>...</p>
</section>

<section>
    <h2>Hvorfor jeg valgte IM</h2>
    <p>...</p>
</section>
```

**Test:** kan du gi denne delen en overskrift som gir mening? Da er det sannsynligvis en `<section>`.
Grupperer du bare noe for å style det, er det en `<div>`.

### `<article>`

Innhold som gir mening **helt for seg selv**, løsrevet fra resten av siden.

```html
<article>
    <h2>Tur til Besseggen</h2>
    <p>Vi gikk opp klokka seks...</p>
</article>
```

**Test:** kunne dette vært klippet ut og delt alene — som et innlegg i en app, en nyhetssak i et
nyhetsvarsel, eller et søkeresultat? Da er det en `<article>`.

Typiske artikler: en blogpost, en nyhetssak, en produktomtale, en kommentar, et innlegg i en feed.

Forskjellen på `<section>` og `<article>` forvirrer mange, og selv erfarne utviklere er uenige i
grensetilfeller. Ikke bruk mye tid på tvilstilfellene — bruk `<article>` når innholdet klart står på
egne ben, og `<section>` ellers.

### `<aside>`

Innhold som hører løselig til, men ikke er en del av hovedpoenget: faktabokser, «relatert innhold»,
en sidespalte, en annonse.

```html
<aside>
    <h2>Visste du at...</h2>
    <p>Besseggen har rundt 60 000 besøkende i året.</p>
</aside>
```

**Test:** kan du fjerne den uten at hovedinnholdet mister mening? Da er det en `<aside>`.

### `<footer>`

Bunnen av siden eller av en seksjon: hvem som står bak, årstall, kontaktinfo, kildehenvisninger.

```html
<footer>
    <p>Laget av Nora Hansen, Vg1 IM — 2026</p>
</footer>
```

---

## 8.5 Slik henger det sammen

```
body
├── header
│   └── nav
├── main
│   ├── h1
│   ├── section
│   ├── section
│   └── aside
└── footer
```

Legg merke til at `<header>`, `<main>` og `<footer>` ligger på samme nivå, som søsken. `<nav>` ligger
inni `<header>` fordi menyen er en del av toppen.

**Oppgave 8.1 – Kartlegg en ekte nettside**

Velg et nettsted du bruker ofte. Ta et skjermbilde av forsiden og tegn rammer rundt delene:
Hvor er `<header>`? `<nav>`? `<main>`? Finnes det `<aside>` eller `<article>`? Hvor slutter `<main>`
og begynner `<footer>`?

Åpne så utviklerverktøyet og se hva de faktisk har brukt. Traff du? Bruker de semantiske elementer i
det hele tatt, eller er det div-suppe?

**Oppgave 8.2 – Rydd opp i div-suppa**

Skriv om denne koden med semantiske elementer. Innholdet skal være uendret — bare elementene byttes.

```html
<div>
    <div>Turbloggen</div>
    <div>
        <a href="index.html">Hjem</a>
        <a href="turer.html">Turer</a>
        <a href="om.html">Om</a>
    </div>
</div>

<div>
    <div>Turer i Jotunheimen</div>

    <div>
        <div>Besseggen</div>
        <div>En av landets mest kjente fjellturer.</div>
    </div>

    <div>
        <div>Galdhøpiggen</div>
        <div>Norges høyeste fjell, 2469 meter.</div>
    </div>

    <div>
        <div>Godt å vite</div>
        <div>Sesongen varer fra juni til september.</div>
    </div>
</div>

<div>Laget av Nora, 2026</div>
```

Tenk gjennom: er de to turene `<section>` eller `<article>`? Hva med «Godt å vite»?

---

## 8.6 Hvorfor dette faktisk betyr noe

Det er lett å tenke at semantikk er teori. Her er de fire konkrete konsekvensene.

### 1. Skjermlesere

En blind bruker navigerer ikke ved å skrolle. Skjermleseren tilbyr en liste over sidens **landemerker**
— «banner», «navigasjon», «hovedinnhold», «bunntekst» — og brukeren hopper rett til det hen vil.

Er alt `<div>`, finnes ingen landemerker. Da må brukeren høre hele siden lest opp fra toppen, hver
eneste gang. Det er forskjellen mellom å ha en innholdsfortegnelse og å måtte bla gjennom hele boka.

### 2. Universell utforming er lovpålagt

Norske nettsteder er omfattet av krav om universell utforming. Semantisk oppmerking er ett av de
grunnleggende kravene — ikke en bonus for spesielt flinke.

### 3. Søkemotorer

Google bruker strukturen til å forstå hva som er hovedinnholdet på siden, og hva som bare er meny og
pynt. En side der innholdet er tydelig markert, vurderes bedre.

### 4. Kode du selv kan lese om tre uker

Dette merker du raskest selv. Åpne en fil med 200 linjer `<div>` og finn menyen. Åpne en fil med
`<header>`, `<main>` og `<footer>` og gjør det samme. Den andre tar to sekunder.

**Oppgave 8.3 – Se landemerkene**

Chrome har en innebygd tilgjengelighetstest. Åpne utviklerverktøyet (`F12`), gå til fanen
**Lighthouse**, huk av for **Accessibility** og kjør testen.

Lag to testfiler med henholdsvis versjon A og versjon B fra avsnitt 8.1, kjør testen på begge, og
sammenlikn. Skriv ned hva verktøyet sier om den ene som det ikke sier om den andre.

---

## 8.7 Navn på delene: `class` og `id`

Semantiske elementer sier hva noe **er**. Men du trenger også å kunne gi delene dine egne **navn**,
slik at du kan style dem i del 2.

Til det har vi to attributter:

```html
<section class="turliste">...</section>
<section class="turliste">...</section>

<footer id="bunn">...</footer>
```

| Attributt | Betyr | Antall |
|---|---|---|
| `class` | En merkelapp som **flere** elementer kan dele | så mange du vil |
| `id` | Et **unikt** navn på ett bestemt element | bare én av hvert navn per side |

Tommelfingerregel: **bruk `class` som standard.** `id` bruker du bare når du trenger å peke på ett
helt bestemt element — for eksempel til en ankerlenke, slik du gjorde i kapittel 5.

### Gode klassenavn

Navnet skal si hva innholdet **er**, ikke hvordan det ser ut:

| ❌ Dårlig | ✅ Bedre | Hvorfor |
|---|---|---|
| `class="rod-tekst"` | `class="advarsel"` | Hva om fargen endres til oransje? |
| `class="boks2"` | `class="turkort"` | Sier ingenting om innholdet |
| `class="stor"` | `class="ingress"` | Beskriver utseende, ikke rolle |

Regler for navnene: små bokstaver, ingen mellomrom, bindestrek som ordskille, ingen æøå.
Et element kan ha flere klasser, adskilt med mellomrom:

```html
<article class="turkort utvalgt">...</article>
```

**Oppgave 8.4 – Sett navn**

Gå tilbake til den semantiske versjonen din fra oppgave 8.2 og legg til fornuftige klassenavn på
delene. Tenk på hva de **er**, ikke hvordan de skal se ut.

---

## 8.8 Bygg om ditt eget nettsted

**Oppgave 8.5 – Semantikk på alle sider**

Gå gjennom alle sidene dine og bygg dem om:

- pakk toppen med nettstedsnavn og meny i `<header>`
- pakk menylista i `<nav>`
- pakk sidens eget innhold i `<main>` — nøyaktig én per side
- del innholdet i `<section>`, én for hvert tema, hver med sin `<h2>`
- bruk `<article>` der noe står på egne ben (for eksempel hvert bilde i galleriet, eller hver
  tur eller oppskrift)
- legg til en `<aside>` med en faktaboks eller «relatert innhold» et sted det passer
- pakk bunnen i `<footer>`

Kontroller til slutt i utviklerverktøyet at strukturen ser fornuftig ut, og kjør én side gjennom
[validator.w3.org](https://validator.w3.org).

> Dette er en stor jobb, men den gir deg sidemalen du bruker resten av kurset. Får du strukturen
> riktig nå, blir hele del 2 enklere — CSS er nemlig mye lettere å skrive når det finnes tydelige
> deler å feste stilene på.

---

## 8.9 Oppsummering

- **Semantikk** = å velge element ut fra hva innholdet *er*, ikke hvordan det skal se ut.
- `<div>` betyr ingenting. Den er en nøytral boks til gruppering — bruk den når ingenting annet passer.
- `<header>` topp, `<nav>` navigasjon, `<main>` sidens eget innhold, `<footer>` bunn.
- **Én `<main>` per side.** Meny og bunntekst ligger utenfor.
- `<section>` = tematisk del med overskrift. `<article>` = innhold som står på egne ben.
  `<aside>` = kan fjernes uten at hovedpoenget forsvinner.
- Semantikk gir skjermlesere landemerker å hoppe mellom, og er en del av lovpålagt universell utforming.
- `class` er en merkelapp flere kan dele. `id` er et unikt navn på ett element. Bruk `class` som standard.
- Klassenavn skal beskrive **rolle**, ikke utseende.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Semantikk | At elementet sier noe om hva innholdet betyr |
| `<div>` | Nøytral boks uten mening, brukt til gruppering |
| Div-suppe | Kode der alt er `<div>` og ingenting forteller hva noe er |
| `<header>` | Toppen av siden eller en seksjon |
| `<nav>` | Hovednavigasjon – en samling lenker videre |
| `<main>` | Sidens eget hovedinnhold; nøyaktig én per side |
| `<section>` | Tematisk avgrenset del, bør ha overskrift |
| `<article>` | Innhold som gir mening helt for seg selv |
| `<aside>` | Tilleggsinnhold som kan fjernes uten tap av hovedpoeng |
| `<footer>` | Bunnen av siden eller en seksjon |
| Landemerke | Region skjermlesere lar brukeren hoppe direkte til |
| `class` | Navn flere elementer kan dele |
| `id` | Unikt navn på ett element |

---

## Innlevering – kapittel 8

Lever i læringsloggen din:

1. Kartleggingen fra oppgave 8.1: skjermbilde med dine rammer, og hva nettstedet faktisk brukte.
2. Den omskrevne koden fra oppgave 8.2, med klassenavn (oppgave 8.4).
3. Resultatene fra Lighthouse-testen i oppgave 8.3 — begge versjoner.
4. Nettstedet ditt bygget om semantisk (oppgave 8.5), med skjermbilde av Elements-fanen som viser
   strukturen på én side.

**Sjekkliste før du går videre:**

- [ ] Alle sidene mine har `<header>`, `<nav>`, `<main>` og `<footer>`
- [ ] Hver side har nøyaktig én `<main>`
- [ ] Menyen og bunnteksten ligger utenfor `<main>`
- [ ] Hver `<section>` har en overskrift
- [ ] Jeg bruker `<div>` bare der ingenting annet passer
- [ ] Klassenavnene mine sier hva innholdet er, ikke hvordan det ser ut
- [ ] Sidene validerer uten feil

---

**Neste kapittel:** Vi binder sidene sammen til ett nettsted, og gjør del 1 ferdig.

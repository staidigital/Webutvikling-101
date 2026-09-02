# Kapittel 13 – Typografi

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - velge og koble på skrifttyper, med fallback som virker
> - forklare forskjellen på `px`, `em` og `rem`, og vite hvorfor det betyr noe
> - sette linjeavstand og linjelengde slik at tekst faktisk er behagelig å lese
> - bygge et tydelig typografisk hierarki

---

## 13.1 Nesten alt på nett er tekst

Farger legger du merke til først. Men det er skriften som avgjør om noen orker å lese siden.

Og det meste av det du styrer her, er ikke hvilken skrifttype du velger. Det er **størrelse,
avstand og linjelengde**. En helt vanlig skrift satt riktig, er lettere å lese enn en fancy skrift
satt feil.

---

## 13.2 Skriftfamilier

```css
body {
    font-family: Verdana, Geneva, sans-serif;
}
```

Legg merke til at det står tre navn. Det er en **fallback-stabel**, og den finnes av en grunn:

> Nettleseren kan bare bruke skrifttyper som allerede finnes på brukerens maskin — eller som du
> laster ned til dem.

Har ikke brukeren Verdana, prøver nettleseren Geneva. Har de ikke den heller, brukes en hvilken som
helst skrift uten seriffer. **Siste navn i lista skal alltid være en av de fem generiske familiene:**

| Generisk familie | Kjennetegn | Brukes til |
|---|---|---|
| `serif` | små føtter på bokstavene | tradisjonelt, trykt preg |
| `sans-serif` | uten føtter | rent, moderne, mest brukt på nett |
| `monospace` | alle tegn like brede | kode |
| `cursive` | håndskriftpreg | sjelden |
| `fantasy` | dekorativ | nesten aldri |

Har navnet mellomrom, skal det i anførselstegn:

```css
font-family: "Times New Roman", Times, serif;
```

**Oppgave 13.1 – Se fallback virke**

Skriv denne regelen med en skrift som garantert ikke finnes:

```css
h1 {
    font-family: Finnesikke, "Comic Sans MS", serif;
}
```

Hva skjer? Fjern så `"Comic Sans MS"` og se hva som skjer da. Forklar med egne ord hva nettleseren gjør.

---

## 13.3 Skrifter fra nettet

Vil du bruke en skrift brukeren ikke har, må den lastes ned sammen med siden. Den vanligste kilden er
**Google Fonts** — gratis, lovlig å bruke, og enkelt å koble på.

Slik gjør du det:

1. Gå til [fonts.google.com](https://fonts.google.com)
2. Velg en skrift, og velg hvilke tykkelser du vil ha (for eksempel 400 og 700)
3. Kopier `<link>`-koden og lim den inn i `<head>`, **over** din egen `<link>` til `style.css`
4. Bruk skriften i CSS-en

```html
<head>
    <meta charset="utf-8">
    <title>Om meg</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Source+Sans+3:wght@400;600&display=swap">
    <link rel="stylesheet" href="style.css">
</head>
```

```css
body {
    font-family: "Source Sans 3", Verdana, sans-serif;
}
```

Merk at fallback fortsatt skal være med. Går nedlastingen galt — dårlig nett, blokkert innhold — skal
siden fortsatt være lesbar.

**Velg få tykkelser.** Hver tykkelse er en egen fil som må lastes ned. To holder nesten alltid: én til
brødtekst og én til overskrifter.

> **To skrifter er nok.** Én til overskrifter, én til brødtekst — eller bare én til alt, i ulike
> tykkelser. Tre eller flere blir rotete, og det er en av de sikreste måtene å få en side til å se
> amatørmessig ut.

**Oppgave 13.2 – Velg skriftene dine**

Gå til Google Fonts og finn:

- én skrift til brødtekst — den skal være lettlest i liten størrelse
- én skrift til overskrifter — den kan ha mer karakter

Test dem sammen. Skriv ned hvilke du valgte og hvorfor du synes de passer sammen med nettstedet ditt.

Koble dem på alle sidene dine.

---

## 13.4 Størrelse: `px`, `em` og `rem`

Dette avsnittet er det som skiller en gjennomtenkt side fra en tilfeldig en.

### `px` — piksler

```css
font-size: 18px;
```

En fast størrelse. Enkel og forutsigbar.

**Problemet:** brukere som ser dårlig, kan skru opp standard skriftstørrelse i nettleseren sin.
Skriver du `px`, skjer ingenting. Du har overstyrt valget deres.

### `rem` — i forhold til roten

```css
font-size: 1.125rem;
```

`rem` regnes ut fra **rotstørrelsen**, altså nettleserens standard skriftstørrelse. Den er som regel
16 px:

| Verdi | Blir | Hvis brukeren har skrudd opp til 20 px |
|---|---|---|
| `1rem` | 16 px | 20 px |
| `1.5rem` | 24 px | 30 px |
| `0.875rem` | 14 px | 17,5 px |

Skriver du `rem`, følger hele siden med når brukeren justerer. **Det er derfor `rem` er anbefalt for
skriftstørrelser.**

Enkel omregning: del pikselverdien på 16. 24 px blir `1.5rem`, 20 px blir `1.25rem`.

### `em` — i forhold til forelderen

```css
font-size: 1.2em;
```

`em` regnes ut fra **elementet over**. Det gjør den nyttig, men også lumsk:

```html
<div style="font-size: 1.2em">
    <div style="font-size: 1.2em">
        <div style="font-size: 1.2em">Denne teksten er nå 1,7 ganger så stor</div>
    </div>
</div>
```

Verdiene **ganges sammen** nedover. Nøster du `em` i flere lag, vokser teksten fort ut av kontroll.

**Regelen i dette kurset:** bruk `rem` til skriftstørrelser. `px` går fint til rammer og små avstander.
`em` bruker du bevisst når noe skal skalere sammen med teksten det står i.

**Oppgave 13.3 – Se forskjellen selv**

1. Lag en testside med to overskrifter: én satt i `px`, én i `rem`.
2. Endre nettleserens standard skriftstørrelse: i Chrome under **Innstillinger → Utseende →
   Skriftstørrelse**, sett den til «Stor».
3. Se på testsiden. Hvilken av de to endret seg?
4. Sett innstillingen tilbake.

Skriv én setning om hva dette betyr for en bruker som ser dårlig.

---

## 13.5 Linjeavstand

```css
body {
    line-height: 1.6;
}
```

`line-height` er avstanden mellom linjene. **Skriv den uten enhet** — da blir den en multiplikator av
skriftstørrelsen, og den skalerer riktig overalt.

| Verdi | Passer til |
|---|---|
| 1,1–1,2 | store overskrifter |
| **1,5–1,7** | **brødtekst** |
| 1,8+ | luftig, korte tekster |

Standardverdien i nettleseren er rundt 1,2. Det er for tett for brødtekst.

Dette er kanskje den **enkleste enkeltendringen** som gjør en side mer lesbar. Prøv å sette
`line-height: 1.6` på brødteksten din og se hva som skjer.

---

## 13.6 Linjelengde

Her er et krav som overrasker mange: en tekstlinje bør være **50–75 tegn** lang.

Blir linjene mye lengre, mister øyet sporet på vei tilbake til neste linje, og man leser den samme
linjen om igjen uten å skjønne hvorfor det er slitsomt. Aviser og bøker har visst dette i hundrevis av
år — derfor spalter.

På en bred skjerm blir en tekst uten begrensning fort 150 tegn bred. Løsningen:

```css
main {
    max-width: 65ch;
}
```

Enheten `ch` er bredden på tegnet «0» i den skriften du bruker. `65ch` er altså omtrent 65 tegn — akkurat
det du vil ha.

Du kan også bruke piksler (`max-width: 700px`), men `ch` er mer presist fordi den følger skriften.

**Oppgave 13.4 – Mål linjene dine**

1. Åpne en av tekstsidene dine i fullskjerm på en bred skjerm.
2. Tell antall tegn i den lengste linjen. (Omtrent — tell ordene og gang med seks.)
3. Sett `max-width: 65ch` på `<main>` og se igjen.
4. Ta skjermbilde før og etter.

Hvilken av dem er behageligst å lese?

---

## 13.7 De andre tekstegenskapene

| Egenskap | Hva den gjør | Eksempelverdier |
|---|---|---|
| `font-weight` | tykkelse | `400` (normal), `600`, `700` (fet), `bold` |
| `font-style` | kursiv | `normal`, `italic` |
| `text-align` | justering | `left`, `center`, `right` |
| `text-transform` | endrer store/små bokstaver | `uppercase`, `lowercase`, `capitalize` |
| `text-decoration` | strek | `none`, `underline` |
| `letter-spacing` | avstand mellom bokstaver | `0.05em`, `-0.01em` |

Noen råd som er verdt mer enn de ser ut:

**Ikke midtstill brødtekst.** Midtstilt tekst har ujevn venstrekant, og øyet må lete etter starten på
hver linje. Midtstilling er greit til korte overskrifter, aldri til avsnitt.

**`text-transform: uppercase` trenger `letter-spacing`.** Store bokstaver ligger for tett når de er
satt sammen. Legg til `letter-spacing: 0.06em`, så puster de.

**Bruk `text-transform` framfor å skrive med caps lock.** Skriver du «OM MEG» i HTML-en, leser en
skjermleser det kanskje bokstav for bokstav. Skriver du «Om meg» og bruker CSS, står det riktig i
koden og ser ut som du vil på skjermen.

**Fet skrift virker best sparsomt.** Er alt uthevet, er ingenting uthevet.

---

## 13.8 Hierarki og typografisk skala

**Hierarki** er at leseren ser hva som er viktigst uten å tenke over det. Du bygger det med tre
virkemidler:

1. **Størrelse** — større betyr viktigere
2. **Tykkelse** — fetere betyr viktigere
3. **Avstand** — luft rundt noe gir det oppmerksomhet

En **typografisk skala** er et sett med faste størrelser du holder deg til, i stedet for å velge
tilfeldige tall for hvert element. Et ryddig utgangspunkt:

```css
:root { }                          /* rot = 16px som standard */

body   { font-size: 1rem;     line-height: 1.6; }   /* 16 px */
small  { font-size: 0.875rem; }                     /* 14 px */
h3     { font-size: 1.25rem;  line-height: 1.3; }   /* 20 px */
h2     { font-size: 1.75rem;  line-height: 1.2; }   /* 28 px */
h1     { font-size: 2.5rem;   line-height: 1.1; }   /* 40 px */
```

Legg merke til to ting:

- **størrelsene hopper tydelig** — 16, 20, 28, 40. Ligger de for tett (16, 17, 18, 20), ser det bare
  ut som en feil.
- **linjeavstanden synker når skriften vokser.** Store overskrifter trenger tettere linjer, ellers
  faller de fra hverandre.

**Oppgave 13.5 – Din egen skala**

Sett opp en typografisk skala for nettstedet ditt: `body`, `h1`, `h2`, `h3` og eventuelt en ingress.
Skriv den øverst i CSS-fila under en kommentar `/* ===== Typografi ===== */`.

Krav:

- alle størrelser i `rem`
- tydelige sprang mellom nivåene
- lavere `line-height` jo større skriften er
- brødtekst på 1,5–1,7 i linjeavstand

**Oppgave 13.6 – Redd en stygg side**

Lag en fil `typografi-test.html` med denne teksten, uten annen CSS enn det du skriver selv:

```
Fjellvett
Fjellvettreglene ble laget i 1952 etter flere ulykker i påskefjellet. De er ikke lover, men råd som har vist seg å redde liv.
Planlegg turen
Meld fra hvor du går. Sjekk værmeldingen. Ta med det utstyret du trenger, og vurder om turen passer for gruppa.
Vend i tide
Det er ingen skam å snu. Dette er kanskje den mest kjente av reglene, og den vanskeligste å følge.
```

Marker den opp med riktige elementer, og gjør den **så lesbar du klarer** — kun med typografi og
farge. Ingen layout, ingen bilder, ingen rammer.

Bruk: skriftvalg, skala, linjeavstand, linjelengde, tykkelse og luft.

Dette er en av de mest lærerike oppgavene i hele kurset. Med bare tekst som virkemiddel ser du hvor
mye typografien alene har å si.

**Oppgave 13.7 – Sett skalaen i verk**

Bruk skalaen din på hele nettstedet, sammen med skriftene fra oppgave 13.2 og linjelengden fra 13.4.

Klikk gjennom alle sidene. Ser de ut som ett nettsted, og er de behagelige å lese?

---

## 13.9 Oppsummering

- `font-family` skal alltid ha en **fallback-stabel** som ender i en generisk familie.
- Google Fonts kobles på med en `<link>` i `<head>`, over ditt eget stilark. Velg få tykkelser.
- **To skrifter er nok.**
- **`rem` til skriftstørrelser** — da følger siden med når brukeren justerer skriftstørrelsen i
  nettleseren. `px` overstyrer det valget.
- `em` regnes fra elementet over og ganges sammen i flere lag. Bruk den bevisst.
- `line-height` skrives **uten enhet**. 1,5–1,7 på brødtekst.
- Linjelengde: **50–75 tegn**. `max-width: 65ch` løser det.
- Ikke midtstill brødtekst. Store bokstaver trenger `letter-spacing`.
- Hierarki bygges av **størrelse, tykkelse og luft** — og en skala med tydelige sprang.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Fallback-stabel | Lista av skrifter nettleseren prøver i tur og orden |
| Generisk familie | `serif`, `sans-serif`, `monospace` m.fl. – siste utvei i stabelen |
| Serif | Skrift med små føtter på bokstavene |
| Sans-serif | Skrift uten føtter |
| Webfont | Skrift som lastes ned sammen med siden, f.eks. fra Google Fonts |
| `px` | Fast størrelse i piksler |
| `rem` | Størrelse i forhold til nettleserens rotstørrelse |
| `em` | Størrelse i forhold til elementet over |
| `line-height` | Linjeavstand; skrives uten enhet |
| `ch` | Enhet som tilsvarer bredden på tegnet «0» |
| Linjelengde | Antall tegn per linje; bør være 50–75 |
| `font-weight` | Skrifttykkelse, 400 normal og 700 fet |
| Typografisk skala | Det faste settet med skriftstørrelser du holder deg til |
| Hierarki | At leseren ser hva som er viktigst, uten å tenke |

---

## Innlevering – kapittel 13

Lever i læringsloggen din:

1. `typografi-test.html` fra oppgave 13.6, med skjermbilde.
2. Typografiseksjonen fra `style.css` (oppgave 13.5).
3. Nettstedet med ny typografi — skjermbilde av samme side før og etter.
4. Skjermbildene fra linjelengdemålingen (oppgave 13.4).
5. Svaret fra oppgave 13.3 om `px` mot `rem`, med en setning om hva det betyr for brukeren.
6. Hvilke skrifter du valgte, og hvorfor.

**Sjekkliste før du går videre:**

- [ ] Alle skriftstørrelsene mine er i `rem`
- [ ] `font-family` har fallback som ender i en generisk familie
- [ ] Brødteksten har `line-height` mellom 1,5 og 1,7
- [ ] Ingen tekstlinjer er over ca. 75 tegn
- [ ] Jeg bruker maks to skrifter
- [ ] Overskriftsnivåene har tydelig ulik størrelse
- [ ] Ingen avsnitt er midtstilt

---

**Neste kapittel:** Boksmodellen — hvorfor alt på en nettside egentlig er firkanter, og hvordan du
styrer plassen de tar.

# Kapittel 3 – HTML-grunnstruktur

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - skrive et gyldig HTML-dokument fra bunnen av, uten å kopiere
> - forklare hva `<!DOCTYPE html>`, `<html>`, `<head>` og `<body>` gjør
> - bruke ordene **tag**, **element**, **attributt** og **verdi** riktig
> - nøste elementer riktig og finne feil når nøstingen er gal

---

## 3.1 Koden fra sist – nå tar vi den fra hverandre

I forrige kapittel skrev du dette uten å vite hva det betydde:

```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="utf-8">
    <title>Min første nettside</title>
</head>
<body>
    <h1>Hei!</h1>
    <p>Dette er den aller første nettsiden jeg har laget.</p>
</body>
</html>
```

Dette kalles **grunnstrukturen**, og den er lik på *hver eneste nettside i verden*. NRK, Netflix,
skolens plattform – alle starter med de samme linjene. Lærer du dem nå, skriver du dem uten å tenke
resten av kurset.

Vi går gjennom linje for linje.

---

## 3.2 Tag, element, attributt og verdi

Først må vi ha ordene på plass. Dette er fire begreper du skal bruke presist, og de kommer garantert
på prøven.

HTML betyr **H**yper**T**ext **M**arkup **L**anguage. Det siste ordet er nøkkelen: HTML er et
*oppmerkingsspråk*. Du tar vanlig tekst og setter merkelapper rundt for å si hva teksten **er**.

```
<h1>Fjelltur</h1>
│   │       │
│   │       └── sluttag
│   └────────── innhold
└────────────── starttag
```

- **Tag** (merkelapp) er det som står mellom `<` og `>`. Her er `<h1>` starttagen og `</h1>` sluttagen.
  Sluttagen har alltid en skråstrek.
- **Element** er *hele greia*: starttag + innhold + sluttag. `<h1>Fjelltur</h1>` er ett element.

Noen elementer trenger mer informasjon. Da bruker vi attributter:

```
<html lang="no">
      │     │
      │     └── verdi (i anførselstegn)
      └──────── attributt
```

- **Attributt** er en ekstra opplysning om elementet. Det står alltid inne i **starttagen**.
- **Verdi** er innholdet i attributtet, alltid i doble anførselstegn.

Et element kan ha flere attributter, adskilt med mellomrom:

```html
<img src="bilder/katt.jpg" alt="En sovende katt" width="400">
```

Her har `<img>` tre attributter: `src`, `alt` og `width`.

**Oppgave 3.1 – Sett navn på delene**

Skriv av linjene under og merk av hva som er tag, element, attributt og verdi:

1. `<p>Velkommen hit.</p>`
2. `<a href="side2.html">Neste side</a>`
3. `<img src="logo.png" alt="Logo">`
4. `<html lang="no">`

*(I nr. 2: hvor mange attributter finnes det? Hva er innholdet i elementet?)*

---

## 3.3 Tomme elementer

De fleste elementer har både start- og sluttag. Noen har bare starttag, fordi de ikke har noe innhold
å pakke inn. De kalles **tomme elementer**:

```html
<br>              <!-- linjeskift -->
<hr>              <!-- vannrett strek -->
<img src="...">   <!-- bilde -->
<meta charset="utf-8">
```

Det finnes ingen `</br>` eller `</img>`. Alt disse elementene trenger, ligger i attributtene.

> Du vil av og til se skrivemåten `<br />` med skråstrek på slutten. Det er en gammel skrivemåte fra
> en variant som het XHTML. Den fungerer fortsatt, men er unødvendig. Vi bruker `<br>`.

---

## 3.4 Linje for linje

### `<!DOCTYPE html>`

Første linje i enhver HTML-fil. Den sier til nettleseren: *dette er en moderne HTML-side, tolk den
etter dagens regler.*

Dette er ikke et vanlig element – det er en instruksjon til nettleseren, derfor utropstegnet og
derfor ingen sluttag. Uten den går nettleseren inn i noe som kalles «quirks mode», der den later som
den er 20 år gammel. Da blir CSS-en din uforutsigbar. Ta den alltid med.

### `<html lang="no">`

**Rotelementet.** Alt annet på siden ligger inni dette. Det er det ytterste laget.

Attributtet `lang="no"` sier at siden er på norsk. Det virker som en bagatell, men:

- skjermlesere for blinde velger riktig uttale ut fra dette
- nettleseren vet om den skal foreslå å oversette siden
- stavekontroll i skjemafelter bruker riktig språk

Bruk `lang="no"` på norske sider, `lang="en"` på engelske.

### `<head>`

Her ligger informasjon **om** siden. **Ingenting i `<head>` vises på selve siden.**

Tenk på det som konvolutten rundt et brev: adressen, frimerket og avsenderen står utenpå, men er ikke
en del av brevet du leser.

I `<head>` legger vi tittel, tegnsett, lenke til stilarket (kommer i kapittel 10), og informasjon til
søkemotorer (kapittel 25).

### `<meta charset="utf-8">`

**Tegnsettet.** Dette bestemmer hvordan bokstavene tolkes.

Datamaskinen lagrer egentlig bare tall. `utf-8` er avtalen om hvilket tall som betyr hvilken bokstav –
og det er avtalen som omfatter æ, ø, å og alle andre språks tegn.

Glemmer du denne linjen, får du gjerne dette på skjermen:

```
KjÃ¸p pÃ¥ lÃ¸rdag
```

i stedet for «Kjøp på lørdag». Det er en av de vanligste feilene, og løsningen er alltid den samme:
sjekk at `<meta charset="utf-8">` står øverst i `<head>`.

### `<title>`

Teksten som vises i **fanen** øverst i nettleseren. Den vises også som overskrift i Google-treff og
når noen bokmerker siden.

Legg merke til: `<title>` er ikke det samme som `<h1>`. `<title>` står i `<head>` og vises i fanen.
`<h1>` står i `<body>` og vises på siden. De kan gjerne si omtrent det samme, men det er to ulike ting.

### `<body>`

Alt brukeren faktisk ser. Tekst, bilder, lenker, menyer, knapper – alt sammen ligger her.

Fra og med neste kapittel er det nesten bare `<body>` vi jobber i.

**Oppgave 3.2 – Head eller body?**

Hvor hører hver av disse hjemme? Begrunn kort.

1. En overskrift som sier «Om meg»
2. Tittelen som vises i fanen
3. Et bilde av deg selv
4. Informasjonen om at siden bruker utf-8
5. Et avsnitt med tekst
6. Lenken til stilarket ditt

---

## 3.5 Nøsting – elementer inni elementer

Elementer legges inni hverandre. Det kalles **nøsting**, og det er slik en nettside får struktur.

Regelen er enkel og absolutt: **det du åpner sist, må du lukke først.**

✅ Riktig:

```html
<p>Dette er <strong>viktig</strong> å huske.</p>
```

`<strong>` åpnes inni `<p>`, og lukkes før `</p>`. Som esker inni esker.

❌ Feil:

```html
<p>Dette er <strong>viktig å huske.</p></strong>
```

Her krysser elementene hverandre. Nettleseren gjør sitt beste for å gjette hva du mente, og noen ganger
ser det tilfeldigvis riktig ut – men før eller siden gir det merkelig oppførsel som er vanskelig å feilsøke.

### Siden er et tre

Nøstingen gjør at et HTML-dokument egentlig er et **tre**:

```
html
├── head
│   ├── meta
│   └── title
└── body
    ├── h1
    └── p
```

Sammenlikn med innrykkene i koden din: hvert innrykk er ett nivå ned i treet. Det er derfor innrykk
er verdt å holde orden på – de tegner strukturen for deg.

**Oppgave 3.3 – Tegn treet**

Tegn strukturen som et tre, slik som over:

```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="utf-8">
    <title>Turer</title>
</head>
<body>
    <h1>Mine turer</h1>
    <p>I sommer gikk jeg <strong>fem</strong> topper.</p>
    <p>Neste år blir det flere.</p>
</body>
</html>
```

Kontroller svaret ditt: åpne utviklerverktøyet (`F12`) på din egen side og se på Elements-fanen.
Der vises nøyaktig dette treet, og du kan klappe grenene sammen og ut igjen.

---

## 3.6 Kommentarer

En kommentar er tekst i koden som nettleseren hopper over. Den er til deg og til andre som leser koden.

```html
<!-- Dette er en kommentar. Den vises ikke på siden. -->

<!-- Menyen starter her -->
<h1>Velkommen</h1>
```

Kommentarer brukes til to ting:

1. **forklare** hva en del av koden gjør
2. **midlertidig slå av** kode uten å slette den – nyttig når du feilsøker

Hurtigtast: marker linjene og trykk `Ctrl + /`.

> **Husk:** kommentarer er ikke hemmelige. Alle kan lese dem med Vis kildekode. Skriv aldri noe der
> du ikke vil at andre skal se.

---

## 3.7 Nettleseren tilgir – men det gjør ikke du

Prøv dette: lag en fil med bare denne ene linjen, og åpne den i nettleseren.

```html
Hei
```

Den vises. Ingen feilmelding. Nettleseren fyller stilltiende inn `<html>`, `<head>` og `<body>` for deg.

**Så hvorfor skal du skrive alt riktig, når nettleseren likevel fikser det?**

Fordi nettleseren *gjetter*. Den gjetter ofte riktig på små sider, og ofte feil på store. Da får du en
side som ser rar ut uten at det finnes en feilmelding å lete etter. Det er en av de mest frustrerende
formene for feilsøking som finnes.

I tillegg leses koden din av andre enn nettlesere: søkemotorer, skjermlesere – og lærere og kolleger.

Dette skiller HTML fra de fleste andre programmeringsspråk. Gjør du en skrivefeil i Python, stopper
programmet og sier fra. HTML sier aldri fra. Ansvaret er ditt.

---

## 3.8 Finn feilen

**Oppgave 3.4**

I hver av de fem kodesnuttene er det nøyaktig én feil. Finn den, forklar hva som er galt, og skriv den
riktige versjonen.

**A**
```html
<!DOCTYPE html>
<html lang="no">
<head>
    <title>Min side</title>
</head>
<body>
    <h1>Hei</h1>
    <p>Velkommen.</p>
</html>
```

**B**
```html
<body>
    <h1>Sykling</h1>
    <p>Jeg syklet <em>hele veien</p></em>
</body>
```

**C**
```html
<head>
    <meta charset="utf-8">
    <title>Om meg</title>
    <h1>Om meg</h1>
</head>
<body>
    <p>Jeg heter Nora.</p>
</body>
```

**D**
```html
<html lang="no">
<head>
    <title>Kontakt<title>
</head>
<body>
    <p>Send meg en melding.</p>
</body>
</html>
```

**E**
```html
<!DOCTYPE html>
<html lang="no">
<head>
    <title>Turer</title>
</head>
<body>
    <h1>Turer</h1>
    <img src="fjell.jpg" alt="Fjell"></img>
</body>
</html>
```

---

## 3.9 Hva gjør denne koden?

**Oppgave 3.5**

```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="utf-8">
    <title>Kake</title>
</head>
<body>
    <!-- <h1>Sjokoladekake</h1> -->
    <p>Deilig og enkel.</p>
</body>
</html>
```

1. Hva står det i nettleserfanen?
2. Hva vises på selve siden?
3. Hvorfor vises ikke «Sjokoladekake»?

**Oppgave 3.6**

En elev har skrevet `<title>` inne i `<body>` i stedet for i `<head>`. Hva tror du skjer i fanen?
Sjekk etterpå i nettleseren om du hadde rett.

---

## 3.10 Skriv den selv

**Oppgave 3.7 – Uten å kopiere**

Lag en ny fil i prosjektet ditt: `om-meg.html`.

Skriv hele grunnstrukturen **fra hukommelsen**. Ikke se på `index.html`, og ikke kopier fra dette
dokumentet. Får du det ikke til, ta en titt – lukk igjen, og prøv på nytt.

Siden skal inneholde:

- riktig doctype og språkkode
- riktig tegnsett
- en tittel i fanen som er ditt navn
- en `<h1>` med teksten «Om meg»
- to avsnitt om deg selv
- minst én kommentar i koden

Kontroller til slutt at innrykkene er ryddige (`Shift + Alt + F`), og at siden vises riktig med Live Server.

> **Snarvei du får bruke – etterpå:** Skriv `!` og trykk `Tab` i en tom HTML-fil i VS Code, så skrives
> hele grunnstrukturen automatisk. Dette heter Emmet. Bruk den gjerne resten av kurset – men først når
> du klarer å skrive strukturen selv. På prøven finnes ingen Tab-tast.

---

## 3.11 Oppsummering

- **Grunnstrukturen er lik på alle nettsider.** Lær den utenat.
- **Tag** = merkelappen. **Element** = starttag + innhold + sluttag. **Attributt** = ekstra
  opplysning i starttagen. **Verdi** = innholdet i attributtet, i anførselstegn.
- **Tomme elementer** (`<br>`, `<hr>`, `<img>`, `<meta>`) har ingen sluttag.
- `<!DOCTYPE html>` – si at dette er moderne HTML
- `<html lang="no">` – rotelementet, med språk
- `<head>` – informasjon om siden, vises ikke
- `<meta charset="utf-8">` – gjør at æ, ø og å virker
- `<title>` – teksten i fanen
- `<body>` – alt brukeren ser
- **Nøsting:** det du åpner sist, lukker du først.
- Nettleseren sier ikke fra når du gjør feil. Det er derfor du må kunne dette.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| HTML | HyperText Markup Language – oppmerkingsspråket for nettsider |
| Oppmerking | Å sette merkelapper rundt innhold for å si hva det er |
| Tag | Merkelappen mellom `<` og `>` |
| Starttag / sluttag | `<p>` og `</p>` – sluttagen har skråstrek |
| Element | Hele enheten: starttag + innhold + sluttag |
| Tomt element | Element uten sluttag, f.eks. `<br>` og `<img>` |
| Attributt | Ekstra opplysning inne i starttagen, f.eks. `lang` |
| Verdi | Innholdet i attributtet, i doble anførselstegn |
| Grunnstruktur | Rammeverket alle HTML-sider har |
| `<!DOCTYPE html>` | Forteller nettleseren at dette er moderne HTML |
| Rotelement | `<html>` – elementet alt annet ligger inni |
| `<head>` | Informasjon om siden; vises ikke på siden |
| `<body>` | Innholdet brukeren ser |
| Tegnsett / `utf-8` | Avtalen om hvordan bokstaver lagres – gjør æøå mulig |
| Nøsting | Elementer som ligger inni hverandre |
| Kommentar | `<!-- tekst -->` – ignoreres av nettleseren |

---

## Innlevering – kapittel 3

Lever i læringsloggen din:

1. `om-meg.html` fra oppgave 3.7, og et skjermbilde av siden i nettleseren.
2. Svarene på oppgave 3.1 og 3.2.
3. Treet du tegnet i oppgave 3.3.
4. Alle fem feilene fra oppgave 3.4, med forklaring på hva som var galt.
5. Svarene på oppgave 3.5.

**Sjekkliste før du går videre:**

- [ ] Jeg kan skrive grunnstrukturen uten å se på noe
- [ ] Jeg vet forskjellen på en tag og et element
- [ ] Jeg kan peke ut attributt og verdi i en linje kode
- [ ] Jeg vet hva som skal i `<head>` og hva som skal i `<body>`
- [ ] Jeg vet hvorfor `<meta charset="utf-8">` må være med

---

**Neste kapittel:** Nå har vi rammen. Da fyller vi den med innhold – overskrifter, avsnitt og
tekst som er merket opp riktig.

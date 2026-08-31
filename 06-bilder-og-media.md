# Kapittel 6 – Bilder og media

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - legge inn bilder på nettsiden din med riktig sti
> - skrive gode alt-tekster og forklare hvorfor de er obligatoriske
> - velge riktig bildeformat og fornuftig filstørrelse
> - finne bilder du faktisk har lov til å bruke, og oppgi kilde

---

## 6.1 Bildet ligger ikke i HTML-fila

Dette er det første du må forstå, og det overrasker mange:

> **Et bilde er ikke en del av nettsiden. Det er en egen fil som nettsiden peker på.**

HTML-fila di sier bare: «her skal det være et bilde, og det ligger der borte.» Nettleseren gjør så en
helt ny forespørsel til tjeneren for å hente det – akkurat den prosessen du lærte om i kapittel 1.

Konsekvensen: peker du feil, kommer bildet aldri. HTML-en din er fortsatt helt riktig. Fila er bare
ikke der du sa den var.

Elementet heter `<img>`:

```html
<img src="bilder/profil.jpg" alt="Portrett av meg foran skolen">
```

- `<img>` er et **tomt element** – ingen sluttag
- `src` (*source*) er stien til bildefila
- `alt` er en tekstlig beskrivelse av bildet

**Begge attributtene skal alltid være med.**

---

## 6.2 Stien igjen

Her får du bruk for alt fra forrige kapittel. Reglene er nøyaktig de samme som for lenker:

```
webkurs/
├── index.html
├── bilder/
│   └── profil.jpg
└── turer/
    └── besseggen.html
```

Fra `index.html`:

```html
<img src="bilder/profil.jpg" alt="...">
```

Fra `turer/besseggen.html`:

```html
<img src="../bilder/profil.jpg" alt="...">
```

**De tre klassiske grunnene til at et bilde ikke vises:**

1. **Feil sti** – bildet ligger ikke der du sier
2. **Feil filnavn** – `Profil.JPG` er ikke det samme som `profil.jpg` på en ekte tjener
3. **Bildet er ikke kopiert inn i prosjektmappen** – det ligger fortsatt i Nedlastinger

Nummer tre er den vanligste. Bildet må **flyttes eller kopieres inn i `bilder/`-mappen** før du peker
på det. Ligger det i Nedlastinger, virker siden på din maskin akkurat nå, og ingen andre steder.

**Oppgave 6.1 – Første bilde**

1. Finn eller ta et bilde.
2. Gi det et lovlig filnavn: små bokstaver, ingen mellomrom, ingen æøå.
3. Kopier det inn i `bilder/`-mappen i prosjektet ditt.
4. Legg det inn på `om-meg.html` med `<img>` og en beskrivende alt-tekst.
5. Legg det samme bildet inn på en side som ligger i `turer/`-mappen. Legg merke til at stien blir
   en annen.

---

## 6.3 Alt-teksten

`alt` er en tekst som beskriver bildet. Den brukes i tre situasjoner:

- **Skjermlesere** leser den opp. For en blind bruker *er* alt-teksten bildet.
- **Bildet lastes ikke** – dårlig nett, feil sti – og teksten vises i stedet.
- **Søkemotorer** bruker den til å forstå hva bildet viser.

I Norge er dette ikke bare god skikk. Nettsider er omfattet av kravene til universell utforming, og
manglende alt-tekst er et av de vanligste bruddene.

### Hvordan skrive en god alt-tekst

Spør deg selv: **hvis jeg måtte lese denne siden opp for noen på telefon, hva ville jeg sagt om bildet?**

| ❌ Dårlig | ✅ Bedre | Hvorfor |
|---|---|---|
| `alt="bilde"` | `alt="Elev som koder på en bærbar PC"` | Sier faktisk hva det er |
| `alt="IMG_2049.jpg"` | `alt="Utsikt fra Besseggen mot Gjende"` | Filnavn er ikke en beskrivelse |
| `alt="bilde av en hund som løper over en gressplen mens solen går ned bak trærne i bakgrunnen"` | `alt="Hund som løper over en gressplen"` | Kort og presist slår langt og detaljert |
| `alt="klikk her"` | `alt="Last ned timeplanen"` | Beskriv innholdet, ikke handlingen |

Regler som sitter:

- Ikke start med «bilde av» – skjermleseren sier allerede at det er et bilde
- Hold deg til én kort setning
- Beskriv det som er **relevant i sammenhengen**. Et bilde av en katt i en dyrebutikkannonse og i en
  artikkel om kattesykdommer trenger ikke samme beskrivelse.

### Når alt-teksten skal være tom

Er bildet ren dekorasjon – en pyntestrek, et bakgrunnsmønster – skal `alt` være tomt:

```html
<img src="bilder/pyntelinje.png" alt="">
```

Da vet skjermleseren at den trygt kan hoppe over det. **Tomt er ikke det samme som å utelate `alt`.**
Utelater du attributtet helt, leser skjermleseren gjerne opp filnavnet i stedet – og «i-m-g-underscore-
to-null-fire-ni-punktum-j-p-g» hjelper ingen.

**Oppgave 6.2 – Skriv alt-tekster**

Skriv alt-tekst for hvert av disse bildene, i den sammenhengen de står:

1. Et portrett av deg på «Om meg»-siden
2. Skolens logo øverst på forsiden
3. Et diagram som viser at søkertallet til IM steg fra 120 til 180
4. En dekorativ bølgestrek mellom to seksjoner
5. Et skjermbilde av VS Code i en veiledning om Live Server

*(Nr. 3 er den vanskeligste: alt-teksten må formidle det diagrammet **viser**, ikke at det er et diagram.)*

---

## 6.4 Bildeformater

Å velge riktig format er en reell faglig vurdering, ikke en detalj.

| Format | Bruk til | Gjennomsiktighet | Merknad |
|---|---|---|---|
| **JPG** | Fotografier | Nei | Komprimerer godt, mister litt kvalitet |
| **PNG** | Grafikk, logoer, skjermbilder | Ja | Skarpe kanter, større filer |
| **SVG** | Logoer, ikoner, illustrasjoner | Ja | Tegnet med matematikk – skalerer uendelig |
| **WEBP** | Alt, egentlig | Ja | Moderne, minst filstørrelse |
| **GIF** | Korte animasjoner | Delvis | Gammelt og dårlig kvalitet – unngå til foto |

**Enkel regel:** foto → JPG (eller WEBP). Grafikk med skarpe kanter eller gjennomsiktighet → PNG.
Logo eller ikon → SVG hvis du har det.

### SVG er noe helt annet

JPG og PNG er **punktgrafikk**: et rutenett av fargede piksler. Forstørrer du dem, blir de uskarpe.

SVG er **vektorgrafikk**: en beskrivelse av former – «en sirkel her, en linje dit». Nettleseren tegner
den på nytt i akkurat den størrelsen som trengs. Derfor er en SVG-logo like skarp på 20 piksler som på
2000, og fila er ofte bare noen få kilobyte.

En SVG-fil er faktisk tekst. Åpne en i VS Code, så ser du kode som ligner mistenkelig på HTML.

---

## 6.5 Filstørrelse betyr noe

Et bilde rett fra mobilkameraet er typisk 4000 × 3000 piksler og 5 MB. På en nettside skal det kanskje
vises i 600 pikslers bredde.

Legger du inn originalen, må hver eneste besøkende laste ned alle 5 MB – for å se en sekstendedel av
den oppløsningen. På mobil, på dårlig nett, koster det både tid og datatrafikk.

**Tommelfingerregler:**

| Bruk | Fornuftig bredde | Fornuftig filstørrelse |
|---|---|---|
| Lite bilde i en tekst | 600–800 px | under 100 kB |
| Stort bilde over hele bredden | 1600–2000 px | under 300 kB |
| Logo | så liten som mulig | under 50 kB |

Endre størrelsen **før** du legger bildet i prosjektet. Du kan bruke Photos/Forhåndsvisning, Paint,
Photopea eller et hvilket som helst bilderedigeringsprogram.

> **Å sette `width="600"` i HTML gjør ikke fila mindre.** Den fulle fila lastes ned uansett, og
> krympes bare på skjermen. Størrelsen må endres i selve bildefila.

**Oppgave 6.3 – Mål effekten**

1. Ta et bilde rett fra mobilen og legg det i prosjektet. Noter filstørrelsen.
2. Lag en kopi som er 800 piksler bred og lagre som JPG. Noter filstørrelsen.
3. Legg begge inn på en testside ved siden av hverandre, begge vist i 800 pikslers bredde.
4. Ser du forskjell på skjermen? Hvor mange ganger mindre ble fila?

Skriv én setning om hva dette betyr for en bruker på mobilnett.

---

## 6.6 Størrelse i HTML

```html
<img src="bilder/profil.jpg" alt="Portrett" width="600" height="400">
```

Attributtene `width` og `height` oppgis i piksler, uten enhet.

Her er en detalj som er verdt å vite: **oppgi begge, i bildets faktiske forhold.** Da vet nettleseren
hvor mye plass bildet skal ha *før* det er lastet ned, og siden slutter å hoppe rundt mens innholdet
kommer inn. Du har garantert opplevd å trykke på feil sted fordi siden flyttet seg i siste liten –
dette er en av grunnene.

Oppgir du bare den ene, eller feil forhold, blir bildet strukket og ser rart ut.

Fra kapittel 12 og utover styrer vi som regel bildestørrelse med CSS i stedet, fordi det gir mer
kontroll. Men `width` og `height` i HTML har fortsatt denne ene nyttige jobben.

---

## 6.7 Bilde med bildetekst

Hører bildeteksten til bildet, binder du dem sammen:

```html
<figure>
    <img src="bilder/besseggen.jpg" alt="Smal fjellrygg med vann på begge sider">
    <figcaption>Utsikten fra Besseggen mot Gjende. Foto: Nora Hansen</figcaption>
</figure>
```

`<figure>` er en enhet som hører sammen; `<figcaption>` er teksten som forklarer den.

Merk at alt-tekst og bildetekst ikke er det samme, og ikke skal si det samme:

- **alt** beskriver *hvordan bildet ser ut*, for den som ikke kan se det
- **figcaption** gir *tilleggsinformasjon*, og leses av alle

`<figure>` kan også brukes om diagrammer, kodeeksempler og tabeller – alt som er en avgrenset enhet med
en forklarende tekst.

**Oppgave 6.4 – Et lite galleri**

Lag en ny side `bilder.html` med tre til fem bilder, hvert i sin `<figure>` med bildetekst og alt-tekst.
Legg til menyen din øverst, og legg siden inn i menyen på alle de andre sidene.

Bildene skal være skalert til fornuftig størrelse, ha lovlige filnavn og ligge i `bilder/`-mappen.

---

## 6.8 Har du lov til å bruke bildet?

Kortversjonen: **et bilde du finner ved å google, har du som regel ikke lov til å bruke.**

Alle bilder har en opphavsperson, og den som har tatt bildet bestemmer over det. Det gjelder også
bilder som ligger fritt tilgjengelig på nett.

### Steder du kan hente bilder du har lov til å bruke

- **Unsplash**, **Pexels**, **Pixabay** – gratis foto, fri bruk
- **Wikimedia Commons** – enorm samling, men les lisensen for hvert bilde
- **openverse.org** – søker på tvers av flere kilder med åpne lisenser
- **Dine egne bilder** – alltid trygt

### Creative Commons

Mange bilder er merket med en CC-lisens som sier hva du får lov til:

| Merking | Betyr |
|---|---|
| CC0 | Fri bruk, ingen krav |
| CC BY | Fri bruk, men du **må** oppgi opphavsperson |
| CC BY-SA | Som over, og din versjon må ha samme lisens |
| CC BY-NC | Bare ikke-kommersiell bruk |
| CC BY-ND | Du kan ikke endre bildet |

**Oppgi alltid kilde**, også når du ikke må. Det koster én linje:

```html
<figcaption>Foto: Ola Nordmann / Unsplash</figcaption>
```

### Og bilder av mennesker

Er noen gjenkjennelige på bildet, trenger du samtykke fra dem før du legger det ut. Det gjelder også
medelever. Er du i tvil: spør, eller bruk et annet bilde.

**Oppgave 6.5 – Finn og krediter**

Finn tre bilder du lovlig kan bruke i prosjektet ditt. For hvert bilde, noter i loggen:

1. Hvor du fant det
2. Hvilken lisens det har
3. Hvem som har tatt det
4. Hvordan du har kreditert det på siden

---

## 6.9 Video og lyd

```html
<video src="video/tur.mp4" controls width="600"></video>

<audio src="lyd/intervju.mp3" controls></audio>
```

`controls` gir avspillingsknapper. Uten det får brukeren ingen måte å starte på.

Andre attributter du vil møte: `autoplay`, `loop` og `muted`. Vær varsom med `autoplay` – video som
starter av seg selv med lyd er en av de tingene brukere misliker sterkest, og de fleste nettlesere
blokkerer det uansett med mindre videoen er `muted`.

Videofiler er store. Legger du en telefonvideo rett inn, snakker vi fort hundrevis av megabyte. Derfor
legger de fleste video på YouTube eller Vimeo og bygger den inn i stedet:

```html
<iframe width="560" height="315"
        src="https://www.youtube.com/embed/VIDEO-ID"
        title="Beskrivelse av videoen"
        allowfullscreen></iframe>
```

`<iframe>` er et vindu inn i en annen nettside. Den brukes også til kart, kalendere og skjemaer.
På YouTube får du koden ved å velge **Del → Bygg inn**.

**Oppgave 6.6 – Bygg inn noe**

Legg til én av delene på en av sidene dine:

- en video du selv har laget, med `<video controls>`, eller
- et innebygd YouTube-klipp som passer til innholdet, eller
- et Google-kart over et sted du skriver om

---

## 6.10 Oppsummering

- Bildet er en **egen fil** som HTML-en peker på med `src`.
- Stien til bildet følger nøyaktig samme regler som lenker: `bilder/x.jpg`, `../bilder/x.jpg`.
- Bildet må ligge **inni prosjektmappen**, ikke i Nedlastinger.
- `alt` er obligatorisk. Tom `alt=""` for rene pyntebilder – men attributtet skal være der.
- **JPG** til foto, **PNG** til grafikk og gjennomsiktighet, **SVG** til logoer og ikoner, **WEBP** når du kan.
- Skaler bildet **før** du legger det inn. `width` i HTML gjør ikke fila mindre.
- Oppgi `width` og `height` i riktig forhold, så slutter siden å hoppe under lasting.
- `<figure>` + `<figcaption>` binder bilde og bildetekst sammen.
- Bilder du finner på nett er som regel opphavsrettsbeskyttet. Bruk frie kilder og oppgi alltid fotograf.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| `<img>` | Bildeelementet – et tomt element |
| `src` | Attributtet som peker på bildefila |
| `alt` | Tekstlig beskrivelse av bildet |
| Punktgrafikk | Bilde bygget av piksler (JPG, PNG) – blir uskarpt ved forstørring |
| Vektorgrafikk | Bilde beskrevet med former (SVG) – skarpt i alle størrelser |
| Komprimering | Å redusere filstørrelsen, ofte med litt tap av kvalitet |
| Oppløsning | Antall piksler i bredden og høyden |
| `<figure>` / `<figcaption>` | Bilde med tilhørende bildetekst |
| `<iframe>` | Vindu som viser innhold fra en annen nettside |
| Opphavsrett | Retten skaperen har til å bestemme over sitt eget verk |
| Creative Commons | Lisenssystem som sier hva du har lov til med et verk |
| Kreditering | Å oppgi hvem som har laget det du bruker |

---

## Innlevering – kapittel 6

Lever i læringsloggen din:

1. `bilder.html` fra oppgave 6.4, med skjermbilde.
2. Alt-tekstene fra oppgave 6.2.
3. Målingen fra oppgave 6.3: filstørrelse før og etter, og din vurdering.
4. Kildelista fra oppgave 6.5 med lisens for hvert bilde.
5. Skjermbilde av det innebygde innholdet fra oppgave 6.6.

**Sjekkliste før du går videre:**

- [ ] Alle bildene mine ligger i `bilder/`-mappen med lovlige filnavn
- [ ] Alle `<img>` har `alt` – beskrivende, eller tom hvis bildet er ren pynt
- [ ] Ingen av bildene mine er større enn de trenger å være
- [ ] Jeg har oppgitt kilde på bilder jeg ikke har tatt selv
- [ ] Bildene vises også fra sider som ligger i undermapper

---

**Neste kapittel:** Lister og tabeller – og menyen din blir endelig en ordentlig liste.

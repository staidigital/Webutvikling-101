# Webutvikling – HTML & CSS
### Kursstruktur for Vg1 Informasjonsteknologi og medieproduksjon (Elvebakken vgs)

**Omfang:** 3 perioder · **Verktøy:** VS Code + Live Server · **Innhold:** rent HTML og CSS (ingen JavaScript)
**Vurdering:** skriftlig prøve uten hjelpemidler med vekt på forståelse + deloppgaver underveis
**Status:** utkast til struktur – kapitler og stikkord

---

## Bærende idé

Kurset bygger én ferdighet av gangen, og hvert kapittel avsluttes med små, konkrete deloppgaver
framfor ett stort hopp til slutt. Elevene bygger parallelt på **én sammenhengende nettside** som
vokser gjennom hele kurset, samtidig som de gjør korte frittstående øvelser for å drille enkeltemner.

Tre gjennomgående oppgavetyper, som også er oppgavetypene på prøven:

| Type | Hva eleven gjør | Trener |
|---|---|---|
| **Bygg** | Skriver kode fra bunnen etter en beskrivelse | Produksjon |
| **Les koden** | Forklarer hva en kodesnutt gjør / hvordan siden blir seende ut | Forståelse |
| **Finn feilen** | Retter kode som ikke virker eller mangler noe | Feilsøking |

---

## Periodeoversikt

| Periode | Del | Hovedinnhold | Kapitler |
|---|---|---|---|
| **1** | Grunnmuren | Hvordan nettet virker, verktøy, all sentral HTML, semantikk, flersides nettsted | 1–9 |
| **2** | Utseendet | CSS fra selektorer til boksmodell, Flexbox, Grid og responsivt design | 10–20 |
| **3** | Håndverket | Skjemaer, tilgjengelighet, design, feilsøking, publisering, repetisjon | 21–26 |

---

# DEL 1 – GRUNNMUREN (HTML)

## Kapittel 1 – Hva er egentlig en nettside?

**Mål:** Eleven kan forklare hva som skjer fra man skriver en adresse til siden vises.

**Stikkord:** internett vs. web · klient og tjener · nettleser · nettadresse (URL) · domene · HTTP(S) ·
kildekode · HTML = innhold og struktur, CSS = utseende, JavaScript = oppførsel · frontend vs. backend ·
filtypene .html og .css

**Deloppgaver:**
- Åpne «vis kildekode» på tre kjente nettsider og finn igjen `<h1>`, `<img>` og `<a>`
- Bruk utviklerverktøyet til å endre en overskrift på en avisforside og ta skjermbilde
- Tegn i to setninger + en enkel skisse hva som skjer når du skriver inn en nettadresse

---

## Kapittel 2 – Verktøy og arbeidsflyt

**Mål:** Eleven har et fungerende utviklingsmiljø og en ryddig prosjektmappe.

**Stikkord:** VS Code · utvidelser · Live Server · mappestruktur · `index.html` · undermapper (`bilder/`, `css/`) ·
filnavn uten æøå og mellomrom · lagre og oppdatere · hurtigtaster · innrykk og formatering (Shift+Alt+F)

**Deloppgaver:**
- Sett opp mappen `webkurs/` med `index.html`, `style.css` og `bilder/`
- Start Live Server og se at endringer vises umiddelbart
- Ryddeoppgave: gitt en rotete filliste – hvor hører hver fil hjemme?

---

## Kapittel 3 – HTML-grunnstruktur

**Mål:** Eleven kan skrive et gyldig HTML-dokument fra bunnen av og bruke riktige fagbegreper.

**Stikkord:** `<!DOCTYPE html>` · `<html lang="no">` · `<head>` vs `<body>` · `<title>` · `<meta charset="utf-8">` ·
tag / element / attributt / verdi · start- og sluttag · tomme elementer (`<br>`, `<img>`) ·
nøsting (elementer inni elementer) · kommentarer `<!-- -->` · innrykk som lesbarhet

**Deloppgaver:**
- Skriv hele grunnstrukturen for hånd uten å kopiere
- **Finn feilen:** fem dokumenter med manglende sluttag, feil nøsting, tag i feil seksjon
- **Les koden:** pek ut tag, element, attributt og verdi i en gitt linje

---

## Kapittel 4 – Tekst og innhold

**Mål:** Eleven kan strukturere en tekstside med riktig hierarki.

**Stikkord:** `<h1>`–`<h6>` og overskriftshierarki (kun én `<h1>`) · `<p>` · `<br>` og `<hr>` ·
`<strong>` og `<em>` (betydning) vs `<b>` og `<i>` (utseende) · `<span>` · `<blockquote>` ·
mellomrom som HTML ignorerer · spesialtegn (`&nbsp;`, `&amp;`, `&lt;`)

**Deloppgaver:**
- Marker opp en gitt råtekst (f.eks. en artikkel) med riktige overskriftsnivåer og avsnitt
- **Les koden:** hvorfor blir ikke de fem linjeskiftene i editoren synlige i nettleseren?
- Lag «Om meg»-siden – første side i det gjennomgående prosjektet

---

## Kapittel 5 – Lenker

**Mål:** Eleven kan lenke både internt og eksternt, og forstår filstier.

**Stikkord:** `<a href="...">` · absolutt vs. relativ sti · `./`, `../`, undermapper ·
lenke til annen side i eget prosjekt · `target="_blank"` · `title` · ankerlenker med `id` (`href="#kontakt"`) ·
`mailto:` og `tel:` · hva som er god lenketekst («les mer» er dårlig)

**Deloppgaver:**
- Lag en meny som lenker mellom tre sider i eget prosjekt
- Stioppgave: gitt en mappestruktur – skriv riktig `href` fra fil A til fil B (5 varianter)
- **Finn feilen:** fire lenker som er brutte, med ulik årsak

---

## Kapittel 6 – Bilder og media

**Mål:** Eleven kan legge inn bilder på en riktig og hensiktsmessig måte.

**Stikkord:** `<img src alt>` · alt-tekst og hvorfor den er obligatorisk · `width`/`height` som attributt vs. CSS ·
filformater: JPG, PNG, SVG, WEBP, GIF · filstørrelse og lastetid · opphavsrett, frie bilder, kildehenvisning ·
`<figure>` og `<figcaption>` · `<video>` og `<audio>` med `controls` · innebygd innhold med `<iframe>` (kart, video)

**Deloppgaver:**
- Legg inn tre bilder fra egen `bilder/`-mappe med gode alt-tekster
- Sammenlign samme bilde i tre formater/størrelser – hvilket velger du og hvorfor?
- **Les koden:** hva vises hvis `src` er feil, men `alt` er riktig?

---

## Kapittel 7 – Lister og tabeller

**Mål:** Eleven velger riktig element til riktig type innhold.

**Stikkord:** `<ul>`, `<ol>`, `<li>` · nøstede lister · `<dl>`, `<dt>`, `<dd>` ·
`<table>`, `<tr>`, `<th>`, `<td>` · `<thead>`, `<tbody>` · `<caption>` · `colspan`/`rowspan` ·
tabeller er for data, ikke for layout

**Deloppgaver:**
- Lag en meny/oppskrift med nøstede lister
- Sett opp en timeplan eller resultattabell med overskriftsrad
- **Les koden:** hvor mange kolonner har denne tabellen?

---

## Kapittel 8 – Semantisk HTML

**Mål:** Eleven kan bygge opp en side med meningsbærende elementer, ikke bare `<div>`.

**Stikkord:** `<div>` som nøytral boks · semantikk = mening · `<header>`, `<nav>`, `<main>`, `<section>`,
`<article>`, `<aside>`, `<footer>` · hvorfor semantikk betyr noe (skjermlesere, søkemotorer, lesbar kode) ·
«div-suppe» · `id` og `class` som navn på deler av siden

**Deloppgaver:**
- Skriv om en ferdig side full av `<div>` til semantiske elementer
- Tegn kart over en kjent nettside og sett navn på hver region
- **Les koden:** hvilke deler av siden mangler semantikk her?

---

## Kapittel 9 – Et helt nettsted

**Mål:** Eleven kan lage og navigere mellom flere sider med felles struktur.

**Stikkord:** flere HTML-filer · felles meny på alle sider · konsekvent struktur · aktiv side i menyen ·
`index.html` som forside · navngiving av filer · gjenbruk ved kopiering (og hvorfor det er slitsomt)

**Deloppgaver:**
- Utvid prosjektet til fire sider med lik meny
- Sjekkliste-gjennomgang av egen HTML før del 2 starter

> **Sjekkpunkt 1 – HTML:** kort quiz + innlevering av nettstedet uten CSS. Alt skal fungere og være riktig
> strukturert *før* utseendet kommer inn.

---

# DEL 2 – UTSEENDET (CSS)

## Kapittel 10 – Kom i gang med CSS

**Mål:** Eleven kan koble CSS til HTML og lese CSS-syntaks presist.

**Stikkord:** tre måter: inline, `<style>` i head, ekstern fil · `<link rel="stylesheet" href="style.css">` ·
regel = selektor + deklarasjonsblokk · deklarasjon = egenskap: verdi; · semikolon og krøllparenteser ·
kommentarer `/* */` · hvorfor ekstern fil er best

**Deloppgaver:**
- Koble `style.css` til alle sidene og gi hele nettstedet én bakgrunnsfarge
- **Finn feilen:** fem CSS-regler med manglende `;`, `}`, kolon eller feil filsti
- **Les koden:** navngi delene i regelen `h1 { color: red; }`

---

## Kapittel 11 – Selektorer, kaskade og arv

**Mål:** Eleven kan treffe akkurat de elementene den vil style.

**Stikkord:** elementselektor · klasse `.` · id `#` · når bruke klasse vs. id · gruppering `h1, h2` ·
etterkommer `nav a` · barn `>` · universell `*` · attributtselektor · pseudoklasser `:hover`, `:focus`,
`:first-child`, `:nth-child()` · spesifisitet · rekkefølge/kaskade · arv (hva arves, hva arves ikke) ·
utviklerverktøy: se hvilken regel som vinner

**Deloppgaver:**
- Selektor-jakt: treff 10 gitte elementer på en side, én selektor til hver
- **Les koden:** to regler treffer samme element – hvilken vinner, og hvorfor?
- CSS Diner (nettøvelse) som drilling

---

## Kapittel 12 – Farger og bakgrunn

**Mål:** Eleven kan bruke farger bevisst og forstår fargeformatene.

**Stikkord:** fargenavn · HEX `#3a7bd5` · RGB / RGBA · HSL · gjennomsiktighet og `opacity` ·
`color` vs `background-color` · `background-image`, `background-size: cover`, `background-position`,
`background-repeat` · `linear-gradient()` · kontrast og lesbarhet · fargepalett og fargevelgerverktøy

**Deloppgaver:**
- Lag tre fargepaletter til nettstedet og velg én med begrunnelse
- Konverteringsøvelse: samme farge i navn, HEX og RGB
- **Les koden:** hvilken tekst blir usynlig her, og hvorfor?

---

## Kapittel 13 – Typografi

**Mål:** Eleven kan sette lesbar og bevisst tekst.

**Stikkord:** `font-family` og fallback-stabel · serif / sans-serif / monospace · Google Fonts og `@import`/`<link>` ·
`font-size` · enhetene `px`, `em`, `rem`, `%` · `font-weight` · `font-style` · `line-height` og lesbarhet ·
`letter-spacing` · `text-align` · `text-transform` · `text-decoration` (og å fjerne strek under lenker) ·
typografisk hierarki

**Deloppgaver:**
- Sett opp en typografiskala for nettstedet (h1, h2, brødtekst)
- Sammenlign `px`, `em` og `rem` i praksis – hva skjer når rot-størrelsen endres?
- Redesign av en «stygg» tekstside, kun med typografi

---

## Kapittel 14 – Boksmodellen

**Mål:** Eleven kan forklare og styre plassen et element tar.

**Stikkord:** innhold · `padding` · `border` · `margin` · kortform (`margin: 10px 20px`) ·
`width`, `height`, `max-width`, `min-height` · `box-sizing: border-box` og hvorfor · marginkollaps ·
sentrering med `margin: 0 auto` · `border-radius` · boksmodellen i utviklerverktøyet

**Deloppgaver:**
- Regn ut total bredde på et element med padding og border (med og uten `border-box`)
- Gjenskap tre gitte bokser pikselnøyaktig
- **Les koden:** hvorfor er det 40 px mellom disse to boksene og ikke 60?

---

## Kapittel 15 – Display og flyt

**Mål:** Eleven forstår hvordan elementer plasserer seg som standard.

**Stikkord:** normal dokumentflyt · `display: block` / `inline` / `inline-block` / `none` ·
hvilke elementer er hva som standard · `visibility: hidden` vs `display: none` · `overflow`

**Deloppgaver:**
- Eksperiment: gjør `<span>` til block og `<div>` til inline – beskriv hva som skjer
- **Les koden:** hvorfor legger disse to boksene seg under hverandre?

---

## Kapittel 16 – Posisjonering

**Mål:** Eleven kan flytte elementer ut av normal flyt når det trengs.

**Stikkord:** `position: static / relative / absolute / fixed / sticky` · `top`, `right`, `bottom`, `left` ·
posisjonering i forhold til hva? · `z-index` og lagdeling · fast toppmeny · «klistrete» overskrift ·
når posisjonering *ikke* er riktig verktøy

**Deloppgaver:**
- Lag et bilde med tekst-badge oppe i hjørnet
- Lag en meny som blir liggende fast ved skrolling
- **Finn feilen:** `top: 20px` som ikke gjør noe – hvorfor?

---

## Kapittel 17 – Flexbox

**Mål:** Eleven kan bygge fleksible rader og kolonner. *(Bygges rolig opp – dette er nøkkelkapitlet.)*

**Stikkord:** `display: flex` · flex-container vs. flex-element · hovedakse og kryssakse ·
`flex-direction: row / column` · `justify-content` · `align-items` · `align-content` · `gap` ·
`flex-wrap` · `flex-grow`, `flex-shrink`, `flex-basis` · kortformen `flex: 1` · `align-self` · `order` ·
nøstede flex-containere

**Deloppgaver:**
- Flexbox Froggy (nettøvelse) – alle 24 nivåer
- Bygg en horisontal navigasjonsmeny med logo til venstre og lenker til høyre
- Bygg et kortgalleri med tre kort på rad og luft mellom
- Sentrer et element både vannrett og loddrett
- Gjenskap fem gitte layoutskisser (økende vanskegrad)
- **Les koden:** hvilken vei legger elementene seg når `flex-direction` endres?

---

## Kapittel 18 – CSS Grid

**Mål:** Eleven kan bygge rutenettbaserte layouter i to dimensjoner.

**Stikkord:** `display: grid` · `grid-template-columns` / `-rows` · enheten `fr` · `repeat()` · `gap` ·
`grid-column` / `grid-row` som spenn · navngitte områder med `grid-template-areas` ·
`minmax()` og `auto-fit` · når Grid er bedre enn Flexbox (og omvendt)

**Deloppgaver:**
- Grid Garden (nettøvelse)
- Bygg et bildegalleri der ett bilde spenner over to kolonner
- Bygg en klassisk sidelayout (header / meny / innhold / sidefelt / footer) med `grid-template-areas`
- **Les koden:** hvor mange kolonner gir `repeat(3, 1fr)`, og hvor brede blir de?

---

## Kapittel 19 – Responsivt design

**Mål:** Eleven kan lage en side som fungerer på både mobil og PC.

**Stikkord:** hvorfor responsivt (skjermstørrelser, mobilbruk) · `<meta name="viewport">` ·
relative enheter `%`, `vw`, `vh`, `rem` · `max-width` på bilder og containere · media queries `@media` ·
brytepunkter · mobile first vs. desktop first · responsiv meny (uten JavaScript: enkel omorganisering) ·
teste med utviklerverktøyets enhetsvisning

**Deloppgaver:**
- Gjør kortgalleriet fra kapittel 17 responsivt: 3 → 2 → 1 kolonne
- Sett tre brytepunkter på hele nettstedet og dokumenter med skjermbilder
- **Finn feilen:** side som «zoomer feil» på mobil fordi viewport-metataggen mangler

---

## Kapittel 20 – Detaljer, effekter og struktur i CSS

**Mål:** Eleven kan gi siden en gjennomført finish og holde CSS-filen ryddig.

**Stikkord:** `box-shadow` og `text-shadow` · `border-radius` · `transition` · `transform`
(`scale`, `rotate`, `translate`) · hover-effekter · `cursor` · `opacity` ·
CSS-variabler i `:root` (`--hovedfarge`) og `var()` · kommentarer og seksjonering av CSS-filen ·
navnekonvensjoner for klasser · rekkefølge på regler · enkel «reset»/normalisering

**Deloppgaver:**
- Gjør hele fargepaletten om til CSS-variabler og bytt tema ved å endre fire linjer
- Lag en knapp med hover- og fokus-effekt og myk overgang
- Rydd i egen CSS-fil: kommentarer, gruppering, fjern duplikater

> **Sjekkpunkt 2 – CSS:** nettstedet er ferdig stylet og responsivt. Elevene presenterer to valg de
> har tatt og begrunner dem.

---

# DEL 3 – HÅNDVERKET

## Kapittel 21 – Skjemaer

**Mål:** Eleven kan lage og style et brukbart skjema.

**Stikkord:** `<form>` med `action` og `method` · `<input>` og typene (text, email, password, number, date,
checkbox, radio, color, range, file) · `<label for>` og `id` · `placeholder` er ikke en etikett ·
`<textarea>` · `<select>` og `<option>` · `<button>` · `required`, `min`, `max`, `pattern` ·
`<fieldset>` og `<legend>` · styling av skjemafelter og `:focus`

**Deloppgaver:**
- Lag et kontaktskjema til nettstedet
- Lag et påmeldingsskjema med minst seks ulike felttyper
- **Finn feilen:** skjema der klikk på etiketten ikke fokuserer feltet

---

## Kapittel 22 – Universell utforming og tilgjengelighet

**Mål:** Eleven kan begrunne og gjennomføre grep som gjør siden brukbar for flere.

**Stikkord:** hvorfor UU (og at det er lovpålagt i Norge) · skjermleser · tastaturnavigasjon og `:focus` ·
alt-tekst · semantikk som tilgjengelighet · fargekontrast og kontrastsjekker · tekststørrelse ·
lenketekst som gir mening alene · WCAG-prinsippene på overordnet nivå · ARIA nevnt kort

**Deloppgaver:**
- Naviger eget nettsted kun med tastatur – noter alt som ikke fungerer, og fiks det
- Kontrastsjekk av egen fargepalett
- Vurder en offentlig nettside opp mot en enkel UU-sjekkliste

---

## Kapittel 23 – Design og planlegging

**Mål:** Eleven kan planlegge en nettside før den kodes.

**Stikkord:** målgruppe og formål · innholdsstruktur og sidekart · skisse / wireframe ·
visuelt hierarki · hvitrom · rutenett og justering · nærhet og gruppering · konsistens ·
fargepalett og typografivalg som system · inspirasjon og kildekritikk · fra skisse til kode

**Deloppgaver:**
- Skisse på papir av en tenkt nettside, med sidekart
- Analyse: hva gjør denne nettsiden god / dårlig? (3 sider, faguttrykk skal brukes)
- Kode opp egen skisse som statisk side

---

## Kapittel 24 – Feilsøking og god kodeskikk

**Mål:** Eleven kan finne og rette feil selv.

**Stikkord:** utviklerverktøyet: Elements, Styles, Computed, enhetsvisning · «hvorfor skjer ingenting?»-sjekkliste ·
HTML-validator og CSS-validator · vanlige feil (feil filsti, manglende sluttag, stavefeil i klassenavn,
manglende semikolon, spesifisitet) · innrykk og lesbar kode · kommentarer · navngiving ·
å lese dokumentasjon (MDN, W3Schools) · hvordan søke godt etter svar

**Deloppgaver:**
- Feilsøkingsverksted: fem ødelagte nettsider som skal repareres på tid
- Kodegjennomgang to og to: gi hverandre tre konkrete tilbakemeldinger
- Kjør egen side gjennom validator og fiks alle feil

---

## Kapittel 25 – Fra fil til nett

**Mål:** Eleven forstår hva som skal til for at siden blir tilgjengelig for andre.

**Stikkord:** lokal fil vs. publisert side · webhotell / hosting · domenenavn · DNS på oversiktsnivå ·
FTP · statisk nettsted · gratis publisering (GitHub Pages / Netlify) · favicon ·
`<meta name="description">` og enkel SEO · deling og opphavsrett

**Deloppgaver:**
- Legg til favicon og meta-beskrivelse
- (Valgfritt) Publiser nettstedet og del lenken i klassen

---

## Kapittel 26 – Repetisjon og prøveforberedelse

**Mål:** Eleven kan bruke fagbegrepene presist og lese kode den ikke har skrevet selv.

**Stikkord:** begrepsliste for hele kurset · oppsummerende kart over HTML-elementer og CSS-egenskaper ·
øvingsprøve med samme oppgavetyper som den ekte

**Deloppgaver:**
- Begrepsdrill (hva heter det, og hva gjør det?)
- «Hva gjør denne koden?» – 15 kodesnutter
- «Hva mangler her?» – 15 snutter med én feil hver
- Skisse-til-kode: gitt et bilde av en layout, beskriv hvilke CSS-egenskaper som er brukt
- Øvingsprøve med retting i par

---

# Vurdering

**Skriftlig prøve uten hjelpemidler – vekt på forståelse, ikke å skrive kode for hånd.**

Oppgavetyper på prøven:

1. **Begreper** – forklar `class`, `padding`, `selektor`, `semantisk element`, `brytepunkt` …
2. **Hva gjør denne koden?** – kodesnutt inn, beskrivelse av resultatet ut
3. **Hva mangler her?** – kodesnutt med én feil, eleven identifiserer og forklarer
4. **Koble kode til skjermbilde** – hvilken av tre CSS-varianter gir dette resultatet?
5. **Velg riktig element/egenskap** – hva ville du brukt til denne oppgaven, og hvorfor?
6. **Kort refleksjon** – f.eks. hvorfor semantikk og alt-tekst betyr noe

Underveisvurdering: deloppgaver per kapittel, to sjekkpunkter (etter del 1 og del 2), og
det gjennomgående nettstedet som vokser gjennom kurset.

---

# Ressurser

- **MDN Web Docs** – oppslagsverk, presist og oppdatert
- **W3Schools** – enkle eksempler og «prøv selv»
- **Flexbox Froggy** og **Grid Garden** – spillbaserte øvelser
- **CSS Diner** – selektortrening
- **Can I Use** – nettleserstøtte
- Kontrastsjekker (WebAIM) og HTML/CSS-validator (W3C)

---

# Videre arbeid med opplegget

- [ ] Skrive ut hvert kapittel som elevtekst med eksempler
- [ ] Lage startfiler og fasit til deloppgavene
- [ ] Bygge oppgavebank til «finn feilen» og «hva gjør koden»
- [ ] Koble kapitlene til kompetansemål i programfagene
- [ ] Lage øvingsprøve + prøve

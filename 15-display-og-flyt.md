# Kapittel 15 – Display og flyt

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - forklare hvorfor noen elementer legger seg under hverandre og andre på rad
> - endre et elements `display` og forutsi hva som skjer
> - forklare forskjellen på `display: none` og `visibility: hidden`
> - lage en vannrett meny

---

## 15.1 Hvorfor legger de seg slik?

Skriv dette og se på resultatet:

```html
<p>Første avsnitt</p>
<p>Andre avsnitt</p>

<strong>Første</strong>
<strong>Andre</strong>
```

Avsnittene legger seg **under hverandre**. De to `<strong>`-elementene legger seg **på rad**.

Du har ikke bedt om noe av delene. Nettleseren gjorde det av seg selv.

Grunnen er at hvert element har en standardverdi for egenskapen `display`, og den bestemmer hvordan
elementet oppfører seg i **normal flyt** — måten nettleseren stabler innhold når ingen har sagt noe
annet.

Forstår du dette, forstår du hvorfor layout oppfører seg som den gjør. Og du er klar for Flexbox.

---

## 15.2 Normal flyt

**Normal flyt** er nettleserens standard: den leser HTML-en ovenfra og ned, og plasserer hvert element
etter tur.

- **Blokkelementer** får en ny linje for seg selv og fyller hele bredden
- **Inline-elementer** legger seg etter hverandre på samme linje, som ord i en setning, og brytes til
  ny linje når det blir trangt

Det er hele systemet. Alt annet i CSS-layout — posisjonering, Flexbox, Grid — handler om å bryte ut av
denne flyten når du trenger noe annet.

---

## 15.3 `display: block`

Et blokkelement:

- starter på ny linje
- **fyller hele bredden** som er tilgjengelig, selv om innholdet er kort
- godtar `width`, `height`, `margin` og `padding` i alle retninger

Elementer som er blokk som standard:

```
div  p  h1–h6  ul  ol  li  section  article  header  nav  main  footer  figure  form
```

Legg merke til bredden: gi en `<div>` en bakgrunnsfarge uten å sette `width`, så farges hele linjen ut
til høyre kant — også der det ikke står noe. Det er ikke en feil. Det er slik blokkelementer er.

---

## 15.4 `display: inline`

Et inline-element:

- starter **ikke** på ny linje
- er **bare så bredt som innholdet**
- **ignorerer `width` og `height`**
- ignorerer margin over og under (venstre og høyre virker)
- padding over og under *tegnes*, men skyver ikke naboene unna — den flyter oppå

Elementer som er inline som standard:

```
span  a  strong  em  b  i  small  code  label
```

Den siste egenskapen er den som forvirrer mest. Prøv selv:

```css
a {
    background-color: yellow;
    padding: 20px;
}
```

Den gule flaten blir høy, men linjene over og under flytter seg ikke unna — den legger seg oppå dem.

**Oppgave 15.1 – Bryt reglene**

Lag en testside `flyt.html` og gjør disse fem eksperimentene. Skriv én setning om hva du observerte
etter hver.

1. Gi tre `<span>`-elementer hver sin bakgrunnsfarge. Hvordan ligger de?
2. Gi de samme `<span>`-ene `width: 300px`. Hva skjedde? Hvorfor?
3. Sett `display: block` på dem. Hva skjedde nå?
4. Gi tre `<div>`-er bakgrunnsfarge og sett `display: inline` på dem.
5. Gi en lenke `padding: 30px` og bakgrunnsfarge, midt i et avsnitt med flere linjer. Beskriv hva som
   skjer med linjene rundt.

---

## 15.5 `display: inline-block`

`inline-block` kombinerer det beste fra begge:

- legger seg på rad, som inline
- godtar `width`, `height`, `margin` og `padding` i alle retninger, som blokk

```css
nav a {
    display: inline-block;
    padding: 0.75rem 1.25rem;
}
```

Nå ligger lenkene på rad, **og** de har en ordentlig stor flate rundt seg.

### Hvorfor det siste betyr noe

En inline-lenke er bare like stor som teksten. På mobil betyr det at brukeren må treffe et par
millimeter med fingeren.

Med `inline-block` og padding blir hele flaten klikkbar. Anbefalt minstestørrelse på noe man skal
trykke på, er omtrent **44 × 44 piksler** — omtrent en fingertupp.

Dette er ikke pynt. Det er forskjellen på en meny som er lett å bruke og en som er irriterende.

---

## 15.6 Menyen din blir vannrett

Menyen din ligger fortsatt under hverandre. Nå fikser vi det — med det du har lært til nå.

```css
/* ===== Meny ===== */

nav ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

nav li {
    display: inline-block;
}

nav a {
    display: inline-block;
    padding: 0.75rem 1.25rem;
    text-decoration: none;
}
```

`<li>` er et blokkelement som standard — derfor lå punktene under hverandre. Setter du dem til
`inline-block`, legger de seg på rad.

**Oppgave 15.2 – Vannrett meny**

Gjør menyen din vannrett med `inline-block`. Sørg for at:

- punktene ligger på rad
- hele flaten rundt hver lenke er klikkbar, ikke bare teksten
- `:hover` og `:focus` markerer hele flaten, ikke bare bokstavene
- den aktive siden fortsatt skiller seg ut

Test klikkflaten: klikk litt over og under teksten. Virker det?

> **Én rar ting du vil oppdage:** det er en liten glipe mellom menypunktene som du ikke har bedt om.
> Den kommer av at inline-elementer behandler linjeskift i HTML-koden som et mellomrom — akkurat som
> mellomrom mellom ord, slik du lærte i kapittel 4.
>
> Det finnes klønete triks for å bli kvitt den. Vi skal ikke bruke dem. I kapittel 17 løser Flexbox
> problemet fullstendig med én linje, og da forstår du hvorfor Flexbox ble laget.

---

## 15.7 `display: none`

```css
.skjult {
    display: none;
}
```

Elementet forsvinner **helt**. Det tar ingen plass, og resten av siden lukker seg som om det aldri
fantes.

Sammenlikn med:

```css
.usynlig {
    visibility: hidden;
}
```

Her blir elementet usynlig, men **plassen står igjen** — det blir et tomt hull.

| | Synlig | Tar plass | Leses av skjermleser |
|---|---|---|---|
| normal | ja | ja | ja |
| `visibility: hidden` | nei | **ja** | nei |
| `display: none` | nei | nei | **nei** |

Den siste kolonnen er verdt å merke seg: `display: none` fjerner elementet også for skjermlesere. Det
er som regel det du vil — men det betyr at du **ikke** kan bruke det til å skjule noe visuelt som
blinde fortsatt skal få lest opp.

`display: none` brukes mye sammen med JavaScript (menyer som åpnes og lukkes) og i responsivt design
(skjule noe på mobil). Begge deler kommer senere.

**Oppgave 15.3 – Sammenlikn**

Lag tre bokser med bakgrunnsfarge på rad. Sett `display: none` på den midterste. Ta skjermbilde.
Bytt til `visibility: hidden`. Ta skjermbilde.

Forklar forskjellen med egne ord.

---

## 15.8 `overflow` — når innholdet ikke får plass

Hva skjer om innholdet er større enn boksen?

```css
.boks {
    width: 200px;
    height: 100px;
    overflow: auto;
}
```

| Verdi | Hva som skjer |
|---|---|
| `visible` | innholdet renner ut av boksen (standard) |
| `hidden` | det som ikke får plass, kuttes bort |
| `scroll` | rullefelt alltid synlig |
| `auto` | rullefelt bare når det trengs — som regel det beste |

Dette er en av grunnene til at fast `height` er risikabelt, slik du lærte i forrige kapittel: blir
innholdet lengre enn du planla, renner det ut.

`overflow-x: auto` er spesielt nyttig på **brede tabeller**. Da får tabellen sitt eget rullefelt i
stedet for at hele siden må skrolles sidelengs.

**Oppgave 15.4 – Redd tabellen**

Har du en tabell som blir for bred på en smal skjerm, pakk den inn slik:

```html
<div class="tabell-wrapper">
    <table>...</table>
</div>
```

```css
.tabell-wrapper {
    overflow-x: auto;
}
```

Test ved å gjøre nettleservinduet smalt. Nå skroller tabellen for seg selv, mens resten av siden står
stille.

---

## 15.9 Alle display-verdiene du kommer til å møte

| Verdi | Oppførsel |
|---|---|
| `block` | egen linje, full bredde |
| `inline` | på rad, bare så bred som innholdet |
| `inline-block` | på rad, men godtar bredde og høyde |
| `none` | borte |
| `flex` | **kapittel 17** |
| `grid` | **kapittel 18** |

Legg merke til de to siste. Flexbox og Grid er ikke egne systemer ved siden av CSS — de er
**verdier av `display`**. Du skriver `display: flex` på en boks, og da endres reglene for hvordan
innholdet i den boksen plasseres.

Det er derfor dette kapitlet kommer først. Skal du forstå hva Flexbox endrer, må du vite hva den
endrer *fra*.

**Oppgave 15.5 – Rydd i nettstedet**

Gå gjennom nettstedet ditt og se etter:

1. Elementer som ligger under hverandre, men burde ligget på rad
2. Lenker eller knapper med for liten klikkflate
3. Tabeller eller kodeblokker som blir for brede på smal skjerm

Fiks det du finner med `inline-block` og `overflow`.

---

## 15.10 Oppsummering

- **Normal flyt** er nettleserens standard: blokk under hverandre, inline på rad.
- **Blokk** fyller bredden, godtar alle mål. Standard for `div`, `p`, `h1`, `li`, `section` osv.
- **Inline** er bare så bred som innholdet, **ignorerer `width` og `height`**, og loddrett padding
  skyver ikke naboene. Standard for `span`, `a`, `strong`, `em`.
- **`inline-block`** ligger på rad og godtar mål — nyttig til menypunkter og knapper.
- Klikkflater bør være omtrent **44 × 44 piksler**.
- `display: none` fjerner elementet helt, også for skjermlesere.
  `visibility: hidden` skjuler det, men plassen blir igjen.
- `overflow: auto` gir rullefelt når innholdet ikke får plass. `overflow-x: auto` redder brede tabeller.
- **`flex` og `grid` er også display-verdier.** Det er neste steg.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Normal flyt | Måten nettleseren plasserer elementer når ingenting annet er bestemt |
| Blokkelement | Element som tar egen linje og full bredde |
| Inline-element | Element som ligger på rad og er like bredt som innholdet |
| `inline-block` | Ligger på rad, men godtar bredde, høyde og margin |
| `display: none` | Fjerner elementet helt – også for skjermlesere |
| `visibility: hidden` | Skjuler elementet, men plassen blir stående |
| `overflow` | Hva som skjer når innholdet er større enn boksen |
| Klikkflate | Området som reagerer på klikk eller trykk |

---

## Innlevering – kapittel 15

Lever i læringsloggen din:

1. `flyt.html` med de fem eksperimentene fra oppgave 15.1, og observasjonene dine.
2. Den vannrette menyen (oppgave 15.2), med skjermbilde av normal, hover og aktiv tilstand.
3. De to skjermbildene fra oppgave 15.3, med forklaringen på forskjellen.
4. Skjermbilde av tabellen som skroller for seg selv på smal skjerm (oppgave 15.4).
5. Hva du fant og fikset i oppgave 15.5.

**Sjekkliste før du går videre:**

- [ ] Menyen min ligger vannrett
- [ ] Hele flaten rundt menylenkene er klikkbar
- [ ] Jeg kan forklare hvorfor `width` ikke virker på et inline-element
- [ ] Jeg vet forskjellen på `display: none` og `visibility: hidden`
- [ ] Ingenting på sidene mine tvinger hele siden til å skrolle sidelengs

---

**Neste kapittel:** Posisjonering — hvordan du flytter et element ut av flyten når du trenger det.

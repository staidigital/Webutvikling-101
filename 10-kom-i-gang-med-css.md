# Kapittel 10 – Kom i gang med CSS

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - koble et stilark til alle sidene dine
> - lese og skrive CSS-syntaks presist, med riktige fagord
> - forklare hvorfor ekstern CSS er bedre enn de to andre måtene
> - bruke utviklerverktøyet til å se hvilke stiler som gjelder for et element

---

## Del 2 begynner her

Nettstedet ditt fungerer. Strukturen er riktig, lenkene virker, innholdet er på plass — og det er
svart tekst på hvit bakgrunn i Times New Roman.

Fra nå av bestemmer du hvordan det skal se ut.

**CSS** står for *Cascading Style Sheets*. Det er et eget språk, med egne regler, som du skriver i egne
filer. HTML sier hva noe **er**. CSS sier hvordan det skal **se ut**.

---

## 10.1 Tre måter å legge til CSS

Det finnes tre steder du kan skrive CSS. Du skal kunne kjenne igjen alle tre — og bruke bare den siste.

### 1. Inline — rett i elementet

```html
<h1 style="color: red;">Overskrift</h1>
```

Stilen legges i et `style`-attributt på selve elementet.

**Fungerer, men er dårlig.** Har du 40 overskrifter som skal være røde, må du skrive det 40 ganger.
Skal fargen endres, må du endre 40 steder. Og du blander innhold og utseende i samme linje — akkurat
det vi prøver å unngå.

### 2. Internt — i `<head>`

```html
<head>
    <style>
        h1 { color: red; }
    </style>
</head>
```

Nå gjelder regelen for alle `<h1>` på **denne siden**. Bedre — men bare denne siden. Har du seks sider,
må du gjenta det seks ganger.

### 3. Eksternt — i en egen fil

```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```

Og i `style.css`:

```css
h1 {
    color: red;
}
```

Nå gjelder regelen for **hele nettstedet**. Én linje i én fil endrer alle sidene samtidig.

### Hvorfor den siste vinner

Husker du kapittel 5, der du måtte inn i fire filer for å oppdatere menyen? Og hvor slitsomt det var?

Ekstern CSS er det motsatte. Én endring, alle sidene. Det er derfor alle profesjonelle nettsteder
gjør det slik:

- **Vedlikehold** — endre ett sted, virker overalt
- **Oversikt** — HTML-fila handler om innhold, CSS-fila om utseende
- **Fart** — nettleseren laster ned `style.css` én gang og gjenbruker den på alle sidene

> **Regelen i dette kurset:** all CSS skrives i `style.css`. Inline og intern brukes bare når du
> raskt vil teste noe.

---

## 10.2 Koble på stilarket

`<link>` legges i `<head>`:

```html
<head>
    <meta charset="utf-8">
    <title>Om meg – Nettstedet mitt</title>
    <link rel="stylesheet" href="style.css">
</head>
```

- `rel="stylesheet"` sier hva slags fil dette er — et stilark
- `href` er stien til fila, med nøyaktig samme regler som lenker og bilder

`<link>` er et **tomt element**. Ingen sluttag.

Ligger siden i en undermappe, må stien opp igjen:

```html
<link rel="stylesheet" href="../style.css">
```

**Oppgave 10.1 – Koble på**

1. Åpne `style.css` (du lagde den i kapittel 2 — den er antakelig fortsatt tom).
2. Skriv denne ene regelen:

```css
body {
    background-color: #f4f1ec;
}
```

3. Legg `<link>`-linjen i `<head>` på **alle** sidene dine.
4. Åpne siden med Live Server.

Fikk alle sidene beige bakgrunn? Da virker koblingen. Fikk én av dem det ikke, er det stien i `href`
som er feil på akkurat den siden.

**Oppgave 10.2 – Kjenn på forskjellen**

Endre fargen i `style.css` til noe helt annet. Lagre. Klikk deg gjennom alle sidene.

Alle endret seg, fra én linje. **Dette er hele poenget med CSS.**

---

## 10.3 Syntaksen

CSS har en fast oppbygning, og det finnes fagord for hver del. Du skal kunne dem presist.

```
h1 {
  color: red;
}
│  │  │      │
│  │  │      └── verdi
│  │  └───────── egenskap
│  └──────────── deklarasjonsblokk (alt mellom { })
└─────────────── selektor
```

- **Regel** — hele greia, fra selektor til siste krøllparentes
- **Selektor** — *hvem* skal endres. Her: alle `<h1>` på siden
- **Deklarasjonsblokk** — alt mellom `{` og `}`
- **Deklarasjon** — ett par av egenskap og verdi: `color: red;`
- **Egenskap** *(property)* — *hva* du endrer. Her: tekstfargen
- **Verdi** *(value)* — *hvordan*. Her: rød

En regel kan ha så mange deklarasjoner du vil:

```css
h1 {
    color: darkblue;
    background-color: white;
    text-align: center;
}
```

Les det som en setning: «Alle h1-elementer skal ha mørkeblå tekst, hvit bakgrunn og midtstilt tekst.»

**Oppgave 10.3 – Sett navn på delene**

Skriv av regelen under og merk av hva som er selektor, egenskap, verdi og deklarasjon.
Hvor mange deklarasjoner er det til sammen?

```css
p {
    color: #333333;
    line-height: 1.6;
}
```

---

## 10.4 Tegnsettingen

CSS er kresen på tegn. Fire ting må sitte:

| Tegn | Hvor | Hva som skjer uten |
|---|---|---|
| `{ }` | rundt deklarasjonsblokken | regelen virker ikke i det hele tatt |
| `:` | mellom egenskap og verdi | deklarasjonen ignoreres |
| `;` | etter hver deklarasjon | **denne og ofte den neste** slutter å virke |
| stavemåte | overalt | ingenting skjer |

### Og her er det som gjør CSS frustrerende

**CSS gir ingen feilmeldinger.** Akkurat som HTML.

Skriver du `colr` i stedet for `color`, sier ingen fra. Nettleseren hopper stilltiende over den linjen
og går videre. Du sitter og lurer på hvorfor ingenting skjer.

Det er derfor det siste semikolonet er verdt å ta med, selv om det teknisk sett ikke trengs på siste
deklarasjon: legger du til en linje under senere, virker den med en gang.

**Oppgave 10.4 – Fire ødelagte regler**

Her er fire regler som ikke virker. Finn feilen i hver, og skriv den riktige versjonen.

```css
h1 {
    color: navy
    font-size: 40px;
}
```

```css
p
    color: gray;
}
```

```css
body {
    background-color; lightblue;
}
```

```css
h2 {
    colour: green;
}
```

*(Den siste er den lumskeste, og den er lett å gjøre i et norsk klasserom.)*

---

## 10.5 Kommentarer

```css
/* Dette er en kommentar i CSS */

/* ---- Meny ---- */
nav {
    background-color: white;
}
```

Merk at CSS bruker `/* */`, ikke `<!-- -->` som HTML. To språk, to skrivemåter.

Kommentarer brukes til å dele opp fila i seksjoner og til å slå av kode midlertidig når du feilsøker.
Hurtigtast i VS Code: `Ctrl + /`.

Etter hvert blir `style.css` lang. En fil med tydelige seksjoner er langt lettere å jobbe i:

```css
/* ===== Grunnstil ===== */

/* ===== Meny ===== */

/* ===== Innhold ===== */

/* ===== Bunntekst ===== */
```

---

## 10.6 Nok egenskaper til å komme i gang

Farger får et helt kapittel (12) og typografi et annet (13). Her er bare nok til at du kan gjøre noe
nå:

| Egenskap | Hva den gjør | Eksempel |
|---|---|---|
| `color` | tekstfarge | `color: darkblue;` |
| `background-color` | bakgrunnsfarge | `background-color: #f4f1ec;` |
| `font-family` | skrifttype | `font-family: Verdana, sans-serif;` |
| `font-size` | skriftstørrelse | `font-size: 18px;` |
| `text-align` | justering av tekst | `text-align: center;` |
| `line-height` | linjeavstand | `line-height: 1.6;` |

Fargen kan skrives som navn (`red`, `darkblue`, `peachpuff`) eller som en heksadesimal kode
(`#f4f1ec`). Vi går grundig gjennom det i kapittel 12 — bruk navn så lenge.

**Oppgave 10.5 – Eksperimenter**

Prøv ut alle seks egenskapene i tabellen på ulike elementer i nettstedet ditt. For hver av dem:
Hva skjedde? Var det som du forventet?

Prøv også noe som *ikke* står i tabellen — gjett på et engelsk navn og se om det finnes. Noter to
egenskaper du fant på egen hånd.

---

## 10.7 Utviklerverktøyet er også et CSS-verktøy

I del 1 brukte du Elements-fanen til å se HTML-strukturen. Nå får panelet til høyre mening.

**Oppgave 10.6 – Se stilene**

1. Åpne en av sidene dine og trykk `F12`.
2. Klikk på en overskrift i Elements-panelet.
3. Se på **Styles** til høyre.

Der ser du:

- **hvilke regler** som gjelder for akkurat dette elementet
- **hvilken fil og linje** hver regel kommer fra
- **hva nettleseren har bestemt på egen hånd** (`user agent stylesheet` — nettleserens innebygde stiler)
- deklarasjoner med **strek over**: regler som er blitt overstyrt av en annen regel

4. Klikk på en verdi og skriv noe annet. Trykk Enter. Siden endrer seg umiddelbart.
5. Huk av og på avkrysningsboksene ved siden av deklarasjonene.

Dette er den raskeste måten å prøve ut ideer på. Husk bare at endringene forsvinner ved oppdatering —
**det er `style.css` som er fasiten.** Fant du noe som funker, må du skrive det inn i fila.

Legg spesielt merke til `user agent stylesheet`. Det er svaret på et spørsmål du kanskje har lurt på:
hvorfor er `<h1>` stor og fet, og hvorfor har `<p>` luft rundt seg, når du ikke har bedt om det?
Fordi nettleseren har sitt eget innebygde stilark. Du overstyrer det.

---

## 10.8 Gi nettstedet ditt en grunnstil

**Oppgave 10.7 – Første ordentlige stilark**

Skriv et `style.css` som gir hele nettstedet ditt en grunnstil. Del fila i seksjoner med kommentarer,
og ta med minst dette:

- en bakgrunnsfarge på `body`
- en tekstfarge som er lesbar mot den bakgrunnen
- en skrifttype for hele siden
- en linjeavstand på brødteksten som gjør den behagelig å lese
- en egen farge på `h1`
- en annen farge eller bakgrunn på `footer`

Klikk deg gjennom alle sidene etterpå. Ser det ut som **ett nettsted** nå?

> Det kommer ikke til å bli pent ennå. Du mangler avstander, plassering og layout — alt det kommer i
> kapitlene framover. Men det skal se ut som noen har bestemt noe.

**Oppgave 10.8 – Vurder to nettsteder**

Finn to nettsteder du synes ser veldig ulike ut. Åpne utviklerverktøyet på begge og se på Styles for
brødteksten:

- Hvilken `font-family` bruker de?
- Hvilken `font-size` og `line-height`?
- Hvilken tekstfarge — er den helt svart, eller nesten svart?

Skriv ned tallene. Du kommer til å ha nytte av dem når du skal velge dine egne i kapittel 13.

---

## 10.9 Oppsummering

- CSS er et **eget språk** i en **egen fil**, koblet på med `<link rel="stylesheet" href="style.css">`.
- Tre måter finnes: inline, internt og eksternt. **Bruk eksternt.**
- Én linje i `style.css` endrer alle sidene som er koblet til den.
- **Regel** = selektor + deklarasjonsblokk. **Deklarasjon** = egenskap + verdi.
- Tegnsettingen må sitte: `{ }` rundt blokken, `:` mellom egenskap og verdi, `;` etter hver deklarasjon.
- **CSS gir ingen feilmeldinger.** En stavefeil betyr bare at ingenting skjer.
- Kommentarer i CSS skrives `/* slik */` — ikke som i HTML.
- Nettleseren har sitt eget innebygde stilark (`user agent stylesheet`). Du overstyrer det.
- Styles-panelet i utviklerverktøyet viser hvilke regler som gjelder, og hvor de kommer fra.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| CSS | Cascading Style Sheets – språket som bestemmer utseende |
| Stilark | CSS-fila, f.eks. `style.css` |
| `<link>` | Elementet som kobler stilarket til HTML-sida |
| Inline CSS | Stil skrevet i et `style`-attributt på elementet |
| Intern CSS | Stil skrevet i `<style>` i `<head>` |
| Ekstern CSS | Stil i egen fil – den vi bruker |
| Regel | Selektor + deklarasjonsblokk |
| Selektor | Hvilke elementer regelen gjelder for |
| Deklarasjonsblokk | Alt mellom `{` og `}` |
| Deklarasjon | Ett par av egenskap og verdi |
| Egenskap (*property*) | Hva som endres, f.eks. `color` |
| Verdi (*value*) | Hvordan, f.eks. `darkblue` |
| User agent stylesheet | Nettleserens innebygde standardstiler |

---

## Innlevering – kapittel 10

Lever i læringsloggen din:

1. `style.css` fra oppgave 10.7, med kommentarseksjoner.
2. Skjermbilde av to av sidene dine som viser at de deler samme grunnstil.
3. De fire rettede reglene fra oppgave 10.4, med forklaring på hva som var galt.
4. Svaret på oppgave 10.3.
5. De to egenskapene du fant på egen hånd i oppgave 10.5.
6. Tallene du noterte fra de to nettstedene i oppgave 10.8.

**Sjekkliste før du går videre:**

- [ ] Alle sidene mine er koblet til `style.css`
- [ ] Jeg har ingen inline- eller intern CSS igjen
- [ ] Jeg kan si hva selektor, egenskap og verdi er i en gitt regel
- [ ] `style.css` er delt i seksjoner med kommentarer
- [ ] Jeg vet hvor jeg ser hvilke regler som gjelder for et element

---

**Neste kapittel:** Selektorer — hvordan du treffer akkurat de elementene du vil endre, og hva som
skjer når to regler er uenige.

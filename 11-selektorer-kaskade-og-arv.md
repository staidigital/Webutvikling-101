# Kapittel 11 – Selektorer, kaskade og arv

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - treffe akkurat de elementene du vil endre, med riktig selektor
> - style menyen din slik at den ser ut som en meny
> - forklare hvorfor én regel vinner over en annen når to er uenige
> - bruke utviklerverktøyet til å finne ut hvilken regel som faktisk gjelder

---

## 11.1 Å treffe riktig

I forrige kapittel styret du hele elementtyper: alle `<h1>`, alle `<p>`, hele `<body>`.

Det holder ikke lenge. Du vil ha én rød overskrift og resten svarte. Du vil at lenkene i menyen skal
se annerledes ut enn lenkene inne i teksten. Du vil at det aktive menypunktet skal skille seg ut.

Til det trenger du **selektorer** — måter å peke ut nøyaktig de elementene du er ute etter.

---

## 11.2 De tre grunnleggende

### Elementselektor

Treffer alle elementer av én type:

```css
p {
    color: gray;
}
```

Alle avsnitt på hele nettstedet blir grå.

### Klasseselektor

Treffer alle elementer med en bestemt `class`. Skrives med **punktum** foran:

```html
<p class="ingress">Dette er ingressen.</p>
<p>Dette er vanlig tekst.</p>
```

```css
.ingress {
    font-size: 20px;
}
```

Bare avsnittet med `class="ingress"` blir større. Så mange elementer som helst kan dele samme klasse.

### Id-selektor

Treffer det ene elementet med en bestemt `id`. Skrives med **firkanttegn** foran:

```html
<footer id="bunn">...</footer>
```

```css
#bunn {
    background-color: #333;
}
```

Husk fra kapittel 8: en `id` skal være unik på siden.

### Hvilken bruker du?

| Situasjon | Selektor |
|---|---|
| Alle elementer av en type skal se likt ut | element |
| Noen bestemte elementer skal se likt ut | **klasse** ← bruk denne som standard |
| Nøyaktig ett element på siden | id — men klasse går som regel like bra |

**Klasse er standardvalget.** Den er fleksibel: du kan gjenbruke den, og du kan gi ett element flere
klasser. `id` reserverer du til ankerlenker og virkelig unike ting.

---

## 11.3 Å kombinere selektorer

Her blir det virkelig nyttig.

### Gruppering — samme stil til flere

```css
h1, h2, h3 {
    font-family: Georgia, serif;
}
```

Komma betyr «og». Alle tre overskriftsnivåene får samme skrifttype.

### Etterkommer — inni noe annet

```css
nav a {
    color: white;
}
```

Mellomrom betyr «inni». Dette treffer alle `<a>` som ligger **et sted inni** `<nav>` — uansett hvor
dypt. Lenker andre steder på siden røres ikke.

Dette er antakelig den mest brukte selektortypen som finnes, og det er den som gjør at du kan gi
menylenker og tekstlenker helt ulikt utseende.

### Barn — rett inni

```css
nav > ul {
    list-style: none;
}
```

`>` betyr «rett inni», altså bare ett nivå ned. En `<ul>` som ligger dypere inne, treffes ikke.

Forskjellen på `nav a` og `nav > a`: den første treffer alle lenker uansett dybde, den andre bare de
som ligger rett inni `<nav>`.

### Element med klasse

```css
a.aktiv {
    color: orange;
}
```

Ingen mellomrom betyr «samme element». Dette treffer `<a>`-elementer som **også** har klassen `aktiv`.

### Universell

```css
* {
    margin: 0;
}
```

`*` treffer absolutt alt. Brukes stort sett bare til å nullstille nettleserens standardstiler helt
øverst i fila.

**Oppgave 11.1 – Selektorjakt**

Bruk denne HTML-en. Skriv én selektor for hver oppgave.

```html
<header>
    <nav>
        <ul>
            <li><a href="index.html">Forsiden</a></li>
            <li><a href="om.html" class="aktiv">Om meg</a></li>
        </ul>
    </nav>
</header>

<main>
    <h1>Om meg</h1>
    <p class="ingress">Kort om hvem jeg er.</p>
    <section class="turkort">
        <h2>Besseggen</h2>
        <p>En fin tur. <a href="https://ut.no">Les mer hos UT</a>.</p>
    </section>
    <section class="turkort">
        <h2>Galdhøpiggen</h2>
        <p>Norges høyeste.</p>
    </section>
</main>
```

Treff:

1. Alle avsnitt
2. Bare ingressen
3. Alle lenker i menyen — men ingen andre lenker
4. Det aktive menypunktet
5. Begge `<h2>`-ene, men ikke `<h1>`
6. Alle seksjoner med klassen `turkort`
7. Overskriftene inne i turkortene
8. Lenken inne i et turkort — men ikke menylenkene
9. Både `h1` og `h2`, med samme regel
10. Listepunktene som ligger rett inni `<ul>`

---

## 11.4 Pseudoklasser — elementet i en bestemt tilstand

En pseudoklasse beskriver en **tilstand** eller en **posisjon**. Den skrives med kolon.

```css
a:hover {
    color: red;
}
```

Nå blir lenken rød *mens musepekeren er over den*.

De viktigste:

| Pseudoklasse | Når den gjelder |
|---|---|
| `:hover` | musepekeren er over elementet |
| `:focus` | elementet er valgt med tastatur eller klikk |
| `:active` | akkurat i det man trykker |
| `:visited` | lenke brukeren har besøkt før |
| `:first-child` | første element blant søsknene sine |
| `:last-child` | siste element blant søsknene |
| `:nth-child(2)` | nummer to |
| `:nth-child(odd)` | annenhver — 1., 3., 5. … |

Rekkefølgen betyr noe for lenker: `:link`, `:visited`, `:hover`, `:active` — i den rekkefølgen.
Skriver du `:hover` før `:visited`, virker ikke hover-effekten på besøkte lenker.

### `:focus` er ikke valgfritt

`:hover` er for de som bruker mus. `:focus` er for de som bruker **tastatur** — enten fordi de ikke
kan bruke mus, eller bare fordi det går fortere.

Prøv å trykke `Tab` gjentatte ganger på en nettside. Du ser en markering hoppe fra lenke til lenke.
Det er `:focus`.

Noen fjerner den markeringen fordi de synes den er stygg (`outline: none`). **Ikke gjør det.** Da blir
siden umulig å navigere for alle som ikke bruker mus. Vil du ha en penere markering, lag din egen:

```css
a:focus {
    outline: 3px solid orange;
    outline-offset: 2px;
}
```

**Oppgave 11.2 – CSS Diner**

Gå til [flukeout.github.io](https://flukeout.github.io) og gjennomfør CSS Diner. Det er 32 nivåer med
selektortrening, og det tar 20–30 minutter.

Noter hvilke nivåer du satt fast på — de sier noe om hva du bør repetere.

---

## 11.5 Menyen din blir en meny

Nå får du betalt for arbeidet fra kapittel 7 og 9.

Menyen din er en `<ul>` inni en `<nav>`, med `class="aktiv"` på det aktive punktet. Alt ligger klart.

```css
/* ===== Meny ===== */

nav ul {
    list-style: none;      /* vekk med kulene */
    padding: 0;            /* vekk med innrykket nettleseren la på */
}

nav a {
    color: #1f4e79;
    text-decoration: none; /* vekk med understreken */
    font-weight: 600;
}

nav a:hover {
    color: #b8442a;
    text-decoration: underline;
}

nav a.aktiv {
    color: #b8442a;
    border-bottom: 3px solid #b8442a;
}

nav a:focus {
    outline: 3px solid #1f4e79;
    outline-offset: 3px;
}
```

Punktene ligger fortsatt under hverandre — de skal på rad, og det gjør vi med Flexbox i kapittel 17.
Men menyen ser nå ut som noen har bestemt noe, og den aktive siden er markert.

**Oppgave 11.3 – Style menyen**

Skriv menystilen inn i din egen `style.css`. Velg dine egne farger. Krav:

- ingen kuler
- ingen understrek på lenkene i normal tilstand
- tydelig `:hover`-effekt
- den aktive siden skal skille seg synlig ut
- en `:focus`-markering som er lett å se

Test til slutt med **Tab-tasten**: klarer du å se hvor du er, hele veien gjennom menyen?

**Oppgave 11.4 – Skill menylenker fra tekstlenker**

Gi lenker som ligger inne i `<main>` et annet utseende enn menylenkene — for eksempel understrek og
en annen farge. Bruk etterkommerselektorer.

---

## 11.6 Arv

Noen egenskaper går **i arv** fra et element til alt som ligger inni det:

```css
body {
    font-family: Verdana, sans-serif;
    color: #333;
}
```

Nå har alt på siden Verdana og mørkegrå tekst — også overskrifter, avsnitt og listepunkter du aldri har
nevnt. De arver fra `body`.

| Arves | Arves ikke |
|---|---|
| `color` | `background-color` |
| `font-family` | `border` |
| `font-size` | `margin` og `padding` |
| `line-height` | `width` og `height` |
| `text-align` | `display` |

Enkel regel: **det som handler om tekst, arves. Det som handler om boksen, arves ikke.**

Dette er svært nyttig. Sett skrifttype og tekstfarge på `body` én gang, så slipper du å gjenta det
overalt.

**Oppgave 11.5 – Se arven virke**

Sett `font-family` og `color` på `body`. Klikk deg gjennom sidene og se hvor mange elementer som
endret seg uten at du nevnte dem.

Prøv så å sette `background-color` på `body` og se om `<h1>` arver den. Hvorfor / hvorfor ikke?

---

## 11.7 Kaskaden — når to regler er uenige

C-en i CSS står for **Cascading**. Kaskade betyr «fossefall»: reglene renner nedover og legger seg
oppå hverandre.

Hva skjer når to regler sier noe forskjellig om samme element?

```css
p { color: blue; }
p { color: green; }
```

Teksten blir **grønn**. Ved lik styrke vinner den som står **sist** i fila.

Men reglene har ikke alltid lik styrke. Da gjelder **spesifisitet**.

### Spesifisitet

Tenk på det som poeng. Jo mer presist du peker, jo flere poeng:

| Selektortype | Poeng |
|---|---|
| elementselektor (`p`, `h1`, `nav`) | 1 |
| klasse og pseudoklasse (`.ingress`, `:hover`) | 10 |
| id (`#bunn`) | 100 |

Regelen med flest poeng vinner — uansett rekkefølge.

```css
p            { color: blue; }    /* 1 poeng   */
.ingress     { color: green; }   /* 10 poeng  */
#hovedtekst  { color: red; }     /* 100 poeng */
```

Et avsnitt som er både `class="ingress"` og `id="hovedtekst"` blir **rødt**.

Poengene legges sammen:

```css
nav a          /* 1 + 1  = 2  */
nav a.aktiv    /* 1 + 1 + 10 = 12 */
.meny .aktiv   /* 10 + 10 = 20 */
```

### Rekkefølgen på det hele

Når nettleseren skal bestemme:

1. **Spesifisitet** — flest poeng vinner
2. **Rekkefølge** — ved lik poengsum vinner den som står sist
3. **Arv** — har ingen regel sagt noe, arves verdien fra elementet over

Dette er grunnen til at det er lurt å skrive de generelle reglene øverst i `style.css` og de mer
spesielle nedover. Da jobber du med kaskaden i stedet for mot den.

### `!important`

Det finnes et nødbremseord:

```css
p { color: blue !important; }
```

Det overstyrer alt annet, uansett poeng.

**Ikke bruk det.** Det virker som en løsning i øyeblikket og blir et problem senere: neste gang du
skal endre noe, virker ingenting, og da må du bruke enda et `!important`. Til slutt har du en fil
ingen kan styre.

Fristes du til `!important`, er svaret nesten alltid at du skal skrive en mer presis selektor i stedet.

**Oppgave 11.6 – Regn ut hvem som vinner**

For hvert par: hvilken regel vinner, og hvorfor?

```css
/* A */
h2 { color: black; }
.turkort h2 { color: navy; }
```

```css
/* B */
nav a { color: white; }
a { color: blue; }
```

```css
/* C */
.aktiv { color: red; }
nav ul li a.aktiv { color: green; }
```

```css
/* D */
p { color: gray; }
p { color: black; }
```

**Oppgave 11.7 – Se det i utviklerverktøyet**

Lag med vilje to regler som krangler om samme element i `style.css`. Åpne utviklerverktøyet, klikk på
elementet og se i Styles-panelet.

Den tapende regelen står med **strek over**. Nettleseren viser deg altså hele kampen — hvem som vant,
hvem som tapte, og hvilken linje i fila hver av dem kom fra.

Dette panelet er svaret på «hvorfor skjer det ingenting når jeg endrer fargen?». Som regel skjer det
noe — det blir bare overstyrt av en annen regel lenger nede.

---

## 11.8 Oppsummering

- **Element** (`p`), **klasse** (`.ingress`), **id** (`#bunn`). Bruk klasse som standard.
- Komma = flere selektorer. Mellomrom = «inni». `>` = «rett inni». Ingen mellomrom = samme element.
- **Pseudoklasser** beskriver tilstand: `:hover`, `:focus`, `:first-child`, `:nth-child()`.
- `:focus` skal alltid være synlig — ellers blir siden ubrukelig med tastatur.
- **Arv:** det som handler om tekst arves nedover, det som handler om boksen gjør ikke.
- **Kaskaden:** flest spesifisitetspoeng vinner (element 1, klasse 10, id 100). Ved likt vinner den
  som står sist.
- **`!important` er ikke løsningen.** Skriv en mer presis selektor.
- Styles-panelet viser hvilke regler som gjelder, og streker over dem som tapte.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Selektor | Den delen av regelen som peker ut hvilke elementer den gjelder |
| Klasseselektor | `.navn` – treffer alle med den klassen |
| Id-selektor | `#navn` – treffer det ene elementet med den id-en |
| Gruppering | Flere selektorer adskilt med komma |
| Etterkommerselektor | `nav a` – treffer alt inni, uansett dybde |
| Barneselektor | `nav > ul` – treffer bare ett nivå ned |
| Pseudoklasse | Selektor for en tilstand, f.eks. `:hover` |
| Arv | At verdier går videre fra et element til innholdet i det |
| Kaskade | Systemet som avgjør hvilken regel som gjelder |
| Spesifisitet | Hvor presist en selektor peker; avgjør hvem som vinner |
| `!important` | Nødbrems som overstyrer alt – bør unngås |

---

## Innlevering – kapittel 11

Lever i læringsloggen din:

1. De ti selektorene fra oppgave 11.1.
2. Menyen din, ferdig stylet — skjermbilde av normal tilstand, hover og aktiv side (oppgave 11.3).
3. Skjermbilde som viser `:focus`-markeringen når du bruker Tab.
4. Svarene på oppgave 11.6, med begrunnelse for hvert par.
5. Skjermbilde fra utviklerverktøyet der en regel er streket over (oppgave 11.7), og en setning om
   hvorfor den tapte.
6. Hvilke nivåer du satt fast på i CSS Diner.

**Sjekkliste før du går videre:**

- [ ] Menyen min har ingen kuler og ingen understrek i normal tilstand
- [ ] Den aktive siden er synlig markert i menyen
- [ ] Jeg har en tydelig `:focus`-markering, og har testet den med Tab
- [ ] Menylenker og tekstlenker ser forskjellige ut
- [ ] Jeg har satt skrifttype og tekstfarge på `body` og lar arven gjøre jobben
- [ ] Jeg bruker ikke `!important` noe sted
- [ ] Jeg kan finne ut hvorfor en regel ikke virker, ved hjelp av Styles-panelet

---

**Neste kapittel:** Farger — hex, rgb og hsl, og hvordan du velger en palett som faktisk henger sammen.

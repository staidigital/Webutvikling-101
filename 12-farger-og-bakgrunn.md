# Kapittel 12 – Farger og bakgrunn

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - skrive farger som navn, HEX, RGB og HSL, og vite når du bruker hva
> - sette sammen en fargepalett som henger sammen
> - kontrollere at teksten din har nok kontrast til å være lesbar
> - bruke bakgrunnsbilder og fargeoverganger

---

## 12.1 Farge er ikke pynt

Farge er det første folk oppfatter på en nettside — før de har lest et eneste ord. Den sier noe om
hva slags nettsted dette er, den styrer hvor blikket går, og den avgjør om teksten i det hele tatt er
mulig å lese.

Derfor er dette kapitlet delt i to: først **hvordan** du skriver farger i CSS, så **hvilke** du bør
velge.

---

## 12.2 Fire måter å skrive en farge

### Fargenavn

```css
color: red;
color: darkslateblue;
color: peachpuff;
```

Det finnes rundt 140 navngitte farger i CSS. De er praktiske når du tester noe raskt, men gir deg lite
kontroll — du får akkurat de nyansene som finnes, ikke den du vil ha.

### HEX

```css
color: #b8442a;
```

Dette er den vanligste skrivemåten på nett. Den ser kryptisk ut, men er enkel når du vet hva den betyr:

```
#b8 44 2a
 │  │  │
 │  │  └── blått
 │  └───── grønt
 └──────── rødt
```

Tre par, ett for hver grunnfarge, hver med en verdi fra `00` (ingenting) til `ff` (maks).

- `#000000` = alt av → svart
- `#ffffff` = alt på → hvitt
- `#ff0000` = bare rødt → knallrødt

Verdiene er **heksadesimale** — de teller `0 1 2 3 4 5 6 7 8 9 a b c d e f`, altså 16 trinn per
siffer i stedet for 10. Du trenger ikke regne på det. Du trenger å vite at `ff` er høyest og `00`
lavest.

Er begge sifrene i hvert par like, kan du forkorte: `#ffcc00` kan skrives `#fc0`.

### RGB

```css
color: rgb(184, 68, 42);
```

Samme system, men med vanlige tall fra 0 til 255. Lettere å lese for mennesker, mindre vanlig i praksis.

Med gjennomsiktighet:

```css
background-color: rgb(184, 68, 42, 0.5);   /* 50 % gjennomsiktig */
```

Siste tallet er *alfa* — 0 er helt usynlig, 1 er helt tett.

### HSL

```css
color: hsl(11, 63%, 44%);
```

Dette er den mest nyttige skrivemåten når du skal **lage en palett**, og den er verdt å forstå ordentlig.

```
hsl(11, 63%, 44%)
     │   │    │
     │   │    └── lyshet:    0 % er svart, 100 % er hvitt
     │   └─────── metning:   0 % er grått, 100 % er full farge
     └─────────── fargetone: 0–360 grader rundt fargesirkelen
```

Fargetonen er en runde rundt regnbuen:

| Grader | Farge |
|---|---|
| 0 | rød |
| 60 | gul |
| 120 | grønn |
| 180 | turkis |
| 240 | blå |
| 300 | magenta |

Poenget: **du kan endre én ting av gangen.** Vil du ha en lysere variant av samme farge, endrer du bare
lyshetstallet:

```css
hsl(11, 63%, 44%)   /* grunnfarge */
hsl(11, 63%, 75%)   /* lysere variant */
hsl(11, 63%, 25%)   /* mørkere variant */
```

Med HEX måtte du gjettet deg fram til tre nye koder. Med HSL er det ett tall.

**Oppgave 12.1 – Bli kjent med fargeformatene**

1. Åpne utviklerverktøyet på en av sidene dine og klikk på en farge i Styles-panelet. Du får opp en
   fargevelger.
2. I fargevelgeren: klikk på tekstetiketten ved siden av fargekoden. Den bytter mellom HEX, RGB og HSL
   — samme farge, tre skrivemåter.
3. Noter én farge i alle tre formatene.
4. Dra i fargevelgeren og se hvordan tallene endrer seg. Hva skjer med HSL-tallene når du drar
   nedover? Og til siden?

**Oppgave 12.2 – Lag en fargefamilie**

Velg én fargetone du liker. Lag fem varianter av den med HSL, der du bare endrer lyshet:
en veldig lys, en lys, grunnfargen, en mørk og en veldig mørk.

Lag en testside der du viser alle fem som fargefelter under hverandre.

---

## 12.3 Bakgrunn

### Bakgrunnsfarge

```css
body {
    background-color: #f7f5f0;
}
```

Legg merke til at bakgrunnsfarge **ikke arves**. Setter du den på `body`, dekker den hele siden fordi
`body` fyller hele siden — ikke fordi barna arver den.

### Bakgrunnsbilde

```css
header {
    background-image: url("bilder/fjell.jpg");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
```

De fire egenskapene henger sammen:

| Egenskap | Hva den gjør | Vanlige verdier |
|---|---|---|
| `background-image` | hvilket bilde | `url("...")` |
| `background-size` | hvordan det fyller boksen | `cover`, `contain`, `100%` |
| `background-position` | hvilken del som vises | `center`, `top`, `bottom` |
| `background-repeat` | om det gjentas | `no-repeat`, `repeat` |

`cover` betyr «fyll hele boksen, beskjær om nødvendig». `contain` betyr «vis hele bildet, la det bli
tomrom om nødvendig». `cover` er det du vil ha ni av ti ganger.

> **Merk stien.** `url("bilder/fjell.jpg")` regnes ut fra **CSS-fila**, ikke fra HTML-fila. Ligger
> `style.css` i rotmappen, stemmer stien over. Ligger den i en `css/`-mappe, må du skrive
> `url("../bilder/fjell.jpg")`. Dette er en klassisk snubletråd.

### Bakgrunnsbilde og lesbarhet

Tekst rett oppå et fotografi er nesten alltid vanskelig å lese, fordi bildet har både lyse og mørke
partier. Løsningen er å legge et halvgjennomsiktig lag imellom:

```css
header {
    background-image:
        linear-gradient(rgb(0, 0, 0, 0.5), rgb(0, 0, 0, 0.5)),
        url("bilder/fjell.jpg");
    background-size: cover;
    color: white;
}
```

Her ligger to bakgrunner oppå hverandre: en svart halvgjennomsiktig flate øverst, bildet under.
Det første som står i lista, ligger øverst.

### Fargeoverganger

```css
background-image: linear-gradient(#1f4e79, #b8442a);
background-image: linear-gradient(to right, #1f4e79, #b8442a);
background-image: radial-gradient(#ffffff, #cccccc);
```

`linear-gradient` går rett fram, `radial-gradient` går utover fra midten. Du kan oppgi retning og så
mange farger du vil.

Fargeoverganger er lette å overdrive. Én rolig overgang på ett sted virker; fem sprikende overganger
på samme side gjør ikke det.

**Oppgave 12.3 – Bakgrunn på toppen**

Gi `<header>` på nettstedet ditt et bakgrunnsbilde med `cover`, og legg et mørkt lag over slik at hvit
tekst blir lesbar oppå. Test at det ser bra ut både på et bredt og et smalt vindu.

---

## 12.4 Kontrast — det viktigste avsnittet i kapitlet

En farge kan være aldri så fin. Er teksten vanskelig å lese, er den feil.

**Kontrast** er forskjellen i lyshet mellom tekst og bakgrunn. Den måles som et forholdstall:

| Forholdstall | Betyr |
|---|---|
| 21 : 1 | svart på hvitt — maks |
| 4,5 : 1 | **minstekravet for vanlig tekst** |
| 3 : 1 | minstekravet for stor tekst (fra 24 px, eller 19 px fet) |
| 1 : 1 | samme farge — usynlig |

Kravet på 4,5 : 1 kommer fra **WCAG**, den internasjonale standarden for tilgjengelighet på nett. Den
gjelder for norske nettsteder gjennom kravene til universell utforming. Vi går grundigere inn på dette
i kapittel 22.

### Hvorfor det gjelder alle

Det er lett å tenke at dette handler om blinde brukere. Det gjør det ikke — blinde bruker skjermleser
og ser ikke fargene i det hele tatt.

Kontrast handler om alle andre:

- de som har svekket syn, og det er mange
- de som er fargeblinde (rundt 8 % av gutter)
- alle som leser på mobil i sollys
- alle som bruker en billig skjerm eller har den skrudd ned i lysstyrke
- deg selv, om tjue år

Lys grå tekst på hvit bakgrunn ser stilrent ut på en god skjerm i et mørkt rom. Ute i verden er den
uleselig.

**Oppgave 12.4 – Mål kontrasten**

Gå til [webaim.org/resources/contrastchecker](https://webaim.org/resources/contrastchecker/).

1. Lim inn tekstfargen og bakgrunnsfargen du bruker på nettstedet ditt nå. Hva blir forholdstallet?
   Består du 4,5 : 1?
2. Test disse tre kombinasjonene og noter resultatet:
   - `#777777` på `#ffffff`
   - `#ffffff` på `#1f4e79`
   - `#ffff00` på `#ffffff`
3. Finn en farge som *så vidt* består kravet, og en som *så vidt* stryker. Hvor liten er forskjellen?

Rett opp alle kombinasjoner på nettstedet ditt som ikke består.

---

## 12.5 Å velge en palett

Nå til det vanskelige: hvilke farger?

### Hvor mange

En vanlig og trygg oppskrift:

| Rolle | Antall | Brukes til |
|---|---|---|
| Bakgrunn | 1 | sidens flate — som regel nesten hvit eller nesten svart |
| Tekst | 1 | brødtekst — sjelden helt svart, ofte veldig mørk grå |
| Hovedfarge | 1 | menyen, overskrifter, det som skal kjennes igjen |
| Aksentfarge | 1 | knapper, lenker, det ene som skal fange blikket |
| Nøytral | 1–2 | rammer, skillelinjer, dempet tekst |

**Fem farger er nok.** Nybegynnere bruker for mange, ikke for få. En side med to farger og god
typografi ser proff ut; en side med ni farger ser rotete ut uansett hvor pene de er hver for seg.

### Sett dem sammen med HSL

Nå får du bruk for HSL. Tre pålitelige metoder:

**1. Én fargetone, ulike lysheter** — rolig og enkelt å få til:

```css
hsl(210, 40%, 96%)   /* bakgrunn  */
hsl(210, 30%, 25%)   /* tekst     */
hsl(210, 60%, 40%)   /* hovedfarge */
```

**2. Nabofarger** — behagelig, litt mer liv. Fargetoner som ligger 30 grader fra hverandre:
`hsl(200, …)`, `hsl(230, …)`.

**3. Motsatte farger** — sterk kontrast. Fargetoner 180 grader fra hverandre, for eksempel 210 (blå)
og 30 (oransje). Bruk den ene mye og den andre lite; to sterke farger i like store mengder slåss.

### Nyttige verktøy

- **coolors.co** — trykk mellomrom for nye paletter, lås fargene du liker
- **color.adobe.com** — bygger paletter etter fargeteori
- **Fargevelgeren i utviklerverktøyet** — for å justere en farge du nesten liker
- **Et bilde du liker** — hent fargene fra et fotografi; de henger sammen fordi virkeligheten gjorde
  jobben for deg

**Oppgave 12.5 – Tre paletter**

Lag tre ulike fargepaletter til nettstedet ditt, hver med fem farger i rollene over. Skriv dem opp med
HSL og HEX.

Lag en testside `farger.html` der du viser alle tre palettene som fargefelter med kodene ved siden av.

Velg til slutt én, og skriv tre–fire setninger om hvorfor: hva passer den til, hvilken stemning gir
den, og hvordan går den sammen med innholdet ditt?

**Oppgave 12.6 – Sett paletten i verk**

Bruk den valgte paletten på hele nettstedet:

- bakgrunnsfarge på `body`
- tekstfarge på `body`
- hovedfargen i menyen og på overskriftene
- aksentfargen på lenker og den aktive menysiden
- en nøytral farge på skillelinjer og bunnteksten

Kjør deretter kontrasttesten på **alle** kombinasjonene du har laget. Alt som ikke består 4,5 : 1,
justeres.

**Oppgave 12.7 – Se på ekte paletter**

Velg tre nettsteder med tydelig ulikt uttrykk. Bruk utviklerverktøyet og finn ut:

- Hvor mange farger bruker de egentlig?
- Er bakgrunnen helt hvit, eller litt tonet?
- Er brødteksten helt svart, eller nesten?
- Hvilken farge er brukt minst — og til hva?

Den siste er den interessante. På de fleste gode nettsteder er den *minst* brukte fargen den som
markerer det viktigste.

---

## 12.6 Oppsummering

- Farger skrives som navn, **HEX** (`#b8442a`), **RGB** eller **HSL**.
- HEX er vanligst. **HSL er best når du skal lage en palett**, fordi du kan endre lyshet alene.
- Alfa (`rgb(0,0,0,0.5)`) gir gjennomsiktighet.
- `background-color` arves ikke.
- Bakgrunnsbilde: `background-size: cover` fyller boksen, `background-position: center` velger utsnitt.
- Stien i `url()` regnes fra **CSS-fila**, ikke HTML-fila.
- Legg et halvgjennomsiktig lag mellom bilde og tekst for å få teksten lesbar.
- **Kontrast må være minst 4,5 : 1** for vanlig tekst. Dette er et krav, ikke en anbefaling.
- Fem farger er nok: bakgrunn, tekst, hovedfarge, aksent, nøytral.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| HEX | Fargekode på formen `#rrggbb` |
| RGB | Farge angitt som rødt, grønt og blått fra 0 til 255 |
| HSL | Farge angitt som fargetone, metning og lyshet |
| Fargetone (*hue*) | Plasseringen på fargesirkelen, 0–360 grader |
| Metning (*saturation*) | Hvor sterk fargen er; 0 % er grått |
| Lyshet (*lightness*) | Hvor lys fargen er; 0 % svart, 100 % hvitt |
| Alfa | Grad av gjennomsiktighet, 0–1 |
| `background-size: cover` | Bakgrunnsbildet fyller hele boksen, beskjæres om nødvendig |
| Fargeovergang (*gradient*) | Myk overgang mellom to eller flere farger |
| Kontrast | Forskjellen i lyshet mellom tekst og bakgrunn |
| WCAG | Internasjonal standard for tilgjengelighet på nett |
| Palett | Det avgrensede settet med farger et nettsted bruker |

---

## Innlevering – kapittel 12

Lever i læringsloggen din:

1. `farger.html` med de tre palettene (oppgave 12.5), og begrunnelsen for valget ditt.
2. Nettstedet med paletten i bruk (oppgave 12.6), med skjermbilde av to sider.
3. Kontrastmålingene fra oppgave 12.4, og hva du måtte rette.
4. Fargefamilien fra oppgave 12.2.
5. Funnene fra oppgave 12.7 — særlig: hvilken farge brukte de minst, og til hva?

**Sjekkliste før du går videre:**

- [ ] Nettstedet mitt bruker maks fem–seks farger
- [ ] Alle tekst-og-bakgrunn-kombinasjoner består 4,5 : 1
- [ ] Jeg kan skrive den samme fargen i HEX, RGB og HSL
- [ ] Jeg vet hvorfor HSL er praktisk når jeg lager varianter av en farge
- [ ] Bakgrunnsbildet mitt har lesbar tekst oppå
- [ ] Jeg har skrevet fargene mine ned et sted, så jeg bruker de samme overalt

---

**Neste kapittel:** Typografi. Farger merkes først — men det er skriften som avgjør om siden faktisk
blir lest.

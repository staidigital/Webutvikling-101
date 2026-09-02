# Kapittel 14 – Boksmodellen

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - forklare de fire lagene i boksmodellen og hva hvert av dem gjør
> - regne ut hvor bred en boks faktisk blir
> - bruke `box-sizing: border-box` og forklare hvorfor
> - gi nettstedet ditt luft, bredde og sentrering

---

## 14.1 Alt er firkanter

Åpne en hvilken som helst nettside. Trykk `F12`, og hold musepekeren over ulike deler av siden i
Elements-panelet.

Legg merke til hva som skjer: hver eneste ting du peker på, markeres som en **firkant**. Overskrifter,
avsnitt, bilder, knapper, hele menyen. Selv en rund knapp er egentlig en firkant med avrundede hjørner.

> **Alt i CSS er bokser.** Layout på nett handler om å bestemme hvor store boksene er, hvor mye luft
> det er inni dem, og hvor mye luft det er mellom dem.

Dette kapitlet handler om den ene boksen. Kapittel 15 til 18 handler om hvordan boksene forholder seg
til hverandre.

---

## 14.2 De fire lagene

Hver boks har fire lag, innenfra og ut:

```
+-------------------------------------+
|              margin                 |   luft utenfor - mellom denne og andre bokser
|   +-----------------------------+   |
|   |           border            |   |   selve kanten
|   |   +---------------------+   |   |
|   |   |       padding       |   |   |   luft inni - mellom kant og innhold
|   |   |   +-------------+   |   |   |
|   |   |   |   innhold   |   |   |   |   teksten eller bildet
|   |   |   +-------------+   |   |   |
|   |   +---------------------+   |   |
|   +-----------------------------+   |
+-------------------------------------+
```

| Lag | Hva det er | Enkel huskeregel |
|---|---|---|
| **innhold** | teksten eller bildet | det du faktisk skrev |
| **padding** | luft **inni** boksen | polstring, mellom kant og innhold |
| **border** | selve kanten | rammen |
| **margin** | luft **utenfor** boksen | avstand til naboene |

Den viktigste forskjellen å få inn: **padding er innenfor kanten, margin er utenfor.**

Har boksen bakgrunnsfarge, farges padding-området — men ikke margin-området. Det er en god måte å se
forskjellen på.

**Oppgave 14.1 – Se lagene**

1. Åpne en av sidene dine og trykk `F12`.
2. Klikk på et avsnitt i Elements-panelet.
3. Bla helt ned i Styles-panelet til du finner et fargelagt diagram med fire lag.

Det diagrammet er boksmodellen for akkurat det elementet, med tall for hvert lag. Blå er innhold,
grønt er padding, gult er border, oransje er margin.

4. Hold musepekeren over hvert lag i diagrammet, og se at det tilsvarende området markeres på siden.
5. Dobbeltklikk på et tall og endre det. Se hva som skjer.

Dette diagrammet er verktøyet du kommer tilbake til hver gang noe har feil størrelse eller avstand.

---

## 14.3 Å skrive verdiene

Alle fire sidene kan settes hver for seg:

```css
padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
```

Men det finnes kortformer, og de brukes hele tiden:

```css
padding: 10px;                  /* alle fire like              */
padding: 10px 20px;             /* topp/bunn, venstre/høyre    */
padding: 10px 20px 30px;        /* topp, venstre/høyre, bunn   */
padding: 10px 20px 30px 40px;   /* topp, høyre, bunn, venstre  */
```

Rekkefølgen med fire verdier går **med klokka fra toppen**: topp → høyre → bunn → venstre.

Formen med to verdier er den du kommer til å bruke mest: `padding: 1rem 1.5rem` betyr «litt luft over
og under, litt mer på sidene».

Nøyaktig samme system gjelder for `margin`.

### Border

```css
border: 2px solid #b8442a;
```

Tre verdier: tykkelse, strektype og farge.

Strektyper: `solid`, `dashed`, `dotted`, `none`. Du kan også sette bare én side:

```css
border-bottom: 3px solid #b8442a;
```

Denne brukes mye — for eksempel understreken under det aktive menypunktet du lagde i kapittel 11.

### Avrundede hjørner

```css
border-radius: 8px;
border-radius: 50%;   /* helt rundt, hvis boksen er kvadratisk */
```

`border-radius` virker selv om boksen ikke har `border`.

---

## 14.4 Bredde og høyde

```css
.kort {
    width: 300px;
    height: 200px;
}
```

Men her er et råd som er verdt å ta på alvor:

> **Sett sjelden fast `height`.** La innholdet bestemme høyden.

Setter du fast høyde og innholdet blir lengre enn du trodde, renner teksten ut av boksen eller blir
kuttet. Innhold varierer — noen overskrifter er lange, noen korte.

Trenger du en minstehøyde, bruk `min-height`. Da vokser boksen om det trengs.

For bredde er `max-width` som regel bedre enn `width`:

```css
main {
    max-width: 65ch;
}
```

`width: 800px` betyr «alltid 800 piksler» — også på en mobilskjerm som er 375 piksler bred. Da stikker
innholdet ut, og siden må skrolles sidelengs.

`max-width: 800px` betyr «maks 800, men bli gjerne smalere om det er trangt». Den er automatisk
mobilvennlig, og du får den effekten gratis før du i det hele tatt har lært om responsivt design.

---

## 14.5 `box-sizing` — den viktigste linjen i kurset

Her kommer noe som overrasker alle, og som har ødelagt uendelig mange layouter.

```css
.boks {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
}
```

**Hvor bred blir denne boksen på skjermen?**

Ikke 300 piksler. Den blir:

```
300  (innhold)
+ 20 (padding venstre)
+ 20 (padding høyre)
+  5 (border venstre)
+  5 (border høyre)
= 350 piksler
```

Som standard gjelder `width` bare **innholdet**. Padding og border legges utenpå.

Det er upraktisk. Sier du at noe skal være 300 bredt, mener du som regel at det skal ta 300 piksler på
skjermen — ikke 350.

### Løsningen

```css
* {
    box-sizing: border-box;
}
```

Nå betyr `width: 300px` at **hele boksen** blir 300 piksler, inkludert padding og border. Innholdet
krymper i stedet.

```
300 totalt = 5 border + 20 padding + 250 innhold + 20 padding + 5 border
```

Dette er så mye mer fornuftig at praktisk talt alle utviklere skriver linjen øverst i stilarket sitt.
Standardoppførselen finnes bare fordi den ble bestemt for lenge siden og ikke kan endres uten å ødelegge
gamle nettsider.

**Oppgave 14.2 – Regn ut**

Regn ut den faktiske bredden på skjermen for hver boks — først uten `border-box`, så med.

| | `width` | `padding` | `border` |
|---|---|---|---|
| A | 200px | 10px | 0 |
| B | 400px | 20px | 2px |
| C | 100px | 0 | 5px |
| D | 300px | 15px 30px | 1px |

Sjekk svarene i utviklerverktøyet etterpå.

**Oppgave 14.3 – Sett den globalt**

Legg dette helt øverst i `style.css`, over alt annet:

```css
/* ===== Grunnleggende ===== */

* {
    box-sizing: border-box;
}
```

Se om noe på nettstedet ditt endret seg. Beskriv hva.

---

## 14.6 Marginkollaps

Enda en overraskelse. To bokser over hverandre:

```css
.boks-a { margin-bottom: 30px; }
.boks-b { margin-top: 20px; }
```

Hvor stor blir avstanden mellom dem? Ikke 50 piksler. **30 piksler.**

Loddrette marginer mellom naboer **kollapser**: den største vinner, i stedet for at de legges sammen.

Dette gjelder bare:

- **loddrett** — venstre og høyre margin legges alltid sammen
- **margin**, ikke padding

Hvorfor finnes denne regelen? Fordi den gir fornuftige resultater i løpende tekst. Alle avsnitt har
margin både over og under, og uten kollaps ville avstanden mellom to avsnitt blitt dobbelt så stor som
avstanden fra det første avsnittet opp til overskriften.

**Praktisk konsekvens:** når du skal lage avstand mellom elementer i en liste eller et sett med kort,
er det ryddigere å bruke bare `margin-bottom` på alle — eller `gap`, som du får i kapittel 17.

**Oppgave 14.4 – Se kollapsen**

Lag to bokser med bakgrunnsfarge under hverandre. Gi den øverste `margin-bottom: 40px` og den nederste
`margin-top: 30px`.

Mål avstanden i utviklerverktøyet. Hva ble den? Bytt så `margin-top` til `padding-top` på den nederste
og mål igjen. Hva skjedde nå, og hvorfor?

---

## 14.7 Sentrering

Den klassiske:

```css
main {
    max-width: 65ch;
    margin: 0 auto;
}
```

`auto` betyr «fordel plassen som er igjen likt på begge sider». Med `margin: 0 auto` får du null margin
over og under, og automatisk like mye på venstre og høyre — altså midtstilt.

To ting må være på plass for at det skal virke:

1. elementet må ha en **bredde** (`width` eller `max-width`)
2. det må være et **blokkelement** (mer om det i neste kapittel)

Uten bredde fyller elementet allerede hele plassen, og da er det ingenting igjen å fordele.

> Merk at dette sentrerer **boksen**, ikke teksten inni den. Skal teksten midtstilles, er det
> `text-align: center`. To ulike ting som ofte forveksles.

---

## 14.8 Gi nettstedet ditt luft

Nå kommer den store gevinsten i dette kapitlet. Nettstedet ditt har antakelig tekst som klistrer seg
helt inntil kanten av vinduet, og elementer som ligger tett i tett.

**Oppgave 14.5 – Pust**

Gjør disse endringene i `style.css`, én om gangen, og se på siden mellom hver:

1. `* { box-sizing: border-box; }` øverst
2. `body { margin: 0; }` — fjern nettleserens standardmargin
3. `main { max-width: 65ch; margin: 0 auto; padding: 2rem 1.5rem; }`
4. Gi `header` og `footer` `padding: 1.5rem`
5. Gi overskriftene litt luft over: `h2 { margin-top: 2.5rem; }`
6. Gi et element en `border-bottom` som skillelinje

Ta skjermbilde før du begynner og etter at du er ferdig. Forskjellen er som regel større enn elevene
tror den skal bli.

**Oppgave 14.6 – Bygg tre bokser**

Lag en testside `bokser.html` og gjenskap disse tre så nøyaktig du klarer:

**Boks A** — 300 piksler bred totalt, hvit bakgrunn, 1 piksel grå ramme, 20 piksler luft inni,
lett avrundede hjørner.

**Boks B** — maks 500 piksler bred, midtstilt på siden, lys bakgrunn, ingen ramme unntatt en tykk
farget strek på venstre side, mer luft på sidene enn over og under.

**Boks C** — kvadratisk, 120 × 120 piksler, helt rund, farget bakgrunn, hvit tekst midtstilt.

For hver boks: skriv ned hvilke egenskaper du brukte.

**Oppgave 14.7 – Kortstil**

Lag en klasse `.kort` som du kan bruke på gjentakende innhold — for eksempel turene, bildene eller
oppskriftene dine. Den skal ha bakgrunnsfarge eller ramme, padding, avrundede hjørner og
`margin-bottom`.

Bruk klassen på minst tre elementer. De ligger fortsatt under hverandre — å legge dem side om side er
Flexbox-jobben i kapittel 17.

---

## 14.9 Oppsummering

- Alt på en nettside er en **boks** med fire lag: innhold, padding, border, margin.
- **Padding er inni kanten. Margin er utenfor.**
- Kortform med fire verdier går med klokka fra toppen: topp, høyre, bunn, venstre.
- **`* { box-sizing: border-box; }`** gjør at `width` betyr den faktiske bredden. Skriv den alltid.
- Sett sjelden fast `height`. Bruk `min-height` om du må.
- **`max-width` er nesten alltid bedre enn `width`** — den er mobilvennlig av seg selv.
- Loddrette marginer **kollapser**: den største vinner, de legges ikke sammen.
- `margin: 0 auto` midtstiller boksen. Det krever at boksen har en bredde.
- `text-align: center` midtstiller teksten inni. Det er noe annet.
- Boksmodell-diagrammet i utviklerverktøyet viser alle tallene for ett element.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Boksmodellen | Systemet med innhold, padding, border og margin |
| `padding` | Luft mellom innholdet og kanten – innenfor boksen |
| `border` | Kanten rundt boksen |
| `margin` | Luft utenfor boksen – avstand til andre elementer |
| Kortform | Å sette flere sider i én deklarasjon, f.eks. `padding: 10px 20px` |
| `box-sizing: border-box` | Gjør at `width` gjelder hele boksen, ikke bare innholdet |
| `max-width` | Største tillatte bredde; boksen kan bli smalere |
| `min-height` | Minste høyde; boksen kan bli høyere |
| Marginkollaps | At loddrette marginer mellom naboer slås sammen til den største |
| `margin: 0 auto` | Midtstiller en boks med bredde |
| `border-radius` | Avrundede hjørner |

---

## Innlevering – kapittel 14

Lever i læringsloggen din:

1. Utregningene fra oppgave 14.2, med og uten `border-box`.
2. `bokser.html` fra oppgave 14.6, med skjermbilde og hvilke egenskaper du brukte på hver boks.
3. Skjermbilde av nettstedet ditt **før og etter** oppgave 14.5.
4. Målingen og forklaringen fra oppgave 14.4 om marginkollaps.
5. Skjermbilde av boksmodell-diagrammet i utviklerverktøyet for ett av elementene dine.

**Sjekkliste før du går videre:**

- [ ] `box-sizing: border-box` står øverst i stilarket mitt
- [ ] Innholdet mitt klistrer seg ikke inntil kanten av vinduet lenger
- [ ] `<main>` har en maksbredde og er midtstilt
- [ ] Jeg bruker `max-width` framfor `width` der det gir mening
- [ ] Jeg kan forklare forskjellen på padding og margin
- [ ] Jeg vet hvor boksmodell-diagrammet ligger i utviklerverktøyet

---

**Neste kapittel:** Display og flyt — hvorfor noen elementer legger seg under hverandre og andre på
rad, helt av seg selv.

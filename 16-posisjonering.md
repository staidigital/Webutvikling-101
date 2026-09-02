# Kapittel 16 – Posisjonering

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - bruke `relative`, `absolute`, `fixed` og `sticky` bevisst
> - forklare hva et absolutt plassert element egentlig plasserer seg i forhold til
> - styre hva som ligger øverst med `z-index`
> - vurdere når posisjonering *ikke* er riktig verktøy

---

## 16.1 Å bryte ut av flyten

I forrige kapittel lærte du normal flyt: elementene stiller seg pent opp etter hverandre, og hvert
element tar sin plass.

Noen ganger vil du ikke det. Du vil ha et merke oppe i hjørnet av et bilde. Du vil ha en meny som blir
liggende når man skroller. Du vil ha en knapp som svever over innholdet.

Da bruker du `position`.

> **Advarsel med en gang:** posisjonering er ikke verktøyet du bygger layout med. Det er verktøyet du
> bruker til de få tingene som skal ut av flyten. Kolonner, rader og rutenett hører hjemme i Flexbox
> og Grid, som kommer i de to neste kapitlene.
>
> Elever som oppdager `position: absolute` tidlig, prøver gjerne å bygge hele siden med den. Det
> fungerer på akkurat den skjermstørrelsen de sitter med, og faller sammen på alle andre.

---

## 16.2 De fem verdiene

| Verdi | Hva den gjør |
|---|---|
| `static` | standard — elementet er i normal flyt |
| `relative` | i flyten, men kan forskyves fra sin egen plass |
| `absolute` | ute av flyten, plasseres i forhold til nærmeste posisjonerte forelder |
| `fixed` | ute av flyten, plasseres i forhold til nettleservinduet |
| `sticky` | i flyten, men fester seg når man skroller forbi |

Sammen med `position` bruker du fire egenskaper som sier **hvor**:

```css
top: 20px;
right: 20px;
bottom: 0;
left: 0;
```

De virker ikke på `position: static`. Det er derfor `top: 20px` av og til ikke gjør noe som helst — den
vanligste nybegynnerfellen i dette kapitlet.

---

## 16.3 `relative` — flytt deg litt

```css
.merke {
    position: relative;
    top: 10px;
    left: 20px;
}
```

Elementet flytter seg 10 piksler ned og 20 til høyre **fra der det ville stått**.

Det viktige: **plassen står igjen.** Elementet er fortsatt med i flyten, og naboene oppfører seg som
om det ikke har flyttet seg. Det ser bare ut som det har rykket til side.

Å bruke `relative` til å flytte ting er sjeldent. Den viktigste bruken er noe helt annet — den kommer
i neste avsnitt.

---

## 16.4 `absolute` — og det store spørsmålet

```css
.merke {
    position: absolute;
    top: 10px;
    right: 10px;
}
```

Nå er elementet **helt ute av flyten**. Plassen forsvinner, og de andre elementene lukker seg som om
det aldri fantes.

Men 10 piksler fra toppen av **hva**?

> **Et absolutt plassert element plasserer seg i forhold til nærmeste forelder som selv er
> posisjonert.** Finnes ingen slik, brukes hele siden.

«Posisjonert» betyr her at forelderen har `position` satt til noe annet enn `static` — altså
`relative`, `absolute`, `fixed` eller `sticky`.

Dette er kapitlets viktigste setning, og det er den som forklarer hvorfor merket ditt havner oppe i
hjørnet av *hele siden* i stedet for i hjørnet av bildet.

### Paret som løser det

Derfor brukes `relative` og `absolute` nesten alltid sammen, i par:

```css
.bildekort {
    position: relative;      /* jeg er utgangspunktet */
}

.bildekort .merke {
    position: absolute;      /* jeg plasserer meg i forhold til den over */
    top: 10px;
    right: 10px;
}
```

Forelderen får `position: relative` uten `top`/`left` — den flytter seg altså ikke i det hele tatt.
Den er der bare for å si: *mål fra meg*.

**Oppgave 16.1 – Merke på et bilde**

Lag et bilde med et lite farget merke oppe i høyre hjørne — for eksempel «Ny», «Utvalgt» eller et
årstall.

```html
<figure class="bildekort">
    <img src="bilder/fjell.jpg" alt="Utsikt fra Besseggen">
    <span class="merke">Utvalgt</span>
</figure>
```

Krav:

- merket ligger oppe i hjørnet av **bildet**, ikke av siden
- det har bakgrunnsfarge, padding og avrundede hjørner
- teksten er lesbar mot bakgrunnen (husk kontrastkravet fra kapittel 12)

**Prøv først uten `position: relative` på forelderen.** Se hvor merket havner. Legg den så til, og se
forskjellen. Det er den beste måten å forstå regelen på.

---

## 16.5 `fixed` — låst til vinduet

```css
header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
}
```

Elementet plasserer seg i forhold til **nettleservinduet** og blir liggende der uansett hvor mye man
skroller.

Brukes til toppmenyer, «tilbake til toppen»-knapper og informasjonsbokser om informasjonskapsler.

### To ting du må huske

**1. Innholdet legger seg under.** Fordi elementet er ute av flyten, vet ikke resten av siden at det
er der. Toppen av innholdet ditt havner under menyen. Løsningen er å dytte innholdet ned:

```css
body {
    padding-top: 70px;   /* omtrent høyden på menyen */
}
```

**2. Fast meny spiser plass på mobil.** En meny som tar 70 piksler av en skjerm som er 600 høy, spiser
over ti prosent av alt brukeren ser — hele tiden. Hold den lav, eller la den være vanlig på små
skjermer.

---

## 16.6 `sticky` — det beste fra begge

```css
header {
    position: sticky;
    top: 0;
}
```

`sticky` oppfører seg som `relative` — helt til elementet ville skrollet ut av synet. Da fester det seg
og oppfører seg som `fixed`.

Fordelene mot `fixed`:

- elementet er fortsatt i flyten, så ingenting legger seg under det
- du slipper å kompensere med padding
- innholdet får ligge i fred til det faktisk trengs

Tre ting må være på plass for at `sticky` skal virke:

1. du må oppgi hvor den skal feste seg — som regel `top: 0`
2. forelderen må ikke ha `overflow: hidden`
3. forelderen må være høy nok til at det finnes noe å skrolle

Punkt 2 er den vanligste grunnen til at `sticky` «ikke virker».

**Oppgave 16.2 – Klistret meny**

Gjør menyen din klistret med `position: sticky; top: 0;`.

Legg til en bakgrunnsfarge — uten den ser du innholdet skinne gjennom når det skroller under.

Test på en av de lange sidene dine. Blir menyen liggende? Ligger den oppå innholdet, eller under?

**Oppgave 16.3 – Sammenlikn**

Prøv den samme menyen med `position: fixed` i stedet. Hva skjedde med toppen av innholdet ditt?
Hvor mye padding måtte du legge på for å rette det opp?

Skriv to setninger om hvilken av de to du velger, og hvorfor.

---

## 16.7 `z-index` — hvem ligger øverst

Når elementer overlapper, må noe avgjøre hvem som er nærmest deg.

Standardregelen er at **den som står sist i HTML-en, ligger øverst**. Det vil du ikke alltid ha:

```css
header {
    position: sticky;
    top: 0;
    z-index: 100;
}
```

Høyere tall ligger nærmere deg. Tallene er bare rekkefølge — `z-index: 100` og `z-index: 2` gir samme
resultat hvis ingenting ligger imellom.

**`z-index` virker bare på posisjonerte elementer.** Er `position` fortsatt `static`, skjer ingenting.
Det er den vanligste grunnen til at `z-index` ikke ser ut til å gjøre noe.

Et praktisk råd: bruk noen få faste nivåer i stedet for tilfeldige tall.

```css
/* z-index-nivåer:
   1   – vanlig innhold som må ligge over noe
   100 – meny
   200 – dialogbokser
*/
```

Uten et system ender man med `z-index: 9999` overalt, og da er man like langt.

**Oppgave 16.4 – Stable tre bokser**

Lag tre bokser som overlapper hverandre, hver med sin farge. Sett dem opp slik at:

1. først ligger de i standardrekkefølge — noter hvilken som er øverst
2. bruk `z-index` slik at den **første** i HTML-en havner øverst
3. fjern `position` fra én av dem og se hva som skjer med `z-index` på den

---

## 16.8 Bonus: hopp til innhold

Her er en teknikk som kombinerer alt du kan om posisjonering, `:focus` og tilgjengelighet.

Brukere som navigerer med tastatur, må tabbe seg gjennom hele menyen på **hver eneste side** før de
kommer til innholdet. Løsningen er en lenke som er skjult helt til den får fokus:

```html
<body>
    <a href="#innhold" class="hopp-til-innhold">Hopp til hovedinnhold</a>
    <header>...</header>
    <main id="innhold">...</main>
```

```css
.hopp-til-innhold {
    position: absolute;
    top: -100px;              /* utenfor skjermen */
    left: 0;
    background: white;
    padding: 1rem;
    z-index: 300;
}

.hopp-til-innhold:focus {
    top: 0;                   /* kommer fram når den får fokus */
}
```

**Oppgave 16.5 – Lag den**

Legg inn en hopp-til-innhold-lenke på alle sidene dine. Test den: last siden på nytt, trykk `Tab` én
gang. Kom lenken fram? Trykk `Enter` — hoppet du forbi menyen?

Dette er et standardgrep på profesjonelle nettsteder. Prøv `Tab` som første handling på nrk.no eller
et offentlig nettsted, så finner du den samme lenken der.

---

## 16.9 Når posisjonering er feil verktøy

For å si det tydelig, siden fristelsen er stor:

| Du vil ha… | Ikke bruk | Bruk |
|---|---|---|
| tre kort på rad | `absolute` | Flexbox (kap. 17) |
| meny til venstre, logo til høyre | `absolute` | Flexbox |
| et rutenett med bilder | `absolute` | Grid (kap. 18) |
| en sidespalte ved siden av innholdet | `absolute` | Flexbox eller Grid |
| et merke i hjørnet av et bilde | | **`absolute`** ✓ |
| en meny som følger med | | **`sticky`** ✓ |
| en dialogboks over alt | | **`fixed`** ✓ |

Kjennetegnet på riktig bruk: du plasserer **én liten ting** i forhold til **én annen ting**. Skal
flere elementer fordele plass mellom seg, er det en layoutjobb, og da finnes det bedre verktøy.

Grunnen er at absolutt plasserte elementer ikke vet om hverandre. De kan ikke flytte seg unna, ikke
tilpasse seg innhold som blir lengre, og ikke reagere på at skjermen blir smalere. Alt du bygger med
dem, må du selv holde styr på i alle situasjoner.

---

## 16.10 Oppsummering

- `position: static` er standard. `top`, `right`, `bottom` og `left` virker ikke på den.
- `relative` flytter elementet fra sin egen plass, men **plassen står igjen**.
- `absolute` tar elementet ut av flyten og plasserer det i forhold til **nærmeste posisjonerte
  forelder**.
- Derfor brukes `relative` på forelderen og `absolute` på barnet — i par.
- `fixed` låser til vinduet. Husk at innholdet legger seg under.
- `sticky` er som regel bedre enn `fixed` til menyer — den er fortsatt i flyten.
- `z-index` bestemmer hvem som ligger øverst, og **virker bare på posisjonerte elementer**.
- Posisjonering er for enkeltting ut av flyten. **Layout bygger du med Flexbox og Grid.**

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| `position: static` | Standard – elementet ligger i normal flyt |
| `position: relative` | Forskjøvet fra egen plass, men plassen står igjen |
| `position: absolute` | Ute av flyten, plassert i forhold til nærmeste posisjonerte forelder |
| `position: fixed` | Ute av flyten, låst til nettleservinduet |
| `position: sticky` | I flyten, men fester seg ved skrolling |
| Posisjonert forelder | Element med `position` satt til noe annet enn `static` |
| `z-index` | Rekkefølge i dybden – hvem som ligger øverst |
| Hopp-til-innhold | Skjult lenke som lar tastaturbrukere hoppe forbi menyen |

---

## Innlevering – kapittel 16

Lever i læringsloggen din:

1. Bildekortet med merke fra oppgave 16.1 — skjermbilde **før og etter** at forelderen fikk
   `position: relative`.
2. Den klistrede menyen (oppgave 16.2), med skjermbilde midt i skrolling.
3. Sammenlikningen fra oppgave 16.3: `sticky` mot `fixed`, og hva du valgte.
4. De tre stablede boksene fra oppgave 16.4, med forklaring på hva som skjedde i punkt 3.
5. Skjermbilde av hopp-til-innhold-lenken når den er synlig (oppgave 16.5).

**Sjekkliste før du går videre:**

- [ ] Jeg kan forklare hva et absolutt plassert element måler fra
- [ ] Menyen min følger med når jeg skroller
- [ ] Jeg har en hopp-til-innhold-lenke som virker med Tab
- [ ] Jeg vet hvorfor `z-index` av og til ikke gjør noe
- [ ] Jeg bruker ikke `position: absolute` til å bygge layout

---

**Neste kapittel:** Flexbox. Nå kommer verktøyet som er laget nettopp for å fordele plass mellom
elementer — og menyen din blir endelig slik du ville hatt den hele tiden.

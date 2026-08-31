# Kapittel 5 – Lenker

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - lage lenker til andre nettsteder, til dine egne sider og til steder på samme side
> - skrive riktig filsti fra én fil til en annen, også mellom mapper
> - lage en meny som binder sidene dine sammen til ett nettsted
> - skrive lenketekst som gir mening

---

## 5.1 Lenken er hele poenget med weben

Weben heter *World Wide Web* – et verdensvevd nett. Det er lenkene som er trådene.

Uten dem ville nettet vært en samling løse dokumenter uten forbindelse. Det var lenken Tim Berners-Lee
egentlig fant opp: muligheten til å peke fra ett dokument til et hvilket som helst annet dokument i
verden, og komme dit med ett klikk.

Elementet heter `<a>`, for *anchor* (anker):

```html
<a href="https://www.nrk.no">Gå til NRK</a>
```

- `<a>` er elementet
- `href` er attributtet – *hypertext reference*, altså «hvor peker denne?»
- verdien er adressen
- teksten mellom taggene er det brukeren ser og klikker på

Standardutseendet er blå og understreket. Det kan vi endre med CSS senere, men vær forsiktig: folk har
lært seg at blå og understreket betyr «klikk her».

---

## 5.2 To slags adresser

Dette avsnittet er kapitlets viktigste. Nesten alle lenkeproblemer – og senere alle problemer med
bilder og stilark – handler om stier.

### Absolutt sti

En **absolutt sti** er hele adressen, med protokoll og domenenavn. Den peker på ett bestemt sted i
verden, og virker uansett hvor du bruker den fra.

```html
<a href="https://www.udir.no">Utdanningsdirektoratet</a>
```

Absolutte stier brukes til **andre nettsteder**.

### Relativ sti

En **relativ sti** sier hvor fila ligger *i forhold til fila du står i nå*. Ingen protokoll, ikke noe
domenenavn – bare veien videre.

```html
<a href="om-meg.html">Om meg</a>
```

Dette betyr: «finn fila `om-meg.html` i samme mappe som denne fila.»

Relative stier brukes til **dine egne sider**.

### Hvorfor ikke bare bruke absolutte stier overalt?

Fordi da måtte du skrevet noe slikt:

```html
<a href="file:///C:/Users/elev/OneDrive/webkurs/om-meg.html">Om meg</a>
```

Den lenken virker på din maskin, og ingen andre steder i universet. Den ryker i det øyeblikket du
legger siden ut på nett, bytter maskin, eller flytter mappen.

> **Regel:** absolutt sti til andre nettsteder, relativ sti til dine egne filer. Alltid.

---

## 5.3 Å finne veien mellom mapper

Så langt ligger alt i samme mappe. Snart gjør det ikke det. Da trenger du tre skrivemåter:

| Skrivemåte | Betyr |
|---|---|
| `fil.html` | i samme mappe |
| `mappe/fil.html` | ned i en undermappe |
| `../fil.html` | opp ett nivå, altså ut av mappen jeg står i |

`..` betyr «mappen over». Du kan bruke den flere ganger: `../../fil.html` går opp to nivåer.

Se på dette prosjektet:

```
webkurs/
├── index.html
├── om-meg.html
├── style.css
├── bilder/
│   └── profil.jpg
└── turer/
    ├── index.html
    └── besseggen.html
```

Fra `index.html` (øverst) til `turer/besseggen.html`:

```html
<a href="turer/besseggen.html">Besseggen</a>
```

Fra `turer/besseggen.html` tilbake til forsiden:

```html
<a href="../index.html">Til forsiden</a>
```

Fra `turer/besseggen.html` til `turer/index.html`:

```html
<a href="index.html">Alle turer</a>
```

Fra `turer/besseggen.html` til bildet i `bilder/`:

```
../bilder/profil.jpg
```

Altså: først **opp** ett nivå med `..`, så **ned** i `bilder`.

> **Les stien høyt.** `../bilder/profil.jpg` blir «gå opp én mappe, inn i bilder, finn profil.jpg».
> Klarer du å si den høyt, er den som regel riktig.

**Oppgave 5.1 – Finn veien**

Bruk mappestrukturen over. Skriv riktig `href` for hver av disse:

1. Fra `index.html` til `om-meg.html`
2. Fra `index.html` til `turer/index.html`
3. Fra `turer/besseggen.html` til `om-meg.html`
4. Fra `turer/index.html` til `besseggen.html`
5. Fra `om-meg.html` til bildet `bilder/profil.jpg`
6. Fra `turer/besseggen.html` til `bilder/profil.jpg`

**Oppgave 5.2 – Test at du hadde rett**

Lag faktisk mappen `turer/` med de to filene, og legg inn lenkene fra oppgave 5.1. Åpne med Live Server
og klikk deg gjennom alle sammen. Virker de? En sti du bare *tror* er riktig, er ikke riktig før du har
klikket på den.

---

## 5.4 En meny som binder nettstedet sammen

Nå har du flere sider. De skal henge sammen, og brukeren skal komme seg fram og tilbake fra alle sider.

Løsningen er en meny som ligger **øverst på hver eneste side**, med nøyaktig samme innhold:

```html
<p>
    <a href="index.html">Forsiden</a> |
    <a href="om-meg.html">Om meg</a> |
    <a href="nasjonalparker.html">Nasjonalparker</a>
</p>
```

Ja, dette blir stygt akkurat nå. Det ser ut som en tekstlinje med streker mellom. I kapittel 7 lærer du
å bygge menyen som en liste, i kapittel 8 å pakke den i `<nav>`, og i kapittel 17 å gjøre den til en
ordentlig menylinje med Flexbox. Vi bygger den i lag.

**Oppgave 5.3 – Meny på alle sider**

Legg den samme menyen øverst på alle sidene dine: `index.html`, `om-meg.html`, `nasjonalparker.html`
og `artikkel.html`.

Test at du kommer deg til alle sider fra alle sider, uten å bruke tilbakeknappen én eneste gang.

> **Legg merke til hvor slitsomt dette er.** Skal du legge til en femte side, må du inn i fire filer og
> oppdatere menyen manuelt. Akkurat dette problemet er en av grunnene til at profesjonelle nettsteder
> bruker programmering og publiseringssystemer. Nå vet du hvorfor.

---

## 5.5 Lenker til steder på samme side

Er en side lang, kan du lenke til et bestemt punkt på den. Det gjøres i to steg.

**Steg 1:** gi elementet du vil hoppe til et `id`-attributt. En `id` er et navn på ett bestemt element,
og navnet må være unikt på siden:

```html
<h2 id="kontakt">Kontakt meg</h2>
```

**Steg 2:** lenk til det med `#` foran navnet:

```html
<a href="#kontakt">Hopp til kontaktinfo</a>
```

Du kan også kombinere: lenke til et bestemt sted på en *annen* side:

```html
<a href="om-meg.html#interesser">Les om interessene mine</a>
```

Og `href="#top"` – eller bare `href="#"` – tar deg til toppen av siden.

Regler for `id`-navn: små bokstaver, ingen mellomrom, ingen æøå, og bare én av hvert navn per side.

**Oppgave 5.4 – Innholdsfortegnelse**

Gå til `nasjonalparker.html`. Gi hver `<h2>` en `id`, og lag en liten innholdsfortegnelse øverst på
siden som lenker til hver av dem. Legg inn nok tekst til at siden faktisk må skrolles, ellers ser du
ikke effekten.

Legg til slutt inn en «Til toppen»-lenke nederst på siden.

---

## 5.6 Andre ting du kan lenke til

En lenke trenger ikke gå til en nettside.

```html
<a href="mailto:post@eksempel.no">Send meg en e-post</a>
<a href="tel:+4712345678">Ring meg</a>
<a href="dokumenter/timeplan.pdf">Last ned timeplanen (PDF)</a>
```

- `mailto:` åpner brukerens e-postprogram
- `tel:` starter en oppringing – nyttig på mobil
- lenker du til en fil nettleseren ikke kan vise, blir den lastet ned i stedet

> Skriver du e-postadressen din slik på en åpen nettside, vil den før eller siden bli plukket opp av
> roboter som samler adresser til søppelpost. Det er verdt å vite før du legger ut din egen.

---

## 5.7 Åpne i ny fane

```html
<a href="https://www.nrk.no" target="_blank" rel="noopener">NRK</a>
```

`target="_blank"` åpner lenken i en ny fane. `rel="noopener"` er en sikkerhetsopplysning som bør følge
med – den hindrer at siden du åpner får tilgang til å manipulere din egen.

**Bruk dette sparsomt.** Mange brukere blir irriterte når nettsteder overstyrer hvordan nettleseren
deres skal oppføre seg, og tilbakeknappen slutter å virke slik de forventer. Vanlig praksis:

- **egne sider:** samme fane
- **eksterne nettsteder eller PDF-er:** ny fane kan forsvares

---

## 5.8 Lenketekst er en ferdighet

Dette er en av de tingene som skiller en gjennomtenkt nettside fra en amatørmessig.

❌ Dårlig:

```html
<p>For å lese mer om opptakskravene, <a href="opptak.html">klikk her</a>.</p>
```

✅ Bedre:

```html
<p>Se <a href="opptak.html">opptakskravene til IM</a>.</p>
```

Hvorfor betyr det noe?

Brukere **skanner** nettsider – de leser ikke ordentlig, de hopper mellom det som skiller seg ut, og
lenker skiller seg ut. En side full av «klikk her» gir ingen informasjon når man skanner den.

Verre er det for de som bruker skjermleser. Et vanlig grep der er å be programmet lese opp alle lenkene
på siden som en liste, for å finne fram raskt. Da høres siden din slik ut:

> «klikk her, klikk her, les mer, her, klikk her»

**Testen:** dekk over resten av teksten og les bare lenketeksten. Skjønner du fortsatt hvor den fører?

**Oppgave 5.5 – Skriv om lenkene**

Skriv om disse setningene slik at lenketeksten står på egne ben:

1. `For informasjon om skolestart, <a href="...">trykk her</a>.`
2. `Timeplanen finner du <a href="...">her</a>.`
3. `<a href="...">Les mer</a> om linjene våre.`
4. `Last ned skjemaet <a href="...">her</a> og lever det innen fredag.`

**Oppgave 5.6 – Gå gjennom dine egne**

Se over alle lenkene du har laget så langt. Har noen av dem dårlig lenketekst? Rett dem opp.

---

## 5.9 Lenkens fire tilstander

En lenke ser ulik ut avhengig av hva som skjer med den. Nettleseren gjør dette automatisk:

| Tilstand | Hva det betyr | Standardutseende |
|---|---|---|
| normal | ikke besøkt | blå, understreket |
| besøkt | brukeren har vært der før | lilla |
| hover | musepekeren er over | pekefinger-markør |
| aktiv | akkurat i det du klikker | rød et lite øyeblikk |

At besøkte lenker skifter farge er faktisk nyttig – brukeren ser hvor hen allerede har vært. Mange
nettsteder slår av dette av designhensyn, og det er ikke alltid en god idé.

I kapittel 11 lærer du å style alle disse tilstandene selv.

**Oppgave 5.7 – Observer**

Åpne siden din, klikk på en lenke og gå tilbake. Har lenken skiftet farge? Hold musepekeren over en
lenke og se nederst i venstre hjørne av nettleseren: der vises adressen lenken går til. Prøv det på en
nettavis også – det er slik man sjekker hvor en lenke *egentlig* fører før man klikker.

---

## 5.10 Oppsummering

- `<a href="...">Lenketekst</a>` er lenken. `href` sier hvor den peker.
- **Absolutt sti** (`https://...`) til andre nettsteder. **Relativ sti** til dine egne filer.
- `mappe/fil.html` går ned i en mappe, `../fil.html` går opp ett nivå.
- Les stien høyt for å sjekke om den er riktig – og klikk på lenken for å være sikker.
- Samme meny på alle sider binder nettstedet sammen.
- `id` på et element + `href="#navn"` gir lenke til et sted på siden.
- `mailto:` og `tel:` lenker til e-post og telefon.
- `target="_blank"` åpner i ny fane – bruk det sparsomt.
- Lenketeksten skal gi mening alene. «Klikk her» gir det ikke.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| `<a>` | Lenkeelementet (*anchor*) |
| `href` | Attributtet som sier hvor lenken peker |
| Absolutt sti | Full adresse med protokoll og domene |
| Relativ sti | Sti i forhold til fila du står i nå |
| `../` | Ett nivå opp i mappestrukturen |
| `id` | Unikt navn på ett element på siden |
| Ankerlenke | Lenke til et `id` på samme eller annen side, med `#` |
| `target="_blank"` | Åpner lenken i ny fane |
| `mailto:` / `tel:` | Lenker som åpner e-post eller oppringing |
| Lenketekst | Den klikkbare teksten – skal gi mening alene |
| Besøkt lenke | Lenke brukeren har fulgt før; skifter farge automatisk |

---

## Innlevering – kapittel 5

Lever i læringsloggen din:

1. Svarene på oppgave 5.1, og skjermbilde som viser at mappen `turer/` fungerer (oppgave 5.2).
2. Nettstedet ditt med meny på alle sider – skjermbilde av to ulike sider der menyen er lik.
3. `nasjonalparker.html` med innholdsfortegnelse og «Til toppen»-lenke.
4. De omskrevne lenketekstene fra oppgave 5.5.

**Sjekkliste før du går videre:**

- [ ] Alle sidene mine har den samme menyen
- [ ] Jeg kommer meg til alle sider fra alle sider
- [ ] Ingen av lenkene mine er brutte
- [ ] Jeg vet forskjellen på absolutt og relativ sti, og når jeg bruker hvilken
- [ ] Jeg vet hva `../` betyr
- [ ] Ingen av lenkene mine heter «klikk her»

---

**Neste kapittel:** Bilder – og med dem kommer stiene fra dette kapitlet tilbake, denne gangen for alvor.

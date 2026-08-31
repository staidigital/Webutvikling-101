# Kapittel 4 – Tekst og innhold

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - bygge opp en tekstside med riktig overskriftshierarki
> - velge riktig element til riktig type tekst
> - forklare forskjellen på `<strong>` og `<b>` – og hvorfor den betyr noe
> - styre linjeskift og mellomrom slik du faktisk vil ha dem

---

## 4.1 Nå fyller vi rammen

Forrige kapittel ga deg rammen: doctype, `<head>` og `<body>`. Fra nå av jobber vi nesten bare inni
`<body>`.

Det aller meste av innholdet på nettet er tekst. Selv på sider som ser ut som de mest handler om bilder
og video, er det tekst som bærer strukturen. Derfor begynner vi her.

---

## 4.2 Avsnitt

Elementet `<p>` lager et **avsnitt** (*paragraph*). Det er det vanligste elementet på nett.

```html
<p>Jeg går første året på informasjonsteknologi og medieproduksjon.</p>
<p>På fritiden spiller jeg håndball og redigerer video.</p>
```

Nettleseren gir automatisk litt luft over og under hvert avsnitt. Du trenger ikke gjøre noe for å få
avstand mellom dem – det ordner seg selv.

**Ett avsnitt = én tanke.** Har du fire setninger om to helt ulike ting, er det som regel to avsnitt.

---

## 4.3 Overskrifter og hierarki

Det finnes seks nivåer av overskrifter, fra `<h1>` til `<h6>`:

```html
<h1>Norske nasjonalparker</h1>
    <h2>Jotunheimen</h2>
        <h3>Galdhøpiggen</h3>
        <h3>Besseggen</h3>
    <h2>Rondane</h2>
        <h3>Rondslottet</h3>
```

*(Innrykkene over er bare for å vise strukturen – overskrifter ligger ikke inni hverandre i koden.)*

Tenk på det som innholdsfortegnelsen i en bok. `<h1>` er boktittelen, `<h2>` er kapitlene,
`<h3>` er underkapitlene.

### To regler

**1. Bare én `<h1>` per side.** Den sier hva hele siden handler om.

**2. Ikke hopp over nivåer.** Etter en `<h2>` kommer enten en ny `<h2>` eller en `<h3>` – aldri
rett til `<h4>`.

### Overskrifter er ikke skriftstørrelse

Dette er det viktigste i hele kapitlet, og det er en felle nesten alle går i:

> Velg overskriftsnivå ut fra **hvor viktig innholdet er**, aldri ut fra hvor stor teksten blir.

Det er fristende å bruke `<h4>` fordi «`<h2>` ble så stor». Ikke gjør det. Skal teksten være mindre,
fikser vi det med CSS i del 2 av kurset. Overskriftsnivået skal si noe om *strukturen*.

Grunnen er at overskriftene brukes av mer enn øynene dine:

- **Skjermlesere** lar blinde brukere hoppe mellom overskriftene for å finne fram på siden. Hopper du
  over nivåer, blir den navigasjonen ubrukelig.
- **Søkemotorer** bruker overskriftene til å forstå hva siden handler om.
- **Nettleserens leservisning** bygger på det samme.

**Oppgave 4.1 – Marker opp en tekst**

Under står en råtekst uten oppmerking. Lag en ny fil `nasjonalparker.html` med full grunnstruktur, og
marker opp teksten med riktige overskriftsnivåer og avsnitt.

```
Norske nasjonalparker
Norge har 47 nasjonalparker. Her er tre av de mest besøkte.

Jotunheimen
Jotunheimen ligger mellom Gudbrandsdalen og Sogn, og har over 250 topper over 1900 meter.

Galdhøpiggen
Norges høyeste fjell, 2469 meter over havet. Turen tar rundt seks timer tur-retur.

Besseggen
En av landets mest kjente fjellturer. Utsikten over Gjende er grunnen til at folk kommer.

Rondane
Norges første nasjonalpark, opprettet i 1962.

Rondslottet
Det høyeste punktet i Rondane, 2178 meter.
```

Sjekk til slutt: bruker du nøyaktig én `<h1>`? Hopper du over noen nivåer?

**Oppgave 4.2 – Kontroller strukturen**

Åpne siden din i nettleseren, trykk `F12` og velg fanen **Elements**. Klapp sammen elementene og se
strukturen ovenfra. Ser overskriftene ut som en fornuftig innholdsfortegnelse?

Prøv deretter det samme på `nrk.no`: finn `<h1>` og se hvordan overskriftsnivåene er brukt der.

---

## 4.4 Mellomrom og linjeskift oppfører seg ikke som du tror

Skriv dette i en fil og se på resultatet:

```html
<p>Dette          er        en        test.</p>
<p>Første linje
Andre linje
Tredje linje</p>
```

Resultatet blir:

```
Dette er en test.
Første linje Andre linje Tredje linje
```

**HTML slår sammen alle mellomrom og linjeskift til ett enkelt mellomrom.**

Det høres irriterende ut, men er faktisk grunnen til at du kan rykke inn koden din så mye du vil uten
at siden endrer seg. Uten denne regelen ville innrykkene dine dukket opp som mellomrom på siden.

**Oppgave 4.3 – Test det selv**

Lag et avsnitt der du med vilje legger inn ti mellomrom, tre linjeskift og en tabulator midt i teksten.
Se hva som skjer i nettleseren. Skriv én setning i loggen om hva du observerte.

### Når du faktisk vil ha linjeskift

Trenger du et linjeskift *inne i* et avsnitt, bruker du `<br>`:

```html
<p>
    Sondre Stai<br>
    Elvebakken videregående skole<br>
    Oslo
</p>
```

Dette er riktig bruk: adresser, dikt, sangtekster – tekst der linjedelingen er en del av innholdet.

**Ikke** bruk `<br><br>` for å lage luft mellom avsnitt. Da skal du bruke to `<p>`-elementer.
Avstand er utseende, og utseende hører hjemme i CSS.

### Skillelinje

`<hr>` lager en vannrett strek som markerer et tematisk skille:

```html
<h2>Sommer</h2>
<p>Vi var i Spania.</p>

<hr>

<h2>Høst</h2>
<p>Så begynte skolen.</p>
```

Både `<br>` og `<hr>` er tomme elementer – ingen sluttag.

---

## 4.5 Utheving: mening eller utseende?

Her er fire elementer som ser like ut, men betyr ulike ting.

```html
<p>Dette er <strong>veldig viktig</strong>.</p>
<p>Dette er <b>fet tekst</b>.</p>
<p>Jeg leser <em>helst</em> om kvelden.</p>
<p>Boka heter <i>Sult</i>.</p>
```

På skjermen ser `<strong>` og `<b>` helt like ut – begge blir fete. `<em>` og `<i>` blir begge kursive.
Forskjellen ligger i **hva du sier med dem**:

| Element | Betyr | Brukes til |
|---|---|---|
| `<strong>` | Dette er viktig | Advarsler, nøkkelord, «husk dette» |
| `<b>` | Bare fet skrift, uten ekstra mening | Produktnavn i en liste, stikkord |
| `<em>` | Trykk på dette ordet | Betoning som endrer meningen i setningen |
| `<i>` | Bare kursiv, uten ekstra mening | Boktitler, fremmedord, tanker |

En skjermleser leser `<strong>` og `<em>` med annen stemme eller trykk. `<b>` og `<i>` leses helt
nøytralt. Det er hele forskjellen – men det er en reell forskjell for de som bruker en.

Legg merke til hva `<em>` gjør med denne setningen:

- «Jeg sa aldri at *hun* tok pengene.»
- «Jeg sa aldri at hun *tok* pengene.»

Samme ord, ulik mening. Det er derfor elementet finnes.

**Tommelfingerregel:** velg `<strong>` og `<em>` når du er i tvil. Det er mening du som regel er ute
etter, ikke bare tykk skrift.

**Oppgave 4.4 – Velg riktig element**

Skriv opp hvilket av de fire elementene du ville brukt, og begrunn kort:

1. Ordet «ikke» i setningen «Du må **ikke** trykke på denne knappen.»
2. Boktittelen «Sult» i en bokanmeldelse
3. Ordet «gratis» i «Kurset er **gratis** for alle elever.»
4. Det latinske navnet *Ursus arctos* i en tekst om bjørn
5. Ordet «i dag» i «Fristen er **i dag**.»

---

## 4.6 Sitater

Er sitatet et helt avsnitt, bruker du `<blockquote>`:

```html
<blockquote>
    <p>Det er ikke lett å lage noe enkelt.</p>
</blockquote>
```

Er det bare noen ord midt i en setning, bruker du `<q>`:

```html
<p>Hun sa at det var <q>helt greit</q>.</p>
```

`<q>` legger automatisk på anførselstegn – du skal ikke skrive dem selv.

Har du en kilde, oppgir du den slik:

```html
<blockquote cite="https://www.nrk.no/artikkel">
    <p>Antall søkere økte med 12 prosent.</p>
</blockquote>
<p>– NRK, 2026</p>
```

---

## 4.7 Span

`<span>` er et element helt uten mening. Det gjør ingenting i seg selv.

```html
<p>Prisen er <span>249 kroner</span> per måned.</p>
```

Siden ser nøyaktig lik ut med og uten det. Poenget kommer først i del 2 av kurset: `<span>` er en
**krok å henge CSS på**, slik at du kan style en bit tekst midt inne i et avsnitt uten å endre hva
teksten betyr.

Vi nevner det her fordi du vil se det, men bruker det ikke ordentlig før kapittel 11.

---

## 4.8 Spesialtegn

Noen tegn har en egen jobb i HTML og kan ikke skrives rett fram. Skriver du dette:

```html
<p>5 < 10</p>
```

...tror nettleseren at `< 10` er starten på en ny tag, og teksten forsvinner.

Løsningen er **entiteter** – erstatningskoder som alltid starter med `&` og slutter med `;`:

| Skriv dette | Får du | Navn |
|---|---|---|
| `&lt;` | `<` | mindre enn |
| `&gt;` | `>` | større enn |
| `&amp;` | `&` | og-tegn |
| `&nbsp;` | mellomrom som ikke brytes | hardt mellomrom |
| `&copy;` | © | copyright |
| `&hellip;` | … | tre prikker |

Æ, ø og å trenger *ikke* entiteter så lenge du har `<meta charset="utf-8">` på plass.

`&nbsp;` er nyttig når to ord ikke skal havne på hver sin linje:

```html
<p>Møtet varer i 5&nbsp;timer.</p>
```

Nå følger «5» og «timer» hverandre uansett hvor smal skjermen blir.

**Oppgave 4.5 – Skriv det umulige**

Lag et avsnitt på siden din som viser denne teksten nøyaktig slik den står, med tegnene synlige:

```
Bruk <p> og </p> rundt avsnitt. Husk & mellom navnene.
```

Dette er en klassisk nybegynnerhindring, og løsningen er alltid entiteter.

---

## 4.9 Fyllstoff når du mangler tekst

Når du skal teste hvordan en side ser ut, men ikke har ekte tekst ennå, bruker utviklere latinsk
fyllstoff kalt **lorem ipsum**.

I VS Code: skriv `lorem30` og trykk `Tab`, så får du 30 ord med fyllstoff. Skriv `p*3>lorem20` og
trykk `Tab`, så får du tre avsnitt.

Nyttig når du eksperimenterer. Husk å bytte det ut med ekte innhold før du leverer.

---

## 4.10 Bygg videre på nettstedet ditt

**Oppgave 4.6 – «Om meg» med ordentlig innhold**

Åpne `om-meg.html` fra forrige kapittel og fyll den med innhold:

- én `<h1>` med navnet ditt
- minst to `<h2>`-seksjoner, for eksempel «Interesser» og «Hvorfor jeg valgte IM»
- minst fire avsnitt til sammen
- et sted der du bruker `<strong>` eller `<em>` fordi det gir mening – ikke bare for å ha gjort det
- en adresse eller lignende med `<br>` mellom linjene
- én `<hr>` som skiller to deler
- minst én kommentar i koden som forklarer strukturen

Til slutt: rydd innrykkene med `Shift + Alt + F` og se over at nøstingen er riktig.

**Oppgave 4.7 – Skriv om en ekte side**

Velg en kort artikkel fra en nettavis. Kopier teksten inn i en ny fil `artikkel.html` og marker den opp
selv, uten å se på nettavisens kode: overskrift, ingress, mellomtitler, avsnitt, sitater.

Sammenlikn til slutt med avisens egen kode via Vis kildekode. Hva gjorde de likt som deg? Hva gjorde de
annerledes?

---

## 4.11 Oppsummering

- `<p>` er avsnitt. Nettleseren gir automatisk luft mellom dem.
- `<h1>`–`<h6>` er overskrifter. **Én `<h1>` per side, og aldri hopp over nivåer.**
- Overskriftsnivå velges ut fra **struktur**, ikke ut fra ønsket skriftstørrelse.
- HTML slår sammen alle mellomrom og linjeskift til ett mellomrom.
- `<br>` gir linjeskift inni et avsnitt. `<hr>` gir en tematisk skillelinje. Begge er tomme elementer.
- `<strong>` og `<em>` bærer **mening**. `<b>` og `<i>` er bare utseende. Velg de to første når du er i tvil.
- `<blockquote>` er et helt sitat, `<q>` er et kort sitat i en setning.
- `<span>` betyr ingenting – det er en krok for CSS senere.
- Entiteter som `&lt;`, `&gt;` og `&amp;` lar deg skrive tegn som ellers er opptatt.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Avsnitt / `<p>` | Én sammenhengende tekstblokk |
| Overskriftshierarki | Systemet `<h1>`–`<h6>` som viser hva som er over- og underordnet |
| `<br>` | Linjeskift inni et avsnitt |
| `<hr>` | Vannrett strek som markerer et tematisk skille |
| `<strong>` | Innhold som er viktig; leses med trykk av skjermleser |
| `<em>` | Betoning av et ord; kan endre meningen i setningen |
| `<b>` / `<i>` | Fet og kursiv uten ekstra betydning |
| `<blockquote>` | Sitat som utgjør et helt avsnitt |
| `<q>` | Kort sitat inne i en setning |
| `<span>` | Nøytralt element uten mening, brukes som feste for CSS |
| Entitet | Erstatningskode for et tegn, f.eks. `&amp;` |
| Skjermleser | Program som leser opp nettsiden for blinde og svaksynte |
| Lorem ipsum | Fyllstofftekst brukt mens man tester utseende |

---

## Innlevering – kapittel 4

Lever i læringsloggen din:

1. `nasjonalparker.html` fra oppgave 4.1.
2. Den oppdaterte `om-meg.html` fra oppgave 4.6, med skjermbilde.
3. Svarene fra oppgave 4.4, med begrunnelser.
4. Løsningen på oppgave 4.5.
5. Sammenlikningen fra oppgave 4.7 – to–tre setninger om hva avisen gjorde annerledes enn deg.

**Sjekkliste før du går videre:**

- [ ] Sidene mine har nøyaktig én `<h1>` hver
- [ ] Jeg hopper ikke over overskriftsnivåer
- [ ] Jeg vet hvorfor `<strong>` ikke er det samme som `<b>`
- [ ] Jeg vet hvorfor tre linjeskift i koden ikke gir tre linjeskift på siden
- [ ] Jeg kan skrive `<` og `&` som tekst på en nettside

---

**Neste kapittel:** Lenker – det som gjør en samling sider til et nettsted, og som ga weben navnet sitt.

# Kapittel 2 – Verktøy og arbeidsflyt

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - bruke VS Code til å skrive og lagre kode
> - sette opp en ryddig prosjektmappe med fornuftige filnavn
> - starte Live Server og se endringene dine med én gang
> - forklare hvorfor forsiden alltid heter `index.html`

---

## 2.1 Verktøyet er ikke poenget – men det må sitte

En nettside er bare tekst, som du lærte i forrige kapittel. Du *kunne* i prinsippet skrevet den i
Notisblokk eller Word. Men proffe utviklere bruker en **kodeeditor**, og det er det du skal bruke også.

En kodeeditor er et skriveprogram laget for kode. Den gjør fire ting for deg:

- **fargelegger** koden så du ser strukturen
- **fullfører** det du skriver, så du slipper å taste alt
- **sier fra** når noe er skrevet feil
- **holder orden** på hele prosjektmappen din i ett vindu

Vi bruker **Visual Studio Code**, ofte kalt bare *VS Code*. Det er gratis, det er det mest brukte
verktøyet i bransjen, og det er det du kommer til å møte igjen hvis du jobber med dette senere.

> **Merk:** Word og Google Docs kan *ikke* brukes til kode. De legger inn usynlig formatering,
> bytter ut anførselstegn med «krøllete» varianter, og lagrer i feil filformat. Koden din vil ikke virke.

---

## 2.2 Kom i gang med VS Code

**Oppgave 2.1 – Åpne og bli kjent**

Åpne VS Code. Er den ikke installert på maskinen din, si fra til læreren.

Finn disse fire delene av vinduet, og skriv ned hva du tror hver av dem brukes til:

1. **Aktivitetslinjen** helt til venstre – smale ikoner loddrett nedover
2. **Utforskeren** (*Explorer*, det øverste ikonet) – viser filene i prosjektet ditt
3. **Redigeringsområdet** i midten – her skriver du koden
4. **Statuslinjen** nederst – viser info om fila du står i

Du trenger ikke skjønne alt. Vi bruker en liten del av VS Code i dette kurset.

**Tips:** Er menyene på engelsk og du vil ha norsk (eller motsatt)? Trykk `Ctrl + Shift + P`
(`Cmd + Shift + P` på Mac), skriv «display language» og velg språk.

---

## 2.3 Prosjektmappen

Dette avsnittet virker kjedelig. Det er likevel det avsnittet som kommer til å spare deg for flest
frustrerende timer senere i kurset. Nesten alle feil elever får med bilder og stilark, handler egentlig
om at filene ligger feil sted.

En nettside er ikke én fil. Det er en **mappe med filer** som peker på hverandre. Flytter du én av
dem, mister de andre kontakten.

Slik skal prosjektet ditt se ut:

```
webkurs/
├── index.html
├── style.css
└── bilder/
    ├── profilbilde.jpg
    └── logo.png
```

- `webkurs/` er **rotmappen** – hele prosjektet ligger inni denne
- `index.html` er forsiden
- `style.css` er stilarket (det kommer i kapittel 10, men vi lager mappen riktig nå)
- `bilder/` er en undermappe for alle bildene

**Oppgave 2.2 – Lag prosjektmappen**

1. Lag en mappe som heter `webkurs` et sted du finner den igjen – i OneDrive-mappen din, ikke på skrivebordet.
2. I VS Code: **Fil → Åpne mappe** og velg `webkurs`.
3. I Utforskeren til venstre: bruk ikonet **Ny fil** og lag `index.html`.
4. Lag også `style.css`.
5. Bruk ikonet **Ny mappe** og lag `bilder`.

Nå skal Utforskeren i VS Code vise nøyaktig treet over.

> **Viktig:** Åpne alltid *mappen* i VS Code, aldri bare én enkelt fil. Live Server trenger å vite
> hvor rotmappen er for å kunne finne resten av filene.

---

## 2.4 Regler for filnavn

Filnavn på nett følger strengere regler enn filnavn på PC-en din. Tjenere er ofte Linux-maskiner, og de
er langt mer nøye enn Windows.

| Regel | Ikke gjør dette | Gjør dette |
|---|---|---|
| Ingen mellomrom | `mitt bilde.jpg` | `mitt-bilde.jpg` |
| Ingen æ, ø, å | `påske.html` | `paaske.html` |
| Bare små bokstaver | `Forside.HTML` | `forside.html` |
| Ingen spesialtegn | `pris#2 (ny).png` | `pris-2-ny.png` |
| Bruk bindestrek | `om_meg.html` | `om-meg.html` |
| Riktig filtype | `index.txt` | `index.html` |

Bruk **bindestrek** som ordskille. Det er standarden på nett, blant annet fordi søkemotorer leser
bindestrek som mellomrom, men understrek som en del av ordet.

**Store og små bokstaver er ikke det samme.** På din Windows-PC vil `Bilde.jpg` og `bilde.jpg` fungere
om hverandre. På en ekte tjener er de to helt forskjellige filer. Dette er en klassisk feil: siden ser
perfekt ut på skolen, og så er alle bildene borte når den legges ut på nett. Hold deg til små bokstaver
overalt, alltid.

**Oppgave 2.3 – Rydd opp**

En elev har levert dette prosjektet. Skriv om hvert filnavn, og plasser filene i riktig mappe:

```
Min Nettside/
├── Forside (ferdig!).html
├── side2.html
├── stil.css
├── Skjermbilde 2026-08-14 kl. 13.05.png
├── ny mappe/
│   └── bilde av meg på tur.JPG
└── notater.docx
```

Skriv opp den ryddige versjonen, og forklar for hver endring hvorfor du gjorde den.
Er det noen fil som ikke hører hjemme i prosjektmappen i det hele tatt?

---

## 2.5 Hvorfor heter forsiden `index.html`?

Når du går til `https://elvebakken.vgs.no`, ber du ikke om noen bestemt fil. Du ber bare om mappen.

Da har tjeneren en regel: *finnes det en fil som heter `index.html` her, så send den.*

Derfor er `index.html` alltid navnet på forsiden. Kaller du den `forside.html` eller `hjem.html`,
vet ikke tjeneren hva den skal sende, og brukeren får en feilmelding.

Regelen gjelder i hver mappe. `nettsted.no/bilder/` sender `bilder/index.html` hvis den finnes.

---

## 2.6 Live Server

Nå kommer den delen som gjør koding gøy.

Du *kan* åpne `index.html` rett i nettleseren og trykke `F5` hver gang du endrer noe. Det blir slitsomt
fort. **Live Server** er en utvidelse til VS Code som gjør to ting:

1. Den gjør maskinen din til en liten **tjener** – akkurat den typen du lærte om i kapittel 1.
2. Den **oppdaterer nettleseren automatisk** hvert eneste gang du lagrer.

Du skriver kode på den ene halvdelen av skjermen og ser resultatet på den andre, i sanntid.

**Oppgave 2.4 – Installer og start Live Server**

1. Klikk på **Utvidelser** i aktivitetslinjen (ikonet med fire firkanter), eller trykk `Ctrl + Shift + X`.
2. Søk etter **Live Server**. Velg den av **Ritwick Dey** – den har flere titalls millioner nedlastinger.
3. Klikk **Installer**.
4. Åpne `index.html`.
5. Klikk **Go Live** nederst til høyre i statuslinjen.

Nettleseren åpner seg. Adressen ser omtrent slik ut:

```
http://127.0.0.1:5500/index.html
```

Legg merke til at det ikke står noe domenenavn her. `127.0.0.1` betyr «denne maskinen» – det er
maskinens adresse til seg selv. `5500` er portnummeret Live Server bruker. Ingen andre på internett
kan se denne siden; den finnes bare på din PC.

Siden er helt hvit og tom. Det er riktig – `index.html` er jo tom.

---

## 2.7 Din første nettside

Skriv dette i `index.html`. **Skriv det, ikke kopier det.**

```html
<!DOCTYPE html>
<html lang="no">
<head>
    <meta charset="utf-8">
    <title>Min første nettside</title>
</head>
<body>
    <h1>Hei!</h1>
    <p>Dette er den aller første nettsiden jeg har laget.</p>
</body>
</html>
```

Lagre med `Ctrl + S`. Se på nettleseren.

Du skal se en stor fet overskrift og en linje med vanlig tekst. Du har laget en nettside.

Du forstår sannsynligvis ikke alt som står der ennå – hele kapittel 3 handler om nettopp denne
strukturen. Akkurat nå er poenget bare å bekrefte at verktøyene virker.

**Oppgave 2.5 – Se den oppdatere seg live**

1. Legg vinduene ved siden av hverandre: VS Code til venstre, nettleseren til høyre.
   (`Windows-tast + venstre/høyre pil` på Windows.)
2. Endre teksten inni `<h1>` til navnet ditt. Lagre.
3. Legg til et avsnitt til: `<p>Jeg går på Elvebakken.</p>`. Lagre.
4. Se at nettleseren oppdaterer seg hver gang, uten at du rører den.

Ta skjermbilde av begge vinduene side om side.

---

## 2.8 Fire hurtigtaster som er verdt å lære

| Hurtigtast (Windows) | Mac | Hva den gjør |
|---|---|---|
| `Ctrl + S` | `Cmd + S` | Lagre. Bruk hele tiden – Live Server viser bare lagrede endringer |
| `Shift + Alt + F` | `Shift + Option + F` | Rydd opp innrykk i hele fila automatisk |
| `Ctrl + /` | `Cmd + /` | Gjør linjen du står på om til en kommentar |
| `Ctrl + Z` | `Cmd + Z` | Angre |

**Innrykk** er de små mellomrommene foran linjene. Nettleseren bryr seg ikke om dem i det hele tatt –
siden ser helt lik ut uten. De er der for **mennesker**, så du kan se hva som ligger inni hva.
Rotete innrykk er den vanligste grunnen til at elever ikke finner sine egne feil.

**Oppgave 2.6 – Prøv formateringen**

Slett alle innrykkene i `index.html` slik at alt ligger helt til venstre. Lagre, og se på nettleseren.
Endret siden seg? Trykk deretter `Shift + Alt + F` og se hva som skjer med koden.

---

## 2.9 Hva gjør denne koden?

**Oppgave 2.7**

En elev har fått denne adressen i nettleseren sin:

```
file:///C:/Users/elev/Desktop/webkurs/index.html
```

En annen elev har denne:

```
http://127.0.0.1:5500/index.html
```

Hva er forskjellen på hva de to har gjort? Hvem av dem bruker Live Server?

**Oppgave 2.8 – Hva mangler her?**

Tre elever får problemer. Forklar for hver av dem hva som sannsynligvis er galt:

1. «Jeg trykker Go Live, men nettleseren sier *Cannot GET /*.»
   *(Hint: hva heter fila, og hvilken mappe er åpnet i VS Code?)*
2. «Jeg endrer koden, men ingenting skjer på siden.»
3. «Bildet mitt vises på skolen, men ikke når jeg åpner siden hjemme.»
   *(Hint: hvor lå bildet, og hva het det?)*

---

## 2.10 Oppsummering

- **VS Code** er kodeeditoren vår. Åpne alltid *mappen*, ikke enkeltfiler.
- Prosjektet er en **rotmappe** med `index.html`, `style.css` og en `bilder/`-mappe.
- Filnavn: **små bokstaver, ingen mellomrom, ingen æøå, bindestrek som ordskille**.
- Forsiden må hete **`index.html`** – det er fila tjeneren sender når ingen fil er spesifisert.
- **Live Server** gjør maskinen din til en tjener og oppdaterer nettleseren når du lagrer.
- **`127.0.0.1`** betyr «min egen maskin». Siden er ikke synlig for andre.
- **Innrykk** er for mennesker, ikke for maskiner – men de er viktige likevel.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Kodeeditor | Skriveprogram laget for kode, f.eks. VS Code |
| Utvidelse (*extension*) | Tilleggsfunksjon du installerer i VS Code, f.eks. Live Server |
| Rotmappe | Den øverste mappen i prosjektet – alt annet ligger inni den |
| Undermappe | Mappe inni en annen mappe, f.eks. `bilder/` |
| `index.html` | Standardnavnet på forsiden i en mappe |
| Live Server | Utvidelse som kjører en lokal tjener og oppdaterer nettleseren automatisk |
| Lokal tjener | Tjener som kjører på din egen maskin, ikke på nett |
| `127.0.0.1` / localhost | Maskinens adresse til seg selv |
| Port | Nummeret etter kolon i adressen, f.eks. `:5500` |
| Innrykk | Mellomrom foran kodelinjer som viser strukturen |
| Kommentar | Tekst i koden som er til mennesker, og som ignoreres av maskinen |

---

## Innlevering – kapittel 2

Lever i læringsloggen din:

1. Skjermbilde av VS Code der Utforskeren viser prosjektmappen din med alle filene.
2. Skjermbildet fra oppgave 2.5 – kode og nettside side om side.
3. Den ryddede fillisten fra oppgave 2.3, med begrunnelser.
4. Svarene på oppgave 2.7 og 2.8.

**Sjekkliste før du går videre:**

- [ ] Mappen `webkurs` er åpnet i VS Code
- [ ] Den inneholder `index.html`, `style.css` og mappen `bilder/`
- [ ] Live Server er installert og «Go Live» virker
- [ ] Navnet mitt vises som overskrift på siden
- [ ] Jeg vet hvor på maskinen mappen min ligger

---

**Neste kapittel:** Nå tar vi koden du nettopp skrev fra hverandre, linje for linje, og finner ut hva
hver eneste del betyr.

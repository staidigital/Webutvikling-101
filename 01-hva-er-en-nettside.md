# Kapittel 1 – Hva er egentlig en nettside?

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - forklare hva som skjer fra du skriver inn en nettadresse til siden vises på skjermen
> - forklare forskjellen på internett og web
> - forklare hva HTML, CSS og JavaScript gjør – hver for seg
> - åpne kildekoden til en hvilken som helst nettside og kjenne igjen deler av den

---

## 1.1 Du har brukt nettsider i mange år. Nå skal du lage dem.

Du har sannsynligvis besøkt flere tusen nettsider. Du vet hvordan de oppfører seg: du klikker,
det skjer noe, du skroller videre. Men du har antakelig aldri sett hva en nettside faktisk *er*.

Svaret er kanskje overraskende enkelt:

> **En nettside er en tekstfil.**

Ikke et bilde. Ikke et program. En helt vanlig tekstfil som ligger på en datamaskin et sted i verden,
og som nettleseren din henter og *tegner opp* på skjermen. Alt du ser på nettet – TikTok, Vy, skolens
læringsplattform – begynner som tekst noen har skrevet.

Og du kan lese den teksten. Akkurat nå.

---

## 1.2 Prøv selv: se bak kulissene

**Oppgave 1.1 – Vis kildekode**

1. Åpne en nettside du bruker ofte, for eksempel `nrk.no` eller `vg.no`.
2. Høyreklikk et sted på siden og velg **Vis sidekilde** / *View page source*.
   (Hurtigtast: `Ctrl + U` på Windows, `Cmd + Alt + U` på Mac.)
3. Se på det som kommer opp.

Det ser rotete ut. Det skal det få lov til – ekte nettsider er store. Men prøv å finne igjen dette:

- noe som starter med `<h1` – det er en hovedoverskrift
- noe som starter med `<img` – det er et bilde
- noe som starter med `<a href` – det er en lenke
- helt øverst: `<!DOCTYPE html>`

**Skriv ned:** finn én overskrift og én lenke, og lim dem inn i læringsloggen din.

Det du nettopp leste er **HTML**. Det er dette språket du skal lære i de neste ukene, og det er
akkurat like enkelt som det ser ut: tekst, pakket inn i merkelapper.

---

## 1.3 Internett og web er ikke det samme

Folk bruker ordene om hverandre, men de betyr ulike ting.

| | Hva det er | Sammenlikning |
|---|---|---|
| **Internett** | Selve nettverket: kabler, fiber, rutere, mobilmaster og avtaler om hvordan maskiner snakker sammen | Veinettet |
| **Web (WWW)** | Én av mange tjenester som kjører *oppå* internett: nettsider koblet sammen med lenker | Bilene som kjører på veiene |

E-post, Spotify-strømming, nettspill og Snapchat bruker også internett – men de er ikke web.
Weben er den delen som består av nettsider du åpner i en nettleser.

Weben ble funnet opp av **Tim Berners-Lee** i 1989–1991, mens han jobbet ved forskningssenteret CERN.
Han fant opp tre ting samtidig: HTML (språket), HTTP (måten filer sendes på) og nettleseren.
Den første nettsiden i verden var bare tekst og lenker. Ingen farger, ingen bilder.

---

## 1.4 Klient og tjener

Dette er det viktigste begrepsparet i kapitlet.

- **Klienten** er maskinen din. Den *spør* etter en nettside.
- **Tjeneren** (*serveren*) er en datamaskin som står påslått døgnet rundt et sted, og som *svarer*
  med filene den har liggende.

Tenk på det som å bestille mat:

```
Du (klienten)          "Kan jeg få forsiden til nrk.no?"     →     Kjøkkenet (tjeneren)
Du (klienten)     ←    "Værsågod, her er filene."                  Kjøkkenet (tjeneren)
```

En tjener er ikke en spesiell type maskin. Det er bare en datamaskin med en jobb: å ligge og vente på
spørsmål, og sende ut filer når noen spør. Datamaskinen din kan være en tjener – faktisk skal den bli det
i neste kapittel, når du starter Live Server.

---

## 1.5 Hva skjer når du skriver inn en adresse?

La oss ta det stegvis. Du skriver `www.elvebakken.vgs.no` og trykker Enter:

1. **Nettleseren finner ut hvor tjeneren er.**
   Adressen `elvebakken.vgs.no` er et navn mennesker kan huske. Maskiner bruker tall – en *IP-adresse*,
   for eksempel `93.184.216.34`. Nettleseren spør derfor en slags telefonkatalog for internett, kalt **DNS**,
   om å oversette navnet til et tall.

2. **Nettleseren sender en forespørsel.**
   Den sier, på et språk som heter **HTTP**: «send meg forsiden.»

3. **Tjeneren svarer.**
   Den sender tilbake en HTML-fil. Ren tekst.

4. **Nettleseren leser HTML-filen ovenfra og ned.**
   Underveis oppdager den at den trenger mer: et stilark (`style.css`), noen bilder, kanskje en
   skrifttype. For hver av dem sender den en ny forespørsel til tjeneren.

5. **Nettleseren tegner opp siden.**
   Den bygger siden av HTML-en, farger og plasserer alt etter CSS-en, og kjører eventuell JavaScript.

Alt dette tar vanligvis under ett sekund.

### Adressen, bit for bit

```
https://www.elvebakken.vgs.no/elevinfo/timeplan.html
└─┬──┘   └────────┬─────────┘ └──────────┬─────────┘
protokoll      domenenavn                sti til filen
```

- **Protokoll** – reglene for overføringen. `https` er `http` med kryptering, slik at ingen kan lese
  det som sendes underveis. Nesten alt bruker https i dag; hengelåsen i adressefeltet betyr dette.
- **Domenenavn** – navnet på tjeneren. Noen har betalt for å eie akkurat dette navnet.
- **Sti** – hvilken fil på tjeneren du vil ha. Legg merke til at den slutter på `.html`.

**Oppgave 1.2 – Les adressen**

Del opp disse adressene i protokoll, domenenavn og sti:

1. `https://www.nrk.no/sport/fotball.html`
2. `https://developer.mozilla.org/en-US/docs/Web/HTML`
3. `http://sondre-nettside.no/bilder/katt.png`

---

## 1.6 De tre språkene

En moderne nettside er bygget av tre språk som har hver sin jobb. Dette er den viktigste
oppdelingen i hele faget, og du kommer til å høre den mange ganger.

| Språk | Jobb | Sammenlikning med et hus | Filtype |
|---|---|---|---|
| **HTML** | Innhold og struktur | Selve bygget: vegger, rom, dører | `.html` |
| **CSS** | Utseende | Maling, tapet, møbler, farger | `.css` |
| **JavaScript** | Oppførsel | Lysbrytere, garasjeport, alarm | `.js` |

Poenget er at de skal holde seg til sitt. Man kan *jukse* og skrive utseende inn i HTML-en, men da
blir koden rotete og vanskelig å endre. En av tingene du skal lære i dette kurset er å holde
innhold og utseende adskilt.

I dette kurset jobber vi med **HTML og CSS**. JavaScript kommer senere i skoleåret.

### Samme innhold, ulikt utseende

Ta et eksempel. Denne HTML-en:

```html
<h1>Velkommen</h1>
<p>Dette er nettsiden min.</p>
```

gir en svart overskrift på hvit bakgrunn med standard skrifttype. Legger du til denne CSS-en:

```css
h1 {
  color: white;
  background-color: darkblue;
  font-family: Arial;
}
```

...så er *innholdet nøyaktig det samme*. Teksten «Velkommen» er der fortsatt. Men den ser helt
annerledes ut. HTML-en sier hva noe **er**, CSS-en sier hvordan det skal **se ut**.

---

## 1.7 Frontend og backend

To ord du vil møte hvis du leser om webutvikling:

- **Frontend** er alt som skjer i nettleseren din: HTML, CSS og JavaScript. Det du kan se og trykke på.
- **Backend** er alt som skjer på tjeneren: databaser, brukerkontoer, betalingsløsninger.

Når du logger inn på skolens plattform, er innloggingsskjemaet frontend. Sjekken av om passordet
faktisk er riktig skjer i backend – for hvis den sjekken lå i nettleseren din, kunne du bare
åpnet kildekoden og lest passordet.

I dette kurset lager vi frontend.

---

## 1.8 Prøv selv: endre en nettside

Du kan ikke endre nettsider for andre – men du kan endre din egen *kopi* av dem, den nettleseren
din nettopp har lastet ned. Dette er et av de mest nyttige verktøyene du kommer til å bruke i kurset.

**Oppgave 1.3 – Utviklerverktøyet**

1. Gå til forsiden på en avis.
2. Høyreklikk på hovedoverskriften og velg **Undersøk** / *Inspect*.
   (Hurtigtast: `F12`, eller `Cmd + Alt + I` på Mac.)
3. Et panel åpner seg. Til venstre ser du HTML-en, til høyre CSS-en for det du klikket på.
4. Dobbeltklikk på selve overskriftsteksten i HTML-panelet og skriv noe annet. Trykk Enter.
5. Ta skjermbilde.
6. Trykk `F5` for å laste siden på nytt.

**Tenk gjennom og skriv ned:** Hvorfor kom den opprinnelige overskriften tilbake da du oppdaterte?
Hva sier det om hvor endringen din egentlig ble gjort?

*(Og for ordens skyld: denne teknikken er også grunnen til at du aldri skal stole på et skjermbilde
av en nettside som «bevis» på noe.)*

---

## 1.9 Hva gjør denne koden?

Vi skal øve på denne oppgavetypen gjennom hele kurset, så vi begynner allerede nå. Du trenger ikke
kunne HTML for å svare – bare tenke logisk.

**Oppgave 1.4**

```html
<h1>Fjelltur</h1>
<img src="bilder/topp.jpg" alt="Utsikt fra toppen">
<p>Vi gikk opp på tre timer.</p>
<a href="https://ut.no">Finn flere turer</a>
```

Beskriv med egne ord hva som vises på skjermen. Hvor mange ting ser brukeren?
Hva skjer hvis brukeren klikker på det nederste?

**Oppgave 1.5 – Hva mangler her?**

```html
<h1>Fjelltur
<p>Vi gikk opp på tre timer.</p>
```

Sammenlikn med koden over. Hva er forskjellen? Hva tror du kan skje?

---

## 1.10 Oppsummering

- En nettside er en **tekstfil** som nettleseren henter og tegner opp.
- **Internett** er nettverket; **weben** er nettsidene som kjører på det.
- **Klienten** spør, **tjeneren** svarer.
- En **nettadresse** består av protokoll, domenenavn og sti.
- **DNS** oversetter domenenavn til IP-adresser; **HTTP(S)** er reglene for selve overføringen.
- **HTML** = innhold og struktur. **CSS** = utseende. **JavaScript** = oppførsel.
- **Frontend** skjer i nettleseren, **backend** på tjeneren.
- **Utviklerverktøyet** lar deg se og midlertidig endre en hvilken som helst nettside.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| Nettleser | Programmet som henter og viser fram nettsider (Chrome, Safari, Firefox, Edge) |
| Klient | Maskinen som ber om en nettside |
| Tjener / server | Maskinen som lagrer nettsiden og sender den ut |
| URL / nettadresse | Den fullstendige adressen til en fil på nettet |
| Domenenavn | Navnet på tjeneren, f.eks. `nrk.no` |
| IP-adresse | Tallet som identifiserer en maskin på internett |
| DNS | Systemet som oversetter domenenavn til IP-adresser |
| HTTP / HTTPS | Reglene for hvordan nettsider overføres. S = sikker (kryptert) |
| Kildekode | Selve teksten nettsiden er skrevet i |
| HTML | Språket som gir nettsiden innhold og struktur |
| CSS | Språket som gir nettsiden utseende |
| JavaScript | Språket som gir nettsiden oppførsel |
| Frontend | Delen som kjører i nettleseren |
| Backend | Delen som kjører på tjeneren |
| Utviklerverktøy | Nettleserens innebygde verktøy for å undersøke og feilsøke sider |

---

## Innlevering – kapittel 1

Lever i læringsloggen din:

1. Skjermbildet fra oppgave 1.3, med svaret på spørsmålet under.
2. Overskriften og lenken du fant i oppgave 1.1.
3. Svarene på oppgave 1.2, 1.4 og 1.5.
4. **Én setning:** forklar til en som ikke kan noe om data hva som skjer når man skriver inn en nettadresse.

---

**Neste kapittel:** Vi setter opp VS Code og Live Server, og lager din første egne nettside.

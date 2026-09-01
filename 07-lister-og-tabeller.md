# Kapittel 7 – Lister og tabeller

> **Mål for kapitlet**
> Når du er ferdig med dette kapitlet skal du kunne
> - lage punktlister, nummererte lister og lister inni lister
> - bygge en tabell med overskriftsrad og forstå hvordan rader og celler henger sammen
> - velge riktig element til riktig type innhold
> - bygge menyen din som en ordentlig liste

---

## 7.1 Innhold som hører sammen

Så langt har du jobbet med løpende tekst: overskrifter og avsnitt. Men mye innhold på nett er ikke
løpende tekst. Det er **oppramsinger** og **oppstillinger**:

- ingredienser i en oppskrift
- punkter i en meny
- resultater i en tabell
- en timeplan
- en trinnvis framgangsmåte

For alt dette finnes det egne elementer. Å bruke dem riktig er ikke pynt — det er å si hva innholdet
faktisk er, slik at både nettlesere, skjermlesere og søkemotorer forstår det.

---

## 7.2 Punktliste

En **uordnet liste** brukes når rekkefølgen ikke betyr noe:

```html
<ul>
    <li>Melk</li>
    <li>Brød</li>
    <li>Egg</li>
</ul>
```

- `<ul>` = *unordered list*, selve lista
- `<li>` = *list item*, ett punkt

Nettleseren tegner automatisk kuler foran punktene og rykker inn hele lista.

**Viktig regel:** direkte inni `<ul>` kan det bare stå `<li>`. Du kan ikke ha løs tekst eller et
avsnitt liggende rett inni lista. Men *inni* et `<li>` kan du ha nesten hva som helst — tekst, lenker,
bilder, til og med en ny liste.

---

## 7.3 Nummerert liste

En **ordnet liste** brukes når rekkefølgen betyr noe:

```html
<ol>
    <li>Åpne VS Code</li>
    <li>Lag en ny fil</li>
    <li>Skriv grunnstrukturen</li>
    <li>Lagre med Ctrl + S</li>
</ol>
```

`<ol>` = *ordered list*. Nettleseren nummererer punktene selv — **du skriver ikke tallene**. Setter du
inn et nytt steg i midten, nummereres alt om automatisk.

To nyttige attributter:

```html
<ol type="a">      <!-- a, b, c i stedet for 1, 2, 3 -->
<ol start="5">     <!-- begynner å telle på 5 -->
<ol reversed>      <!-- teller nedover -->
```

**Spørsmålet du stiller deg:** *ville det vært feil om punktene sto i en annen rekkefølge?*
Ja → `<ol>`. Nei → `<ul>`.

En handleliste er `<ul>`. En oppskrift er `<ol>`. En liste over interessene dine er `<ul>`.
Topp 10-lista over noe er `<ol>`.

**Oppgave 7.1 – Velg riktig listetype**

Skriv ned om du ville brukt `<ul>` eller `<ol>`, og begrunn:

1. Fagene du har på skolen
2. Framgangsmåten for å installere Live Server
3. De fem høyeste fjellene i Norge
4. Utstyr du trenger på en fjelltur
5. Rekkefølgen på oppgavene i en innlevering

---

## 7.4 Lister inni lister

Et `<li>` kan inneholde en hel ny liste. Da får du undernivåer:

```html
<ul>
    <li>Frukt
        <ul>
            <li>Eple</li>
            <li>Banan</li>
        </ul>
    </li>
    <li>Grønnsaker
        <ul>
            <li>Gulrot</li>
            <li>Brokkoli</li>
        </ul>
    </li>
</ul>
```

Legg nøye merke til hvor sluttagene står. Den indre `<ul>` ligger **inni** `<li>`-elementet, og
`</li>` kommer **etter** den indre lista er lukket.

Dette er stedet der nøstingen fra kapittel 3 virkelig settes på prøve. Rykk inn koden ordentlig, så
ser du strukturen. Roter du til innrykkene her, finner du aldri feilen.

**Oppgave 7.2 – Nøstet liste**

Lag en side `oppskrift.html` med:

- en `<h1>` med navnet på retten
- en `<h2>` «Ingredienser» med en `<ul>` som har minst to undernivåer
  (for eksempel «Til deigen» og «Til fyllet», hver med sine ingredienser)
- en `<h2>` «Slik gjør du» med en `<ol>` der rekkefølgen faktisk betyr noe
- minst ett `<li>` som inneholder både tekst og en lenke

Kjør `Shift + Alt + F` til slutt og se om innrykkene ser fornuftige ut.

---

## 7.5 Menyen din blir en liste

Husker du menyen fra kapittel 5?

```html
<p>
    <a href="index.html">Forsiden</a> |
    <a href="om-meg.html">Om meg</a> |
    <a href="bilder.html">Bilder</a>
</p>
```

Den fungerer, men den lyver litt: dette er ikke et avsnitt. Det er en **liste med lenker**. Og det er
faktisk slik profesjonelle nettsteder bygger menyer — åpne utviklerverktøyet på nesten hvilken som
helst nettside, så finner du en `<ul>` inni menyen.

```html
<ul>
    <li><a href="index.html">Forsiden</a></li>
    <li><a href="om-meg.html">Om meg</a></li>
    <li><a href="bilder.html">Bilder</a></li>
    <li><a href="oppskrift.html">Oppskrift</a></li>
</ul>
```

Nå ligger lenkene under hverandre med kuler foran. Det ser *mindre* ut som en meny enn før.

Det er helt som forventet. Strukturen er nå riktig, og i del 2 av kurset fjerner vi kulene med CSS
(`list-style: none`) og legger punktene på rad med Flexbox. Da får vi en ekte menylinje — bygget på et
element som forteller sannheten om hva innholdet er.

**Oppgave 7.3 – Bygg om menyen**

Bytt ut menyen med en `<ul>` på **alle** sidene dine. Test at alle lenkene fortsatt virker.

---

## 7.6 Beskrivelsesliste

Det finnes en tredje listetype som er mindre kjent, men veldig nyttig: lista over **begreper med
forklaringer**.

```html
<dl>
    <dt>HTML</dt>
    <dd>Språket som gir nettsiden innhold og struktur.</dd>

    <dt>CSS</dt>
    <dd>Språket som bestemmer hvordan nettsiden ser ut.</dd>

    <dt>Tjener</dt>
    <dd>Maskinen som lagrer nettsiden og sender den ut.</dd>
</dl>
```

- `<dl>` = *description list*
- `<dt>` = *description term*, begrepet
- `<dd>` = *description details*, forklaringen

Ett begrep kan ha flere forklaringer, og flere begreper kan dele én forklaring. Brukes til ordlister,
ofte stilte spørsmål, og nøkkelinformasjon som «Sted:», «Tid:», «Pris:».

**Oppgave 7.4 – Din egen ordliste**

Lag en side `ordliste.html` med en `<dl>` som forklarer minst åtte begreper du har lært til nå i
kurset. Bruk dine egne ord — ikke kopier fra kapitlene.

Denne siden bygger du videre på gjennom hele kurset. Den blir repetisjonsmaterialet ditt før prøven.

---

## 7.7 Tabeller

En tabell er for **data i to dimensjoner** — noe som har både rader og kolonner. En timeplan, en
resultatliste, en prisoversikt.

```html
<table>
    <tr>
        <th>Dag</th>
        <th>Fag</th>
        <th>Rom</th>
    </tr>
    <tr>
        <td>Mandag</td>
        <td>Teknologiforståelse</td>
        <td>B204</td>
    </tr>
    <tr>
        <td>Tirsdag</td>
        <td>Programmering</td>
        <td>B211</td>
    </tr>
</table>
```

Elementene:

| Element | Betyr | Merk |
|---|---|---|
| `<table>` | hele tabellen | |
| `<tr>` | *table row* – én rad | |
| `<th>` | *table header* – overskriftscelle | blir fet og midtstilt |
| `<td>` | *table data* – vanlig celle | |

### Tabeller bygges radvis

Dette er det som forvirrer flest: **du skriver ikke kolonner.** Du skriver rad for rad, og
kolonnene oppstår fordi hver rad har like mange celler.

Antall kolonner bestemmes altså av hvor mange `<td>` det er i én rad. Har én rad fire celler og de
andre tre, blir tabellen skjev.

### Overskriftsceller er ikke bare pynt

`<th>` blir fet og midtstilt av seg selv — men det er ikke poenget. Poenget er at cella sier
«jeg er overskriften for denne kolonnen».

En skjermleser bruker dette til å lese opp sammenhengen. I stedet for «B204» sier den
«Rom: B204». Uten `<th>` er en tabell nærmest ubrukelig for en blind bruker.

Har du overskrifter langs venstre side i stedet, sier du fra om det:

```html
<th scope="row">Mandag</th>
```

---

## 7.8 Struktur og tittel på tabellen

Større tabeller deles i seksjoner, og bør ha en tittel:

```html
<table>
    <caption>Timeplan uke 36</caption>
    <thead>
        <tr>
            <th>Dag</th>
            <th>Fag</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Mandag</td>
            <td>Teknologiforståelse</td>
        </tr>
        <tr>
            <td>Tirsdag</td>
            <td>Programmering</td>
        </tr>
    </tbody>
</table>
```

- `<caption>` er tabellens tittel. Den skal stå **først**, rett etter `<table>`, og leses opp av
  skjermlesere før innholdet.
- `<thead>` og `<tbody>` skiller overskriftsraden fra dataene.

Skal en celle strekke seg over flere kolonner eller rader:

```html
<td colspan="2">Går over to kolonner</td>
<td rowspan="3">Går over tre rader</td>
```

Bruk det med måte. Tabeller med mye sammenslåing blir raskt vanskelige både å kode og å lese.

**Oppgave 7.5 – Bygg en tabell**

Lag en side `timeplan.html` med en tabell over skoleuka di:

- `<caption>` med tittel
- `<thead>` med overskriftsrad
- `<tbody>` med minst fem rader
- riktig antall celler i hver rad
- minst én celle med `colspan` (for eksempel en dobbelttime eller lunsj)

Legg siden inn i menyen på alle sidene dine.

**Oppgave 7.6 – Utforsk en ekte tabell**

Finn en tabell på et ekte nettsted — sportsresultater, værvarsel, en prisliste. Åpne
utviklerverktøyet og se på koden. Bruker de `<th>`? Har de `<caption>`? Er tabellen bygget slik du
akkurat lærte?

Skriv to–tre setninger om hva du fant.

---

## 7.9 Tabeller er ikke for layout

Her kommer en advarsel med litt historie i seg.

På 1990- og tidlig 2000-tall fantes ikke CSS på den måten vi har det i dag. Skulle du plassere noe til
venstre og noe annet til høyre, var det bare én måte: du lagde en usynlig tabell og la innholdet i
hver sin celle. Hele nettsteder ble bygget som gigantiske nøstede tabeller.

Det fungerte visuelt, og det var forferdelig:

- koden ble uleselig
- sidene var umulige å endre
- skjermlesere leste dem opp som datatabeller, noe de ikke var
- de kunne ikke tilpasse seg mobilskjermer

I dag har vi Flexbox og Grid til akkurat dette, og du lærer begge deler i del 2.

> **Regelen:** bruk tabell når innholdet **er** en tabell — data med rader og kolonner. Aldri for å
> plassere ting på siden.

Du vil fortsatt møte tabell-layout ett sted: i **HTML-e-poster**. E-postprogrammer har henget etter i
tjue år, og der er tabeller fremdeles vanlig. Men det er unntaket som bekrefter regelen.

**Oppgave 7.7 – Riktig element til riktig innhold**

For hvert innhold: hvilket element ville du brukt, og hvorfor?

1. Ingrediensene i en oppskrift
2. Næringsinnholdet per 100 gram, med kolonner for energi, protein og fett
3. Trinnene i en framgangsmåte
4. En meny med fem sider
5. Forklaringer på ti fagbegreper
6. Et bilde til venstre og en tekst til høyre, side om side

*(Nummer 6 er en felle.)*

---

## 7.10 Oppsummering

- `<ul>` når rekkefølgen ikke betyr noe, `<ol>` når den gjør det. `<li>` er ett punkt.
- Du skriver ikke tallene i en `<ol>` — nettleseren teller selv.
- Direkte inni `<ul>` og `<ol>` kan det bare stå `<li>`.
- En liste kan ligge inni et `<li>` og gir da undernivåer. Pass på nøstingen.
- **Menyer bygges som lister** — det er det de er.
- `<dl>`, `<dt>` og `<dd>` er for begreper med forklaringer.
- Tabeller bygges **radvis**: `<tr>` er en rad, `<td>` en celle, `<th>` en overskriftscelle.
- `<caption>` gir tabellen en tittel, `<thead>` og `<tbody>` deler den i seksjoner.
- Tabeller er for **data**, aldri for å plassere ting på siden.

---

## Begreper du skal kunne

| Begrep | Betydning |
|---|---|
| `<ul>` | Uordnet liste – rekkefølgen betyr ikke noe |
| `<ol>` | Ordnet liste – rekkefølgen betyr noe |
| `<li>` | Ett punkt i en liste |
| Nøstet liste | Liste inni et listepunkt, gir undernivåer |
| `<dl>` / `<dt>` / `<dd>` | Beskrivelsesliste: begrep og forklaring |
| `<table>` | Tabellen |
| `<tr>` | Én rad i tabellen |
| `<td>` | En vanlig celle |
| `<th>` | Overskriftscelle – forteller hva kolonnen inneholder |
| `<caption>` | Tabellens tittel |
| `<thead>` / `<tbody>` | Seksjonene i en tabell |
| `colspan` / `rowspan` | Lar en celle strekke seg over flere kolonner eller rader |
| Tabell-layout | Utdatert praksis: å bruke tabeller til å plassere innhold |

---

## Innlevering – kapittel 7

Lever i læringsloggen din:

1. `oppskrift.html` med nøstede lister (oppgave 7.2).
2. `timeplan.html` med tabell, og skjermbilde (oppgave 7.5).
3. `ordliste.html` med minst åtte begreper (oppgave 7.4).
4. Skjermbilde som viser at menyen din nå er en `<ul>` på alle sider.
5. Svarene på oppgave 7.1 og 7.7, med begrunnelser.
6. Funnene fra oppgave 7.6.

**Sjekkliste før du går videre:**

- [ ] Menyen min er bygget som en liste på alle sidene
- [ ] Jeg vet når jeg skal bruke `<ul>` og når jeg skal bruke `<ol>`
- [ ] Den nøstede lista mi har riktig plasserte sluttager
- [ ] Tabellen min har `<th>` i overskriftsraden og en `<caption>`
- [ ] Alle radene i tabellen min har like mange celler
- [ ] Jeg vet hvorfor tabeller ikke skal brukes til å plassere innhold

---

**Neste kapittel:** Semantikk — vi setter navn på delene av siden, og du får svar på hvorfor `<div>`
ikke alltid er godt nok.

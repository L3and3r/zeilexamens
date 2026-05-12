# ZV Canisius Leerplatform

**Digitaal leerplatform voor Roeien en Zeilen bij ZV Canisius Nijmegen.**  
Werkt op telefoon, tablet en laptop — geen app nodig, geen account, gewoon de browser.

🌐 **Ga naar het platform:** https://l3and3r.github.io/Leerplatform-Zeeverkenners/

✏️ **Inhoud bewerken:** https://l3and3r.github.io/Leerplatform-Zeeverkenners/beheer.html

---

## Wat staat er in het platform?

Het platform bevat lesstof en oefeningen voor alle zeilsport-examens van de vereniging:

| Cursus | Modules | Oefenvragen | Examenvragen |
|---|---|---|---|
| 🚣 Roeien | 21 | 77 | 23 |
| ⛵ Zeilen Lichtmatroos | 5 | 15 | 10 |
| ⛵ Zeilen Rood (KB I) | 5 | 15 | 10 |
| ⛵ Zeilen Groen (KB II) | 5 | 16 | 10 |
| ⛵ Zeilen Kielboot III | 6 | 18 | 10 |

Elke module bestaat uit lesschermen die je één voor één doorloopt, gevolgd door een oefenquiz. Aan het einde van een cursus kun je een volledig oefenexamen doen.

---

## Hoe gebruik je het platform? (voor cursisten)

1. Open de link bovenaan deze pagina op je telefoon of laptop
2. Typ je naam in en kies je cursus
3. Werk modules door in je eigen tempo — je voortgang wordt onthouden
4. Oefen met de vragen aan het einde van elke module
5. Maak het oefenexamen als je denkt dat je er klaar voor bent

Je voortgang wordt opgeslagen in de browser van je eigen apparaat. Als je een ander apparaat gebruikt, begin je opnieuw.

---

## Hoe pas je inhoud aan? (voor instructeurs)

> Je hebt hiervoor geen technische kennis nodig. Alles werkt via de browser.

### Optie 1 — Beheerpagina (aanbevolen)

De makkelijkste manier. Open de beheerpagina:

**https://l3and3r.github.io/Leerplatform-Zeeverkenners/beheer.html**

Wat je kunt doen:
- Een vraag aanpassen (tekst, antwoorden, uitleg)
- Een vraag toevoegen of verwijderen
- Lestekst aanpassen

De eerste keer moet je een GitHub-token instellen (zie hieronder bij [Eerste keer instellen](#eerste-keer-instellen-voor-beheerders)).
Na het opslaan is de wijziging binnen 1–2 minuten live op het platform.

---

### Optie 2 — Direct via GitHub

Als je gewend bent om op GitHub te werken, kun je ook rechtstreeks de JSON-bestanden bewerken:

1. Ga naar dit GitHub-repository
2. Klik op `vragen.json` (voor vragen) of `modules.json` (voor lesinhoud)
3. Klik op het **potloodje** rechtsboven in het bestandsscherm
4. Pas de tekst aan
5. Klik onderaan op **Commit changes**
6. Na ~1 minuut is de wijziging live

Zie [INSTRUCTEURS.md](INSTRUCTEURS.md) voor een uitleg van de bestandsstructuur.

---

## Hoe voeg je een nieuw zeilvaartniveau toe?

Het platform is zo gebouwd dat je een nieuw niveau (bv. "Zeilen Lichtblauw") kunt toevoegen door alleen de JSON-bestanden uit te breiden — zonder ook maar één regel code aan te passen.

**Stap 1:** Voeg het niveau toe in `modules.json` onder de sleutel `"zeilen"`:

```json
"lichtblauw": {
  "naam": "Zeilen Lichtblauw",
  "icoon": "🔵",
  "kleur": "#1E90FF",
  "modules": [
    {
      "id": "lb-knopen",
      "sectie": "exam",
      "icoon": "⚓",
      "titel": "Knopen Lichtblauw",
      "beschrijving": "Korte omschrijving",
      "lessen": [
        { "titel": "De paalsteek", "inhoud": "<p>Uitleg hier.</p>" }
      ]
    }
  ]
}
```

**Stap 2:** Voeg de bijbehorende vragen toe in `vragen.json` onder `"zeilen"`:

```json
"lichtblauw": {
  "modules": {
    "lb-knopen": {
      "quiz": [
        {
          "vraag": "Welke knoop gebruik je om een lijn vast te zetten?",
          "opties": ["Paalsteek", "Achtknoop", "Mastworp", "Schootsteek"],
          "correct": 0,
          "uitleg": "De paalsteek maakt een vaste lus die niet dichttrekt."
        }
      ]
    }
  },
  "examen": []
}
```

De sleutelnaam (`"lichtblauw"`) moet in beide bestanden gelijk zijn. Het platform herkent het nieuwe niveau automatisch.

---

## Eerste keer instellen (voor beheerders)

Om wijzigingen via de beheerpagina op te slaan, heb je een **GitHub Personal Access Token** nodig. Dit is een soort wachtwoord dat de beheerpagina toegang geeft om bestanden in dit repository bij te werken.

### Token aanmaken

1. Log in op [github.com](https://github.com)
2. Klik rechtsboven op je profielfoto → **Settings**
3. Scroll helemaal naar beneden in het linkermenu → **Developer settings**
4. Klik op **Personal access tokens** → **Tokens (classic)**
5. Klik op **Generate new token (classic)**
6. Geef het een naam, bv. `beheer-leerplatform`
7. Kies een vervaldatum (bv. 1 jaar)
8. Vink aan: **repo** (het hele blok)
9. Klik **Generate token**
10. **Kopieer het token** — het begint met `ghp_` en je ziet het maar één keer

### Token invullen in de beheerpagina

1. Open de beheerpagina en log in
2. Klik op **⚙️ Instellingen** in het linkermenu
3. Plak het token in het veld **GitHub Personal Access Token**
4. Klik **Verbinding opslaan**

Het token en wachtwoord worden opgeslagen in de browser van jouw apparaat. Je hoeft dit maar één keer in te voeren.

### Medewerkers uitnodigen

Wil je dat andere instructeurs ook via de beheerpagina kunnen opslaan? Zij hebben allemaal hun eigen token nodig. Stuur ze de instructies hierboven.

Als je wil dat iemand ook bestanden direct via GitHub kan bewerken, ga dan naar:  
**Settings → Collaborators → Add people** in dit repository.

---

## Bestanden in dit repository

| Bestand | Wat staat erin | Aanpasbaar? |
|---|---|---|
| `leerplatform.html` | De volledige app (lesschermen, quizzen, examens) | Nee — alleen door ontwikkelaar |
| `vragen.json` | Alle quiz- en examenvragen | ✅ Ja — via beheerpagina of GitHub |
| `modules.json` | Alle lesinhoud (tekst per module) | ✅ Ja — via beheerpagina of GitHub |
| `beheer.html` | Beheerpagina voor instructeurs | Nee — alleen door ontwikkelaar |
| `index.html` | Doorverwijzing naar het platform | Nee |
| `.nojekyll` | Technisch bestandje voor GitHub Pages | Nee |
| `INSTRUCTEURS.md` | Uitgebreide handleiding voor instructeurs | — |

---

## Technische achtergrond (voor ontwikkelaars)

Het platform is een **single-page app** gebouwd als één HTML-bestand zonder externe frameworks of buildtools. De inhoud staat los van de code in twee JSON-bestanden die via `fetch()` worden geladen.

- **Hosting:** GitHub Pages (gratis, automatisch gedeployed bij elke commit op `main`)
- **Geen server nodig:** alles draait in de browser
- **Voortgang:** opgeslagen in `localStorage` per apparaat
- **SVG-afbeeldingen:** gegenereerd door JavaScript-functies in `leerplatform.html`; in de JSON opgeslagen als `{{svg:functienaam:arg}}` en bij het laden omgezet via `resolveSvgRef()`
- **Beheerpagina:** gebruikt de [GitHub Contents API](https://docs.github.com/en/rest/repos/contents) om `vragen.json` en `modules.json` direct te lezen en bij te werken zonder backend

### Lokaal ontwikkelen

```bash
# Clone het repository
git clone https://github.com/L3and3r/Leerplatform-Zeeverkenners.git
cd Leerplatform-Zeeverkenners

# Start een lokale webserver (fetch() werkt niet via file://)
npx serve .
# of: python -m http.server 8000
```

Open daarna `http://localhost:3000` (of poort 8000) in je browser.

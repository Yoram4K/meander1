# Meander1 — website van de VvE

De officiële website van Vereniging van Eigenaren Meander1, Van der Palmkade, Amsterdam.

**Live:** https://yoram4k.github.io/meander1

Een volledig statische site (gewone HTML/CSS/JavaScript, geen build-stap, geen server nodig) met tweetalige content (NL/EN), gehost via GitHub Pages.

## Inhoud

- [Mappenstructuur](#mappenstructuur)
- [Lokaal bekijken](#lokaal-bekijken)
- [Teksten aanpassen](#teksten-aanpassen)
- [Een pagina toevoegen](#een-pagina-toevoegen)
- [Foto's toevoegen](#fotos-toevoegen)
- [Nieuwsbrief bijwerken](#nieuwsbrief-bijwerken)
- [Het paaltje-formulier (Formspree)](#het-paaltje-formulier-formspree)
- [Publiceren](#publiceren)
- [Contact](#contact)

## Mappenstructuur

```
index.html          → de homepage (moet in de hoofdmap blijven staan,
                       anders werkt de site niet meer op de hoofd-URL)
pages/               → alle overige pagina's (over.html, wonen.html, contact.html, ...)
css/styles.css       → alle opmaak (kleuren, lettertypes, layout, responsive gedrag)
js/main.js           → alle interactiviteit: taalwisselaar (NL/EN), mobiel menu,
                       submenu's, het paaltje-formulier, scroll-animaties
uploads/             → foto's, logo's en andere afbeeldingen
```

Pagina's binnen `pages/` verwijzen onderling gewoon naar elkaar (bijv. `href="wonen.html"`). Vanuit `index.html` gaat een link naar een pagina altijd via `pages/...` (bijv. `href="pages/wonen.html"`), en vanuit een pagina terug naar de homepage via `href="../index.html"`.

## Lokaal bekijken

Omdat het puur statische bestanden zijn, kun je `index.html` los in een browser openen. Wil je alles precies zoals live zien (inclusief eventuele toekomstige uitbreidingen die een server nodig hebben), start dan een simpel lokaal servertje vanuit de hoofdmap:

```bash
python3 -m http.server 8000
```

en open <http://localhost:8000>.

## Teksten aanpassen

Elke vertaalbare tekst op de site heeft een `data-i18n="..."`-attribuut in de HTML, en de bijbehorende Nederlandse én Engelse tekst staat in het `dict`-object bovenaan `js/main.js`. Bijvoorbeeld:

```js
"hero.title": { nl: "De bocht<br>in de kade", en: "The bend<br>in the quay" },
```

**Om een tekst aan te passen:**
1. Zoek de key (bijv. `hero.title`) op in `js/main.js` en pas `nl`/`en` aan.
2. Pas ook de tekst tussen de HTML-tags aan op dezelfde plek (dit is de tekst die héél even zichtbaar is voordat het script inlaadt, en wat een zoekmachine leest) — zoek dezelfde `data-i18n="..."` in het bijbehorende `.html`-bestand.

Beide moeten hetzelfde zeggen; de site checkt dit niet automatisch.

**Om een nieuw stukje tekst toe te voegen:** verzin een unieke key (bijv. `wonen.nieuwekaart.titel`), zet die als `data-i18n` op het HTML-element, en voeg een regel toe aan het `dict`-object in `js/main.js` met de NL/EN-tekst.

## Een pagina toevoegen

1. Kopieer een bestaande pagina uit `pages/` die qua opzet lijkt op wat je wil (bijv. `pages/parqy.html` voor een pagina met tekst + factpanel + foto's).
2. Pas de `<title>`, de inhoud en de `data-i18n`-keys aan.
3. Voeg de bijbehorende teksten toe aan `js/main.js`.
4. Link ernaartoe vanaf een logische plek (bijv. een kaart op een hub-pagina zoals `wonen.html`, en/of het menu in de header als het een hoofdonderdeel is).

## Foto's toevoegen

Zet nieuwe afbeeldingen in de `uploads/`-map en verwijs ernaar met een relatief pad:

- Vanuit een pagina in `pages/`: `src="../uploads/jouw-foto.jpg"`
- Vanuit `index.html`: `src="uploads/jouw-foto.jpg"`

Gebruik bij voorkeur foto's die niet groter zijn dan een paar honderd KB (comprimeer grote foto's/screenshots eerst) zodat de site snel blijft laden, en zet `loading="lazy"` op de `<img>`-tag als de foto niet direct bovenaan de pagina staat.

## Nieuwsbrief bijwerken

De nieuwsbrieven staan op `pages/nieuws.html`. Voor een nieuwe nieuwsbrief:

1. Voeg een `<li>` toe aan de lijst, met de link naar de nieuwsbrief en de datum.
2. Voeg een bijbehorende `data-i18n`-key toe in `js/main.js` met de titel (bijv. "Meandernieuws juni 2026").

## Het paaltje-formulier (Formspree)

Het aanvraagformulier op `pages/paaltje.html` verstuurt via [Formspree](https://formspree.io) (endpoint staat in `js/main.js`, bovenaan bij `FORMSPREE_ENDPOINT`). Inzendingen zijn te bekijken door in te loggen op formspree.io met het account waarmee het formulier is aangemaakt. Verplichte velden en hun type worden dáár beheerd (onder "Validations"), niet in de code — zorg dat de daar ingestelde veldnamen exact overeenkomen met de `name`-attributen in het formulier in `paaltje.html`.

## Publiceren

De site staat op GitHub Pages en wordt automatisch bijgewerkt zodra er iets naar de `main`-branch wordt gepusht of gemerged. Een verandering is meestal binnen een minuut of wat zichtbaar op de live site.

## Contact

Vragen over deze website? Mail naar **webmaster@meander1.nl**.

# Lasse Geburtstagseite Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Umbau von `docs/lasse.html` (war Cleo, 9 Jahre) zu einer personalisierten Geburtstagsseite für Lasse (8 Jahre, Junge) mit drei interaktiven Sektionen: Kreuzfahrtschiff, Berge, Weltraum.

**Architecture:** Einzige Datei `docs/lasse.html` — reines HTML/CSS/JS ohne Build-Tools. Die Seite wird in 9 Tasks von oben nach unten umgeschrieben: zuerst CSS-Ergänzungen, dann HTML-Bereiche (Titel → Header → Sektionen → Footer), dann JavaScript.

**Tech Stack:** HTML5, CSS3 (Custom Properties, Flexbox), Vanilla JS, SVG, Google Fonts (Fredoka, Caveat, Nunito)

---

## Dateistruktur

| Datei | Aktion | Verantwortung |
|---|---|---|
| `docs/lasse.html` | Modify | Einzige Datei — alle Änderungen hier |

**Wichtige Zeilenbereiche (Referenz):**
- Z. 6: `<title>` Tag
- Z. 10–845: CSS Styles
- Z. 846: `<body>`
- Z. 852: Flugzeug-Banner Text "Happy Birthday, Cleo!"
- Z. 926–933: `.banner` Div mit eingebettetem Base64-Foto + `.banner-caption`
- Z. 934–947: `<h1>` und `.subtitle`
- Z. 949–1031: Sektion 1 (Körpergröße-Kurve)
- Z. 1033–1133: Sektion 2 (IQ-Kurve)
- Z. 1135–1158: Persönliche Botschaft (alt)
- Z. 1160–1177: Fakten-Box (IQ-Erklärung)
- Z. 1179–1181: Footer
- Z. 1185–1270: JS `data` Objekt
- Z. 1287–1320: JS `.seg` Click-Handler

---

## Task 1: Titel und CSS-Farben aktualisieren

**Files:**
- Modify: `docs/lasse.html` (Z. 6, Z. 11–22, Z. 448–456)

- [ ] **Schritt 1: Titel-Tag ändern**

Suche (Z. 6):
```html
<title>🎉 Herzlichen Glückwunsch! Die magische IQ-Kurve 🎂</title>
```
Ersetze durch:
```html
<title>🎉 Alles Gute, Lasse! Die große Reise 🚀</title>
```

- [ ] **Schritt 2: Neue CSS-Farb-Variablen hinzufügen**

Suche im `:root` Block (Z. 11–22) die Zeile `--shadow-sm: 3px 3px 0 var(--deep);` und füge danach ein:
```css
    --ocean: #006064;
    --ocean-light: #e0f7fa;
    --forest: #2e7d32;
    --forest-light: #e8f5e9;
    --night: #0d1b4b;
    --night-mid: #1a237e;
    --starlight: #90caf9;
```

- [ ] **Schritt 3: Neue Section-Header-Farben hinzufügen**

Suche (Z. 452–456):
```css
  .section-header--pink {
    background: var(--pink);
    color: white;
    transform: rotate(0.6deg);
  }
```
Füge danach ein:
```css
  .section-header--ocean {
    background: var(--ocean);
    color: white;
    transform: rotate(-0.5deg);
  }
  .section-header--forest {
    background: var(--forest);
    color: white;
    transform: rotate(0.4deg);
  }
  .section-header--night {
    background: var(--night-mid);
    color: white;
    transform: rotate(-0.3deg);
  }
  .section-header--ocean .sh-num,
  .section-header--forest .sh-num,
  .section-header--night .sh-num {
    color: var(--deep);
  }
```

- [ ] **Schritt 4: Commit**
```bash
git add docs/lasse.html
git commit -m "Update title and add color variables for Lasse page"
```

---

## Task 2: CSS für Personal Card und Sektion-Karten hinzufügen

**Files:**
- Modify: `docs/lasse.html` (CSS-Bereich, vor `@media`-Queries)

- [ ] **Schritt 1: Personal Card CSS einfügen**

Suche die Zeile `/* Persönliche Botschaft — wie eine Glückwunschkarte */` (ca. Z. 550) und füge **davor** ein:

```css
  /* Personal Card (ersetzt Foto-Banner) */
  .personal-card {
    max-width: 700px;
    margin: 0 auto 48px;
    background: rgba(255,255,255,0.08);
    border: 3px solid rgba(255,255,255,0.25);
    border-radius: 24px;
    padding: 28px 32px;
    position: relative;
  }
  .pc-from {
    font-family: 'Fredoka', sans-serif;
    font-size: 0.8rem;
    letter-spacing: 2px;
    color: var(--yellow);
    margin-bottom: 14px;
    text-transform: uppercase;
  }
  .pc-text {
    font-family: 'Nunito', sans-serif;
    font-size: clamp(0.95rem, 1.8vw, 1.08rem);
    line-height: 1.8;
    color: #e8f0fe;
    font-style: italic;
  }
  .pc-sig {
    text-align: right;
    font-family: 'Caveat', cursive;
    font-size: 1.3rem;
    color: var(--yellow);
    margin-top: 14px;
  }

  /* Ship scene */
  .chart-card--ship { background: linear-gradient(180deg, #87ceeb 0%, #b0e0e6 40%, #006994 40%, #004d73 100%); }
  .chart-card--ship::before { content: "🛳️ Klick aufs Schiff! ⚓"; }

  /* Mountain scene */
  .chart-card--mountain { background: linear-gradient(180deg, #b3d4f5 0%, #87b8e8 35%, #4a7c59 60%, #2e5e35 100%); }
  .chart-card--mountain::before { content: "🏔️ Klick auf einen Gipfel! ❄️"; }

  /* Space scene */
  .chart-card--space {
    background: radial-gradient(ellipse at 30% 40%, #1a237e 0%, #0d1b4b 50%, #050d1f 100%);
  }
  .chart-card--space::before { content: "🚀 Klick auf einen Planeten! ⭐"; color: #90caf9; }

```

- [ ] **Schritt 2: Header-Hintergrund für Nacht-Blau anpassen**

Suche den `header` CSS-Block (ca. Z. 82–87):
```css
  header {
    text-align: center;
    padding: 30px 20px 10px;
    position: relative;
  }
```
Ersetze durch:
```css
  header {
    text-align: center;
    padding: 30px 20px 10px;
    position: relative;
    background: linear-gradient(180deg, var(--night) 0%, #1a3a6b 70%, var(--cream) 100%);
    border-radius: 0 0 40px 40px;
    margin-bottom: 20px;
  }
```

- [ ] **Schritt 3: Commit**
```bash
git add docs/lasse.html
git commit -m "Add CSS for personal card and new section themes"
```

---

## Task 3: Flugzeug-Banner und Header-Text aktualisieren

**Files:**
- Modify: `docs/lasse.html` (Z. 852, Z. 926–947)

- [ ] **Schritt 1: Flugzeug-Banner Text ändern**

Suche (Z. 852):
```html
    <div class="banner-flag">Happy Birthday, Cleo! 🎉</div>
```
Ersetze durch:
```html
    <div class="banner-flag">Happy Birthday, Lasse! 🎉</div>
```

- [ ] **Schritt 2: Photo-Banner und Banner-Caption durch Personal Card ersetzen**

Suche (Z. 926–933) den gesamten Block:
```html
    <div class="banner">
      <div class="banner-img-wrap">
```
(Der Block endet mit `</div>` nach der `.banner-caption`-Zeile — er enthält das Base64-Foto und die Cleo-Grußzeile.)

Dieser gesamte Block — von `<div class="banner">` bis zum schließenden `</div>` (Z. 933) — wird ersetzt durch:

```html
    <div class="personal-card">
      <div class="pc-from">💌 Von Onkel Micha</div>
      <p class="pc-text">
        Lasse, heute wirst du 8 Jahre alt! Weißt du, was alle großen Entdecker gemeinsam haben?
        Sie lieben das Weite. Das Meer, das sich bis zum Horizont erstreckt. Die Berge, die so
        hoch sind, dass die Wolken <em>unter</em> dir liegen. Und den Nachthimmel, der flüstert:
        <em>»Da draußen gibt es noch so viel zu entdecken.«</em>
        <br><br>
        Genau das bist du, Lasse: ein Entdecker. Einer, der still ist und genau hinschaut.
        Der die Dinge wirklich sieht. Und das ist das Größte, was man sein kann. 🌍
      </p>
      <div class="pc-sig">— Dein Onkel Micha 🎂</div>
    </div>
```

- [ ] **Schritt 3: h1 und Subtitle aktualisieren**

Suche (Z. 934–947):
```html
    <h1>
      <span class="word w1">Die</span>
      <span class="word w2">magische</span>
      <span class="word w3">Kurve</span>
    </h1>
    <div class="opening-question">
      <span class="oq-emoji">✨</span>
      <p>Hast du schon mal von der <b>Normalverteilung</b> gehört?</p>
      <span class="oq-emoji">✨</span>
    </div>
    <p class="subtitle">
      Weißt du was Verrücktes? Wenn man bei ganz vielen Menschen <b>irgendetwas</b> misst — wie groß sie sind, wie schwer, oder wie gut sie Rätsel lösen — kommt fast immer die gleiche Form raus: eine <b>Glocken-Kurve</b>! 🔔 Lass uns zwei davon anschauen… 👇
    </p>
```
Ersetze durch:
```html
    <h1>
      <span class="word w1">Lasse,</span>
      <span class="word w2">der</span>
      <span class="word w3">Entdecker</span>
    </h1>
    <div class="opening-question">
      <span class="oq-emoji">🛳️</span>
      <p>Bereit für <b>drei große Abenteuer</b>?</p>
      <span class="oq-emoji">🚀</span>
    </div>
    <p class="subtitle">
      Das Meer, die Berge, die Sterne — drei Welten warten auf dich. Klick dich durch und entdecke die Geheimnisse, die sich dahinter verbergen… 👇
    </p>
```

- [ ] **Schritt 4: Im Browser prüfen**

Seite im Browser öffnen: `docs/lasse.html`. Prüfen:
- Flugzeug-Banner zeigt "Happy Birthday, Lasse! 🎉"
- Header zeigt dunklen Nacht-Blau-Hintergrund
- Personal Card sichtbar mit Onkel Micha Text
- Titel lautet "Lasse, der Entdecker"

- [ ] **Schritt 5: Commit**
```bash
git add docs/lasse.html
git commit -m "Update header, title and replace photo banner with personal card for Lasse"
```

---

## Task 4: Sektion 1 — Kreuzfahrtschiff (ersetzt Körpergröße-Sektion)

**Files:**
- Modify: `docs/lasse.html` (Z. 949–1031)

- [ ] **Schritt 1: Section Header ersetzen**

Suche (Z. 949–953):
```html
  <!-- ===== SECTION HEADER: KÖRPERGRÖSSE ===== -->
  <h2 class="section-header section-header--mint">
    <span class="sh-num">1</span>
    <span class="sh-text">Überleg mal, wie groß sind eigentlich Erwachsene? Sind alle gleich oder alle total unterschiedlich groß?</span>
  </h2>
```
Ersetze durch:
```html
  <!-- ===== SECTION HEADER: KREUZFAHRTSCHIFF ===== -->
  <h2 class="section-header section-header--ocean">
    <span class="sh-num">1</span>
    <span class="sh-text">Stell dir vor: du stehst auf dem Deck und siehst nichts als Meer… 🛳️</span>
  </h2>
```

- [ ] **Schritt 2: Körpergröße-Kurve durch Schiff-SVG ersetzen**

Suche `<!-- ===== KÖRPERGRÖSSE-KURVE ===== -->` (Z. 955) und ersetze den gesamten Block von `<div class="chart-card chart-card--intro">` bis zum schließenden `</div>` (Z. 1023) durch:

```html
  <!-- ===== KREUZFAHRTSCHIFF ===== -->
  <div class="chart-card chart-card--ship">
    <div class="chart-wrap">
      <svg id="ship-svg" viewBox="0 0 900 400" xmlns="http://www.w3.org/2000/svg" aria-label="Kreuzfahrtschiff auf dem Meer">
        <defs>
          <linearGradient id="sky-grad" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#87ceeb"/>
            <stop offset="100%" stop-color="#b0e0e6"/>
          </linearGradient>
          <linearGradient id="sea-grad" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#006994"/>
            <stop offset="100%" stop-color="#004d73"/>
          </linearGradient>
        </defs>

        <!-- Himmel -->
        <rect x="0" y="0" width="900" height="230" fill="url(#sky-grad)" rx="14"/>
        <!-- Meer -->
        <rect x="0" y="230" width="900" height="170" fill="url(#sea-grad)"/>
        <!-- Wellen -->
        <path d="M 0,245 Q 90,235 180,245 Q 270,255 360,245 Q 450,235 540,245 Q 630,255 720,245 Q 810,235 900,245" fill="none" stroke="rgba(255,255,255,0.35)" stroke-width="3"/>
        <path d="M 0,270 Q 90,260 180,270 Q 270,280 360,270 Q 450,260 540,270 Q 630,280 720,270 Q 810,260 900,270" fill="none" stroke="rgba(255,255,255,0.2)" stroke-width="2"/>

        <!-- Schiffsrumpf -->
        <path d="M 140,200 L 760,200 L 790,228 L 110,228 Z" fill="#1565c0" stroke="#0d47a1" stroke-width="3"/>
        <!-- Wasserlinie -->
        <path d="M 110,228 L 790,228" stroke="rgba(255,255,255,0.4)" stroke-width="2"/>

        <!-- Aufbau (Hauptdeck) -->
        <rect x="190" y="138" width="520" height="66" rx="6" fill="#2196f3" stroke="#0d47a1" stroke-width="3"/>

        <!-- Brücke (oberes Deck) -->
        <rect x="330" y="98" width="240" height="44" rx="5" fill="#1976d2" stroke="#0d47a1" stroke-width="2.5"/>

        <!-- Schornstein 1 (klickbar → Fact 3 Anker) -->
        <rect class="ship-part" data-ship-fact="3" x="385" y="60" width="42" height="42" rx="5"
              fill="#ff5722" stroke="#0d47a1" stroke-width="2.5" style="cursor:pointer"/>
        <text class="ship-part" data-ship-fact="3" x="406" y="87" text-anchor="middle"
              font-size="18" style="cursor:pointer;">🔥</text>

        <!-- Schornstein 2 -->
        <rect x="462" y="65" width="36" height="36" rx="4" fill="#ff5722" stroke="#0d47a1" stroke-width="2"/>

        <!-- Fensterreihe (klickbar → Fact 1 Größe) -->
        <rect class="ship-part" data-ship-fact="1" x="200" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>
        <rect class="ship-part" data-ship-fact="1" x="248" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>
        <rect class="ship-part" data-ship-fact="1" x="296" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>
        <rect class="ship-part" data-ship-fact="1" x="572" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>
        <rect class="ship-part" data-ship-fact="1" x="620" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>
        <rect class="ship-part" data-ship-fact="1" x="668" y="150" width="32" height="24" rx="4"
              fill="#e3f2fd" stroke="#0d47a1" stroke-width="2" style="cursor:pointer"/>

        <!-- Wasser-Emoji-Bereich (klickbar → Fact 2 Ozean) -->
        <text class="ship-part" data-ship-fact="2" x="60" y="265"
              font-size="32" style="cursor:pointer;" text-anchor="middle">🌊</text>
        <text class="ship-part" data-ship-fact="2" x="840" y="265"
              font-size="32" style="cursor:pointer;" text-anchor="middle">🌊</text>

        <!-- Anker (klickbar → Fact 4 Navigation) -->
        <text class="ship-part" data-ship-fact="4" x="155" y="218"
              font-size="26" style="cursor:pointer;" text-anchor="middle">⚓</text>

        <!-- Klick-Hinweis -->
        <text x="450" y="390" text-anchor="middle" font-size="13"
              fill="rgba(255,255,255,0.6)" font-family="Nunito, sans-serif">← Klick auf das Schiff! →</text>
      </svg>
    </div>
  </div>
```

- [ ] **Schritt 3: Panel ersetzen**

Suche (Z. 1025–1031):
```html
  <div class="panel" id="panelH">
    <div class="panel-placeholder" id="placeholderH">
      <span class="big-emoji">📏</span>
      <h3>Probier's mal aus!</h3>
      <p>Tippe auf einen bunten Abschnitt oben — dann erkläre ich dir, wer da drin steckt. 👆</p>
    </div>
  </div>
```
Ersetze durch:
```html
  <div class="panel" id="panelShip">
    <div class="panel-placeholder" id="placeholderShip">
      <span class="big-emoji">🛳️</span>
      <h3>Probier's mal aus!</h3>
      <p>Klick auf einen Teil des Schiffes — dann verrate ich dir ein Geheimnis! 👆</p>
    </div>
  </div>
```

- [ ] **Schritt 4: Im Browser prüfen**

Öffne `docs/lasse.html`. Prüfen: Türkiser Section-Header "1 — Stell dir vor…", Schiff-SVG sichtbar, Panel mit Platzhalter-Text.

- [ ] **Schritt 5: Commit**
```bash
git add docs/lasse.html
git commit -m "Replace height curve section with cruise ship section"
```

---

## Task 5: Sektion 2 — Berge (ersetzt IQ-Sektion)

**Files:**
- Modify: `docs/lasse.html` (Z. 1033–1133)

- [ ] **Schritt 1: Section Header ersetzen**

Suche (Z. 1033–1037):
```html
  <!-- ===== SECTION HEADER: IQ ===== -->
  <h2 class="section-header section-header--pink">
    <span class="sh-num">2</span>
    <span class="sh-text">Und jetzt die Frage: können alle Menschen gleich gut Rätsel lösen? 🤔</span>
  </h2>
```
Ersetze durch:
```html
  <!-- ===== SECTION HEADER: BERGE ===== -->
  <h2 class="section-header section-header--forest">
    <span class="sh-num">2</span>
    <span class="sh-text">Wenn du auf einem Gipfel stehst, liegen die Wolken unter dir… 🏔️</span>
  </h2>
```

- [ ] **Schritt 2: IQ-Kurve durch Bergpanorama ersetzen**

Suche `<!-- Klickbare Gaußkurve -->` (Z. 1039) und ersetze den gesamten Block von `<div class="chart-card">` bis zum schließenden `</div>` (Z. 1124) durch:

```html
  <!-- ===== BERGPANORAMA ===== -->
  <div class="chart-card chart-card--mountain">
    <div class="chart-wrap">
      <svg id="mountain-svg" viewBox="0 0 900 400" xmlns="http://www.w3.org/2000/svg" aria-label="Bergpanorama mit klickbaren Gipfeln">
        <defs>
          <linearGradient id="mtn-sky" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#b3d4f5"/>
            <stop offset="100%" stop-color="#87b8e8"/>
          </linearGradient>
        </defs>

        <!-- Himmel -->
        <rect x="0" y="0" width="900" height="300" fill="url(#mtn-sky)" rx="14"/>

        <!-- Hintergrund-Berge (klein, blau-grau) -->
        <polygon points="0,300 120,180 240,300" fill="#7a9ab0" opacity="0.5"/>
        <polygon points="700,300 820,170 900,300" fill="#7a9ab0" opacity="0.5"/>
        <polygon points="600,300 750,150 900,300" fill="#8aabb8" opacity="0.4"/>

        <!-- Wiese/Boden -->
        <rect x="0" y="300" width="900" height="100" fill="#2e5e35" rx="0"/>
        <!-- Gras -->
        <path d="M 0,300 Q 150,290 300,300 Q 450,310 600,300 Q 750,290 900,300" fill="#3a7040" stroke="none"/>

        <!-- Berg links: Mont Blanc (klickbar) -->
        <polygon class="mtn-peak" data-mtn-fact="montblanc"
                 points="60,300 220,95 380,300"
                 fill="#5d7a61" stroke="#2b1a4a" stroke-width="2" stroke-linejoin="round"
                 style="cursor:pointer"/>
        <!-- Schneekappe Mont Blanc -->
        <polygon points="220,95 185,155 255,155" fill="white" opacity="0.9"/>

        <!-- Berg Mitte: Mount Everest (klickbar, höchster) -->
        <polygon class="mtn-peak" data-mtn-fact="everest"
                 points="310,300 490,40 670,300"
                 fill="#4a6741" stroke="#2b1a4a" stroke-width="2.5" stroke-linejoin="round"
                 style="cursor:pointer"/>
        <!-- Schneekappe Everest -->
        <polygon points="490,40 450,105 530,105" fill="white" opacity="0.92"/>

        <!-- Berg rechts: Zugspitze (klickbar) -->
        <polygon class="mtn-peak" data-mtn-fact="zugspitze"
                 points="560,300 710,120 860,300"
                 fill="#567a5a" stroke="#2b1a4a" stroke-width="2" stroke-linejoin="round"
                 style="cursor:pointer"/>
        <!-- Schneekappe Zugspitze -->
        <polygon points="710,120 685,168 735,168" fill="white" opacity="0.88"/>

        <!-- Labels auf den Gipfeln -->
        <text x="220" y="88" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="13" font-weight="700" fill="#0d47a1">Mont Blanc ▲</text>
        <text x="490" y="32" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="14" font-weight="700" fill="#0d47a1">Mt. Everest ▲</text>
        <text x="710" y="113" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="13" font-weight="700" fill="#0d47a1">Zugspitze ▲</text>

        <!-- Klick-Hinweis -->
        <text x="450" y="390" text-anchor="middle" font-size="13"
              fill="rgba(255,255,255,0.7)" font-family="Nunito, sans-serif">← Klick auf einen Gipfel! →</text>
      </svg>
    </div>
  </div>
```

- [ ] **Schritt 3: IQ-Panel durch Berg-Panel ersetzen**

Suche den Block nach dem IQ-Chart (ungefähr Z. 1125–1133):
```html
  <div class="panel" id="panelIQ">
```
(Der genaue Inhalt kann variieren — es ist das `.panel` nach dem IQ-Chart.)

Ersetze den gesamten Block bis `</div>` durch:
```html
  <div class="panel" id="panelMountain">
    <div class="panel-placeholder" id="placeholderMountain">
      <span class="big-emoji">🏔️</span>
      <h3>Probier's mal aus!</h3>
      <p>Klick auf einen Berggipfel — ich verrate dir seine Geheimnisse! 👆</p>
    </div>
  </div>
```

- [ ] **Schritt 4: Im Browser prüfen**

Prüfen: Grüner Section-Header "2 — Wenn du auf einem Gipfel…", Bergpanorama mit drei Gipfeln, Panel mit Platzhalter.

- [ ] **Schritt 5: Commit**
```bash
git add docs/lasse.html
git commit -m "Replace IQ curve section with mountain panorama section"
```

---

## Task 6: Sektion 3 — Weltraum & Astronauten (ersetzt alte persönliche Botschaft)

**Files:**
- Modify: `docs/lasse.html` (Z. 1135–1158)

- [ ] **Schritt 1: Weltraum-Section-Header einfügen und alten pn-Block ersetzen**

Suche den gesamten Block (Z. 1135–1158):
```html
  <!-- Persönliche Botschaft an das Geburtstagskind -->
```
(bis zum schließenden `</div>` der persönlichen Botschaft, Z. 1158)

Ersetze durch:
```html
  <!-- ===== SECTION HEADER: WELTRAUM ===== -->
  <h2 class="section-header section-header--night">
    <span class="sh-num">3</span>
    <span class="sh-text">Manchmal, wenn du vom Schiff aus in den Himmel schaust — siehst du sie alle… 🚀</span>
  </h2>

  <!-- ===== WELTRAUM ===== -->
  <div class="chart-card chart-card--space">
    <div class="chart-wrap">
      <svg id="space-svg" viewBox="0 0 900 400" xmlns="http://www.w3.org/2000/svg" aria-label="Sternenhimmel mit Planeten">
        <defs>
          <radialGradient id="space-bg" cx="30%" cy="40%">
            <stop offset="0%" stop-color="#1a237e"/>
            <stop offset="50%" stop-color="#0d1b4b"/>
            <stop offset="100%" stop-color="#050d1f"/>
          </radialGradient>
          <radialGradient id="earth-grad" cx="35%" cy="35%">
            <stop offset="0%" stop-color="#81d4fa"/>
            <stop offset="100%" stop-color="#0277bd"/>
          </radialGradient>
          <radialGradient id="moon-grad" cx="35%" cy="35%">
            <stop offset="0%" stop-color="#ffcc80"/>
            <stop offset="100%" stop-color="#e65100"/>
          </radialGradient>
          <radialGradient id="sun-grad" cx="35%" cy="35%">
            <stop offset="0%" stop-color="#fff176"/>
            <stop offset="100%" stop-color="#f57f17"/>
          </radialGradient>
          <radialGradient id="mars-grad" cx="35%" cy="35%">
            <stop offset="0%" stop-color="#ef9a9a"/>
            <stop offset="100%" stop-color="#c62828"/>
          </radialGradient>
        </defs>

        <!-- Hintergrund -->
        <rect x="0" y="0" width="900" height="400" fill="url(#space-bg)" rx="14"/>

        <!-- Sterne -->
        <circle cx="50" cy="30" r="1.5" fill="white" opacity="0.9"/>
        <circle cx="120" cy="80" r="1" fill="white" opacity="0.7"/>
        <circle cx="200" cy="20" r="2" fill="#ffd447" opacity="0.8"/>
        <circle cx="300" cy="60" r="1.5" fill="white" opacity="0.6"/>
        <circle cx="400" cy="15" r="1" fill="white" opacity="0.9"/>
        <circle cx="500" cy="45" r="2" fill="#ffd447" opacity="0.7"/>
        <circle cx="600" cy="25" r="1.5" fill="white" opacity="0.8"/>
        <circle cx="700" cy="70" r="1" fill="white" opacity="0.6"/>
        <circle cx="800" cy="30" r="2" fill="white" opacity="0.9"/>
        <circle cx="860" cy="90" r="1.5" fill="#ffd447" opacity="0.7"/>
        <circle cx="150" cy="150" r="1" fill="white" opacity="0.5"/>
        <circle cx="750" cy="120" r="1.5" fill="white" opacity="0.6"/>
        <circle cx="650" cy="160" r="1" fill="white" opacity="0.8"/>
        <circle cx="50" cy="200" r="1.5" fill="white" opacity="0.4"/>
        <circle cx="850" cy="180" r="1" fill="white" opacity="0.7"/>

        <!-- Rakete (animiert) -->
        <g id="rocket-anim" style="animation: rocketFly 6s ease-in-out infinite;">
          <text x="680" y="120" font-size="36" transform="rotate(-45, 680, 120)">🚀</text>
        </g>

        <!-- Erde (klickbar) -->
        <circle class="planet" data-space-fact="earth"
                cx="160" cy="260" r="52"
                fill="url(#earth-grad)" stroke="rgba(255,255,255,0.3)" stroke-width="2"
                style="cursor:pointer; filter: drop-shadow(0 0 12px rgba(100,181,246,0.5));"/>
        <text x="160" y="325" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="14" font-weight="700" fill="#90caf9">Erde</text>

        <!-- Mond (klickbar) -->
        <circle class="planet" data-space-fact="moon"
                cx="320" cy="280" r="32"
                fill="url(#moon-grad)" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"
                style="cursor:pointer; filter: drop-shadow(0 0 8px rgba(255,152,0,0.4));"/>
        <text x="320" y="323" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="13" font-weight="700" fill="#ffcc80">Mond</text>

        <!-- Sonne (klickbar) -->
        <circle class="planet" data-space-fact="sun"
                cx="520" cy="240" r="68"
                fill="url(#sun-grad)" stroke="rgba(255,255,255,0.2)" stroke-width="2"
                style="cursor:pointer; filter: drop-shadow(0 0 20px rgba(255,235,59,0.6));"/>
        <text x="520" y="323" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="14" font-weight="700" fill="#fff176">Sonne</text>

        <!-- Mars (klickbar) -->
        <circle class="planet" data-space-fact="mars"
                cx="730" cy="270" r="40"
                fill="url(#mars-grad)" stroke="rgba(255,255,255,0.25)" stroke-width="1.5"
                style="cursor:pointer; filter: drop-shadow(0 0 10px rgba(244,67,54,0.4));"/>
        <text x="730" y="323" text-anchor="middle" font-family="Fredoka, sans-serif"
              font-size="13" font-weight="700" fill="#ef9a9a">Mars</text>

        <!-- Klick-Hinweis -->
        <text x="450" y="390" text-anchor="middle" font-size="13"
              fill="rgba(255,255,255,0.5)" font-family="Nunito, sans-serif">← Klick auf einen Planeten! →</text>
      </svg>
    </div>
  </div>

  <div class="panel" id="panelSpace">
    <div class="panel-placeholder" id="placeholderSpace">
      <span class="big-emoji">🌌</span>
      <h3>Probier's mal aus!</h3>
      <p>Klick auf einen Planeten — ich verrate dir sein Geheimnis! 👆</p>
    </div>
  </div>
```

- [ ] **Schritt 2: Raketen-Animation CSS hinzufügen**

Suche im CSS-Bereich den `@keyframes float` Block (ca. Z. 69):
```css
  @keyframes float {
```
Füge danach ein:
```css
  @keyframes rocketFly {
    0%, 100% { transform: translate(0, 0); }
    50%       { transform: translate(-30px, -20px); }
  }
```

- [ ] **Schritt 3: Im Browser prüfen**

Prüfen: Dunkelblauer Section-Header "3 — Manchmal, wenn du…", Sternenhimmel mit 4 Planeten, animierte Rakete, Panel mit Platzhalter.

- [ ] **Schritt 4: Commit**
```bash
git add docs/lasse.html
git commit -m "Add space/astronaut section as section 3"
```

---

## Task 7: Persönliche Botschaft und Footer aktualisieren

**Files:**
- Modify: `docs/lasse.html` (Z. 1160–1181)

- [ ] **Schritt 1: IQ-Fakten-Box durch Lasse-Botschaft ersetzen**

Suche den `<!-- Spaß-Fakten -->` Block (Z. 1160–1177):
```html
  <!-- Spaß-Fakten -->
  <div class="facts">
    <div class="fact">
      ...IQ-Inhalt...
    </div>
  </div>
```
Ersetze durch:
```html
  <!-- Abschluss-Botschaft für Lasse -->
  <div class="facts">
    <div class="fact">
      <span class="fact-emoji">🛳️</span>
      <h4>Das Meer ruft!</h4>
      <p>Wer auf einem Kreuzfahrtschiff fährt, sieht täglich neue Länder, neue Küsten, neue Horizonte. Jeder Sonnenaufgang auf dem Meer ist anders — kein einziger gleicht dem anderen. 🌅</p>
    </div>
    <div class="fact">
      <span class="fact-emoji">🏔️</span>
      <h4>Berge lehren Geduld</h4>
      <p>Ein Gipfel wartet. Er läuft nicht weg. Wer ruhig ist und einen Schritt nach dem anderen macht — der kommt irgendwann ganz oben an. So wie du, Lasse. 💚</p>
    </div>
    <div class="fact">
      <span class="fact-emoji">🚀</span>
      <h4>Die Sterne gehören dir</h4>
      <p>Jeder Astronaut hat mal als kleines Kind in den Nachthimmel geschaut und geträumt. Träume groß, Lasse — die Welt da draußen ist wirklich so riesig und wunderschön, wie du dir vorstellst. ⭐</p>
    </div>
  </div>
```

- [ ] **Schritt 2: Footer aktualisieren**

Suche (Z. 1179–1181):
```html
  <footer>
    Mit ganz viel <span class="heart">💖</span> zum Geburtstag gemacht!
  </footer>
```
Ersetze durch:
```html
  <footer>
    Mit ganz viel <span class="heart">💖</span> zum 8. Geburtstag für Lasse gemacht — von Onkel Micha 🎂
  </footer>
```

- [ ] **Schritt 3: Im Browser prüfen**

Prüfen: Drei neue Fact-Boxen (Meer, Berge, Sterne), korrekter Footer mit "Lasse" und "8. Geburtstag".

- [ ] **Schritt 4: Commit**
```bash
git add docs/lasse.html
git commit -m "Update personal message and footer for Lasse"
```

---

## Task 8: JavaScript — Click-Handler für alle drei Sektionen

**Files:**
- Modify: `docs/lasse.html` (Z. ~1186–1320)

- [ ] **Schritt 1: Altes `data`-Objekt und `.seg`-Handler entfernen**

Suche (Z. ~1185):
```javascript
  const data = {
    // ===== Körpergröße =====
    h1: {
```
Ersetze den gesamten Block von `const data = {` bis einschließlich der schließenden `});` des `.seg`-Handlers (Z. ~1320) durch den neuen Code aus Schritt 2.

- [ ] **Schritt 2: Neue Click-Handler einfügen**

```javascript
  // ===== Schiff-Facts =====
  const shipFacts = {
    1: {
      emoji: '🛳️ 🛳️ 🛳️',
      badge: 'Die Größe',
      color: '#006064',
      title: 'Riesenschiff!',
      text: 'Die "Symphony of the Seas" ist <b>362 Meter lang</b> — das sind fast <span class="percent">4 Fußballfelder</span> hintereinander! An Bord leben bis zu 8.000 Menschen gleichzeitig. Eine schwimmende Stadt!'
    },
    2: {
      emoji: '🌊 🐋 🌊',
      badge: 'Das Meer',
      color: '#0277bd',
      title: 'So viel Wasser!',
      text: 'Die Ozeane bedecken <b>71% der Erde</b> — mehr als die Hälfte unseres Planeten ist Wasser! Und der tiefste Punkt, der Marianengraben, ist <span class="percent">11 Kilometer tief</span>. Dort war noch fast kein Mensch.'
    },
    3: {
      emoji: '⚓ 🐘 ⚓',
      badge: 'Der Anker',
      color: '#ff5722',
      title: 'So schwer!',
      text: 'Ein Kreuzfahrtschiff-Anker wiegt bis zu <b>14 Tonnen</b> — so schwer wie <span class="percent">3 Elefanten</span>! Wenn das Schiff ankert, hält dieser Anker es fest, damit es nicht davontreibt.'
    },
    4: {
      emoji: '🧭 ⭐ 🧭',
      badge: 'Navigation',
      color: '#006064',
      title: 'Nach den Sternen!',
      text: 'Früher fuhren Seefahrer nach den Sternen — vor allem nach dem <b>Polarstern</b>, der immer genau nach Norden zeigt. Heute macht das ein Computer. Aber die Sterne zeigen <span class="percent">immer noch den Weg.</span>'
    }
  };

  // ===== Berg-Facts =====
  const mountainFacts = {
    montblanc: {
      emoji: '🇫🇷 🏔️ 🇮🇹',
      badge: 'Mont Blanc · 4.808 m',
      color: '#2e7d32',
      title: 'König der Alpen!',
      text: 'Der Mont Blanc ist <b>4.808 Meter hoch</b> — der höchste Berg der Alpen. Von oben siehst du gleichzeitig <span class="percent">Frankreich, Italien und die Schweiz</span>. Er liegt genau auf der Grenze!'
    },
    everest: {
      emoji: '🏔️ 🌏 🏔️',
      badge: 'Mount Everest · 8.849 m',
      color: '#1b5e20',
      title: 'Dach der Welt!',
      text: 'Der Mount Everest ist mit <b>8.849 Metern</b> der höchste Berg der Welt. Oben ist es so kalt wie eine Tiefkühltruhe — nur <span class="percent">viel kälter: bis −60°C</span>! Und die Luft ist so dünn, dass man kaum atmen kann.'
    },
    zugspitze: {
      emoji: '🇩🇪 🚡 🇩🇪',
      badge: 'Zugspitze · 2.962 m',
      color: '#388e3c',
      title: 'Deutschlands Dach!',
      text: 'Die Zugspitze ist mit <b>2.962 Metern</b> der höchste Berg Deutschlands. Mit der <span class="percent">Seilbahn kommt man in 10 Minuten</span> ganz nach oben — und schaut von dort auf Deutschland, Österreich und Italien hinunter!'
    }
  };

  // ===== Weltraum-Facts =====
  const spaceFacts = {
    earth: {
      emoji: '🌍 🌏 🌎',
      badge: 'Die Erde',
      color: '#0277bd',
      title: 'Unsere blaue Murmel!',
      text: 'Von oben sieht die Erde aus wie eine <b>blaue Murmel</b> im Dunkeln. Astronauten nennen das den "Overview Effect" — und werden dabei ganz still. Sie sagen: <span class="percent">Man sieht keine Grenzen zwischen Ländern</span>. Nur einen wunderschönen blauen Planeten.'
    },
    moon: {
      emoji: '🌙 🚀 🌙',
      badge: 'Der Mond · 384.000 km',
      color: '#e65100',
      title: 'Unser Nachbar!',
      text: 'Der Mond ist <b>384.000 Kilometer</b> von uns entfernt — das sind <span class="percent">10 Reisen rund um die Erde</span>! Apollo 11 brauchte 4 Tage, um dort anzukommen. Neil Armstrong war 1969 der erste Mensch auf dem Mond.'
    },
    sun: {
      emoji: '☀️ 🌞 ☀️',
      badge: 'Die Sonne · 150 Mio. km',
      color: '#f57f17',
      title: 'Riesenball aus Feuer!',
      text: 'Die Sonne ist so riesig, dass <b>1,3 Millionen Erden</b> hineinpassen würden! Ihr Licht braucht <span class="percent">8 Minuten</span>, um zu uns zu kommen. Wenn die Sonne plötzlich erlöschen würde, würden wir es erst 8 Minuten später merken.'
    },
    mars: {
      emoji: '🔴 🚀 👨‍🚀',
      badge: 'Der Mars',
      color: '#c62828',
      title: 'Das nächste Ziel!',
      text: 'Vielleicht landet der <b>erste Mensch auf dem Mars</b>, wenn Lasse erwachsen ist. Der Rote Planet hat Berge, die <span class="percent">dreimal so hoch wie der Everest</span> sind! Vielleicht sogar Lasse selbst? 🚀'
    }
  };

  // Hilfsfunktion: Panel befüllen (gleiche Funktion wie original fillPanel)
  function fillPanel(panelEl, d) {
    panelEl.innerHTML = `
      <div class="panel-content">
        <div class="emoji-row">${d.emoji}</div>
        <span class="panel-badge" style="background:${d.color}; color:white;">
          ${d.badge}
        </span>
        <h2>${d.title}</h2>
        <p>${d.text}</p>
      </div>
    `;
  }

  function scrollToPanel(panelEl) {
    const rect = panelEl.getBoundingClientRect();
    if (rect.top < 0 || rect.bottom > window.innerHeight) {
      panelEl.scrollIntoView({ behavior: 'smooth', block: 'center' });
    }
  }

  // Schiff-Handler
  document.querySelectorAll('.ship-part').forEach(el => {
    el.addEventListener('click', () => {
      const factId = el.dataset.shipFact;
      const d = shipFacts[factId];
      if (!d) return;
      document.querySelectorAll('.ship-part').forEach(p => p.style.opacity = '0.6');
      document.querySelectorAll(`[data-ship-fact="${factId}"]`).forEach(p => p.style.opacity = '1');
      const panel = document.getElementById('panelShip');
      fillPanel(panel, d);
      scrollToPanel(panel);
    });
    el.setAttribute('tabindex', '0');
    el.setAttribute('role', 'button');
    el.addEventListener('keydown', e => {
      if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); el.click(); }
    });
  });

  // Berg-Handler
  document.querySelectorAll('.mtn-peak').forEach(el => {
    el.addEventListener('click', () => {
      const factId = el.dataset.mtnFact;
      const d = mountainFacts[factId];
      if (!d) return;
      document.querySelectorAll('.mtn-peak').forEach(p => p.style.opacity = '0.5');
      el.style.opacity = '1';
      const panel = document.getElementById('panelMountain');
      fillPanel(panel, d);
      scrollToPanel(panel);
    });
    el.setAttribute('tabindex', '0');
    el.setAttribute('role', 'button');
    el.addEventListener('keydown', e => {
      if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); el.click(); }
    });
  });

  // Planeten-Handler
  document.querySelectorAll('.planet').forEach(el => {
    el.addEventListener('click', () => {
      const factId = el.dataset.spaceFact;
      const d = spaceFacts[factId];
      if (!d) return;
      document.querySelectorAll('.planet').forEach(p => p.style.opacity = '0.5');
      el.style.opacity = '1';
      const panel = document.getElementById('panelSpace');
      fillPanel(panel, d);
      scrollToPanel(panel);
    });
    el.setAttribute('tabindex', '0');
    el.setAttribute('role', 'button');
    el.addEventListener('keydown', e => {
      if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); el.click(); }
    });
  });
```

- [ ] **Schritt 3: Im Browser prüfen**

Öffne `docs/lasse.html` und teste alle Interaktionen:
- Klick auf Schiffsfenster → Panel zeigt Schiffs-Fact
- Klick auf 🌊 → Panel zeigt Ozean-Fact
- Klick auf Berggipfel → Panel zeigt Berg-Fact mit korrektem Badge
- Klick auf Planeten → Panel zeigt Weltraum-Fact
- Tastatur (Tab + Enter) funktioniert für alle klickbaren Elemente

- [ ] **Schritt 4: Commit**
```bash
git add docs/lasse.html
git commit -m "Add click handlers for ship, mountain and space sections"
```

---

## Task 9: Finale Überprüfung und Aufräumen

**Files:**
- Modify: `docs/lasse.html`

- [ ] **Schritt 1: Restliche "Cleo"-Referenzen suchen**

```bash
grep -n "Cleo\|cleo\|9. Geburtstag\|IQ\|Glocken-Kurve\|Normalverteilung" docs/lasse.html
```

Prüfen ob noch Reste vorhanden. Falls ja, entsprechend anpassen:
- "Cleo" → "Lasse"
- "9. Geburtstag" → "8. Geburtstag"
- IQ/Glocken/Normalverteilung Reste → entfernen oder ersetzen

- [ ] **Schritt 2: Vollständige Browser-Prüfung**

Öffne `docs/lasse.html` direkt im Browser. Checkliste:
- [ ] Flugzeug fliegt mit Banner "Happy Birthday, Lasse!" 🎉
- [ ] Feuerwerk startet beim Laden
- [ ] Musik-Button funktioniert
- [ ] Personal Card sichtbar mit Onkel Micha Text
- [ ] Titel: "Lasse, der Entdecker"
- [ ] Sektion 1 (türkis): Schiff-SVG, alle 4 Ship-Facts klickbar
- [ ] Sektion 2 (grün): Bergpanorama, alle 3 Berge klickbar
- [ ] Sektion 3 (dunkelblau): Sternenhimmel + Rakete, alle 4 Planeten klickbar
- [ ] Drei Fact-Boxen am Ende (Meer, Berge, Sterne)
- [ ] Footer: "zum 8. Geburtstag für Lasse … von Onkel Micha"
- [ ] Responsiv auf Mobilbreite (DevTools → 375px)

- [ ] **Schritt 3: `.gitignore` prüfen**

```bash
grep "superpowers" .gitignore
```
Falls `.superpowers/` nicht drin ist:
```bash
echo ".superpowers/" >> .gitignore
git add .gitignore
```

- [ ] **Schritt 4: Final-Commit**
```bash
git add docs/lasse.html .gitignore
git commit -m "Finalize Lasse birthday page - complete transformation from Cleo"
```

---

## Zusammenfassung der Änderungen

| Was | Alt (Cleo) | Neu (Lasse) |
|---|---|---|
| Titel | "Die magische IQ-Kurve" | "Die große Reise" |
| Banner | "Happy Birthday, Cleo!" | "Happy Birthday, Lasse!" |
| Foto-Banner | Base64-Foto (700KB) | Personal Card von Onkel Micha |
| Haupttitel | "Die magische Kurve" | "Lasse, der Entdecker" |
| Sektion 1 | Körpergröße-Kurve | Kreuzfahrtschiff-SVG |
| Sektion 2 | IQ-Kurve | Bergpanorama-SVG |
| Sektion 3 | (nicht vorhanden) | Weltraum/Planeten-SVG |
| Persönliche Botschaft | IQ-Erklärung | Meer/Berge/Sterne-Botschaft |
| Footer | "zum Geburtstag gemacht" | "zum 8. Geburtstag für Lasse … von Onkel Micha" |
| Farbschema | Pink/Lila dominant | Ozean/Grün/Nacht-Blau |

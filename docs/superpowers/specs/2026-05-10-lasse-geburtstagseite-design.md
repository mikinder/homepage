# Design: Lasse Geburtstagseite

**Datum:** 2026-05-10  
**Datei:** `docs/lasse.html`  
**Auftraggeber:** Onkel Micha  
**Empfänger:** Lasse, 8 Jahre

---

## Ziel

Umbau der bestehenden `lasse.html` (war für Cleo, 9 Jahre) zu einer personalisierten Geburtstagsseite für Lasse (8 Jahre, Junge). Lasse ist ein ruhiges, sensibles Kind das Kreuzfahrtschiffe, Astronauten und Berglandschaften liebt.

**Kein Foto vorhanden** — der Foto-Banner entfällt, wird durch eine persönliche Karte ersetzt.

---

## Konzept: "Die große Reise"

Alle drei Interessen werden zu einer zusammenhängenden Reise-Erzählung verknüpft. Ton: träumerisch, poetisch, staunend — wie ein Bilderbuch für ein sensibles Kind. Ruhigeres Farbschema als die Cleo-Seite (kein Pink/Lila-dominant).

---

## Seitenstruktur

### Header

- Flugzeug-Banner oben (wie Cleo-Seite, CSS/SVG bleibt): Text → **"Happy Birthday, Lasse! 🎉"**
- Titel: **"Lasse, der Entdecker"** mit Untertitel-Emojis 🛳️ 🏔️ 🚀
- **Persönliche Karte** (ersetzt Foto-Banner): dunkler Nacht-Blau-Hintergrund, handgeschriebener Stil

**Text der persönlichen Karte (von Onkel Micha):**
> "Lasse, heute wirst du 8 Jahre alt! Weißt du, was alle großen Entdecker gemeinsam haben? Sie lieben das Weite. Das Meer, das sich bis zum Horizont erstreckt. Die Berge, die so hoch sind, dass die Wolken *unter* dir liegen. Und den Nachthimmel, der flüstert: »Da draußen gibt es noch so viel zu entdecken.«
>
> Genau das bist du, Lasse: ein Entdecker. Einer, der still ist und genau hinschaut. Der die Dinge wirklich sieht. Und das ist das Größte, was man sein kann.
>
> Alles Gute zum Geburtstag, du kleiner Weltenentdecker. 🌍"
>
> — Dein Onkel Micha 🎂

---

### Sektion 1: Das Kreuzfahrtschiff 🛳️

- **Hintergrundfarbe:** Ozean-Türkis (`#e0f7fa` / `#006064`)
- **Illustration:** SVG-Kreuzfahrtschiff auf dem Meer (Himmel oben, Wasser unten)
- **Interaktion:** Klick auf verschiedene Schiffsbereiche (Fenster, Schornstein, Anker) deckt nacheinander Facts auf
- **Facts:**
  1. 🛳️ *Symphony of the Seas* ist 362m lang — fast 4 Fußballfelder hintereinander
  2. 🌊 71% der Erde ist Wasser — mehr als die Hälfte unseres Planeten
  3. ⚓ Ein Kreuzfahrtschiff-Anker wiegt bis zu 14 Tonnen — so schwer wie 3 Elefanten
  4. 🧭 Früher fuhren Seefahrer nach den Sternen — heute macht das ein Computer. Aber die Sterne zeigen immer noch den Weg.
- **Einleitungstext:** "Stell dir vor: du stehst auf dem Deck und siehst nichts als Meer…"

---

### Sektion 2: Die Berge 🏔️

- **Hintergrundfarbe:** Waldgrün (`#e8f5e9` / `#1b5e20`)
- **Illustration:** SVG-Bergpanorama mit Schnee-Gipfeln und blauem Himmel
- **Interaktion:** Klick auf Gipfel-Label zeigt Facts zum jeweiligen Berg
- **Berge & Facts:**
  1. 🏔️ **Mount Everest** (8.849m) — höchster Berg der Welt; oben bis zu −60°C
  2. 🇫🇷 **Mont Blanc** (4.808m) — höchster Berg der Alpen; von oben sieht man drei Länder
  3. 🇩🇪 **Zugspitze** (2.962m) — höchster Berg Deutschlands; mit Seilbahn in 10 Min. rauf
- **Einleitungstext:** "Wenn du auf einem Gipfel stehst, liegen die Wolken unter dir…"

---

### Sektion 3: Die Sterne & Astronauten 🚀

- **Hintergrundfarbe:** Nacht-Blau (`#1a237e` / `#0d1b4b`)
- **Illustration:** Sternenhimmel-Hintergrund mit animierter Rakete (CSS-Animation)
- **Interaktion:** Klick auf Planeten zeigt Facts
- **Planeten & Facts:**
  1. 🌍 **Erde** — der "Overview Effect": Astronauten werden ganz still, wenn sie die Erde von oben sehen
  2. 🌙 **Mond** — 384.000 km entfernt, Apollo 11 brauchte 4 Tage
  3. ☀️ **Sonne** — 1,3 Millionen Erden würden hineinpassen; ihr Licht braucht 8 Minuten
  4. 🔴 **Mars** — "Vielleicht landet dort der erste Mensch, wenn Lasse erwachsen ist — vielleicht sogar Lasse selbst? 🚀"
- **Einleitungstext:** "Manchmal, wenn du vom Schiff aus in den Himmel schaust — siehst du sie alle…"

---

### Footer

> "Mit ganz viel ❤️ zum 8. Geburtstag gemacht — von Onkel Micha 🎂"

---

## Farbschema

| Rolle | Farbe | Hex |
|---|---|---|
| Nacht-Blau (Header, Space) | Dunkelblau | `#0d1b4b` |
| Ozean (Schiff-Sektion) | Teal | `#006064` |
| Berge (Berg-Sektion) | Dunkelgrün | `#2e7d32` |
| Akzent/Sterne | Gold-Gelb | `#ffd447` |
| Akzent 2 | Warmes Orange | `#ff8c42` |
| Text/Outlines | Tief-Lila | `#2b1a4a` |

---

## Technische Vorgaben

- Reines HTML/CSS/JS — keine Frameworks, keine externen Requests außer Google Fonts
- Bestehende Komponenten wiederverwenden: Flugzeug-SVG (Text anpassen), Konfetti, Feuerwerk-Canvas, Musik-Button
- Alle `Cleo`-Referenzen ersetzen: Name, Alter (9→8), Pronomen (feminine→masculine in German)
- Kein Foto-Banner: `.banner` und `.banner-caption` Styles entfernen oder durch `.personal-card` ersetzen
- IQ-Kurven-Sektionen vollständig ersetzen durch die 3 neuen Sektionen
- Bestehende interaktive Muster (klickbare SVG-Segmente mit Popup) für neue Facts wiederverwenden
- Responsive: funktioniert auf Mobilgerät

---

## Was bleibt vom Original

- Flugzeug-SVG mit Banner (nur Text ändern)
- Konfetti-Hintergrund
- Feuerwerk-Canvas
- Musik-Button
- Allgemeine Layout-Struktur (`.wrap`, header, sections, footer)
- Schriftarten (Fredoka, Caveat, Nunito)
- Interaktionsmuster (klickbare SVG-Elemente → Popup/Fact-Box)

## Was fällt weg

- Foto-Banner (`.banner`, `.banner-caption`)
- Beide Glocken-Kurven (Körpergröße + IQ)
- Alle `Cleo`-spezifischen Texte
- IQ-Erklär-Kasten

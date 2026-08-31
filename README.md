# ÜKDO · Taktikhandbuch

Interaktives, **lokal lauffähiges** Taktikhandbuch der Einheit Überfallkommando.
Eine einzige Datei — `index.html` — ohne Build, ohne Server, ohne Abhängigkeiten.

## Starten

Datei doppelklicken oder in den Browser ziehen:

```
index.html
```

Das war es. Die Seite läuft vollständig offline; lediglich die beiden Schriften
(General Sans, Mulish) werden aus dem Netz nachgeladen — ohne Verbindung greift
automatisch die Systemschrift, das Layout bleibt unverändert.

Zum Verteilen im Intranet oder auf einem Stick genügt es, die Datei zu kopieren.

## Aufbau

| Bereich | Inhalt |
|---|---|
| **Grundprinzipien** | Zehn Sätze, die über allen einzelnen Taktiken stehen |
| **Grundtaktiken** | BuD · NIT · Messer-Intervention · Notzugriff |
| **Besonderheiten** | ÖPNV · Wasser — keine neuen Taktiken, nur örtlich bedingte Anpassungen |
| **Spezialisierungen** | MEDIC · Breaching · Sicherungsschütze |
| **Glossar** | Begriffe und Abkürzungen |
| **Wissenscheck** | Zehn Fragen quer durch das Handbuch |

Jedes Modul ist in Reiter gegliedert (Zweck & Schwelle, Grundsätze, Ablauf,
Rollen, Fehlerbilder) und schließt mit einem Merksatz.

## Bedienung

- **Suche** — Pille unten links im Kopfbereich; Taste <kbd>/</kbd> springt
  direkt hinein. Pfeiltasten wählen, <kbd>Enter</kbd> öffnet das Kapitel.
- **Lernfortschritt** — jedes Modul lässt sich als „durchgearbeitet“ markieren.
  Der Stand liegt im `localStorage` des jeweiligen Geräts, wird also nicht
  übertragen und nicht ausgewertet.
- **Drucken** — <kbd>Strg</kbd>+<kbd>P</kbd> gibt das Handbuch mit allen
  geöffneten Abschnitten als Papierfassung aus (Feld, Kopf und Suche entfallen).
- **Reduzierte Bewegung** — ist die Systemeinstellung gesetzt, entfallen
  Vorspann und Animationen vollständig.

## Inhalte pflegen

Alles Fachliche steht in **einem** Objekt am Anfang des `<script>`-Blocks:

```js
const HANDBUCH = { grundprinzipien: {...}, grundtaktiken: {...}, ... }
```

Layout, Suche, Fortschritt und Wissenscheck lesen ausschließlich daraus — ein
neuer Punkt, ein neues Modul oder eine geänderte Formulierung erfordert keine
zweite Stelle. Reiter-Typen: `text`, `list`, `warn` (rot), `steps`, `roles`.

## Einheitszeichen einsetzen

Ausgeliefert wird ein gezeichnetes Ersatzzeichen, damit die Datei ohne jedes
Beiwerk läuft. Für das echte Logo die Bilddatei als Data-URI einsetzen:

```bash
# erzeugt die Zeile zum Einfügen
printf 'const LOGO_SRC = "data:image/png;base64,%s";\n' "$(base64 -w0 logo.png)"
```

Die Zeile ersetzt im Skript `const LOGO_SRC = "";`. Das Logo erscheint dann im
Kopf **und** im Halbton-Feld des Heros. Ein Data-URI ist bewusst der empfohlene
Weg: ein per `file://` verlinktes Bild dürfte der Browser nicht in die
WebGL-Textur übernehmen.

## Technisches

- **Halbton-Feld** — WebGL2-Fragmentshader, der die Quelle einmal je Rasterzelle
  abtastet und einen weichen Punkt zeichnet; Größe folgt der Helligkeit, der
  Farbton einer Tintenrampe über das Bild. Der Zeiger dreht das Zeichen und legt
  es perspektivisch in die Neigung. Ohne WebGL2 bleibt das Papier leer, die
  Seite funktioniert unverändert.
- **Bewegung** — ein eigener Feder-Integrator mit festem Zeitschritt (1/60 s,
  Masse 1). Keine CSS-Keyframes: Vorspann, Eingänge, Menü und Zeigerreaktionen
  laufen über dieselben Federn.
- **Raster** — der Entwurf ist ein Rahmen von 1440 × 800. Ab 1024 px folgt die
  Wurzel-Schriftgröße dem Viewport (`min(1.111111vw, 2vh)`), darunter fließt das
  Layout in eine scrollende Spalte.

## Hinweis

Interne Ausbildungsunterlage. Die Inhalte fassen allgemein anerkannte
polizeitaktische Grundsätze zusammen und ersetzen **keine** Dienstvorschrift,
keinen Erlass und keine Einsatzbefehle. Verbindlich ist die jeweils aktuelle
Weisungslage der Einheit. Vor der Nutzung im Training durch die
Ausbildungsleitung freigeben und um einheitseigene Verfahren ergänzen.

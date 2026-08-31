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

## Farbkonzept

Grundfläche ist **Graphit, nicht Schwarz**: `#111418` (Carbon Black) hat einen
leichten Blaustich und liegt zwischen zwei weiteren Dunkelstufen — dadurch wirkt
die Seite tief statt plakativ. Reines Schwarz `#0A0A0A` kommt nur dort vor, wo
eine Fläche buchstäblich hinter allem liegt (Vorhänge, Menü, Fußzeile).

Leitfarbe ist **Gold** — das Zeichen der Einheit, und alles, was daran hängt:
Abzeichen im Kopf, das Zeichen im Halbton-Feld, Aktionsflächen, der Balken unter
der Überschrift. Die übrigen Farben stammen aus den drei Vorlagenpaletten und
haben je genau eine Aufgabe.

| Rolle | Farbe | Hex | Kontrast¹ |
|---|---|---|---|
| Grundfläche | Carbon Black | `#111418` | — |
| Karten, Pillen | Graphit (abgeleitet) | `#191E24` | — |
| tiefste Ebene | Jet Black | `#0A0A0A` | — |
| zweite Fläche | Sumi Ink | `#151515` | — |
| Überschriften | Mist White | `#EEF1EA` | 16.2 : 1 |
| Fließtext | Off White | `#F7F7F1` | 17.2 : 1 |
| Beschreibungen | Chrome Silver | `#C9D0D6` | 11.9 : 1 |
| Beiwerk | Stone Path | `#A8A49A` | 7.4 : 1 |
| Ränder, Nav-Punkte | Steel / Smoke Gray | `#707981` / `#6F7780` | 4.2 : 1 |
| **Marke, Aktion** | **Gold** | `#C9A961` | 8.2 : 1 |
| Gold als Schrift | Hellgold | `#E4C87E` | 11.3 : 1 |
| nur Fläche/Rand | Bronze | `#8A6E2F` | 3.8 : 1 |
| erledigt, richtig | Signal Green | `#25C77A` | 8.4 : 1 |
| Achtung, Fehlerbild | Electric Lime | `#C7FF2E` | 15.6 : 1 |
| Besonderheiten | Garden Green | `#75856A` | 5.0 : 1² |
| Spezialisierungen | Fresh Mint | `#B7F3D0` | 15.8 : 1² |
| Merksatz-Fläche | Moss Shadow | `#3F4B3A` | — |
| Schrift darauf | Ice Mint | `#E7FFF2` | 8.8 : 1³ |

¹ gegen die Grundfläche · ² dunkle Schrift auf der Farbfläche · ³ auf Moss Shadow.
WCAG AA verlangt 4.5 : 1 für Fließtext und 3 : 1 für große Schrift und
Bedienelemente — jede Text-Kombination oben liegt darüber.

**Nicht verwendet:** Moss Shadow und Bronze tragen bewusst keinen Text (2.0 bzw.
3.8 : 1 gegen die Grundfläche); sie sind reine Flächen- und Randfarben. Der
Balken unter der Überschrift liegt deshalb unterhalb der Grundlinie statt hinter
den Buchstaben — helle Schrift auf Gold käme nur auf 1.9 : 1.

**Zwei Grüntöne, zwei Bedeutungen:** Signal Green heißt „richtig / erledigt“,
Electric Lime heißt „Achtung / Fehlerbild“. Sie sind in Helligkeit und Sättigung
weit genug auseinander, und beide Zustände sind zusätzlich beschriftet — Farbe
allein trägt nirgends die Aussage.

Gedruckt kehrt sich alles um: weißes Papier, Sumi Ink als Schrift, Bronze statt
Gold, Bereichsfarben neutral. Ein dunkles Handbuch auf Papier wäre eine
Tonerkatastrophe.

Alle Werte stehen als CSS-Variablen im `:root`-Block ganz oben in `index.html`.

## Technisches

- **Halbton-Feld** — WebGL2-Fragmentshader, der die Quelle einmal je Rasterzelle
  abtastet und einen weichen Punkt zeichnet; Größe folgt der Helligkeit, der
  Farbton einer Goldrampe (Hellgold → Gold → Bronze) über das Bild. Der Zeiger dreht das Zeichen und legt
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

# Visitendokumentation Allgemeinchirurgie

Ein klickbarer Baustein-Generator für die chirurgische Visite: Befund per Fingertipp zusammenstellen, in die Zwischenablage kopieren, im KIS einfügen. Eine einzige HTML-Datei, keine Abhängigkeiten, kein Server, kein Internet nötig.

**➜ Online nutzen: [jeskokaiser.de/visitendoku](https://jeskokaiser.de/visitendoku)**

---

## Warum

Visitendokumentation ist repetitiv und trotzdem jedes Mal Tipparbeit. Dieses Werkzeug bildet die Standardformulierungen einer allgemeinchirurgischen Station als anklickbare Bausteine ab. Der Text baut sich live am unteren Fensterrand auf und lässt sich mit einem Klick übernehmen — inklusive fett und unterstrichener Kopfzeile.

## Aufbau der Ausgabe

```
Chirurgische Visite vom 21.07.2026
S: Patientin fühlt sich wohl. Wundschmerz NRS 3/10. Stoma fördert 450 ml/24 h, breiig.
O: Abdomen weich. Wundverhältnisse reizlos und trocken. Blake-Drainage rechts fördert
   30 ml/24 h, serös. Keine Beinödeme.
A: Z.n. laparoskopischer Sigmaresektion am 18.07.2026. Regelrechter postoperativer
   Verlauf, 3. postoperativer Tag.
P: Verbandswechsel morgen. Rücksprache mit dem Oberarzt/der Oberärztin. Entlassung bahnen.
Einliegendes Fremdmaterial:
- PVK (Unterarm li.) für Antibiose, Schmerztherapie
- Blake-Drainage (Oberbauch re.) für Sekretkontrolle
```

Struktur nach **SOAP** plus einliegendes Fremdmaterial. Umschaltbar zwischen **Fließtext** (ein Satz pro Sektion) und **Stichpunkten** (Aufzählung mit Zwischenüberschriften).

## Funktionen

| | |
|---|---|
| **236 Bausteine** | S 47 · O 63 · A 66 · P 60, in Themengruppen sortiert |
| **24 Fremdmaterialien** | Gefäßzugänge, Drainagen, Sonden / Katheter / Stomata |
| **Touch-optimiert** | Alle Schaltflächen mindestens 46 px, für Tablet und Stationsrechner |
| **Inline-Eingaben** | Zahlen und Werte direkt im Baustein: NRS, Fördermenge, VAC-Sog, POD, CRP … |
| **Dropdowns mit Freitext** | Drainagetyp, Sekretqualität, Sonographie-Region, Stuhlkonsistenz — Vorschläge klickbar, eigene Begriffe eintippbar |
| **Sich ausschließende Bausteine** | „Schmerzfrei" wirft „Wundschmerz NRS" automatisch raus — gilt für Schmerzen, Abdomen, Darmgeräusche, Temperatur, Stuhlgang/Stoma, Kostaufbau, Mobilisation, Verlauf, Wundheilung u. a. |
| **Mehrfaches Fremdmaterial** | Zwei PVK an verschiedenen Stellen? Beliebig viele Einträge je Material, jeder mit eigener Lokalisation und Indikation |
| **Materialspezifische Indikationen** | Am PVK stehen nur PVK-Indikationen zur Wahl, an der T-Drainage nur passende |
| **Anrede M / W** | Steuert alle personenbezogenen Formulierungen im Text |
| **Freitext je Sektion** | Individuelles ergänzen, wird an die geklickten Bausteine angehängt |
| **Editierbare Vorschau** | Direkt im Vorschaufeld schreiben; der Automatik-Aufbau pausiert dann sichtbar, bis „↻ Neu aufbauen" |
| **Rich-Text + Plain-Text** | Kopiert beide Formate gleichzeitig — das KIS nimmt, was es versteht |
| **Offline-Kopie** | Button lädt die Seite als eigenständige HTML-Datei herunter |

Tastatur: `⌘/Strg + Enter` kopiert.

## Nutzung

**Online** — [jeskokaiser.de/visitendoku](https://jeskokaiser.de/visitendoku) aufrufen.

**Offline** — auf der Seite oben rechts **⤓ Offline-Kopie** klicken. Die Datei landet als `visitendokumentation.html` im Download-Ordner und funktioniert per Doppelklick ohne Internet. Alternativ `visitendoku.html` aus diesem Repository herunterladen.

**Selbst hosten** — `visitendoku.html` auf einen beliebigen Webspace legen. Es gibt nichts zu bauen und nichts zu installieren; eine einzelne Datei von 50 kB genügt.

## Datenschutz

Es werden **keine Patientendaten gespeichert oder übertragen**. Die Seite enthält keinen Netzwerkzugriff, keine externen Skripte oder Schriftarten, kein Tracking und keine Speicherung in `localStorage` oder Cookies. Alle Eingaben leben ausschließlich im Arbeitsspeicher des Browsers und sind beim Neuladen weg. Als Offline-Kopie läuft die Datei vollständig ohne Verbindung.

## Bausteine anpassen

Der gesamte Inhalt steht als lesbare Datenstruktur oben im `<script>`-Block — keine Templating-Sprache, kein Build-Schritt. Datei im Editor öffnen, Zeile ändern, speichern, fertig.

### Baustein für S / O / A / P

```js
{l:"Wundschmerz NRS", o:"Wundschmerz NRS {n}/10", fields:[{k:"n", t:"num", ph:"0"}]}
```

| Schlüssel | Bedeutung |
|---|---|
| `l` | Beschriftung der Schaltfläche |
| `o` | Ausgabetext, ohne Satzzeichen am Ende |
| `x` | Name einer Ausschlussgruppe — Bausteine mit demselben `x` schließen sich gegenseitig aus |
| `fields` | Eingabefelder, per `{schlüssel}` im Ausgabetext platziert |

Platzhalter `{P}` wird zu `Patient` bzw. `Patientin`, je nach M/W-Schalter.

### Eingabefelder

| Schlüssel | Bedeutung |
|---|---|
| `k` | Feldname, entspricht `{k}` im Ausgabetext |
| `t` | `num` Zahl · `txt` Text · `list` Dropdown mit Freitext · `pills` anklickbare Auswahl |
| `opts` | Auswahlmöglichkeiten bei `list` und `pills` |
| `ph` | Platzhaltertext |
| `dv` | Vorgabewert, beim Aktivieren gesetzt |
| `opt` | `1` = darf leer bleiben und verschwindet dann aus dem Satz (sonst erscheint `___`) |
| `w` / `s` | breites bzw. mittleres Feld |

### Fremdmaterial

```js
{l:"PVK", o:"PVK", loc:L_PVK,
 ind:["Antibiose","Schmerztherapie","Volumentherapie","Medikamentengabe","Kontrastmittelgabe"]}
```

`loc` sind die anklickbaren Lokalisationen, `ind` die zu diesem Material passenden Indikationen. Häufig gebrauchte Lokalisationslisten liegen als Konstanten bereit (`L_PVK`, `L_ZVK`, `L_ABD`, `L_THX` …) und lassen sich wiederverwenden.

### Gemeinsame Auswahllisten

`DRAINTYP`, `SEKRET`, `STUHL`, `SPUELL`, `SONO`, `SEITE`, `DSLOK` — einmal ergänzt, wirken sie überall dort, wo die Liste eingebunden ist. Ein neuer Drainagetyp in `DRAINTYP` erscheint zum Beispiel sofort in allen Drainage-Dropdowns unter O und P.

## Technik

Eine Datei, 976 Zeilen, ~50 kB. Reines HTML, CSS und JavaScript ohne Framework, ohne Build-Prozess, ohne Abhängigkeiten. Helles und dunkles Design folgen der Systemeinstellung.

Beim Kopieren wird zuerst die asynchrone Clipboard-API versucht; scheitert sie — etwa weil die Datei über `file://` geöffnet wurde — greift ein `execCommand`-Fallback, der ebenfalls Rich-Text und reinen Text liefert. Klappt auch das nicht, markiert die Seite den Text, sodass `⌘/Strg + C` genügt.

## Haftungsausschluss

Dieses Werkzeug erzeugt Textvorschläge und ersetzt weder die ärztliche Beurteilung noch die Sorgfaltspflicht bei der Dokumentation. Jeder erzeugte Text ist vor der Übernahme in die Patientenakte auf Richtigkeit und Vollständigkeit zu prüfen. Die Bausteine bilden übliche Formulierungen ab und sind kein Standard und keine Leitlinie.

## Lizenz

MIT

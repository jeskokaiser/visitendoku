# Visitendokumentation Allgemeinchirurgie

Ein klickbarer Baustein-Generator für die chirurgische Visite: Befund per Fingertipp zusammenstellen, in die Zwischenablage kopieren, im KIS einfügen. Eine einzige HTML-Datei, keine Abhängigkeiten, kein Server, kein Internet nötig.

**➜ Online nutzen: [jeskokaiser.de/visitendoku](https://jeskokaiser.de/visitendoku)**

---

## Warum

Visitendokumentation ist repetitiv und trotzdem jedes Mal Tipparbeit. Dieses Werkzeug bildet die Standardformulierungen einer allgemeinchirurgischen Station als anklickbare Bausteine ab. Der Text baut sich live am unteren Fensterrand auf und lässt sich mit einem Klick übernehmen — inklusive fett und unterstrichener Kopfzeile.

## Aufbau der Ausgabe

```
Chirurgische Visite vom 29.07.2026
S: Patientin fühlt sich wohl. Rückläufige Wundschmerzen, NRS 3/10. Beinschmerzen links.
   Stoma fördert regelrecht, 450 ml/24 h, breiig.
O: Abdomen weich. Wundverhältnisse reizlos und trocken. Blake-Drainage rechts fördert
   30 ml/24 h, serös. Keine Beinödeme.
A: Regelrechter postoperativer Verlauf, 3. postoperativer Tag. Z.n. laparoskopischer
   Sigmaresektion am 18.07.2026.
P: Verbandswechsel morgen. Rücksprache mit dem Oberarzt/der Oberärztin. Entlassung bahnen.
Einliegendes Fremdmaterial:
- PVK (Unterarm li.) für Antibiose, Schmerztherapie
- Blake-Drainage (Oberbauch re.) für Sekretkontrolle
```

Struktur nach **SOAP** plus einliegendes Fremdmaterial. Umschaltbar zwischen **Fließtext** (ein Satz pro Sektion) und **Stichpunkten** (Aufzählung mit Zwischenüberschriften).

## Funktionen

| | |
|---|---|
| **87 Bausteine** | S 16 · O 25 · A 14 · P 21 · Fremdmaterial 11 — bewusst knapp gehalten, damit ein Blick zum Finden reicht |
| **Ein Klick = fertiger Satz** | 78 der 87 Bausteine liefern ohne jede Eingabe einen vollständigen Satz. „Abdomen" ergibt sofort „Abdomen weich.", „Antibiose" ergibt „Antibiotische Therapie fortführen." — Präparat und Datum sind Zugabe, keine Pflicht |
| **Touch-optimiert** | Alle Schaltflächen mindestens 36 px, Bausteine 46 px — keine Dropdowns, nur antippbare Flächen |
| **Inline-Eingaben** | Zahlen und Werte direkt im Baustein: NRS, Fördermenge, VAC-Sog, POD … |
| **Mehrfach-Einträge** | Bauchschmerz *und* Beinschmerz, zwei Drainagen, drei PVK: Bausteine wie Schmerzen, Drainage und alle Fremdmaterialien lassen sich beliebig oft anlegen, jeder mit eigener Lokalisation und eigenen Werten |
| **Mehrfachauswahl** | „V.a." sammelt kommagetrennt in einen Satz, „Problem" und „Organisation" erzeugen je einen eigenen Satz |
| **Freitext überall** | Auswahlreihen mit `sonstige`-Feld übernehmen eigene Begriffe und heben die Vorauswahl auf |
| **Sich ausschließende Bausteine** | „Schmerzfrei" wirft „Schmerzen" automatisch raus, „Stuhlgang" und „Stoma" schließen sich aus |
| **Materialspezifische Indikationen** | Am PVK stehen nur PVK-Indikationen zur Wahl, an der Drainage nur passende |
| **Planung am Material** | Jedes Fremdmaterial kann „wird heute entfernt", „wird morgen entfernt", „wird gewechselt" oder „bleibt vorerst belassen" tragen — je Eintrag einzeln |
| **„Kein Fremdmaterial"** | Ein Klick ersetzt die ganze Aufzählung durch „Kein einliegendes Fremdmaterial." und schließt sich mit allen Materialien gegenseitig aus |
| **Anrede M / W** | Steuert alle personenbezogenen Formulierungen im Text |
| **Freitext je Sektion** | Individuelles ergänzen, wird an die geklickten Bausteine angehängt |
| **Editierbare Vorschau** | Direkt im Vorschaufeld schreiben; der Automatik-Aufbau pausiert dann sichtbar, bis „↻ Neu aufbauen". Höhe über die Griffleiste ziehbar, Doppelklick setzt zurück |
| **Lückenwarnung** | Die wenigen Bausteine, die wirklich eine Angabe brauchen (etwa „Z.n. Operation"), zeigen `___`, farbig markiert und neben „Vorschau" gezählt — damit nichts Unfertiges in die Akte wandert. Reine Auswahllisten wie „V.a." bleiben stumm, bis etwas gewählt ist |
| **Schutz vor Datenverlust** | Da nichts gespeichert wird, fragt der Browser vor Reload oder Schließen nach, solange etwas erfasst ist |
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

Alle fünf Reiter — auch das Fremdmaterial — nutzen dasselbe Format.

### Baustein

```js
{l:"Abdomen", o:"Abdomen {z}", fields:[
  {k:"z", t:"pills", dv:"weich", opts:[
    ["weich","weich"], ["gebläht","gebläht und meteoristisch"], ["gespannt","gespannt"]]}]}
```

| Schlüssel | Bedeutung |
|---|---|
| `l` | Beschriftung der Schaltfläche |
| `o` | Ausgabetext mit `{feld}`-Platzhaltern, ohne Satzzeichen am Ende |
| `x` | Name einer Ausschlussgruppe — Bausteine mit demselben `x` schließen sich gegenseitig aus |
| `multi` | `1` = mehrfach anlegbar, es erscheint „+ weiterer Eintrag" |
| `fields` | Eingabefelder und Auswahlreihen |

Platzhalter `{P}` wird zu `Patient` bzw. `Patientin` — auch innerhalb von Auswahlwerten.

### Felder

| Schlüssel | Bedeutung |
|---|---|
| `k` | Feldname, entspricht `{k}` im Ausgabetext |
| `t` | `num` Zahl · `txt` Text · `pills` eine Auswahl · `pillsm` mehrere Auswahlen |
| `opts` | Auswahlmöglichkeiten: `"Text"` oder `["Beschriftung","Ausgabetext"]` — so bleibt die Schaltfläche kurz und der Satz vollständig |
| `lb` | Beschriftung der Auswahlreihe, z. B. `Seite` oder `Sekret` |
| `dv` | Vorauswahl beim Aktivieren — hiermit entsteht der Ein-Klick-Normalbefund |
| `opt` | `1` = darf leer bleiben und verschwindet dann aus dem Satz (sonst erscheint `___`) |
| `pre` / `suf` | Text vor bzw. hinter dem Wert, erscheint **nur** wenn das Feld gefüllt ist — so bleiben Zusätze wie `, NRS 4/10` optional |
| `frei` | `1` = zusätzliches Freitextfeld in der Auswahlreihe |
| `each` | `1` = bei `pillsm` wird jede Auswahl ein eigener Satz statt einer Aufzählung |
| `join` | Trennzeichen bei `pillsm`, Vorgabe `", "` |
| `ph` | Platzhaltertext im Eingabefeld |
| `w` / `s` | breites bzw. mittleres Eingabefeld |

### Mehrfach-Baustein

```js
{l:"PVK", multi:1, o:"PVK{loc}{ind}", fields:[
  {k:"loc", t:"pills",  lb:"Lokalisation", opt:1, pre:" (", suf:")", frei:1, opts:[…]},
  {k:"ind", t:"pillsm", lb:"Indikation",   opt:1, pre:" für ",       frei:1, opts:[…]}]}
```

→ `PVK (Unterarm li.) für Antibiose, Schmerztherapie`

### Gemeinsame Auswahllisten

`DRAIN`, `SEKRET`, `SEITE` sowie das fertige Feld `F_SEITE` — einmal ergänzt, wirken sie überall dort, wo sie eingebunden sind. Ein neuer Drainagetyp in `DRAIN` erscheint zum Beispiel sofort in allen Drainage-Auswahlreihen unter O und P.


## Haftungsausschluss

Dieses Werkzeug erzeugt Textvorschläge und ersetzt weder die ärztliche Beurteilung noch die Sorgfaltspflicht bei der Dokumentation. Jeder erzeugte Text ist vor der Übernahme in die Patientenakte auf Richtigkeit und Vollständigkeit zu prüfen. Die Bausteine bilden übliche Formulierungen ab und sind kein Standard und keine Leitlinie.

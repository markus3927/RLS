# Tagesablauf – RLS-Tracker

Persönliche App zur Erfassung des Tagesablaufs und der RLS-Schübe.
Idee, Konzept und Architektur: Markus Rufer · Technische Umsetzung mit Claude by Anthropic

---

## Was drin ist

| Datei | Zweck |
|---|---|
| `index.html` | die ganze App – eine einzige Datei, keine Abhängigkeiten |
| `manifest.webmanifest` | macht die App installierbar (Name, Farben, Icon) |
| `sw.js` | Service Worker, damit die App auch offline startet |
| `icon-192.png`, `icon-512.png` | App-Icon für Android und den Startbildschirm |
| `apple-touch-icon.png` | App-Icon für iPhone und iPad |
| `icon-96.png` | kleines Icon in Reserve |

Alle Pfade sind relativ (`./`). Die App läuft deshalb auch in einem Unterordner,
etwa `benutzername.github.io/tagesablauf/`.

---

## Auf GitHub stellen

**1. Repository anlegen**
Auf github.com → *New repository* → Name z. B. `tagesablauf` → *Public* → *Create*.

**2. Dateien hochladen (GitHub Desktop)**
Repository klonen, alle sieben Dateien in den Ordner kopieren, in GitHub Desktop
*Commit* schreiben und *Push origin*.

Der Weg über die Webseite (Dateien ins Browserfenster ziehen) funktioniert hier
ebenfalls, weil alle Dateien flach im Hauptordner liegen – keine Unterordner,
also auch kein Problem mit verschachtelten Strukturen.

**3. GitHub Pages einschalten**
Im Repository → *Settings* → *Pages* → unter *Branch* `main` und `/ (root)` wählen → *Save*.
Nach ein bis zwei Minuten ist die App erreichbar unter:

```
https://BENUTZERNAME.github.io/tagesablauf/
```

---

## Auf dem Handy installieren

**Android (Chrome)**
Seite öffnen → Menü ⋮ → *Zum Startbildschirm hinzufügen*. Die App startet danach
ohne Browserleiste, mit eigenem Icon.

**iPhone (Safari)**
Seite öffnen → Teilen-Symbol → *Zum Home-Bildschirm*.

Nach der Installation läuft die App auch ohne Internet.

---

## Wichtig: Daten und Sicherung

Die Daten liegen im `localStorage` des Browsers – auf dem Gerät, nicht in der Cloud.
Daraus folgen drei Dinge:

**Daten wandern nicht mit.** Wer die App zuerst als lokale Datei benutzt und später
über GitHub Pages öffnet, startet dort mit leerer Datenbank. Das ist kein Fehler,
sondern eine Sicherheitsregel des Browsers: jede Adresse hat ihren eigenen Speicher.

→ Vorher im Tab **Daten** auf *Sicherung exportieren*, danach unter der neuen Adresse
auf *Sicherung einlesen*. Dasselbe gilt beim Wechsel zwischen Handy und Computer.

**Browserdaten löschen löscht auch die App-Daten.** Ein „Verlauf und Websitedaten
löschen" nimmt alles mit.

**Darum: regelmässig exportieren.** Einmal pro Woche im Tab *Daten* auf
*Sicherung exportieren* – die JSON-Datei enthält alles: Phasen, Tagesablauf,
Mahlzeiten, Messungen, eigene Ergänzungen. Zusätzlich gibt es zwei CSV-Exporte
für die Auswertung in Excel.

---

## Die App aktualisieren

Neue `index.html` ins Repository legen und pushen. Falls die alte Version hängen
bleibt, in `sw.js` die Zeile `const CACHE = 'tagesablauf-v11';` auf eine neue Nummer
ändern – dann lädt der Service Worker beim nächsten Start alles frisch.

Die gespeicherten Daten bleiben bei einem Update erhalten, solange die Adresse
dieselbe bleibt.

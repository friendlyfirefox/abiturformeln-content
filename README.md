# Formeln – Inhaltsrepo

Dieses Repo liefert die Inhalte für die iPad-App **Formeln**. Die App liest beim Aktualisieren die Dateien dieses Repos.

| Datei | Inhalt |
|---|---|
| `index.json` | Manifest mit allen Formeln und Fächern (Inhalte direkt inline) |
| `version.json` | Versionsnummer, Hinweise und Download-/Repo-Links für die App |
| `README.md` | Diese Schema-Doku |
| `packs/` | Reserve für spätere Einzelpacks – die App liest derzeit alles aus `index.json` |

## Aufbau von `index.json`

```json
{
  "schemaVersion": 1,
  "version": "2026.11",
  "updatedAt": "JJJJ-MM-TT",
  "notes": "Kurztext für die App",
  "packs": [ ]
}
```

| Feld | Pflicht | Bedeutung |
|---|---|---|
| `schemaVersion` | ja | immer `1` |
| `version` | ja | Versionsstand der gesamten Inhalte, z. B. `2026.11` |
| `updatedAt` | ja | Datum der letzten Änderung als `JJJJ-MM-TT` |
| `notes` | nein | Kurztext, den die App anzeigt |
| `packs` | ja | Liste der Fächer-Packs |

### Pack (ein Fach)

| Feld | Pflicht | Bedeutung |
|---|---|---|
| `id` | ja | eindeutige ID in Kleinbuchstaben mit Bindestrichen, z. B. `mathematik-extra` |
| `title` | ja | Anzeigename, z. B. `Mathematik – Ergänzungen` |
| `subject` | nein | Fachname, z. B. `Mathematik` |
| `version` | nein | Versionsstand dieses Packs |
| `notes` | nein | Liste von Hinweisen: `{ "title": "…", "text": "…" }` |
| `categories` | nein | Eigene Kategorien des Packs (siehe unten) |
| `formulas` | ja | Liste der Formeln |

### Formel

**Pflichtfelder:** `id`, `title`, `category`, `topic`, `expression`

| Feld | Bedeutung |
|---|---|
| `id` | eindeutige ID, klein, mit Bindestrichen (z. B. `satz-pythagoras`). Eine ID, die einer eingebauten Formel entspricht, überschreibt diesen Eintrag |
| `title` | Anzeigename |
| `category` | Kategorie-ID (siehe unten) |
| `topic` | Themengruppe innerhalb der Kategorie – lieber ein passendes vorhandenes Topic weiterverwenden als ein fast gleiches neues erfinden |
| `expression` | die Formel als Unicode-Text, z. B. `f′(x) = …`, `√`, `∫`, `π`, `²`, `≤`, `⇒` |
| `explanation` | nein – Erklärung in einem Satz |
| `variables` | nein – Liste: `{ "symbol": "x", "name": "Stelle" }` |
| `example` | nein – ein Rechenbeispiel |
| `steps` | nein – Rechenschritte: `{ "title": "…", "detail": "…" }` |
| `details` | nein – Zusatzhinweise im selben Format |
| `calculator` | nein – Kennung eines eingebauten Rechners (unbekannte Kennungen werden ignoriert) |
| `keywords` | nein – Liste von Suchbegriffen |

## Kategorien

Eingebaute Kategorien: `basics`, `analysis`, `geometry`, `stochastics`.

Neue Kategorien einfach im Pack unter `categories` anlegen – `colorIndex` von 0 bis 7, `symbol` ist ein SF-Symbol (z. B. `atom`, `function`, `triangle`):

```json
"categories": [
  { "id": "physik", "title": "Physik", "subtitle": "Mechanik", "symbol": "atom", "colorIndex": 4 }
]
```

## Rechner-Kennungen

`pqFormel`, `abcFormel`, `scheitelpunkt`, `tangente`, `logarithmus`, `exponentiellesWachstum`, `zinseszins`, `vektorBetrag`, `abstandPunkte`, `skalarprodukt`, `kreuzprodukt`, `winkelZwischenVektoren`, `abstandPunktEbene`, `kreis`, `kugel`, `zylinder`, `kegel`, `pythagoras`, `sinussatz`, `dreiecksflaeche`, `binomialkoeffizient`, `bernoulli`, `binomialKumuliert`, `binomialErwartungswert`, `binomialStandardabweichung`, `bedingteWahrscheinlichkeit`, `zTransformation`, `potenzwert`, `wurzel`, `prozentwert`, `binomischeFormel`

## Inhalte ergänzen

1. In `index.json` die neue Formel ans Ende des passenden Packs einfügen (oder ein neues Pack unter `packs` anlegen).
2. Auf eindeutige IDs prüfen: keine doppelten IDs im Manifest und keine ID aus der eingebauten Liste (sonst wird diese überschrieben).
3. JSON validieren: `python3 -m json.tool index.json`
4. Änderung committen und auf `main` pushen (kleine Commits, Nachrichten auf Deutsch).
5. In der App auf **Inhalte aktualisieren** tippen.

## `version.json`

```json
{
  "version": "0.6",
  "notes": "Kurztext zur neuen Version",
  "downloadURL": "https://github.com/friendlyfirefox/Test/archive/refs/heads/main.zip",
  "repositoryURL": "https://github.com/friendlyfirefox/Test"
}
```

| Feld | Bedeutung |
|---|---|
| `version` | Versionsnummer der Inhalte, die die App zum Vergleichen anzeigt |
| `notes` | Hinweistext zur Version |
| `downloadURL` | ZIP-Download des Repos |
| `repositoryURL` | Link zum Repo |

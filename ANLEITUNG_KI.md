# Anleitung für ChatGPT / Claude: Wochen-Datei anlegen

Dieses Repository versorgt den **Vorsitzender-Generator** (`index.html`) mit dem Programm der
Leben-und-Dienst-Zusammenkunft. Der Generator lädt pro Woche **eine** Datei automatisch nach Datum.
Deine Aufgabe: für eine Woche genau diese eine Datei anlegen. **Ändere keine anderen Dateien.**

## 1. Ablauf

1. Den jw.org-Link öffnen, den du bekommen hast (z. B. `https://www.jw.org/finder?...&docid=...`
   oder `...&alias=meetings&date=JJJJMMTT`). Er führt zum Arbeitsheft-Artikel der Woche
   („Leben und Dienst: Arbeitsheft").
2. Den **Montag** der Woche bestimmen. Dateiname = `wochen/JJJJ-MM-TT.json` (Datum des Montags).
   Beispiel: Woche 9.–15. November 2026 → `wochen/2026-11-09.json`.
3. Programm übertragen (Abschnitt 3).
4. Für jeden Schulteil mit Quelle aus **th** („Werde ein besserer Leser und Lehrer") oder
   **lmd** („Liebt Menschen, macht sie zu Jüngern") die Lektion bzw. den Punkt auf wol.jw.org
   nachschlagen und den Rat **sinngemäß** zusammenfassen (Abschnitt 4).
5. Datei anlegen, gegen die Checkliste prüfen (Abschnitt 6), committen auf `main` mit der
   Nachricht `Woche JJJJ-MM-TT hinzugefügt`.

Hast du keinen Schreibzugriff: gib den vollständigen Dateiinhalt als reines JSON zurück
(kein Text davor oder danach). Der Nutzer fügt ihn im Generator ein.

## 2. Vorlage

`wochen/2026-11-09.json` ist die verbindliche Vorlage. Gleiche Struktur, gleiche Reihenfolge,
gleiche Feldnamen, gleiche Uhrzeiten.

## 3. Format

```json
{
  "meta": {
    "titel": "JEREMIA 51–52",
    "datum": "Do., 12.11.2026",
    "woche": "Woche 9.–15. November 2026",
    "montag": "2026-11-09",
    "erstellt_von": "Claude",
    "geprueft_von": "",
    "versammlung": "Tettnang",
    "saal": "Hauptsaal",
    "vorsitzender": "",
    "hilfsratgeber": ""
  },
  "items": [ ... 16 Einträge, siehe unten ... ]
}
```

| Feld | Regel |
|---|---|
| `titel` | Bibelabschnitt der Woche in GROSSBUCHSTABEN, Bereich mit Halbgeviertstrich „–" |
| `datum` | Donnerstag der Woche (Zusammenkunftstag Tettnang), Format `Do., TT.MM.JJJJ` |
| `woche` | `Woche T.–T. Monat JJJJ` |
| `montag` | Montag der Woche, `JJJJ-MM-TT`, **muss zum Dateinamen passen** |
| `erstellt_von` | Wer die Datei angelegt hat: `Claude` oder `ChatGPT` |
| `geprueft_von` | Beim Anlegen leer `""`. Setzt nur die **andere** KI bei der Zweitmeinung (Abschnitt 7) |
| `versammlung`, `saal` | immer `Tettnang`, `Hauptsaal` |
| `vorsitzender`, `hilfsratgeber` | immer leer `""` |

### Reihenfolge und Uhrzeiten der `items` (immer 16 Einträge)

| # | kind | time | Inhalt |
|---|---|---|---|
| 1 | song | 19:00 | `"title":"Lied NN"`, `"who":"Gebet: "` |
| 2 | note | 19:05 | Einleitende Worte, `"who":"1 Min"`, Felder wie Vorlage |
| 3 | band | – | `"band":"g"`, `"text":"Schätze aus Gottes Wort"` |
| 4 | part | 19:06 | Teil 1 (10 Min.) |
| 5 | part | 19:16 | Teil 2 „Nach geistigen Schätzen graben" (10 Min.) |
| 6 | part | 19:26 | Teil 3 Bibellesung (4 Min.) – mit `rat` |
| 7 | band | – | `"band":"b"`, `"text":"Uns im Dienst verbessern"` |
| 8 | part | 19:31 | Teil 4 – mit `rat` |
| 9 | part | 19:35 | Teil 5 – mit `rat` |
| 10 | part | 19:40 | Teil 6 – mit `rat` |
| 11 | band | – | `"band":"l"`, `"text":"Unser Leben als Christ"` |
| 12 | song | 19:47 | Zwischenlied, `"who":""` |
| 13 | part | 19:51 | Teil 7 (15 Min.), `rat: null` |
| 14 | part | 20:06 | Teil 8 Versammlungsbibelstudium (30 Min.), `rat: null` |
| 15 | note | 20:36 | Schlussworte, `"who":"3 Min"`, Felder wie Vorlage |
| 16 | song | 20:40 | `"title":"Lied NN"`, `"who":"Gebet: "` |

Hat eine Woche ausnahmsweise mehr oder weniger Teile, die Reihenfolge des Arbeitshefts übernehmen
und die Uhrzeiten sinnvoll anpassen.

### Teil (`part`)

```json
{"kind":"part","time":"19:26","title":"3. Bibellesung","sub":"4 Min. · Jer 52:6-20",
 "src":"th Lektion 5","who":"","rat":{ ... } }
```

- `title`: Nummer + Titel wie im Arbeitsheft.
- `sub`: Dauer, dann ` · ` und Bibelstellen, Art (`Von Haus zu Haus`, `Informell`) oder Vortragsthema
  (`Thema: …`).
- `src`: nur die Rat-Quelle(n) des Schulteils, z. B. `lmd Lektion 3, Punkt 4` oder
  `lmd Anhang A Pkt 21 · th Lektion 7`. Bei Teilen ohne th/lmd: `""`.
- `who`: immer `""` – Namen trägt der Nutzer selbst ein.

## 4. Rat (`rat`) – für Teil 3 bis 6

```json
"rat": {
  "lesson": "lmd Lektion 3 „Freundlichkeit“ – Punkt 4",
  "intro": "Punkt 4: Sei freundlich und respektvoll.",
  "bullets": ["Freundlicher Tonfall und respektvolle Wortwahl.",
              "So reden, dass sich niemand verletzt oder belehrt fühlt."],
  "zeit": "4 Min.",
  "feedback": ""
}
```

- `lesson`: Kürzel + Lektionsnummer + Lektionstitel in „…" + Punkt.
  th-Format: `th Lektion 5 – „Korrekt vorlesen“`.
- `intro`: der Kernpunkt in einem Satz (bei lmd: Überschrift des Punktes).
- `bullets`: 2–4 kurze Stichpunkte, **sinngemäß in eigenen Worten** – nie wörtlich abschreiben.
- `zeit`: Dauer des Teils. `feedback`: immer `""`.
- Hat ein Teil eine th- **und** eine lmd-Quelle (z. B. Vortrag mit Thema aus lmd Anhang A):
  `rat` beschreibt den **th**-Lehrpunkt, das lmd-Thema kommt als letzter Stichpunkt dazu.
- Teile ohne th/lmd-Quelle: `"rat": null`.

## 5. Was nicht erlaubt ist

- Nichts erfinden: keine Liedtitel raten (nur `Lied NN`, außer der Titel steht im Arbeitsheft),
  keine Bibelstellen, Themen oder Lektionstitel ergänzen, die nicht nachgeschlagen wurden.
- Keine Namen von Personen.
- Keine langen wörtlichen Zitate aus den Publikationen.
- Keine anderen Dateien ändern (insbesondere nicht `index.html` und nicht bestehende Wochen).

## 6. Checkliste vor dem Commit

- [ ] Gültiges JSON (keine Kommentare, keine abschließenden Kommas).
- [ ] Dateiname `wochen/JJJJ-MM-TT.json` = `meta.montag` = Montag der Woche.
- [ ] 16 Einträge in der Reihenfolge aus Abschnitt 3 (oder begründete Abweichung).
- [ ] Teile 3–6 haben `rat` mit `lesson`, `intro`, 2–4 `bullets`, `zeit`, `feedback: ""`.
- [ ] Alle `who` bei Teilen leer, `vorsitzender`/`hilfsratgeber` leer.
- [ ] `erstellt_von` gesetzt, `geprueft_von` leer (die Prüfung macht die andere KI).
- [ ] Rat-Texte in eigenen Worten.

Nach dem Push prüft eine GitHub-Action (`.github/workflows/pruefen.yml`) die Datei automatisch.
Ist sie rot, Fehlermeldung lesen und korrigieren.

## 7. Zweitmeinung (Review durch die andere KI)

Claude und ChatGPT arbeiten im selben Repository. Eine Woche gilt erst als fertig, wenn die
**jeweils andere** KI sie geprüft hat (Vier-Augen-Prinzip). Wer `erstellt_von` ist, prüft nicht
selbst.

**Auftrag lautet z. B.:** „Zweitmeinung zu `wochen/2026-11-16.json` nach ANLEITUNG_KI.md Abschnitt 7."

Ablauf:

1. Datei `wochen/JJJJ-MM-TT.json` lesen und den Arbeitsheft-Artikel der Woche auf jw.org /
   wol.jw.org selbst öffnen (nicht der Datei vertrauen).
2. Prüfen, Punkt für Punkt:
   - Bibelabschnitt, Datum, Woche, Montag korrekt?
   - Alle Teile vorhanden, Reihenfolge, Titel, Dauer, Bibelstellen, Lieder korrekt?
   - Für jeden `rat`: Lektion und Punkt nachschlagen – stimmt `lesson`, trifft `intro` den
     Kernpunkt, geben die `bullets` den Inhalt **sinngemäß und richtig** wieder? Nichts erfunden,
     nichts wörtlich abgeschrieben?
   - Format nach Abschnitt 3–6 eingehalten?
3. Protokoll anlegen: `reviews/JJJJ-MM-TT.md` nach diesem Muster:

   ```markdown
   # Zweitmeinung Woche JJJJ-MM-TT
   - Geprüft von: ChatGPT
   - Datum: TT.MM.JJJJ
   - Ergebnis: OK | KORRIGIERT | OFFEN

   | # | Fund | Gegenmaßnahme | Status |
   |---|------|---------------|--------|
   | 1 | Teil 5: Punkt 4 statt Punkt 3 eingetragen | lesson/intro/bullets auf Punkt 4 korrigiert | erledigt |
   ```

   Jeder Fund braucht eine konkrete Gegenmaßnahme. Keine Funde → Tabelle mit „keine Funde".
   Unsicheres als „unsicher" kennzeichnen statt zu raten.
4. Eindeutige Fehler direkt in der Wochen-Datei korrigieren. Bei Ermessensfragen (z. B. andere
   Formulierung eines Stichpunkts) **nicht** ändern, sondern nur im Protokoll vermerken (Status
   `OFFEN`) – der Nutzer entscheidet.
5. In der Wochen-Datei `meta.geprueft_von` auf den eigenen Namen setzen (`ChatGPT` bzw. `Claude`),
   nur wenn Ergebnis `OK` oder `KORRIGIERT`.
6. Ein Commit für beides: `Zweitmeinung Woche JJJJ-MM-TT: OK` bzw. `…: KORRIGIERT (n Funde)`.

Ohne Schreibzugriff: das Protokoll und ggf. die korrigierte Datei als Text zurückgeben.

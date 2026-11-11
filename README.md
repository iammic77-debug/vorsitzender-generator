# Vorsitzender-Generator · Leben & Dienst (Tettnang)

Plan und Arbeitsblatt für den Vorsitzenden der Leben-und-Dienst-Zusammenkunft.
Der Generator lädt die **aktuelle Woche automatisch** aus diesem Repository.

## Inhalt

| Datei | Zweck |
|---|---|
| `index.html` | Der Generator (Plan + Arbeitsblatt, Export Word/PDF) |
| `wochen/JJJJ-MM-TT.json` | Eine Datei pro Woche, benannt nach dem **Montag** der Woche |
| `ANLEITUNG_KI.md` | Auftrag + Format für ChatGPT / Claude: Wochen anlegen **und** gegenseitig prüfen |
| `reviews/JJJJ-MM-TT.md` | Protokoll der Zweitmeinung je Woche (Funde + Gegenmaßnahmen) |
| `.github/workflows/pruefen.yml` | Prüft neue Wochen-Dateien automatisch auf Fehler |

## Einmalig einrichten

1. Auf GitHub ein neues Repository **`vorsitzender-generator`** anlegen, Sichtbarkeit **Public**
   (die Dateien enthalten keine Namen – die trägst du nur im Browser ein).
2. Alle Dateien dieses Pakets hochladen („Add file" → „Upload files", Ordner hineinziehen).
3. **Settings → Pages → Build and deployment:** Source „Deploy from a branch",
   Branch `main`, Ordner `/ (root)` → Save.
4. Nach ca. 1 Minute läuft der Generator unter
   `https://iammic77-debug.github.io/vorsitzender-generator/` – als Lesezeichen speichern.

## Jede Woche

- Generator öffnen → die aktuelle Woche ist schon geladen. Mit ◀ ▶ blättern, „Heute" springt zurück.
- Namen, Notizen und Rückmeldungen direkt eintippen – sie bleiben pro Woche **in diesem Browser**
  gespeichert. ↺ verwirft deine Einträge und lädt das Original neu.
- Fehlt eine Woche: „🔗 Woche fehlt?" klicken, jw.org-Link einfügen, Auftrag kopieren und an
  ChatGPT oder Claude schicken. Die KI legt `wochen/JJJJ-MM-TT.json` an; danach Woche neu öffnen.

- **Zweitmeinung:** Oben steht neben der Woche „geprüft (ChatGPT)" oder „ungeprüft". Für eine
  Prüfung „🔎 Zweitmeinung" klicken, Auftrag kopieren und an die **andere** KI schicken
  (hat Claude die Woche angelegt → an ChatGPT, und umgekehrt). Ergebnis steht danach in
  `reviews/JJJJ-MM-TT.md`.

Kurzauftrag, falls du ihn selbst tippst:

> Lege im Repository iammic77-debug/vorsitzender-generator die Woche zu diesem Link an,
> genau nach ANLEITUNG_KI.md: &lt;jw.org-Link&gt;

## Hinweise

- Einträge im Browser sind **nicht** auf anderen Geräten sichtbar. Zum Mitnehmen „💾 Speichern"
  (JSON) bzw. Word/PDF exportieren.
- Der PDF-Export lädt beim ersten Mal eine kleine Bibliothek von cdnjs (Internet nötig).
- Rat-Texte sind sinngemäße Zusammenfassungen – bei Bedarf mit der Broschüre abgleichen.

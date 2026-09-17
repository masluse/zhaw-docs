---
typ: meta
tags:
  - meta
---

# Obsidian Best Practices

> [!tldr] In einem Satz
> Feste Ordner, feste Dateinamen, feste Properties, fester Notizaufbau – jede Information genau einmal, alles andere wird verlinkt.

## 1. Ordnerstruktur

```text
zhaw-docs/
├─ Start.md                 ← Dashboard, Einstiegspunkt
├─ Best Practices.md        ← diese Notiz
├─ Templates/               ← Vorlagen (Modul, Vorlesung, Zusammenfassung)
└─ HS26/                    ← ein Ordner pro Semester
   └─ INCO/                 ← ein Ordner pro Modul
      ├─ INCO.md            ← Modulnotiz (gleicher Name wie der Ordner)
      ├─ 2026-09-17.md      ← eine Notiz pro Vorlesung
      └─ Pictures/          ← Bilder nur dieses Moduls
```

Regeln:

- **Ordner = Struktur, Tags = Querschnitt.** Ordner bilden Semester/Modul ab, Tags alles andere.
- **Keine tieferen Ebenen.** Wer ein viertes Level braucht, braucht meist eine Verlinkung.
- **`Pictures/` pro Modul.** Ist in den Einstellungen als Anhang-Ordner hinterlegt (`./Pictures`), Bilder landen automatisch dort.

## 2. Dateinamen

| Notiztyp | Schema | Beispiel |
|----------|--------|----------|
| Modulnotiz | Modulkürzel | `INCO.md` |
| Vorlesung | `YYYY-MM-DD` | `2026-09-17.md` |
| Zusammenfassung | `Zusammenfassung <Thema>` | `Zusammenfassung Kanalcodierung.md` |
| Bild | sprechend, klein, mit `_` | `einfache_logische_operatoren_symbole.png` |

- Datum als Dateiname sortiert die Vorlesungen automatisch chronologisch – **das Thema steht in der Property `thema`**, nicht im Dateinamen.
- Umlaute und Leerzeichen in Dateinamen vermeiden (ausser bei Zusammenfassungen), das erspart Ärger bei Sync und Git.

## 3. Properties (Frontmatter)

Immer dieselben Schlüssel, immer in derselben Reihenfolge. `typ` ist das Steuerfeld – danach lässt sich später filtern.

**Modulnotiz**

```yaml
typ: modul
modul: INCO
semester: HS26
fach:
dozent:
moodle:
tags:
  - modul/inco
```

**Vorlesung**

```yaml
typ: vorlesung
modul: INCO
datum: 2026-09-17
thema: Digitaltechnik & Kombinatorische Logik
tags:
  - vorlesung
  - modul/inco
```

- `typ` kennt genau fünf Werte: `dashboard`, `meta`, `modul`, `vorlesung`, `zusammenfassung`.
- Leere Felder stehen lassen statt löschen – dann bleibt die Struktur sichtbar und wird später ausgefüllt.

## 4. Tags

- Nur zwei Familien: **`modul/<kürzel>`** und der **Notiztyp** (`vorlesung`, `zusammenfassung`, `moc`, `meta`).
- Keine Themen-Tags wie `#logik` – dafür gibt es Verlinkungen und die Suche.
- Tags immer klein und ohne Umlaute.

## 5. Aufbau einer Vorlesungsnotiz

> [!important] Die wichtigste Regel
> **Theorie oben, Übungen und Praktikum unten.** Beim Lernen liest man von oben nach unten: erst verstehen, dann anwenden. Beim Nachschlagen springt man über die Outline direkt in die Theorie.

```text
# Titel
> [!abstract] Kernaussage      ← 1–3 Sätze, das Wichtigste der Lektion

## Theorie                     ← alles vom Dozenten, in ### unterteilt
## Begriffe                    ← Notation, Definitionen, Abkürzungen

## Übungen                     ← eigene Rechnungen, Serien, Lösungswege
## Praktikum                   ← Auftrag, Vorgehen, Resultat, Abgabe

## Offene Fragen               ← was noch unklar ist
## Zu tun                      ← - [ ] Aufgaben, laufen im Dashboard auf
```

- Die vier oberen Blöcke sind **Wissen**, die vier unteren **Arbeit**. Diese Trennung nie vermischen.
- Innerhalb von `## Theorie` mit `###` und `####` gliedern, nicht mit fetten Absätzen – nur echte Überschriften erscheinen in der Outline (`Cmd/Ctrl + P` → *Outline*).
- Leere Abschnitte stehen lassen. Eine Vorlesung ohne Praktikum hat trotzdem die Überschrift – so sieht jede Notiz gleich aus.

## 6. Jede Information genau einmal

Die häufigste Unordnung entsteht durch Kopien. Darum gilt eine klare Zuständigkeit:

| Information | Gehört in |
|-------------|-----------|
| Dozent, Moodle-Link, Prüfungsform, Notengewicht | **Modulnotiz** |
| Themenübersicht des Semesters | **Modulnotiz** |
| Stoff einer einzelnen Lektion | **Vorlesungsnotiz** |
| Prüfungsrelevante Verdichtung über mehrere Lektionen | **Zusammenfassung** |

Statt kopieren: `[[INCO#Prüfung]]` verlinken oder mit `![[2026-09-17#Theorie]]` einbetten.

## 7. Schreiben in der Notiz

- **Callouts** sparsam und immer mit derselben Bedeutung:
  - `> [!abstract]` Kernaussage zuoberst
  - `> [!note]` Merkhilfe, Randbemerkung
  - `> [!important]` Prüfungsrelevant
  - `> [!question]` offene Frage
  - `> [!example]` durchgerechnetes Beispiel
  - `> [!warning]` typische Falle
- **Formeln** in LaTeX: `$x_0$` im Fliesstext, `$$ … $$` für abgesetzte Formeln.
- **Code und Notation** in Backticks: `` `Z = A & !B` ``. Mehrzeiliges in ```` ```text ```` – das erhält ASCII-Skizzen und Tabellen.
- **Tabellen** für alles Systematische: Wahrheitstabellen, Symbolübersichten, Begriffe.
- **Aufgaben** immer als `- [ ] Aufgabe (bis wann, welches Modul)` – sie sammeln sich automatisch im [[Start|Dashboard]].

## 8. Bilder

- Per Drag & Drop in die Notiz ziehen, sie landen automatisch in `Pictures/`.
- Immer mit Breitenangabe einbetten: `![[symbole.png|426]]` – sonst sprengt das Bild das Layout.
- Bild ersetzt keinen Text: darunter in ein bis zwei Sätzen festhalten, was darauf zu sehen ist. Ein Foto der Folie ist in vier Wochen wertlos, der Satz darunter nicht.

## 9. Automatisch statt manuell

- Notizlisten nie von Hand pflegen, sondern als Query:

  ````text
  ```query
  path:"HS26/INCO" -file:"INCO"
  ```
  ````

- Neue Notiz immer aus einer Vorlage: `Cmd/Ctrl + P` → *Templates: Insert template*.
- Vorlagen liegen in `Templates/`: [[Modul]] · [[Vorlesung]] · [[Zusammenfassung]].

## 10. Pflege

| Wann | Was |
|------|-----|
| Nach jeder Vorlesung | Kernaussage ausformulieren, offene Fragen notieren |
| Wöchentlich | Offene Fragen abarbeiten, Aufgaben im Dashboard durchgehen |
| Nach jedem Themenblock | Zusammenfassung schreiben – sie ist später der Prüfungsstoff |
| Semesterende | Semesterordner bleibt liegen, nichts löschen; neues Semester = neuer Ordner |

> [!warning] Anti-Patterns
> Rohe Folien-Abschriften ohne eigene Worte · dieselbe Information in zwei Notizen · Notizen ohne `typ` und `modul` · Bilder statt Text · Aufgaben, die nur im Kopf existieren.

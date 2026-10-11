# CLAUDE.md

Ein Spiel mit Vue 3, Vite, TypeScript und three.js. Jeder Push auf `main` deployt nach GitHub Pages.

## Befehle

```sh
npm run dev        # Dev-Server
npm run typecheck  # vue-tsc
npm run build      # Typecheck + Produktions-Build nach dist/
```

## PRDs

Bei „erstelle ein PRD": das PRD unter `docs/[slug-des-prd]/PRD.md` ablegen. Der Slug ist der Titel des PRD in Kleinbuchstaben mit Bindestrichen (z. B. `docs/spieler-steuerung/PRD.md`).

## Issues aus einem PRD

Bei „erstelle Issues aus einem PRD": die Issues unter `docs/[slug-des-prd]/ISSUES.md` ablegen, also im selben Ordner wie das zugehörige `PRD.md`. Es werden keine GitHub-Issues angelegt, solange das nicht ausdrücklich verlangt wird.

`ISSUES.md` ist in LLM-Sessions unterteilt. Jede Session ist ein Block, den eine einzelne Session von Anfang bis Ende abarbeitet, eingerahmt von Start- und Stop-Marker:

```md
<!-- SESSION 1 START -->
## Session 1: Kurzer Titel

**Ziel:** Was nach dieser Session funktioniert.
**Voraussetzungen:** Session-Nummern, die vorher abgeschlossen sein müssen, oder „keine".

### Issue 1.1: Titel
- [ ] Aufgabe
- [ ] Aufgabe

**Akzeptanzkriterien:** Woran man erkennt, dass das Issue fertig ist.

### Issue 1.2: Titel
...

**Abschluss:** `npm run build` läuft durch, Änderungen sind committet.
<!-- SESSION 1 STOP -->
```

Regeln für den Zuschnitt der Sessions:

- Eine Session bearbeitet nur den Block zwischen ihrem Start- und Stop-Marker und hört am Stop-Marker auf.
- Jede Session ist in sich abgeschlossen: Am Ende baut das Projekt, und das Ergebnis ist für sich prüfbar. Keine Session hinterlässt einen halb fertigen Zustand.
- Jede Session ist ohne Wissen aus anderen Sessions verständlich. Nötigen Kontext (betroffene Dateien, Entscheidungen aus dem PRD, Schnittstellen aus früheren Sessions) im Block selbst nennen oder auf den Abschnitt im `PRD.md` verweisen.
- Zusammengehörige Aufgaben, die dieselben Dateien anfassen, bleiben in einer Session. Unabhängige Themen werden getrennt.
- Eine Session ist so groß, dass sie bequem in ein Kontextfenster passt: lieber mehrere kleine Sessions als eine große. Richtwert sind zwei bis fünf Issues pro Session.
- Sessions sind in der Reihenfolge nummeriert, in der sie abgearbeitet werden; Abhängigkeiten stehen unter „Voraussetzungen".
- Erledigte Aufgaben werden in `ISSUES.md` abgehakt (`- [x]`).

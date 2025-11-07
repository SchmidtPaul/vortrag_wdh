# CLAUDE.md - Kontext für Claude Code Sessions

**Letzte Aktualisierung:** 07. November 2025

---

## Projekt-Übersicht

**Repository:** `SchmidtPaul/vortrag_wdh`
**Zweck:** Entwicklung einer Quarto-Präsentation für einen Workshop am 28. November 2024
**Thema:** Wiederholungen in landwirtschaftlichen Feldversuchen
**Erstellt mit:** Claude Code (vollständig)

---

## Aktuelle Projekt-Struktur

```
vortrag_wdh/
├── index.qmd                          # Hauptpräsentationsdatei (Quarto)
├── custom.css                         # Custom CSS für Farben und Arial-Font
├── brainstorming_wiederholungen.md   # Konzept und Gliederungsnotizen
├── README.md                          # Projekt-Dokumentation
├── _quarto.yml                        # Quarto Konfiguration (output-dir: _site)
├── .github/workflows/publish.yml     # GitHub Actions Workflow
└── CLAUDE.md                          # Diese Datei (Kontext für Sessions)
```

---

## Workflow & Deployment

### GitHub Actions Setup

**Branch:** `claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT`

**Workflow:**
1. Push zu Branch → GitHub Action triggert automatisch
2. Action installiert R, R-Pakete, Quarto
3. Rendert `index.qmd` zu HTML (in `_site/` Verzeichnis)
4. Deployed zu `gh-pages` Branch
5. GitHub Pages serviert von `gh-pages` Branch

**Live-URL:** https://schmidtpaul.github.io/vortrag_wdh/

**Build-Zeit:**
- Erster Build: ~2-3 Minuten (Pakete werden installiert und gecacht)
- Nachfolgende Builds: ~30-60 Sekunden (R Package Caching aktiv)

**Wichtig:**
- Immer zu Branch `claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT` pushen
- GitHub Pages ist auf "Deploy from branch: gh-pages" konfiguriert
- NICHT direkt zu `main` pushen (403 Fehler wegen Branch-Restrictions)

---

## R-Pakete

Folgende R-Pakete werden in der GitHub Action installiert (mit Caching):

```
rmarkdown, knitr, tidyverse, ggtext, desplot, agridat, broom, emmeans, scales
```

---

## Design & Styling

### Farbpalette (in Reihenfolge der Relevanz)

```css
#00923f  /* Grün - Primärfarbe, Behandlung A, Positive Elemente */
#bce2cc  /* Hellgrün - Behandlung B */
#e9ecef  /* Hellgrau - Hintergründe */
#495057  /* Dunkelgrau - Sektions-Hintergründe */
#4758ab  /* Blau - Behandlung C, Info-Elemente */
#ad0000  /* Rot - Problematische Designs, Warnungen */
#cba135  /* Gold - Akzente */
```

**Verwendung in Plots:**
- Gutes CRD Design: A=#00923f, B=#bce2cc, C=#4758ab
- Schlechtes Design: Gleiche Farben, aber Titel in Rot (#ad0000)
- Split-Plot Problem: A1=#00923f (Nord), A2=#ad0000 (Süd) - zeigt Problem visuell

### Schriftart

**Überall Arial:**
- Quarto CSS: `custom.css` definiert Arial für alle `.reveal` Elemente
- R-Plots: Alle `theme()` Aufrufe haben `family = "Arial"`

---

## Präsentations-Inhalt

### Struktur (basierend auf `brainstorming_wiederholungen.md`)

1. **Agenda & Einleitung**

2. **Sektion 1: Echte/Unabhängige Wiederholungen**
   - Grundprinzip: Parzelle als Versuchseinheit
   - Randomisation ist entscheidend
   - Visualisierung: Gutes vs. schlechtes Design
   - Kernaussage

3. **Sektion 2: Pseudo-Wiederholungen**
   - Definition: Mehrfache Messungen innerhalb einer Parzelle
   - Beispiel 1: Meterstab-Messungen (10 Parzellen × 3 Messungen)
   - Beispiel 2: Moderne Sensortechnik
   - Intuitive Analogie: 3 Blutabnahmen bei 3 Personen vs. 1 Person
   - Kernaussage

4. **Sektion 3: Die Grauzone - Pseudo-Split-Plot**
   - Typisches Problem: Unvollständige Randomisation
   - Konkretes Beispiel: Nord/Süd-Split mit Visualisierung
   - Warum problematisch: Confounding mit räumlichen Effekten
   - Analogie zu Pseudo-Wiederholungen
   - Kernaussage

5. **Sektion 4: Multi-Environment Trials**
   - Wiederholungen über Standorte
   - Fixed vs. Random Effects
   - Genotyp × Environment Interaktion

6. **Zusammenfassung**
   - 4 Kernbotschaften
   - Offene Fragen für Diskussion
   - Kontakt & Dank

### Technische Features

- **Incremental slides:** `::: {.incremental}` - Punkte erscheinen nacheinander
- **Fragments:** `::: {.fragment}` - Elemente erscheinen auf Klick
- **Callout-Boxen:** `important`, `warning`, `tip`, `note`
- **Zwei-Spalten-Layout:** `::: {.columns}`
- **Kleinere Folien:** `{.smaller}` Klasse
- **Speaker Notes:** `::: {.notes}`
- **R-generierte Plots:** Alle Visualisierungen werden live mit ggplot2 erstellt

---

## Wichtige Git-Operationen

### Standard-Workflow

```bash
# Änderungen machen
git add <files>
git commit -m "Beschreibung"
git push -u origin claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT
```

**WICHTIG:**
- Bei Commit-Signing-Fehlern: `sleep 2 &&` vor dem Commit einfügen
- Push triggert automatisch GitHub Action
- Nach ~30-60 Sekunden ist Update live

### Präsentation testen

1. Push durchführen
2. GitHub Actions prüfen: https://github.com/SchmidtPaul/vortrag_wdh/actions
3. Nach grünem Haken: https://schmidtpaul.github.io/vortrag_wdh/ refreshen

---

## User-Präferenzen & Kontext

**User:** Dr. Paul Schmidt (Biostatistiker)
**Expertise:** Landwirtschaftliche Feldversuche, Versuchsdesign, Statistik
**Erfahrung mit Claude Code:** Erstes Mal - experimentiert mit dem Tool
**Kommunikation:** Deutsch, duzen

**Workshop-Details:**
- Datum: 28. November 2024
- Thema: On-Farm-Experimente
- Zielgruppe: Teilnehmer mit Grundkenntnissen zu Wiederholungen
- Fokus: Nuancen und typische Probleme

**Technische Vorlieben:**
- Präsentation soll online verfügbar sein (GitHub Pages)
- Automatisches Rendering via GitHub Actions
- Refresh-basierter Workflow (kein manuelles Rendern lokal)
- Bevorzugt: Schnelle Build-Zeiten (daher Caching implementiert)

---

## Offene Tasks / Nächste Schritte

### Potenzielle Verbesserungen
- [ ] Weitere Beispiel-Daten oder echte Feldversuche einbauen?
- [ ] Mehr visuelle Elemente (Diagramme, Fotos)?
- [ ] Code-Beispiele für statistische Analysen zeigen?
- [ ] Animationen oder Übergänge verbessern?
- [ ] Timing der Präsentation testen?

### Inhaltliche Erweiterungen (aus Brainstorming)
- [ ] Beispieldaten/Grafiken vorbereiten
- [ ] Feldplan-Illustrationen erstellen (teilweise erledigt)
- [ ] R-Code live zeigen? (bisher nur Plots)
- [ ] Zeitplanung: Wie viele Minuten pro Abschnitt?

---

## Troubleshooting

### Häufige Probleme

**Problem:** GitHub Action schlägt fehl
- **Lösung:** Logs prüfen unter Actions-Tab
- **Häufig:** R-Paket fehlt → In `.github/workflows/publish.yml` hinzufügen

**Problem:** Änderungen nicht sichtbar auf GitHub Pages
- **Lösung:**
  1. Action wirklich erfolgreich? (Grüner Haken)
  2. Browser-Cache leeren (Strg+F5 / Cmd+Shift+R)
  3. `gh-pages` Branch prüfen: Sind neue Files da?

**Problem:** Commit-Signing schlägt fehl
- **Lösung:** `sleep 2 &&` vor git commit hinzufügen

**Problem:** 403 Fehler beim Push zu main
- **Lösung:** Nur zu `claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT` pushen!

---

## Nützliche Befehle

### Präsentation lokal prüfen
```bash
# Datei lesen
cat index.qmd

# Nach bestimmten Strings suchen
grep -n "Randomisation" index.qmd
```

### GitHub Actions Status
```bash
# Neueste Actions anzeigen
gh run list --limit 5
```

---

## Session-Historie

### Session 1 (06. November 2025)
- Initial Setup: Repository-Struktur, GitHub Actions, GitHub Pages
- Brainstorming-Dokument erstellt
- Vollständige Präsentation entwickelt (alle Inhalte)
- Custom Farbschema und Arial-Font implementiert
- R Package Caching aktiviert
- README erstellt
- Diese CLAUDE.md Datei angelegt

### Session 2 (07. November 2025)
**Branch:** `claude/read-claude-md-011CUrnBsraRqoGJHHaCHt2j`

**Inhaltliche Verbesserungen:**
- Neue Folie: Definition Versuchseinheit mit "in der Regel" Nuance
- Neue Folie: "Was bedeutet 'keine Statistik möglich'?" mit detaillierter Auflistung
- Neue Folie: Minimalbeispiel n=1 mit Desplot und Wertetabelle
- Korrektur: "Streng genommen mindestens 2 Wiederholungen" (nicht 2-3)
- Neue Folie: Vergleich n=1 vs. n=2 mit Desplots
- Zwei neue ggplot-Visualisierungen:
  - Plot 1: Nur beobachtete Werte (A=10, B=8) mit Shape 21
  - Plot 2: Mit 50 simulierten grauen Punkten um μ=9 im Hintergrund
  - Zeigt: Mit n=1 könnten beide Werte aus gleicher Population stammen

**Strukturelle Änderungen:**
- Umstrukturierung: Pseudo-Wiederholungen VOR echten Wiederholungen
- Neue Übergangsfolie: "Warum 'echte' Wiederholungen?"
- Erweiterte Pseudo-Wiederholungen Sektion mit On-Farm-Beispielen
- Agenda angepasst: 1. Grundlagen, 2. Pseudo, 3. Echte, 4. Grauzone, 5. METs
- ggplot-Folien ohne Titel nach "Vergleich n=1 vs. n=2" verschoben

**Technische Verbesserungen:**
- Globale Farbpalette mit options(ggplot2.discrete.fill/colour)
- theme_BioMath() Funktion für professionelles ggplot-Styling
- library(ggtext) hinzugefügt (für theme_BioMath)
- Alle Feldpläne von ggplot auf desplot umgestellt
- Faktorstufen reduziert (A,B statt A,B,C wo möglich)
- Alle Callout-Boxen auf Deutsch übersetzt ("Kernbotschaft" statt "Take-Home Message")
- Redundante Texte entfernt ("Jeder versteht intuitiv...")

**Workflow-Fixes:**
- GitHub Actions: ggplot2 library zu allen desplot-Chunks hinzugefügt
- Branch claude/read-claude-md-011CUrnBsraRqoGJHHaCHt2j zum Workflow hinzugefügt
- Kompaktere Folien um Überlauf zu vermeiden

---

## Für neue Claude Code Sessions

**Quick Start:**
1. Lies diese Datei vollständig
2. Lies `brainstorming_wiederholungen.md` für inhaltlichen Kontext
3. Prüfe aktuellen Stand: `git status` und `git log --oneline -10`
4. Teste Live-Präsentation: https://schmidtpaul.github.io/vortrag_wdh/
5. Frage User nach gewünschten Änderungen

**Denk daran:**
- Immer zu Branch `claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT` pushen
- Nach Änderungen: Commit, Push, warten (~30-60s), User zum Refresh auffordern
- User duzen, auf Deutsch kommunizieren
- Diese CLAUDE.md am Ende der Session aktualisieren!

---

## Ende der CLAUDE.md

**Diese Datei MUSS am Ende jeder Session aktualisiert werden mit:**
- Datum der letzten Änderung
- Neue Änderungen in "Session-Historie"
- Neue offene Tasks
- Neue Probleme/Lösungen im Troubleshooting

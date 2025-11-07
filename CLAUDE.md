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
- Gutes CRD Design: A=#00923f, B=#bce2cc
- Schlechtes Design: Gleiche Farben, aber Titel in Rot (#ad0000)
- Split-Plot Problem: Verschiedene Farben je nach Kontext

### Schriftart

**Überall Arial:**
- Quarto CSS: `custom.css` definiert Arial für alle `.reveal` Elemente
- R-Plots: Alle `theme()` Aufrufe haben `family = "Arial"`

---

## Präsentations-Inhalt

### Aktuelle Struktur

1. **Agenda & Einleitung**

2. **Sektion 1: Grundlagen - Warum Wiederholungen?**
   - Definition Versuchseinheit ("in der Regel Parzelle")
   - Wieso Wiederholungen? (n=1 Beispiel)
   - "Keine Statistik möglich" - detaillierte Auflistung
   - Mindestanforderungen: n≥2
   - Vergleich n=1 vs. n=2 mit Desplots
   - Zwei ggplot-Visualisierungen:
     - Plot 1: Nur beobachtete Werte (A=10, B=8)
     - Plot 2: Mit simulierten Punkten um μ=9 (zeigt: beide könnten aus gleicher Population stammen)
   - Überleitung: "Warum 'echte' Wiederholungen?"

3. **Sektion 2: Pseudo-Wiederholungen**
   - Definition mit Synonymen (Pseudoreplikation, Messwiederholungen, etc.)
   - Beispiel: 10 Messungen ≠ n=10
   - Intuitive Analogie: Blutabnahme-Beispiel
   - Besonders relevant bei On-Farm-Versuchen (3 Gründe)
   - **NEU:** Wieso Pseudo-Wiederholungen? (Vorteile, aber nicht ausreichend)

4. **Sektion 3: Echte Wiederholungen**
   - Definition echte Wiederholungen
   - **NEU:** Fokus auf Unabhängigkeit als Ziel, Randomisation als Mittel
   - Visualisierung: Randomisiert = Gut
   - Visualisierung: Systematisch = Problematisch
   - **NEU:** Daten aus Blindversuch (Piepho Uniformitätsversuch)
   - **NEU:** "Fazit bis hierhin" - Vergleich 24 systematische vs. 4 randomisierte Parzellen
   - **NEU:** "Okay" Übergangsfolie (mit Emoji 🥱)

5. **Sektion 4: Die Grauzone - Pseudo-Split-Plot**
   - **NEU:** Typisches Szenario beschrieben (2×3 faktoriell)
   - **NEU:** Drei aufeinanderfolgende Desplots:
     - Füllfarbe nach Faktor 2 (1/2/3)
     - Füllfarbe nach Stufenkombination (A1, A2, etc.)
     - Füllfarbe nach Faktor 1 (A/B), Textfarbe nach Faktor 2
   - **Status:** TODO ab hier (Rest noch nicht fertig)

6. **Sektion 5: Multi-Environment Trials** (noch nicht implementiert)

7. **Zusammenfassung** (noch nicht implementiert)

### Technische Features

- **Incremental slides:** `::: {.incremental}` - Punkte erscheinen nacheinander
- **Fragments:** `::: {.fragment}` - Elemente erscheinen auf Klick
- **Callout-Boxen:** Alle auf Deutsch übersetzt ("Kernbotschaft" statt "Take-Home Message")
- **Emojis:** ✅ ❌ statt ✓ ✗
- **Zwei-Spalten-Layout:** `::: {.columns}`
- **Kleinere Folien:** `{.smaller}` Klasse
- **Speaker Notes:** `::: {.notes}`
- **R-generierte Plots:** Alle Visualisierungen werden live erstellt
- **desplot Gitterlinien:** `out1`/`out2` Parameter für Parzellengrenzen

---

## Wichtige Erkenntnisse & Designentscheidungen

### Terminologie (Recherchiert)

**Pseudo-Wiederholungen (Deutsch):**
- Pseudoreplikation, Pseudoreplikate, Unechte Wiederholungen, Technische Replikate, Messwiederholungen, Subsampling, Nested observations

**Pseudoreplication (Englisch):**
- Pseudoreplicates, Technical replicates, Subsamples, Within-unit replicates, Observational units (OUs), Measurement units (MUs)

**Echte Wiederholungen (Deutsch):**
- Unabhängige Wiederholungen, Biologische Replikate, Versuchseinheiten, Wahre Replikate, Randomisationseinheiten

**True Replication (Englisch):**
- Genuine replicates, Biological replicates (häufigster Begriff!), Independent replicates, Experimental units (EUs)

### Piepho-Referenz

**Vollständige Zitation:**
Piepho, H.P. & Williams, E.R. (2010). Linear variance models for plant breeding trials. *Plant Breeding*, 129(1), 1–8. https://doi.org/10.1111/j.1439-0523.2009.01654.x

**Daten:** Uniformitätsversuch Gerste, Ihinger Hof, Hohenheim, 2007
**R-Package:** `agridat::piepho.barley.uniformity`

### Piephos Lackmus-Test

> "Wenn eine Analyse von Mittelwerten pro Randomisationseinheit mit klassischer Varianzanalyse nicht möglich ist, dann ist der Versuchsplan inadäquat!"

**Wichtig aber noch nicht im Vortrag implementiert** - könnte in Grauzone oder Fazit eingefügt werden.

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
**Kommunikation:** Deutsch, duzen

**Workshop-Details:**
- Datum: 28. November 2024
- Thema: On-Farm-Experimente
- Ko-Referent: Prof. Hans-Peter Piepho (spricht über Randomisation im Detail)
- Zielgruppe: Teilnehmer mit Grundkenntnissen zu Wiederholungen
- Fokus: Nuancen und typische Probleme

**Technische Vorlieben:**
- Präsentation soll online verfügbar sein (GitHub Pages)
- Automatisches Rendering via GitHub Actions
- Refresh-basierter Workflow (kein manuelles Rendern lokal)
- RevealJS mit `history: false` (startet immer bei Folie 1)

---

## Offene Tasks / Nächste Schritte

### Noch zu implementieren (ab "TODO ab hier")

- [ ] **Grauzone-Sektion vervollständigen:**
  - Problem erklären: Warum ist systematische Anordnung von Faktor 1 problematisch?
  - Analogie zu Pseudo-Wiederholungen
  - n=1 für Faktor A trotz vieler Parzellen
  - Confounding mit räumlichen Effekten
  - Kernbotschaft

- [ ] **Multi-Environment Trials:**
  - Wiederholungen über Standorte
  - Fixed vs. Random Effects
  - Genotyp × Environment Interaktion
  - Wann sinnvoll?

- [ ] **Zusammenfassung:**
  - 4 Kernbotschaften
  - Offene Fragen für Diskussion
  - Kontakt & Dank

### Potenzielle Verbesserungen

- [ ] Piephos Lackmus-Test irgendwo einbauen?
- [ ] Mehr visuelle Elemente?
- [ ] Timing der Präsentation testen?
- [ ] Geostatistik-Warnung explizit einfügen?

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

**Problem:** RevealJS startet nicht bei Folie 1
- **Lösung:** `history: false` im YAML-Header setzen (bereits implementiert)

---

## Nützliche Befehle

### Präsentation lokal prüfen
```bash
# Datei lesen
cat index.qmd

# Nach bestimmten Strings suchen
grep -n "TODO" index.qmd
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
- Redundante Texte entfernt

**Workflow-Fixes:**
- GitHub Actions: ggplot2 library zu allen desplot-Chunks hinzugefügt
- Branch claude/read-claude-md-011CUrnBsraRqoGJHHaCHt2j zum Workflow hinzugefügt
- Kompaktere Folien um Überlauf zu vermeiden

### Session 3 (07. November 2025) - **AKTUELL**

**Recherche & Terminologie:**
- Umfassende Web-Recherche zu Pseudoreplikation/Pseudo-Wiederholungen
- Synonyme gesammelt (Deutsch/Englisch) für beide Konzepte
- Piepho (2010) Paper vollständig recherchiert und korrekt zitiert
- Piephos "Lackmus-Test" identifiziert (noch nicht implementiert)

**Inhaltliche Ergänzungen:**
- Synonyme für Pseudo-Wiederholungen auf Folie ergänzt
- Neue Folie: "Wieso Pseudo-Wiederholungen?" (Vorteile, aber Grenzen)
- Fokus auf **Unabhängigkeit** als Ziel, **Randomisation** als Mittel
- Uniformitätsversuch von Piepho & Williams (2010) als Beispiel integriert
  - Daten aus `agridat::piepho.barley.uniformity`
  - Zeigt räumliche Variabilität trotz identischer Behandlung
- "Fazit bis hierhin" Folie: Vergleich 24 systematische vs. 4 randomisierte Parzellen
- "Okay" Übergangsfolie mit Emoji 🥱 vor Grauzone
- **Grauzone Intro:** Typisches Szenario (2×3 faktoriell) beschrieben
- **Drei aufeinanderfolgende Desplots** zur schrittweisen Problem-Visualisierung

**Technische Änderungen:**
- Emojis (✅ ❌) statt Unicode-Zeichen (✓ ✗)
- desplot mit `out1`/`out2` für Parzellengrenzen
- desplot mit `gg=FALSE` für bessere Legenden
- Manuelles problematisches Split-Plot Design erstellt (A/B systematisch, 1/2/3 scheinbar randomisiert)
- Chunk-Wiederverwendung: Datensatz einmal erstellen, dann mehrfach plotten
- `guides(label = "none")` zum Verstecken von Text-Legenden

**Status:**
- **Fertig:** Grundlagen, Pseudo-Wiederholungen, Echte Wiederholungen, Grauzone-Intro
- **TODO:** Rest der Grauzone (Problembeschreibung), METs, Zusammenfassung

---

## Für neue Claude Code Sessions

**Quick Start:**
1. Lies diese Datei vollständig
2. Lies `brainstorming_wiederholungen.md` für inhaltlichen Kontext
3. Prüfe aktuellen Stand: `git status` und `git log --oneline -10`
4. Teste Live-Präsentation: https://schmidtpaul.github.io/vortrag_wdh/
5. Frage User nach gewünschten Änderungen
6. Beachte: Vortrag ist bis "TODO ab hier" fertig, danach offene Punkte

**Denk daran:**
- Immer zu Branch `claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT` pushen
- Nach Änderungen: Commit, Push, warten (~30-60s), User zum Refresh auffordern
- User duzen, auf Deutsch kommunizieren
- Diese CLAUDE.md am Ende der Session aktualisieren!
- Piepho ist Ko-Referent → Keine Überschneidungen, sondern Ergänzung!

---

## Ende der CLAUDE.md

**Diese Datei MUSS am Ende jeder Session aktualisiert werden mit:**
- Datum der letzten Änderung
- Neue Änderungen in "Session-Historie"
- Neue offene Tasks
- Neue Probleme/Lösungen im Troubleshooting

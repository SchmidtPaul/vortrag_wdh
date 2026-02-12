# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Projekt

Quarto RevealJS-Praesentation ueber Wiederholungen in landwirtschaftlichen Feldversuchen. Workshop am 28.11.2024, Ko-Referent: Prof. Piepho (spricht ueber Randomisation). Zielgruppe hat Grundkenntnisse; Fokus auf Nuancen und typische Probleme.

Kommunikation: Deutsch, duzen. Code/Kommentare: Englisch.

## Build & Deployment

Kein lokales Rendering noetig. Push triggert GitHub Actions, die `index.qmd` rendert und auf GitHub Pages deployed.

```bash
# Push (NICHT zu main -- 403 wegen Branch-Restrictions)
git push -u origin claude/create-qmd-presentation-011CUrb2F1VWbXo9FpKGNPvT

# Actions-Status pruefen
gh run list --limit 5
```

- **Live-URL:** https://schmidtpaul.github.io/vortrag_wdh/
- **Build-Zeit:** ~30-60s (R Package Caching aktiv)
- **Bei Commit-Signing-Fehlern:** `sleep 2 &&` vor `git commit` einfuegen

## Architektur

- `index.qmd` -- Gesamte Praesentation (einzige Quelldatei, ~900 Zeilen inkl. R-Code)
- `custom.css` -- Arial-Font und Callout-Farben fuer RevealJS
- `_quarto.yml` -- Minimale Quarto-Config (`type: website`, `output-dir: _site`)
- `.github/workflows/publish.yml` -- CI: R + Quarto Setup, Render, Deploy zu gh-pages
- `brainstorming_wiederholungen.md` -- Konzept und Gliederungsnotizen

### R-Setup in index.qmd

Globaler Setup-Chunk definiert:
- `theme_BioMath()` -- Custom ggplot2-Theme (Arial, minimalistisch, aus `ggtext`)
- Farbpalette via `options(ggplot2.discrete.fill/colour)`:
  - `#00923f` Gruen (Primaer, Behandlung A), `#bce2cc` Hellgruen (B), `#4758ab` Blau (C/Info), `#ad0000` Rot (Warnungen), `#cba135` Gold (Akzente)
- Pakete: `ggplot2`, `desplot`, `ggtext` (weitere: `tidyverse`, `agridat`, `broom`, `emmeans`, `scales` in CI)

### Quarto/RevealJS-Patterns

- Inkrementelle Slides: `::: {.incremental}`
- Fragmente: `::: {.fragment}`
- Callout-Boxen auf Deutsch ("Kernbotschaft", "Achtung" etc.)
- Feldplaene via `desplot()` mit `out1`/`out2` fuer Parzellengrenzen
- Speaker Notes: `::: {.notes}`
- Alle Plots: `family = "Arial"` in theme(), Emojis statt Unicode-Symbole

### CI-Pakete (in publish.yml)

Neue R-Pakete muessen in `.github/workflows/publish.yml` unter "Install R packages" hinzugefuegt werden, sonst schlaegt der Build fehl.

## Inhaltlicher Stand

Fertig: Grundlagen, Pseudo-Wiederholungen, Echte Wiederholungen, Grauzone-Intro (Desplots).

### Offene TODOs (ab Kommentar "TODO ab hier" in index.qmd)

- Grauzone vervollstaendigen: Problem erklaeren (n=1 fuer Faktor A, Confounding), Kernbotschaft
- Multi-Environment Trials: Standorte als Wiederholungen, GxE-Interaktion
- Zusammenfassung: 4 Kernbotschaften, Diskussionsfragen
- Piephos Lackmus-Test einbauen: "Wenn Analyse von Mittelwerten pro Randomisationseinheit mit klassischer ANOVA nicht moeglich, ist Versuchsplan inadaequat"

## Fachkontext

- Piepho & Williams (2010): Uniformitaetsversuch Gerste, `agridat::piepho.barley.uniformity`
- Piepho ist Ko-Referent -- keine Ueberschneidungen, sondern Ergaenzung
- Zentrale These: **Unabhaengigkeit** ist das Ziel, **Randomisation** das Mittel

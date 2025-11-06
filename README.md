# Vortrag: Wiederholungen in landwirtschaftlichen Feldversuchen

## Über dieses Repository

Dieses Repository enthält den Vortrag **"Wiederholungen in landwirtschaftlichen Feldversuchen"**, der am **28. November 2024** auf einem Workshop zu On-Farm-Experimenten gehalten wird.

## Kontext

Dieses Projekt dient gleichzeitig zwei Zwecken:

1. **Vortragsentwicklung:** Konzeption und Entwicklung eines Fachvortrags über Wiederholungen im Versuchsdesign von landwirtschaftlichen Feldversuchen
2. **Technisches Experiment:** Erste Erfahrungen mit der Entwicklung von Quarto-Präsentationen vollständig mit **Claude Code** (Anthropic's CLI für Claude)

## Workflow

Die Quarto-Präsentationsdatei (`index.qmd`) wird über **GitHub Actions** automatisch gerendert und auf **GitHub Pages** veröffentlicht:

- ✅ Änderungen an `index.qmd` werden committed und gepusht
- ✅ GitHub Actions rendert die Präsentation automatisch
- ✅ Die fertige Präsentation wird auf GitHub Pages deployed

**Live-Präsentation ansehen:** [https://schmidtpaul.github.io/vortrag_wdh/](https://schmidtpaul.github.io/vortrag_wdh/)

## Inhalt

Der Vortrag fokussiert sich auf verschiedene Aspekte von Wiederholungen in landwirtschaftlichen Versuchsdesigns:

- **Echte/unabhängige Wiederholungen:** Randomisation und räumliche Verteilung
- **Pseudo-Wiederholungen (Messwiederholungen):** Mehrfache Messungen innerhalb derselben Versuchseinheit
- **Die Grauzone:** Probleme bei unvollständiger Randomisation (z.B. Pseudo-Split-Plot-Designs)
- **Multi-Environment Trials:** Wiederholungen über mehrere Standorte

Siehe [`brainstorming_wiederholungen.md`](brainstorming_wiederholungen.md) für detaillierte Konzeptnotizen.

## Technische Details

- **Präsentationsformat:** Quarto Reveal.js
- **Programmiersprache:** R (mit Paketen wie tidyverse, ggplot2, desplot, agridat)
- **Deployment:** GitHub Actions → GitHub Pages
- **Entwicklung:** Vollständig mit Claude Code erstellt

## Dateien

- `index.qmd` - Hauptpräsentationsdatei (Quarto)
- `brainstorming_wiederholungen.md` - Konzept und Gliederungsnotizen
- `.github/workflows/publish.yml` - GitHub Actions Workflow für automatisches Rendering
- `_quarto.yml` - Quarto Projektkonfiguration

## Autor

Dr. Paul Schmidt (Biostatistiker)

## Lizenz

Siehe [LICENSE](LICENSE) Datei für Details.

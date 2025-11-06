# Vortrag: Wiederholungen in landwirtschaftlichen Feldversuchen

## Kontext
- Workshop zu On-Farm-Experimenten in der Landwirtschaft
- Zielgruppe: Teilnehmer mit Grundkenntnissen zu Wiederholungen
- Fokus: Nuancen und typische Probleme bei Wiederholungen
- Spektrum: Von Exaktversuchen mit Kleinparzellen bis zu Großparzellenversuchen (Streifen-Design)

---

## Hauptgliederung des Themas "Wiederholung"

### 1. Echte/Unabhängige Wiederholungen

**Grundprinzip:**
- Versuchseinheit = Parzelle auf einem Feld
- Mindestens 2, oft 3 echte Wiederholungen nötig für Auswertbarkeit
- **Randomisation ist entscheidend:**
  - Parzellen müssen zufällig verteilt liegen
  - Dürfen auch nebeneinander liegen, wenn Randomisation dies ergab
  - **NICHT systematisch** direkt nebeneinander angeordnet
  - Vollständig zufällige Zuweisung: Welche Parzelle → Welche Behandlung → Welche Wiederholung

**Kernaussage:**
Dies sind die echten, unabhängigen Wiederholungen - die Grundlage für statistische Auswertungen.

---

### 2. Pseudo-Wiederholungen (Messwiederholungen)

**Definition:**
Mehrfache Messungen innerhalb derselben Versuchseinheit (Parzelle)

**Beispiele:**

a) **Einfaches Beispiel:**
   - 10 Parzellen auf dem Feld
   - 3 Messungen pro Parzelle (z.B. Pflanzenhöhe mit Meterstab an 3 Stellen)
   - → 30 Messwerte, aber NICHT 30 unabhängige Wiederholungen

b) **Modernes Technologie-Beispiel:**
   - Traktor mit Sensortechnik
   - Viele Messpunkte pro Meter innerhalb einer großen Parzelle
   - Koordinaten-basierte Messungen
   - → Hohe Datenmenge, aber begrenzte statistische Unabhängigkeit

**Intuitive Abgrenzung:**
- **3 Blutabnahmen bei 3 verschiedenen Menschen** ≠ **3 Blutabnahmen bei 1 Person an 3 Stellen**
- Jeder versteht intuitiv: Das ist nicht dasselbe!

**Kernaussage:**
Messungen innerhalb derselben Parzelle sind **nicht unabhängig** voneinander.

---

### 3. Die Grauzone: Confounding durch unvollständige Randomisation

**Szenario: Pseudo-Split-Plot-Design**

**Typische Problemsituation:**
- Zweifaktorieller Versuch: Faktor A × Faktor B
- **Versuch**, ein Split-Plot-Design anzulegen
- **Aber:** Unvollständige/systematische Randomisation von Faktor A

**Konkretes Beispiel:**
```
Feld-Layout:
┌─────────────────────┐
│  NÖRDLICHE HÄLFTE   │
│      A1             │  ← Gesamte Nordhälfte = A1
│  (mit B1, B2, ...)  │
├─────────────────────┤
│  SÜDLICHE HÄLFTE    │
│      A2             │  ← Gesamte Südhälfte = A2
│  (mit B1, B2, ...)  │
└─────────────────────┘
```

**Das Problem:**
- Faktor B ist innerhalb der Hälften randomisiert ✓
- Faktor A ist **NICHT** randomisiert, sondern systematisch (Nord vs. Süd) ✗
- Kombination A1×B1 mag mehrfach vorkommen auf dem Feld
- **ABER:** Alle A1-Parzellen liegen in derselben (nördlichen) Feldhälfte

**Warum ist das problematisch?**
- Die gesamte nördliche Hälfte = 1 unabhängige Fläche für A1
- Die gesamte südliche Hälfte = 1 unabhängige Fläche für A2
- → **Nur n=1 echte Wiederholung pro Stufe von Faktor A!**

**Analogie:**
- Wie bei Pseudo-Wiederholungen: Eine Parzelle mit mehrfachen Messungen
- Hier: Eine Feldhälfte mit mehrfachen Parzellen
- → Systematische räumliche Struktur = fehlende Unabhängigkeit

**Irreführender erster Eindruck:**
- "Ich habe doch viele Parzellen!"
- "Ich habe doch A1×B1 mehrfach auf dem Feld!"
- → **ABER:** Alle Instanzen von A1 teilen dieselbe räumliche Einheit

---

## Weitere Aspekte

### Mehrere Standorte (Multi-Environment Trials)

**Szenario:**
- Einzelner Standort: Keine Wiederholungen möglich
- Lösung: Gleiche Behandlungen an mehreren Standorten
- Erst durch Multiple Standorte wird Auswertung möglich
- → "Standort" wird zu einer weiteren Ebene im Design

**Beachte:**
- Standorte als Blöcke oder als Random Effect?
- Genotyp × Environment Interaktion

---

## Zusammenfassung für den Vortrag

### Kernbotschaften:

1. **Echte Wiederholungen brauchen Randomisation**
   - Räumlich unabhängig
   - Statistisch unabhängig

2. **Messwiederholungen sind keine echten Wiederholungen**
   - Intuitiv verständlich
   - Aber wichtig zu berücksichtigen in der Analyse

3. **Vorsicht vor der Grauzone!**
   - Systematische Anordnung = versteckte Pseudo-Wiederholung
   - Häufiger Fehler bei On-Farm-Versuchen
   - Große Parzellenzahl ≠ Viele unabhängige Wiederholungen

4. **Die Randomisation ist entscheidend**
   - Nicht die Anzahl der Parzellen
   - Sondern die **räumliche Unabhängigkeit** der Behandlungen

---

## Offene Fragen für die Diskussion

- Wie geht man um mit halb-systematischen Designs in der Praxis?
- Wann sind Kompromisse vertretbar?
- Wie kommuniziert man diese Konzepte an Landwirte?
- Welche statistischen Ansätze für suboptimale Designs?

---

## Nächste Schritte

- [ ] Beispieldaten/Grafiken vorbereiten
- [ ] Feldplan-Illustrationen erstellen
- [ ] Entscheiden: R-Code live zeigen?
- [ ] Zeitplanung: Wie viele Minuten pro Abschnitt?

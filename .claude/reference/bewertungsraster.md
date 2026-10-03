# Bewertungsraster Transferarbeit CAS Software Architecture

Single source of truth for the official grading criteria, shared by the `bewertung` and `critical-review` skills. Criteria IDs (e.g. `2.4`) are cited in every finding.

## Official criteria

### 1. Inhalt & Problemlösung

- **1.1 Kontext & Fragestellung:** Werden alle wesentlichen Aspekte des Themenkontexts und der Problemstellung fundiert und lückenlos adressiert?
- **1.2 Nachvollziehbarkeit & Begründung:** Ist der Lösungsweg schlüssig? Werden Architekturentscheidungen klar aus den Projektzielen und Treibern hergeleitet?
- **1.3 Artefakte:** Sind die gewählten Diagramme, Tabellen und Modelle dem Problem angemessen (weder trivial noch Over-Engineering)?
- **1.4 Qualitätsziele & ATAM:** Wurden die definierten Prio-1-Qualitätsziele nachweisbar erreicht? Ist der methodische Nachweis auf Basis von ATAM (Trade-offs, Risiken, Sensitivitätspunkte) sauber und nachvollziehbar erbracht?

### 2. Methodisches Vorgehen

- **2.1 Funktionale Anforderungen:** Maximal 4 funktionale Anforderungen ausgewählt; genau 2 davon detailliert als User Stories oder Use Cases dokumentiert.
- **2.2 Nichtfunktionale Anforderungen (ISO 25010):** NFRs nach ISO/IEC 25010 bestimmt und priorisiert. Maximal 2 Attribute als Top-Prio-1 definiert. Jedes Prio-1-Attribut mit 1 bis 3 konkreten Qualitätsszenarien spezifiziert (Quelle, Stimulus, Artefakt, Umgebung, Antwort, Antwortmass).
- **2.3 Systemvision & Kontext:** Systemvision nach dem agilen Vision-Template. Saubere fachliche und/oder technische Kontextsicht.
- **2.4 Architekturentscheidungen (ADRs):** 4 bis 6 ADRs, vollständig und einheitlich nach einem anerkannten Template. Mindestens 2 davon explizit auf Ebene Technologie/Bausteine.
- **2.5 Zusätzliche Sichten:** Mindestens 2 weitere Architektur-Sichten, formal korrekt in UML und/oder BPMN (z. B. Baustein-, Laufzeit-, Verteilungssicht).

### 3. Sprache, Form & Traceability

- **3.1 Dokumentationsstandard:** Akademisch und professionell formuliert; konsequente Nutzung einer etablierten Vorlage (arc42).
- **3.2 Quellen & Methodenzitate:** Korrekte, einheitliche Zitierweise. Originalquellen der Methoden explizit angegeben (ADR-Template, ATAM/SAAM, UML/BPMN, arc42, ISO 25010).
- **3.3 Architectural Thinking & Traceability:** Fachbegriffe präzise (ISO/IEC/IEEE 42010). Eindeutige Benennung aller Artefakte. Durchgängige Rückverfolgbarkeit: Geschäftsziele → Anforderungen → ADRs → Sichten → Qualitätsprüfung/ATAM.
- **3.4 Abbildungen & Tabellen:** Durchgehend nummeriert, präzise betitelt, im Text aktiv referenziert und inhaltlich erläutert.

### Formal constraints

- Gesamtarbeit max. 50 Seiten; Hauptteil max. 42 Seiten; kein Anhang. Every sentence must earn its space: flag redundancy between chapters.

## Where each criterion lives in this repository

The thesis is LaTeX following arc42; `main.tex` inputs the chapters in order.

| Criterion | Primary files | Traceability neighbours to cross-check |
|---|---|---|
| 1.1, 2.3 | `chapters/01-introduction-and-goals.tex`, `chapters/03-context-and-scope.tex` | `02-architecture-constraints.tex` |
| 2.1 | `chapters/01-introduction-and-goals.tex` (Functional Requirements) | `06-runtime-view.tex` (scenarios should realise the FRs) |
| 2.2 | `chapters/01-introduction-and-goals.tex` (Quality Goals), `chapters/10-quality-requirements.tex` (Quality Scenarios) | ADR header field *Quality goals* |
| 1.2, 2.4 | `chapters/04-solution-strategy.tex`, `chapters/09-architecture-decisions.tex`, `adrs/*.tex` | Decision Log rows ↔ ADR files ↔ quality goals |
| 1.3, 2.5 | `chapters/05-building-block-view.tex`, `06-runtime-view.tex`, `07-deployment-view.tex`, `diagrams-src/`, `pictures/diagrams/` | Building blocks named in ADRs |
| 1.4 | `chapters/10-quality-requirements.tex`, `chapters/11-risks-and-technical-debts.tex` | Prio-1 scenarios ↔ ADRs ↔ risks/sensitivity points |
| 3.2 | `chapters/99-references.tex` | every `\cite{}` |
| 3.3 | `chapters/12-glossary.tex` | terms used across all chapters |
| 3.4 | every `\begin{figure}` / `\begin{table}` / `longtable` | matching `\ref{}` in the text |

## Repository conventions that affect a review

- **arc42 help text:** chapters still contain arc42 template guidance under `\minititle{Contents}`, `Motivation`, `Form`, `Further Information`, and placeholder headings like `\textless Concept 1\textgreater`. That is scaffolding, not authored content: report it as *missing content* for the criterion, and leave its wording uncritiqued.
- **Course comments:** lines starting `% Course comment:` are lecturer hints. Treat them as additional review criteria for that chapter.
- **ADRs** use the Y-Statement template (Zimmermann) from `adrs/01-short-title.tex`, extended with a header (status, date, deciders, quality goals) and a measurable verification criterion. Each ADR file is `\input` in `chapters/09-architecture-decisions.tex` and needs a Decision Log row and a `\label{adr:NN}`.
- **Page count:** `main.pdf` is committed; check its page count (`pdfinfo main.pdf`, needs poppler) or ask the user when reviewing the whole thesis.

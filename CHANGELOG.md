# Changelog

Todos los cambios notables de **po-analytics** se documentan aqui.

El formato sigue [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
y el proyecto usa [Versionado Semantico](https://semver.org/lang/es/).

## [No publicado]

Candidatos a proximas versiones: skills de funnel/conversion, cohortes/retencion,
INVEST checker independiente y Opportunity Solution Tree. Ver seccion "Roadmap" del README.

## [0.1.0] - 2026-07-30

Primera version. Andamiaje completo del plugin y marketplace local.

### Anadido
- **Router** `po-copilot`: detecta la intencion y deriva al skill correcto; cruza los
  lentes de priorizacion y senala las discrepancias como zona de decision.
- **Priorizacion**:
  - `prioritize-rice` — Reach x Impact x Confidence / Effort, con separacion de
    "top por valor" vs. "quick-wins" (evita que un score alto por Effort minimo se
    presente como apuesta de impacto).
  - `prioritize-wsjf` — Cost of Delay / Job Size, estilo SAFe, puntuacion por columna.
  - `prioritize-kano` — clasificacion must-be / performance / attractive / indifferent /
    reverse para decidir el mix de una release.
- **Metricas**: `metrics-north-star` — define la NSM y su arbol de input metrics, con
  ejemplos por tipo de producto y filtro de metricas de vanidad.
- **Backlog**: `story-writer` — user stories con criterios Gherkin, validacion INVEST y
  split SPIDR con generacion de sub-historias.
- **Agile**: `sprint-analytics` — velocity, burndown, cycle time, throughput, WIP y
  scope creep, con diagnostico y acciones.
- **Referencias compartidas** en `skills/po-copilot/references/frameworks.md` (formulas y escalas).
- **Command** `/rice` para priorizacion rapida.
- **Marketplace local** `po-tools` (`.claude-plugin/marketplace.json`) para instalar el plugin.
- **Ejemplo de conectores MCP** (`.mcp.json.example`) para Jira, Linear y Amplitude.
- `.gitignore` que protege el `.mcp.json` real con credenciales.
- Licencia **MIT** (`LICENSE`) y campo `license` en `plugin.json`.

[No publicado]: https://github.com/Ferjapolisgp/PO_interlocutor/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/Ferjapolisgp/PO_interlocutor/releases/tag/v0.1.0

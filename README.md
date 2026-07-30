# PO Analytics

Caja de herramientas **analiticas** para Product Owners, empaquetada como plugin de Claude Code / Claude Desktop.

Complementa a otros dos bundles del ecosistema:

- **`product-manager`** (Pragmatic Framework) — cubre la parte cualitativa/estrategica: discovery, personas, positioning, roadmap, PRD.
- **`product-tracking-skills`** — cubre la instrumentacion de telemetria (disenar plan de tracking, generar codigo de eventos).

`po-analytics` llena el hueco del medio: las **herramientas cuantitativas de decision** que un PO usa cada semana.

## Que incluye

| Skill | Que hace |
|---|---|
| `po-copilot` | Router. Detecta la intencion y orquesta el skill correcto. |
| `prioritize-rice` | Prioriza features con RICE (Reach x Impact x Confidence / Effort). |
| `prioritize-wsjf` | Secuencia por WSJF (Cost of Delay / Job Size), estilo SAFe. |
| `prioritize-kano` | Clasifica features por satisfaccion (must-be / performance / delighters). |
| `sprint-analytics` | Interpreta velocity, burndown, cycle time y salud del sprint. |
| `metrics-north-star` | Define la North Star Metric y su arbol de input metrics. |
| `story-writer` | Genera user stories con criterios de aceptacion en Gherkin. |

Cada skill produce un **artefacto** (tabla o documento Markdown) listo para pegar en Jira/Confluence/Notion.

## Estructura

```
po-analytics/
├─ .claude-plugin/plugin.json     # manifiesto del plugin
├─ skills/
│  ├─ po-copilot/                 # router + referencias compartidas
│  │  ├─ SKILL.md
│  │  └─ references/frameworks.md
│  ├─ prioritize-rice/SKILL.md
│  ├─ sprint-analytics/SKILL.md
│  ├─ metrics-north-star/SKILL.md
│  └─ story-writer/SKILL.md
├─ commands/
│  └─ rice.md                     # /rice
└─ .mcp.json.example              # conectores opcionales (Jira, Linear, Amplitude)
```

## Datos reales (opcional)

Los skills funcionan solos con los datos que le pegues. Para que lean el backlog o las
metricas de verdad, copia `.mcp.json.example` a `.mcp.json` y configura los conectores
(Jira/Linear para backlog, Amplitude/Mixpanel para producto). El patron es:
el **skill** hace el calculo, el **conector** trae los inputs.

## Roadmap del propio plugin

Siguientes candidatos a skill: WSJF, Kano, funnel/conversion, cohortes/retencion,
INVEST checker, story splitting (SPIDR), Opportunity Solution Tree.

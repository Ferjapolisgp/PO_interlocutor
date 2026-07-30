# PO Analytics

Caja de herramientas **analiticas** para Product Owners, empaquetada como plugin de
Claude Code / Claude Desktop.

Complementa a otros dos bundles del ecosistema:

- **`product-manager`** (Pragmatic Framework) — cubre la parte cualitativa/estrategica:
  discovery, personas, positioning, roadmap, PRD.
- **`product-tracking-skills`** — cubre la instrumentacion de telemetria (disenar plan de
  tracking, generar codigo de eventos).

`po-analytics` llena el hueco del medio: las **herramientas cuantitativas de decision** que un
PO usa cada semana. Cada skill produce un **artefacto** (tabla o documento Markdown) listo
para pegar en Jira / Confluence / Notion.

---

## Tabla de contenidos

- [Que incluye](#que-incluye)
- [Instalacion](#instalacion)
- [Uso](#uso)
- [Los skills en detalle](#los-skills-en-detalle)
- [Como se encadenan](#como-se-encadenan)
- [Datos reales via conectores MCP](#datos-reales-via-conectores-mcp)
- [Estructura del repo](#estructura-del-repo)
- [Versionado](#versionado)
- [Extender el plugin](#extender-el-plugin)
- [Licencia](#licencia)

---

## Que incluye

| Skill | Categoria | Que hace |
|---|---|---|
| `po-copilot` | Router | Detecta la intencion y orquesta el skill correcto; cruza lentes de priorizacion. |
| `prioritize-rice` | Priorizacion | Ordena por RICE (Reach x Impact x Confidence / Effort). |
| `prioritize-wsjf` | Priorizacion | Secuencia por WSJF (Cost of Delay / Job Size), estilo SAFe. |
| `prioritize-kano` | Priorizacion | Clasifica por satisfaccion (must-be / performance / delighter). |
| `metrics-north-star` | Metricas | Define la North Star Metric y su arbol de input metrics. |
| `story-writer` | Backlog | User stories con criterios Gherkin, INVEST y split SPIDR. |
| `sprint-analytics` | Agile | Velocity, burndown, cycle time, WIP y salud del sprint. |

---

## Instalacion

El plugin se distribuye como **marketplace local** (`po-tools`). En una terminal `claude`
interactiva:

```
/plugin marketplace add D:\extras\PO_interlocutor
```
```
/plugin install po-analytics@po-tools
```

Reinicia la sesion cuando lo pida. Verifica con `/help`: deberias ver el command `/rice`
y disponer de los 7 skills. Para actualizar tras cambios locales:

```
/plugin marketplace update po-tools
```

> Los slash commands `/plugin` abren un panel interactivo; no funcionan en sesiones no
> interactivas. Corrélos desde la terminal de Claude Code.

---

## Uso

Hay tres formas de invocar las herramientas:

1. **Lenguaje natural (recomendado)** — el router `po-copilot` detecta la intencion:
   - *"prioriza mi backlog"* -> RICE
   - *"secuencia esto por coste de esperar"* -> WSJF
   - *"que features encantan y cuales son solo higiene"* -> Kano
   - *"como va el sprint"* -> sprint analytics
   - *"cual deberia ser nuestra metrica clave"* -> North Star
   - *"escribe la historia de esta feature"* -> story writer

2. **Command directo**:
   ```
   /rice F1 login SSO, F2 export CSV, F3 modo offline
   ```

3. **Skill explicito** — pide un skill por su nombre si quieres saltarte el router.

En todos los casos, si no pegas los datos, el skill te pedira lo minimo necesario y marcara
sus supuestos.

---

## Los skills en detalle

### `po-copilot` (router)
Punto de entrada. Clasifica el pedido, deriva al skill adecuado y **encadena** cuando aporta.
Si corres mas de un metodo de priorizacion sobre el mismo backlog, compara los rankings y
**senala las discrepancias como decision** en vez de esconderlas en el numero. Deriva lo
estrategico a `product-manager` y lo de instrumentacion a `product-tracking-skills`.

### `prioritize-rice`
`Score = (Reach x Impact x Confidence) / Effort`. Reach es un numero absoluto (no escala).
Separa el **top por valor** de los **quick-wins** (score alto por Effort minimo) y marca las
filas con Confidence < 50% como "necesita discovery".

### `prioritize-wsjf`
`WSJF = Cost of Delay / Job Size`, con Cost of Delay = Business Value + Time Criticality +
Risk Reduction/Opportunity Enablement. Puntuacion en Fibonacci relativa **por columna**.
Util cuando importa la urgencia temporal (SAFe, PI planning, ventanas de mercado).

### `prioritize-kano`
Clasifica cada feature en must-be / performance / attractive / indifferent / reverse para
decidir el **mix** de una release (no un orden lineal). Con datos de encuesta Kano (pregunta
funcional + disfuncional) o, sin datos, por heuristica marcada como hipotesis.

### `metrics-north-star`
Elige la unica metrica que captura el valor entregado (validada contra: valor al usuario,
predice ingresos, accionable) y la descompone en 2-4 input metrics. Incluye ejemplos por tipo
de producto (SaaS B2B, marketplace, contenido, fintech, PLG) y filtro de metricas de vanidad.

### `story-writer`
Convierte un requisito en user story "Como / quiero / para" con criterios de aceptacion en
Gherkin (camino feliz + borde/error + reglas). Valida contra INVEST y, si falla "Small",
parte la historia con patrones SPIDR generando sub-historias que entregan valor por si solas.

### `sprint-analytics`
Convierte datos de un tablero en diagnostico: velocity (promedio movil, no un solo sprint),
completion rate, scope change, cycle time (mediana), throughput y WIP. Entrega 2-3 acciones
priorizadas para el siguiente sprint.

---

## Como se encadenan

El valor real aparece al combinarlos. Flujo tipico de planificacion de release:

```
North Star  ->  RICE / WSJF        ->  Kano            ->  Story Writer     ->  Sprint Analytics
(ancla el     (ordenan el backlog;   (decide el mix    (parte el #1 en      (cierra el loop:
 Impact)       cruzados por el        higiene vs.        historias listas)    salud del sprint)
               router)                delighters)
```

- La **North Star** ancla el `Impact` de RICE (no es arbitrario).
- **RICE** y **WSJF** dan dos lentes; el router marca donde coinciden (senal robusta) y donde
  discrepan (zona de decision, p.ej. WSJF sube un item por Time Criticality que RICE penalizo).
- **Kano** dice el *tipo* de cada feature; RICE/WSJF el *orden*.
- **Story Writer** detecta historias demasiado grandes y las parte.
- **Sprint Analytics** suele confirmar el mismo sintoma (historias grandes -> cycle time alto).

---

## Datos reales via conectores MCP

Los skills funcionan solos con lo que pegues. Para leer el backlog o las metricas de verdad,
copia el ejemplo y configura los conectores:

```
cp .mcp.json.example .mcp.json
```

Luego edita `.mcp.json` con tus credenciales:

| Conector | Alimenta a | Trae |
|---|---|---|
| Jira / Atlassian | `prioritize-*`, `sprint-analytics` | backlog, sprints, velocity |
| Linear | `prioritize-*`, `sprint-analytics` | issues, estados, ciclos |
| Amplitude / Mixpanel | `metrics-north-star` | funnels, retencion, eventos |

Patron: el **skill** hace el calculo, el **conector** trae los inputs. El `.mcp.json` real
esta en `.gitignore` (contiene credenciales); solo se versiona el `.example`.

---

## Estructura del repo

```
PO_interlocutor/
├─ .claude-plugin/
│  ├─ plugin.json              # manifiesto del plugin
│  └─ marketplace.json         # marketplace local "po-tools"
├─ skills/
│  ├─ po-copilot/
│  │  ├─ SKILL.md              # router
│  │  └─ references/frameworks.md   # formulas y escalas compartidas
│  ├─ prioritize-rice/SKILL.md
│  ├─ prioritize-wsjf/SKILL.md
│  ├─ prioritize-kano/SKILL.md
│  ├─ metrics-north-star/SKILL.md
│  ├─ story-writer/SKILL.md
│  └─ sprint-analytics/SKILL.md
├─ commands/
│  └─ rice.md                  # /rice
├─ .mcp.json.example           # plantilla de conectores (Jira, Linear, Amplitude)
├─ .gitignore
├─ CHANGELOG.md
└─ README.md
```

---

## Versionado

El proyecto sigue [SemVer](https://semver.org/lang/es/). Los cambios notables se registran en
[CHANGELOG.md](CHANGELOG.md). La version vive en `.claude-plugin/plugin.json` y en el
`marketplace.json`; manten ambas sincronizadas al publicar.

---

## Extender el plugin

Para anadir un skill nuevo:

1. Crea `skills/<nombre>/SKILL.md` con frontmatter `name` + `description`. La `description`
   debe incluir las frases que dispararan el skill (en el vocabulario real del PO).
2. Reutiliza las formulas de `skills/po-copilot/references/frameworks.md` (o anade las nuevas ahi).
3. Registra el skill en la tabla de enrutamiento de `po-copilot/SKILL.md` y en este README.
4. Anota el cambio en `CHANGELOG.md` y sube la version en `plugin.json` + `marketplace.json`.

**Roadmap** de proximos skills: funnel/conversion, cohortes/retencion, INVEST checker
independiente, Opportunity Solution Tree, RICE vs. WSJF comparativo en un solo paso.

---

## Licencia

[MIT](LICENSE) (c) 2026 barroso.ouharriet. Uso, modificacion y redistribucion libres
manteniendo el aviso de copyright.

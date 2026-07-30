---
name: story-writer
description: >
  Convierte una idea, requisito o feature en una user story bien formada con criterios de
  aceptacion en formato Gherkin (Given/When/Then). Valida contra INVEST y, si la historia es
  demasiado grande, la parte con patrones SPIDR y genera las sub-historias. Usalo cuando el
  usuario dice "escribe la historia", "redacta el ticket", "criterios de aceptacion",
  "user story", "parte esta epica", "pasa esto a historia", o pega un requisito informal.
---

# Story Writer

Redacta user stories claras, valiosas y testables, listas para pegar en Jira/Linear. Plantillas
INVEST, Gherkin y patrones de split en `../po-copilot/references/frameworks.md`.

## Procedimiento

1. **Captura quien / que / por que.** Formato:
   "Como <persona>, quiero <accion>, para <beneficio>".
   Si falta la persona o el beneficio, preguntalo — sin beneficio la historia no es *Valuable*
   y no se puede priorizar. No inventes la persona: si no la sabes, pide cual es.

2. **Escribe los criterios de aceptacion en Gherkin.** Cubre:
   - el **camino feliz**,
   - al menos **un caso borde o de error** (input invalido, sin permisos, estado vacio),
   - reglas de negocio explicitas (limites, validaciones).
   Cada criterio debe ser verificable objetivamente por QA sin ambiguedad.

3. **Valida contra INVEST.** Revisa las seis:
   Independent, Negotiable, Valuable, Estimable, Small, Testable.
   Marca cuales pasa y cuales no.

4. **Si falla "Small" (o "Estimable"), parte la historia con SPIDR.** Elige el patron que mejor
   corte por valor (no por capa tecnica):
   - **S — Spike:** hay incertidumbre tecnica -> primero una historia de investigacion acotada.
   - **P — Path:** separa los caminos del flujo (feliz vs. alternativos, cada metodo de pago...).
   - **I — Interface:** separa por canal/UI (web, movil, API) o por dispositivo.
   - **D — Data:** entrega primero un subconjunto de datos/tipos, luego el resto.
   - **R — Rules:** implementa primero las reglas de negocio simples, luego las complejas.
   Genera las sub-historias resultantes, cada una con su propia forma "Como/quiero/para" y con
   criterios de aceptacion. Cada sub-historia debe entregar valor por si sola.

5. **Anade contexto de entrega:** fuera de alcance explicito, dependencias, y (si aplica)
   sub-tareas tecnicas sugeridas para el equipo de desarrollo.

## Formato de salida

```markdown
## <titulo de la historia>

**Como** <persona> **quiero** <accion> **para** <beneficio>.

### Criterios de aceptacion
- **Escenario: <camino feliz>**
  - Given <contexto>
  - When <accion>
  - Then <resultado>
- **Escenario: <caso borde / error>**
  - Given <contexto>
  - When <accion>
  - Then <resultado>

### Fuera de alcance
- ...

### Dependencias
- ...

### Checklist INVEST
Independent [x] Negotiable [x] Valuable [x] Estimable [x] Small [ ] Testable [x]
> "Small" falla: ver split abajo.

### Split sugerido (patron SPIDR: <patron>)
1. **<sub-historia 1>** — Como ... quiero ... para ...
2. **<sub-historia 2>** — Como ... quiero ... para ...

### Sub-tareas tecnicas (opcional)
- [ ] ...
```

## Notas

- El "para <beneficio>" es lo mas importante y lo que mas se omite: sin el, la historia es una tarea, no una historia.
- No escribas el *como* tecnico en la historia; eso es decision del equipo. La historia dice el *que* y el *por que*.
- Si el usuario pega varios requisitos, produce una historia por requisito y senala solapamientos.
- Si hay conector de backlog (Jira/Linear) via MCP, ofrece crear el/los tickets tras la aprobacion del usuario (accion que requiere su confirmacion explicita).

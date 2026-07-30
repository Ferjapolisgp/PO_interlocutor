---
name: sprint-analytics
description: >
  Analiza la salud de un sprint o de un flujo de trabajo: velocity, burndown, cycle time,
  throughput y scope creep. Interpreta las tendencias y da recomendaciones accionables.
  Usalo cuando el usuario dice "como va el sprint", "analiza la velocity", "por que no
  terminamos", "cycle time", "burndown", "salud del sprint", "reporte de sprint", o pega
  datos de un tablero (Jira/Linear/ClickUp).
---

# Sprint Analytics

Convierte datos crudos de un sprint/tablero en un diagnostico con recomendaciones. Definiciones
de cada metrica en `../po-copilot/references/frameworks.md`.

## Procedimiento

1. **Consigue los datos.** Si el usuario los pego, usalos. Si hay conector MCP (Jira/Linear/ClickUp),
   ofrece traer: items del sprint con su estado, story points, fechas de "in progress" y "done",
   y el historico de los ultimos 3-5 sprints para el promedio.

2. **Calcula las metricas clave:**
   - **Velocity** — puntos completados este sprint vs. promedio de los ultimos 3-5.
   - **Completion rate** — % del scope comprometido que se termino.
   - **Scope change** — puntos anadidos/quitados a mitad de sprint (senal de planificacion o presion externa).
   - **Cycle time** — mediana del tiempo in-progress -> done. Usa mediana, no promedio.
   - **Throughput** — # de items terminados.
   - **WIP** — items en progreso simultaneos (alto WIP = poco foco).

3. **Diagnostica, no solo reportes.** Para cada senal, explica la causa probable:
   - Velocity cayo + scope change alto -> interrupciones o mala estimacion.
   - Burndown plano hasta el final -> trabajo en cascada dentro del sprint / bloqueos tardios.
   - Cycle time con outliers -> items demasiado grandes (sugiere split) o dependencias.

4. **Recomienda 2-3 acciones concretas** para el proximo sprint, priorizadas por impacto.

## Formato de salida

```markdown
## Reporte de Sprint — <sprint / fecha>

**Resumen:** completamos X/Y puntos (Z%). Velocity <arriba/abajo> vs promedio (<n>).

| Metrica | Valor | vs. promedio | Lectura |
|---|---|---|---|
| Velocity | 34 pts | -18% | por debajo |
| Completion rate | 78% | -- | scope creep |
| Cycle time (mediana) | 3.2 d | +0.8 d | items grandes |
| WIP promedio | 6 | alto | foco disperso |

**Que paso:** ...

**Acciones para el proximo sprint:**
1. ...
2. ...
```

## Notas

- Nunca uses la velocity de un solo sprint para planificar: usa el promedio movil.
- Velocity NO es productividad ni sirve para comparar equipos. Es solo para *forecasting* del propio equipo.
- Si faltan timestamps para cycle time, dilo y trabaja solo con velocity/completion.

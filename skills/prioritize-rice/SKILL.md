---
name: prioritize-rice
description: >
  Prioriza un backlog de features o iniciativas con el modelo RICE
  (Reach x Impact x Confidence / Effort) y produce una tabla ordenada con el razonamiento.
  Usalo cuando el usuario dice "prioriza estas features", "que construyo primero",
  "ordena el backlog", "compara estas iniciativas", "RICE", o pega una lista de ideas
  a rankear. Para SAFe/scrum con Cost of Delay usa WSJF en su lugar.
---

# Priorizacion RICE

Ordena iniciativas de producto por valor esperado usando RICE. Formula y escalas completas
en `../po-copilot/references/frameworks.md`.

`Score = (Reach x Impact x Confidence) / Effort`

## Procedimiento

1. **Reune los items.** Si el usuario los pego, usalos. Si hay un conector MCP (Jira/Linear),
   ofrece traer el backlog priorizable. Necesitas para cada item: nombre + una linea de contexto.

2. **Estima los 4 factores por item.** Para cada uno pide o infiere:
   - **Reach** — numero real de usuarios/eventos afectados en un periodo fijo (definelo: "por trimestre").
   - **Impact** — 3 / 2 / 1 / 0.5 / 0.25 (masivo -> minimo).
   - **Confidence** — 100% / 80% / 50% segun la evidencia detras de Reach e Impact.
   - **Effort** — persona-mes (diseno + dev + QA).

   Cuando no tengas un dato, propone un valor con un supuesto explicito y marca la confianza.
   No inventes precision falsa.

3. **Calcula el Score** y ordena de mayor a menor.

4. **Marca los riesgos.** Cualquier fila con Confidence < 50% se senala como "necesita discovery".
   Items con Effort muy alto y Score medio: sugiere partirlos (ver skill `story-writer` / SPIDR).

5. **Detecta scores inflados por Effort minimo.** Una fila puede quedar alta en el ranking solo
   porque es baratisima (Effort <= 0.5), aun con Impact bajo. Marca esas filas con la nota
   "score alto por bajo Effort, no por valor" y NO las presentes como top de valor: son quick-wins
   oportunistas, no apuestas de impacto. Distingue en la recomendacion "top por valor" de "quick-wins".

6. **Entrega la tabla** en Markdown y un parrafo de "que haria yo": separa el **top por valor**
   (alto Impact x Reach con confianza solida) de los **quick-wins** (score alto por bajo Effort),
   di por que, y que pieza de evidencia falta para subir la confianza del resto.

## Formato de salida

```markdown
## Priorizacion RICE — <fecha>

| # | Feature | Reach | Impact | Confidence | Effort (pm) | Score | Nota |
|---|---------|------:|-------:|-----------:|------------:|------:|------|
| 1 | ...     |  8000 |    2.0 |        80% |         2.0 |  6400 | listo |
| 2 | ...     |  3000 |    3.0 |        50% |         1.5 |  3000 | discovery |
| 3 | ...     |  8000 |   0.25 |       100% |         0.5 |  4000 | score alto por bajo Effort, no por valor |

**Top por valor:** ... (alto Impact x Reach, confianza solida) porque ... .
**Quick-wins (baratos):** ... — hacerlos si sobra capacidad, no como apuesta de impacto.
**Mayor incertidumbre:** ... se resolveria con <evidencia>.
```

## Notas

- Reach es un **numero absoluto**, no una escala. Es el error mas comun.
- Compara Effort en la misma unidad para todos (persona-mes o persona-sprint, no mezclar).
- Si el usuario tiene una North Star definida, alinea el Impact con cuanto mueve esa metrica.

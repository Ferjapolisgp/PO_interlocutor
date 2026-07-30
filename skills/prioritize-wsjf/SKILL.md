---
name: prioritize-wsjf
description: >
  Prioriza features o iniciativas con WSJF (Weighted Shortest Job First) de SAFe:
  Cost of Delay / Job Size. Ideal cuando el equipo trabaja en scrum/SAFe y quiere secuenciar
  por retorno economico del tiempo. Usalo cuando el usuario dice "WSJF", "cost of delay",
  "que hacemos primero por retorno", "secuenciar el PI", "priorizar por SAFe", o quiere
  priorizar considerando urgencia temporal y reduccion de riesgo, no solo impacto. Para una
  priorizacion mas simple por impacto usa prioritize-rice; para satisfaccion usa kano.
---

# Priorizacion WSJF

Secuencia iniciativas por el retorno economico de hacerlas antes. Formula y escala de Fibonacci
en `../po-copilot/references/frameworks.md`.

`WSJF = Cost of Delay / Job Size`
`Cost of Delay = User/Business Value + Time Criticality + Risk Reduction/Opportunity Enablement`

## Cuando usar WSJF vs. RICE

- **WSJF** — cuando importa la **urgencia temporal** y el coste de esperar (SAFe, PI planning,
  features con ventana de mercado o dependencias). Puntua en **columnas** (compara items entre si).
- **RICE** — cuando quieres una estimacion mas absoluta de impacto x alcance. Ver `prioritize-rice`.

## Procedimiento

1. **Reune los items.** Pegados por el usuario o traidos de Jira/Linear via MCP. Necesitas
   nombre + una linea de contexto por item.

2. **Puntua los 3 componentes de Cost of Delay** con la sucesion de Fibonacci relativa
   (1, 2, 3, 5, 8, 13, 20). Clave: puntuar **por columna**, comparando todos los items entre si,
   no fila por fila. En cada columna deberia existir al menos un "1".
   - **User/Business Value** — valor para el usuario o el negocio si se entrega.
   - **Time Criticality** — cuanto decae el valor con el tiempo (deadline, ventana, competidor).
   - **Risk Reduction / Opportunity Enablement (RR|OE)** — cuanto reduce riesgo o habilita futuro.

3. **Suma el Cost of Delay** = Value + Time Criticality + RR|OE.

4. **Puntua Job Size** (esfuerzo) tambien en Fibonacci relativa, por columna.

5. **Calcula WSJF = CoD / Job Size** y ordena de mayor a menor. Los jobs cortos con alto CoD
   ganan: ese es el sesgo intencional del metodo (entregar valor rapido primero).

6. **Entrega la tabla** y una recomendacion de secuencia: que va primero y por que, y donde
   una estimacion floja de Job Size podria cambiar el orden.

## Formato de salida

```markdown
## Priorizacion WSJF — <fecha>

| # | Feature | Business Value | Time Criticality | RR/OE | Cost of Delay | Job Size | WSJF | Nota |
|---|---------|---------------:|-----------------:|------:|--------------:|---------:|-----:|------|
| 1 | ...     |              8 |               13 |     3 |            24 |        3 | 8.0  | urgente |
| 2 | ...     |             13 |                2 |     5 |            20 |        8 | 2.5  |     |

**Secuencia recomendada:** primero ... porque su coste de esperar es alto y el job es corto.
La incertidumbre esta en el Job Size de ..., que si crece bajaria su WSJF.
```

## Notas

- Fibonacci relativa, no valores absolutos: solo importa el orden entre items dentro de cada columna.
- Reestima el WSJF cada PI/iteracion; el Cost of Delay cambia al acercarse deadlines.
- Un WSJF alto por Job Size muy pequeno + CoD bajo NO es prioridad real: revisa que el CoD sea significativo.
- Si el usuario mezcla equipos, calcula WSJF por equipo (el Job Size solo compara dentro del mismo equipo).

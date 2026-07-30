# Referencias de frameworks — PO Analytics

Formulas, escalas y definiciones compartidas por todos los skills del plugin.

## Priorizacion

### RICE
`Score = (Reach x Impact x Confidence) / Effort`

- **Reach** — # de personas/eventos afectados en un periodo definido (p.ej. usuarios/trimestre). Numero real, no escala.
- **Impact** — escala: 3 = masivo, 2 = alto, 1 = medio, 0.5 = bajo, 0.25 = minimo.
- **Confidence** — % de confianza en las estimaciones: 100% = alto, 80% = medio, 50% = bajo. Por debajo de 50% es un "moonshot": pide mas evidencia.
- **Effort** — persona-mes (o persona-sprint). Incluye diseno + dev + QA.

Regla: si Confidence < 50%, marca la fila y sugiere discovery antes de comprometerla.

### WSJF (SAFe)
`WSJF = Cost of Delay / Job Size`
`Cost of Delay = User/Business Value + Time Criticality + Risk Reduction/Opportunity Enablement`

Cada componente se puntua con la sucesion de Fibonacci relativa (1,2,3,5,8,13,20). Se puntua en columnas (comparando features entre si), no en filas.

### ICE
`Score = Impact x Confidence x Ease` — cada uno 1-10. Version rapida de RICE cuando falta data de Reach.

### Kano
Clasifica features por su efecto en la satisfaccion del cliente (no da ranking lineal):

- **Must-be** — su ausencia frustra, su presencia no entusiasma (higiene).
- **Performance** — mas es mejor, linealmente; aqui se compite.
- **Attractive (delighter)** — sorprende y encanta; su ausencia no molesta.
- **Indifferent** — al cliente le da igual; candidata a no construir.
- **Reverse** — su presencia molesta a algunos clientes.

Se mide con dos preguntas por feature (funcional: "como te sentirias SI la tiene" / disfuncional:
"si NO la tiene"), escala: me gusta / la espero / me da igual / la tolero / me disgusta. Se cruzan
en la tabla de evaluacion Kano. Las categorias se degradan con el tiempo (delighter -> performance -> must-be).

## Metricas de producto

### North Star
Una unica metrica que captura el valor entregado al cliente. Debe: (1) reflejar valor al usuario, (2) predecir ingresos a futuro, (3) ser accionable por el equipo. Se descompone en 2-4 **input metrics** (arbol) que el equipo si puede mover.

### AARRR (Pirate Metrics)
Acquisition -> Activation -> Retention -> Revenue -> Referral. Un funnel de ciclo de vida.

### HEART (Google)
Happiness, Engagement, Adoption, Retention, Task success. Para cada dimension: Goals -> Signals -> Metrics.

## Agile / flujo

- **Velocity** — story points completados por sprint. Usar el promedio de los ultimos 3-5, no el ultimo.
- **Burndown** — puntos restantes vs dias. Ideal es una recta descendente; joroba = scope creep o bloqueos.
- **Cycle time** — tiempo desde "in progress" hasta "done" por item. Mediana > promedio (evita outliers).
- **Throughput** — # de items terminados por unidad de tiempo.
- **Salud del sprint** — combinacion de: % de scope completado, cambios de alcance a mitad, WIP, y bloqueos.

## Historias

### INVEST
Independent, Negotiable, Valuable, Estimable, Small, Testable.

### Gherkin
```
Given <contexto>
When <accion>
Then <resultado esperado>
```

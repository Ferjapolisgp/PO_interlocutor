---
description: Prioriza un backlog de features con RICE y devuelve una tabla ordenada.
---

Prioriza con el modelo RICE los items que el usuario indique a continuacion (o, si hay un
conector de backlog disponible como Jira o Linear, ofrece traerlos).

Aplica el skill `prioritize-rice`: estima Reach, Impact, Confidence y Effort para cada item,
calcula el Score, ordena de mayor a menor, marca las filas con Confidence < 50% como
"necesita discovery", y entrega la tabla Markdown con una recomendacion del top 3.

Items / contexto del usuario: $ARGUMENTS

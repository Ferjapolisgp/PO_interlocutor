---
name: prioritize-kano
description: >
  Clasifica features segun el modelo Kano por su efecto en la satisfaccion del cliente:
  basicas (must-be), de desempeno (performance), atractivas (delighters), indiferentes e
  inversas. Usalo cuando el usuario dice "Kano", "que features encantan vs cuales son
  esperadas", "esto emociona a los clientes?", "diferenciadores vs higiene", "clasificar por
  satisfaccion", o quiere decidir el mix de una release entre lo esperado y lo que sorprende.
  Para ordenar por retorno usa prioritize-rice o prioritize-wsjf; Kano decide el balance, no el orden lineal.
---

# Priorizacion Kano

Clasifica features por como afectan la satisfaccion del cliente, para balancear una release entre
lo que se da por hecho, lo que escala con la inversion, y lo que sorprende. Categorias completas
en `../po-copilot/references/frameworks.md`.

## Que resuelve Kano (y que no)

- **Si:** decidir el **mix** de una release — cuanto de higiene (must-be) vs. desempeno vs. delighters.
- **No:** dar un ranking lineal 1..N. Para eso usa `prioritize-rice` o `prioritize-wsjf`.
  Kano y RICE se complementan: Kano dice *que tipo* es cada feature, RICE *en que orden* dentro del tipo.

## Las cinco categorias

- **Must-be (basica)** — su ausencia frustra; su presencia no entusiasma. Higiene. Hay que tenerla.
- **Performance (desempeno)** — mas es mejor, linealmente. Aqui se compite y se justifica precio.
- **Attractive (delighter)** — sorprende y encanta; su ausencia no molesta porque no se esperaba.
- **Indifferent** — al cliente le da igual. Candidata a no construir.
- **Reverse** — presente, molesta a algunos clientes (p.ej. exceso de features/pasos).

Nota temporal: los delighters se erosionan a must-be con el tiempo (lo que hoy encanta, manana se espera).

## Procedimiento

1. **Reune las features** a clasificar (pegadas o traidas de Jira/Linear via MCP).

2. **Clasifica cada una.** Dos vias:
   - **Con datos de encuesta Kano** (ideal): para cada feature se preguntan dos preguntas al
     cliente — funcional ("como te sentirias SI la tiene?") y disfuncional ("como te sentirias
     si NO la tiene?"), cada una en escala: me gusta / la espero / me da igual / la tolero / me disgusta.
     Cruza ambas respuestas en la tabla de evaluacion Kano para asignar categoria. Si el usuario
     pega respuestas, aplicalo; si no, ofrece disenar las dos preguntas por feature.
   - **Sin datos** (heuristico): clasifica por juicio y **marca cada una como hipotesis** a validar.
     Se explicito en que es una estimacion sin evidencia de cliente.

3. **Detecta reverse e indifferent:** senala features candidatas a recortar (no construir o quitar).

4. **Recomienda el mix de la release:** cubre primero todas las must-be (son entrada de mercado),
   invierte en las performance donde compites, e incluye 1-2 delighters para diferenciar. Evita
   gastar en indifferent.

## Formato de salida

```markdown
## Clasificacion Kano — <release / fecha>

| Feature | Categoria | Base (datos/hipotesis) | Accion |
|---|---|---|---|
| Login con SSO | Must-be | datos | incluir: es entrada de mercado |
| Busqueda semantica | Attractive | hipotesis | delighter: diferenciador, validar |
| Tema oscuro | Indifferent | hipotesis | despriorizar |
| Wizard de 6 pasos | Reverse | datos | simplificar: molesta |

**Mix recomendado para la release:**
- Higiene (must-be): ... (obligatorias)
- Desempeno: invertir en ... porque ahi competimos
- Delighters: incluir ... para diferenciar
- Recortar: ...
```

## Notas

- Sin datos de cliente, Kano es opinion disfrazada: marca siempre las clasificaciones heuristicas como hipotesis.
- No sobreinviertas en must-be (rendimiento decreciente) ni descuides los delighters (son el diferenciador).
- Revisa la clasificacion periodicamente: las categorias se degradan (delighter -> performance -> must-be).

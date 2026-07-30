---
name: metrics-north-star
description: >
  Ayuda a definir la North Star Metric de un producto y su arbol de 2-4 input metrics
  accionables. Usalo cuando el usuario dice "cual es nuestra metrica clave", "north star",
  "que deberiamos medir", "metrica guia", "metrica de vanidad vs real", o quiere conectar la
  estrategia con un numero. Para instrumentar los eventos que alimentan estas metricas,
  deriva a product-tracking-skills.
---

# North Star Metric

Define la unica metrica que captura el valor entregado al cliente, y el arbol de input metrics
que el equipo si puede mover semana a semana. Criterios y frameworks complementarios (AARRR,
HEART) en `../po-copilot/references/frameworks.md`.

## Cuando usar este skill vs. otros

- Aqui: **elegir y estructurar** la metrica guia y sus palancas.
- `product-tracking-skills`: **instrumentar** los eventos que alimentan esas metricas.
- `prioritize-rice`: una vez definida la NSM, alinear el Impact de cada feature con cuanto la mueve.

## Procedimiento

1. **Entiende el valor entregado.** Pregunta o infiere del contexto:
   - Que problema resuelve el producto.
   - Cual es el "momento aha": el instante en que el usuario obtiene valor real por primera vez.
   - Como gana dinero el negocio (para que la NSM prediga ingresos, no los ignore).

2. **Filtra metricas de vanidad.** Descarta las que suben sin reflejar valor: registros totales,
   pageviews, descargas, usuarios acumulados. Una buena NSM baja si el producto empeora.

3. **Propon 2-3 candidatas.** Cada una debe pasar las tres pruebas:
   - **Valor al usuario** — sube cuando el cliente obtiene mas valor.
   - **Predice ingresos** — su crecimiento anticipa revenue futuro.
   - **Accionable** — el equipo puede influirla con su trabajo.

   Presenta las candidatas en una tabla marcando como cumple/falla cada prueba.

4. **Elige una con el usuario** y justifica por que sobre las otras. Una sola NSM; el resto son inputs.

5. **Descompon en 2-4 input metrics** (el arbol). Son las palancas concretas. Una plantilla util
   es multiplicar los factores del negocio, p.ej.:
   `NSM = (usuarios activos) x (frecuencia de la accion de valor) x (tasa de exito)`.

6. **Da la definicion operativa** de cada metrica: como se calcula, sobre que ventana temporal,
   que evento la dispara. Esto es lo que hace la NSM medible y no un eslogan.

## Ejemplos por tipo de producto

| Producto | North Star | Input metrics |
|---|---|---|
| SaaS B2B (colaboracion) | Cuentas que realizan la accion de valor semanalmente (WAA) | Activacion en onboarding, # de acciones/usuario, retencion de cuenta |
| Marketplace | Transacciones completadas | Compradores activos, frecuencia de compra, conversion de busqueda, retencion de vendedores |
| Contenido / media | Tiempo de contenido consumido con intencion | DAU, sesiones/usuario, minutos/sesion, retencion D30 |
| Fintech | Volumen transaccionado por usuario activo | Usuarios que fondean, # de transacciones, ticket promedio, retencion |
| Freemium PLG | Usuarios que alcanzan el momento aha | Signups activados, time-to-value, conversion a pago |

## Formato de salida

```markdown
## North Star — <producto>

**NSM:** <metrica> — <definicion operativa (calculo + ventana temporal)>
**Momento aha:** <cuando el usuario obtiene valor por primera vez>
**Por que esta y no otra:** <justificacion frente a las candidatas descartadas>

### Candidatas evaluadas
| Candidata | Valor al usuario | Predice ingresos | Accionable | Veredicto |
|---|---|---|---|---|
| ... | si | si | parcial | descartada: poco accionable |

### Arbol de input metrics
- **Input 1:** <metrica> — palanca: <como la mueve el equipo>
- **Input 2:** ...
- **Input 3:** ...

### Anti-metricas (vanidad a evitar)
- <metrica de vanidad> — por que enganya
```

## Notas

- Una sola NSM por producto. Si el equipo pide dos, casi siempre una es realmente un input.
- Evita metricas que el equipo no puede mover (p.ej. "cotizacion de la accion").
- Revalida la NSM cuando cambie la estrategia; no es para siempre.
- Si el usuario ya tiene datos en Amplitude/Mixpanel via MCP, ofrece medir el valor actual de la NSM y sus inputs.

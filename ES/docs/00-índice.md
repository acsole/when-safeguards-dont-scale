# Método de trabajo con IA

> Documento canónico. Audiencia: externo-primero (didáctico para terceros, con
> notas internas donde haga falta). Se construye módulo por módulo siguiendo el
> blueprint en [`work-orders/metodo-de-trabajo.md`](../work-orders/metodo-de-trabajo.md).
> Cada módulo pasa por el ciclo: redacción (modelo económico) → revisión (revisor
> independiente) → evaluación y consolidación (director + autoridad humana).
>
> **Estado:** DOCUMENTO COMPLETO — los 9 módulos (M1-M9) consolidados.

---

## Los nueve módulos

| # | Módulo | De qué trata |
|---|--------|--------------|
| 1 | [Visión y propósito](01-vision-y-proposito.md) | Qué problema resuelve el método y por qué existe |
| 2 | [Roles y responsabilidades](02-roles-y-responsabilidades.md) | Los cuatro roles, sus límites de autoridad, y el aseguramiento proporcional a la severidad |
| 3 | [El ciclo de producción](03-ciclo-de-produccion.md) | La secuencia operativa de una tarea, de esqueleto a consolidación |
| 4 | [Memoria persistente](04-memoria-persistente.md) | Cómo se conserva el contexto entre sesiones, y en qué se diferencia del versionado |
| 5 | [Reglas de atomicidad](05-reglas-de-atomicidad.md) | Qué hace atómica a una tarea, y la ficha de encargo como herramienta |
| 6 | [Industrialización](06-industrializacion.md) | Cuándo y cómo automatizar lo repetido: hook, skill o subagente |
| 7 | [Casos de uso](07-casos-de-uso.md) | El método aplicado, con sus resultados y sus lecciones |
| 8 | [Límites](08-limites.md) | Cuándo NO usar el método, sus costos y los supuestos que lo sostienen |
| 9 | [Trazabilidad y reversibilidad](09-trazabilidad-y-reversibilidad.md) | Las cuatro capas: Prevención, Contención, Detección, Recuperación |

**Complemento:** [Aplicabilidad a verticales](10-aplicabilidad-a-verticales.md) mapea el
método a marketing, inmobiliaria e IT, y trae una plantilla para adaptarlo a cualquier sector.

## Orden de lectura sugerido

Si venís sin contexto: **1 → 2 → 5 → 3**. Primero el porqué y los roles, después la
atomicidad, y recién entonces el ciclo que la usa.

Si venís a implementarlo: **2 → 5 → 9**, y de ahí directo a
[la guía de instalación](../install/guia-instalacion.md) y a
[las plantillas](../templates/).

Si venís a evaluar si el método aguanta: **8 → [incident log](../incident-log/) → 9**. Los
límites primero, después los fallos reales, y al final las capas que los contienen.

## Dónde está el resto

- [`incident-log/`](../incident-log/) — los fallos que el propio método atrapó mientras se
  documentaba a sí mismo, incluidos los de sus capas superiores.
- [`work-orders/`](../work-orders/) — las fichas de encargo reales que produjeron esta
  documentación. Sirven de evidencia y de ejemplo trabajado.
- [`install/`](../install/) — la guía de adopción paso a paso.
- [`templates/`](../templates/) — los esqueletos copiables de cada pieza.

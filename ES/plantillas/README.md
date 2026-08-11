# Plantillas copiables

Las cinco piezas que instalan el andamiaje, más la ficha de encargo que lo pone en marcha.
Cada plantilla es un esqueleto para copiar, completar y usar.

## El mapa de las piezas

| Pieza | Qué repetición elimina | Cuándo se dispara | Dónde vive |
|---|---|---|---|
| [Contexto base](CLAUDE.md) | Re-explicar el proyecto en cada sesión | Al iniciar cada sesión | En la **raíz** del proyecto |
| [Memoria persistente](memoria.md) | Reconstruir lo ya decidido | Al consultar el índice | Carpeta de memoria, índice + archivos atómicos |
| [Skill](SKILL.md) | Repetir un cuerpo de convenciones | Por coincidencia de contexto | Carpeta de skills |
| [Subagente](subagente.md) | Re-pegar el preámbulo al delegar | Al delegar una tarea | Carpeta de subagentes |
| [Hook](hook.md) | Verificar a mano una regla dura | Ante un evento (pre o post) | Script + registro en la configuración |

No son alternativas: son **capas que se complementan**. Un subagente ejecutor puede aplicar
una skill de convenciones y tener sus cambios verificados por un hook. Los tres a la vez, cada
uno en su rol.

Y transversal a todas, la herramienta que acota el trabajo:
**[la ficha de encargo](ficha-de-encargo.md)**.

## Cuál elegir

| Síntoma | Pieza |
|---|---|
| "Repito el mismo contexto cada vez que delego" | Subagente |
| "Hay convenciones que aplico siempre" | Skill |
| "Esta regla objetiva NUNCA debe romperse" | Hook |
| "Se pierde lo que decidimos la sesión pasada" | Memoria |
| "Tengo que explicar el proyecto de nuevo" | Contexto base |

**Cuándo instalar una pieza nueva:** después de dos o tres ciclos en que la misma repetición
aparece. Antes es prematuro; después es ineficiencia acumulada.

---

## Checklist de verificación

El andamiaje no está instalado hasta que lo veas activarse solo. Abrí una **sesión nueva** y
verificá pieza por pieza. El principio es el mismo que rige el método: **verificar, no
confiar.**

- [ ] **Contexto base.** Preguntá por una restricción que solo esté escrita ahí. ¿La responde
      sin que se la pegues?
- [ ] **Memoria.** Preguntá por una decisión tomada en otra conversación. ¿La recupera?
- [ ] **Skill.** Trabajá en su contexto sin nombrarla. ¿Aplica sus convenciones sola?
- [ ] **Subagente.** Delegale algo sin explicarle las convenciones. ¿Las respeta igual?
- [ ] **Hook.** Intentá la violación a propósito. ¿Frena de verdad?

Un casillero que no podés tildar es una pieza que **no está instalada**, por más que el
archivo exista. Y probar en condiciones reales revela fallos que el diseño no anticipa: en un
proyecto propio, la prueba en vivo destapó dos errores que la revisión estática había dado
por buenos.

## Requisitos previos

Antes de instalar nada, verificá que se cumplan los tres. Si falta alguno, el método no aplica
en tu contexto actual y solo va a ralentizarte.

- [ ] Acceso a **tres modelos de capacidad diferenciada**: uno que dirija, uno que revise, uno
      económico que ejecute.
- [ ] Un entorno que soporte **contexto base automático, skills, subagentes y hooks**.
- [ ] Un **sistema de control de versiones** activo, que es la capa de Recuperación.

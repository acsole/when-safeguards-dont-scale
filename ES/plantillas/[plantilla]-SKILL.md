# Plantilla: skill auto-activable

> **Qué hace.** Encapsula un cuerpo de conocimiento o de convenciones que se aplica una y
> otra vez, para no repetir el mismo preámbulo en cada conversación.
>
> **Cuándo elegirla.** Cuando el síntoma es *"hay un cuerpo de convenciones que aplico
> siempre"*. Si el síntoma es una regla objetiva que nunca debe romperse, eso es un
> [hook](hook.js). Si es contexto que se repite al delegar, eso es un
> [subagente](subagente.md). Ver [`docs/06-industrializacion.md`](../docs/06-industrializacion.md).
>
> **La skill se CARGA, no se entrena.** Es un archivo que se lee cuando el contexto coincide
> con sus disparadores.
>
> **Cómo verificar que se auto-activó.** Trabajá en el contexto que debería dispararla, sin
> nombrarla. Si aplica sus convenciones sola, la pieza está viva.

---

## El campo decisivo es `description`

La skill se activa por coincidencia de contexto contra su `description`. Una descripción
pobre no dispara nunca, por buena que sea la skill.

Una `description` bien escrita responde tres cosas: **qué** contiene, **cuándo** usarla, y con
**qué frases o situaciones** se dispara. Escribí los disparadores como los diría un usuario
real, no como los nombrarías vos internamente.

---

## Plantilla

```markdown
---
name: <slug-en-kebab-case>
description: <Qué es esta skill y qué resuelve.> Usá esta skill SIEMPRE que <situación
  concreta 1>, <situación 2> o <situación 3>. Activala también cuando aparezcan las palabras
  "<disparador>", "<disparador>", "<disparador>", o cuando <otra skill> necesite <X>.
---

# <Título>

**Alcance:** <a qué proyectos o tareas aplica, y a cuáles explícitamente no>

## 1. <El principio rector>

<Lo que no se negocia. Si hay una sola cosa que alguien debe llevarse, va acá.>

## 2. <Las reglas>

- <Regla concreta y verificable>
- <Regla concreta y verificable>

## 3. Lo que funciona y lo que no

**FUNCIONA:**
- <Práctica validada, con su porqué>

**NO FUNCIONA:**
- <Anti-patrón observado, con su consecuencia real>

## HISTORIAL DE VERSIONES

| Versión | Fecha | Cambios |
|---------|-------|---------|
| 1.0 | AAAA-MM-DD | Versión inicial. |
```

---

## Dos consejos que salen de fallos reales

**Poné el historial de versiones.** Una skill sin versión no se puede corregir con confianza:
nadie sabe si lo que está leyendo es lo acordado o un resto de una iteración anterior.

**Separá el registro de aprendizajes de la skill misma.** Un `LEARNING-LOG.md` al lado
acumula los casos que justificaron cada cambio. La skill dice qué hacer; el log dice por qué.

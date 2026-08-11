# Plantilla: memoria persistente

> **Qué hace.** Da continuidad entre sesiones. El modelo arranca cada conversación sin
> recuerdo de la anterior; la memoria cierra ese hueco con el contexto vivo del proyecto.
>
> **Cómo verificar que se usa.** Abrí una sesión nueva y preguntá por una decisión tomada en
> otra conversación. Si la recupera sin que se la cuentes, la pieza está viva.
>
> **Qué NO guardar:** lo que ya vive en el código o en el repositorio, el historial de
> versiones (eso es del control de versiones), y lo efímero de una charla puntual.
>
> Base conceptual: [`docs/04-memoria-persistente.md`](../docs/04-memoria-persistente.md).

La memoria se organiza como un **índice** más una colección de **archivos atómicos**
enlazados entre sí. Un tema por archivo.

---

## Plantilla del índice

```markdown
# MEMORY INDEX — [Proyecto]

- [nombre-del-archivo.md](nombre-del-archivo.md) — [una línea de qué contiene, escrita para
  decidir si conviene abrirlo o no]
- [otro-archivo.md](otro-archivo.md) — [...]
```

El índice es un mapa, no un resumen. Cada línea existe para que quien lo lea pueda decidir si
necesita abrir ese archivo. Si la línea no permite decidir, está mal escrita.

---

## Plantilla de un archivo de memoria

```markdown
---
name: <slug-en-kebab-case>
description: <una línea; es lo que se lee para decidir si este archivo es relevante>
metadata:
  type: user | feedback | project | reference
---

<El hecho. Para feedback y project, seguir con el porqué y con cómo aplicarlo.>

Relacionado: [[otro-archivo]], [[y-otro]]
```

## Los cuatro tipos

| Tipo | Contenido | Para qué |
|---|---|---|
| **user** | Rol, preferencias, historia, quién es la persona | Personalizar el tono, entender intenciones, respetar límites |
| **feedback** | Correcciones y acuerdos sobre cómo debe trabajar la IA, con su porqué | Refinar el comportamiento sin repetir el mismo error |
| **project** | Metas vigentes, restricciones no derivables del código, decisiones clave | Mantener alineación y evitar retrocesos |
| **reference** | URLs, tableros, tickets, documentos externos | Acceso rápido sin buscar |

## Reglas que evitan los dos fallos más comunes

**Actualizar el índice cuando se actualiza el archivo.** Un archivo corregido con su línea de
índice sin corregir es peor que no haberlo tocado: la próxima sesión lee el resumen viejo y
arranca con la premisa equivocada.

**Convertir fechas relativas en absolutas.** "La semana que viene" no significa nada dentro
de tres meses. Escribí la fecha.

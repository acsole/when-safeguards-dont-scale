# Guía de instalación del método — Fichas de encargo (blueprint)

> **Qué es este archivo.** El *blueprint* del entregable **(B)**: una **guía de
> adopción e instalación paso a paso** del método de trabajo. Una vez instalado en
> un proyecto con IA, el *andamiaje* (roles, fichas, revisión, trazabilidad,
> memoria) se activa **solo en cada sesión nueva, sin re-setup**; las aprobaciones
> humanas siguen vigentes. Cada ficha define una tarea **atómica** de redacción;
> el ejecutor (Haiku 4.5) redacta **una** sección por ficha, el revisor
> (quality-guardian) la audita contra el "Criterio de listo", y Opus + Human-in-the-Loop
> consolidan y commitean. Mismo pipeline de dogfooding que produjo el canónico.
>
>
> **Insumo común a todas las fichas:** el documento canónico
> [`metodo-de-trabajo.md`](metodo-de-trabajo.md) (sobre todo M4 Memoria, M6
> Industrialización, M9 Trazabilidad).

---

## Plantilla de ficha

| Campo | Función |
|---|---|
| **Propósito** | El "para qué" en una línea |
| **Extensión objetivo** | Rango de palabras |
| **Preguntas que debe responder** | Guían el contenido sin escribirlo |
| **Debe contener** | Checklist de puntos a cubrir (no prosa cerrada) |
| **NO debe tocar** | Fronteras explícitas → evita que dos secciones se pisen |
| **Ancla / ejemplo real** | Caso concreto a citar (verdad-base ASLAN) |
| **Plantilla a incluir** | Esqueleto copiable que la sección debe entregar (si aplica) |
| **Errores a evitar** | Lista negativa de anti-patrones |
| **Términos clave** | Mini-glosario para coherencia entre secciones |
| **Criterio de listo** | Vara de revisión |

**Orden de redacción sugerido:** F1→F2→F3→F4→F5→F6→F7→F8→F9→F10→F11→F12.
F4–F8 (instalación pieza por pieza) comparten estructura interna fija:
*qué hace · dónde vive · cómo verificar que se activó sola · plantilla copiable*.

---

## Ficha 1 — Qué instala y qué garantiza

- **Propósito:** Que un recién llegado entienda en una pasada qué deja instalado la guía y qué promete (y qué NO promete).
- **Extensión:** 250–350 palabras.
- **Preguntas que debe responder:**
  1. ¿Qué significa "out-of-the-box en automático" aquí? (el andamiaje se auto-activa por sesión; no hay re-setup manual)
  2. ¿Qué sigue siendo humano? (las aprobaciones; el juicio) → anti-promesa explícita: NO es IA autónoma.
  3. ¿Cuáles son las 5 piezas, nombradas sin desarrollar?
- **Debe contener:** la promesa honesta en 1–2 frases; la distinción *andamiaje automático ≠ decisiones automáticas*; lista de las 5 piezas (CLAUDE.md raíz, memoria, skills, subagentes, hooks) como adelanto.
- **NO debe tocar:** el cómo instalar cada pieza → F4–F8; requisitos → F2; el detalle de qué queda humano → F10.
- **Ancla:** referencia a que estas 5 piezas ya corren juntas en un proyecto real (ASLAN) sin re-setup entre sesiones.
- **Errores a evitar:** prometer autonomía; vender que elimina la supervisión; tono de folleto.
- **Términos clave:** *andamiaje*, *out-of-the-box*, *auto-activación por sesión*, *autoridad humana*.
- **Criterio de listo:** el lector sabe qué tendrá funcionando y qué seguirá decidiendo él.

## Ficha 2 — Requisitos previos

- **Propósito:** Enumerar lo que el proyecto debe tener antes de instalar, para no fallar a mitad de camino.
- **Extensión:** 200–300 palabras.
- **Preguntas que debe responder:**
  1. ¿Qué capacidades de IA hacen falta? (tres ROLES distinguibles: director, ejecutor/revisor, redactor económico)
  2. ¿Qué herramienta/entorno? (uno que soporte cargar contexto base, skills, subagentes y hooks)
  3. ¿Qué infraestructura mínima? (repo de control de versiones para la capa de Recuperación, M9)
- **Debe contener:** checklist verificable de prerrequisitos; nota de que si faltan, el método no aplica (remite a M8). **AJUSTE (2026-06-24): rol ≠ modelo — son sombreros, no modelos distintos; existe una versión REDUCIDA con un solo modelo (produce en una pasada, revisa en otra). El acceso a varios modelos gradúa el rigor pero NO bloquea el arranque; los requisitos DUROS son el entorno y el control de versiones. No presentar "3 modelos" como condición absoluta ("no aplica").**
- **NO debe tocar:** la instalación en sí → F4–F8; los límites conceptuales del método → ya están en M8 (solo remitir).
- **Ancla:** ASLAN cumple los tres (modelos diferenciados, Claude Code, repo git local).
- **Errores a evitar:** asumir herramientas específicas en el cuerpo genérico (eso va al Apéndice F12); dar por obvio el repo git.
- **Términos clave:** *capacidad diferenciada*, *control de versiones*, *entorno con hooks/skills/subagentes*.
- **Criterio de listo:** el lector puede marcar una casilla por requisito antes de empezar.

## Ficha 3 — Mapa de las 5 piezas

- **Propósito:** Dar una tabla-mapa que conecte cada pieza con la repetición que automatiza y cuándo se dispara.
- **Extensión:** 250–350 palabras + tabla.
- **Preguntas que debe responder:**
  1. ¿Qué repetición elimina cada pieza?
  2. ¿Cuándo se activa cada una (al iniciar sesión / por contexto / ante un evento / al delegar)?
  3. ¿Dónde vive cada pieza?
- **Debe contener:** una tabla con columnas *Pieza · Qué automatiza · Cuándo se dispara · Dónde vive*; una frase sobre que las piezas se complementan en capas (no son excluyentes); **una aclaración breve (ajuste 2026-06-24): las 5 piezas son el ANDAMIAJE (organización del trabajo), no dependen de cuántos modelos tengas — eso es cuestión aparte, la de Requisitos (F2). Los ROLES (director/ejecutor/revisor) son "sombreros" o funciones, NO modelos distintos: un mismo modelo puede vestir varios en pasadas separadas (versión reducida). Remitir a F2, sin desarrollar.**
- **NO debe tocar:** las plantillas e instrucciones detalladas → F4–F8; el cuadro de decisión hook/skill/subagente de M6 (citar, no reproducir entero); el detalle de los requisitos de modelos → F2 (solo remitir).
- **Ancla:** espejo del cuadro de decisión de M6 (síntoma → herramienta).
- **Plantilla a incluir:** la tabla-mapa de 5 filas.
- **Errores a evitar:** duplicar el contenido de F4–F8; presentar las piezas como alternativas en vez de capas; **dar a entender que hace falta más de un modelo para usar el andamiaje (confusión frecuente: la persona externa no-técnica creyó que "roles" = "varios modelos").**
- **Términos clave:** *auto-carga*, *auto-activación*, *enforcement*, *precarga de contexto*, *rol ≠ modelo*, *andamiaje*.
- **Criterio de listo:** de un vistazo se entiende qué hace cada pieza y cuándo entra; y queda claro que el andamiaje no exige múltiples modelos.

## Ficha 4 — Instalación: contexto base del proyecto (`CLAUDE.md` en la raíz)

- **Propósito:** Instalar el archivo de contexto que se auto-carga al iniciar cada sesión (invariantes, reglas, restricciones).
- **Extensión:** 300–400 palabras + plantilla.
- **Preguntas que debe responder:** ¿qué hace? ¿dónde vive? ¿cómo verifico que se cargó sola? ¿qué pongo dentro?
- **Debe contener:** las cuatro sub-partes fijas (qué hace · dónde vive · cómo verificar · plantilla); explicación de que va en la RAÍZ del proyecto para auto-cargarse; qué tipo de contenido entra (objetivo, restricciones innegociables, modo de trabajo).
- **NO debe tocar:** memoria persistente → F5 (CLAUDE.md es estático del proyecto, la memoria es viva entre sesiones); detalle de skills/subagentes → F6/F7.
- **Ancla:** un `CLAUDE.md` real de un proyecto (objetivo + restricciones innegociables + modo de trabajo).
- **Plantilla a incluir:** un `CLAUDE.md` base copiable con secciones: Objetivo, Stack/contexto, Restricciones innegociables, Modo de trabajo (aprobación humana).
- **Errores a evitar:** confundir CLAUDE.md (estático) con memoria (viva); plantilla atada a un dominio concreto.
- **Términos clave:** *auto-carga al iniciar sesión*, *invariantes*, *restricciones innegociables*.
- **Criterio de listo:** el lector copia la plantilla, la rellena y la pieza queda funcional.

## Ficha 5 — Instalación: memoria persistente (`MEMORY.md` + archivos)

- **Propósito:** Instalar la memoria que da continuidad entre sesiones (índice + archivos atómicos).
- **Extensión:** 300–400 palabras + plantilla.
- **Preguntas que debe responder:** ¿qué hace? ¿dónde vive? ¿cómo verifico que la IA la consulta? ¿qué estructura tiene?
- **Debe contener:** las cuatro sub-partes fijas; la estructura índice + archivos temáticos; los cuatro tipos (user/feedback/project/reference, remite a M4); qué guardar y qué no (remite a M4).
- **NO debe tocar:** la teoría completa de memoria → ya está en M4 (solo remitir y dar el cómo-instalar); versionado/git → F8/M9.
- **Ancla:** el `MEMORY.md` real del ecosistema (índice con punteros: documento maestro, proyectos paralelos, sesiones pendientes, principios de método).
- **Plantilla a incluir:** un `MEMORY.md` índice copiable + plantilla de archivo de memoria con frontmatter (name/description/type) y cuerpo con enlaces `[[...]]`.
- **Errores a evitar:** repetir la teoría de M4 en vez de instruir la instalación; guardar en memoria cosas que ya viven en el código (anti-patrón de M4).
- **Términos clave:** *índice de memoria*, *archivo atómico*, *frontmatter*, *continuidad entre sesiones*.
- **Criterio de listo:** el lector crea su índice y su primer archivo de memoria siguiendo la plantilla.

## Ficha 6 — Instalación: skills auto-activables

- **Propósito:** Instalar skills que la IA invoca sola por contexto (convenciones del proyecto + el método como skill).
- **Extensión:** 300–400 palabras + plantilla.
- **Preguntas que debe responder:** ¿qué hace? ¿dónde vive? ¿cómo verifico que se auto-activó? ¿qué hace que se dispare sola?
- **Debe contener:** las cuatro sub-partes fijas; el rol decisivo del campo `description`/disparadores (la skill se activa por coincidencia de contexto, no se "entrena"); dos skills recomendadas: convenciones del proyecto y el propio método.
- **NO debe tocar:** subagentes → F7; hooks → F8; la teoría de cuándo industrializar → M6 (remitir).
- **Ancla:** dos skills reales de un proyecto (una con las convenciones técnicas+diseño; otra con el propio método), auto-activadas por sus disparadores.
- **Plantilla a incluir:** un `SKILL.md` copiable: frontmatter con `name` + `description` rica en disparadores (frases que activan), y cuerpo con el conocimiento/convenciones.
- **Errores a evitar:** decir que la skill "se entrena" (se CARGA, verdad-base anti-fabricación); `description` pobre que no dispara.
- **Términos clave:** *auto-activación por contexto*, *disparadores (triggers)*, *la skill se carga, no se entrena*.
- **Criterio de listo:** el lector escribe una skill cuyo `description` la hace activarse sola en el contexto correcto.

## Ficha 7 — Instalación: subagentes precargados

- **Propósito:** Instalar subagentes con rol y contexto precargado (ejecutor con invariantes + revisor `quality-guardian`).
- **Extensión:** 300–400 palabras + plantilla.
- **Preguntas que debe responder:** ¿qué hace? ¿dónde vive? ¿cómo verifico que trae el contexto sin re-pegarlo? ¿qué configuro?
- **Debe contener:** las cuatro sub-partes fijas; los dos subagentes núcleo (ejecutor con invariantes; revisor independiente de calidad); cómo el subagente elimina el re-pegado del preámbulo (remite a M2 roles y M6 subagente).
- **NO debe tocar:** skills → F6; hooks → F8; la teoría de roles → M2 (remitir).
- **Ancla:** dos subagentes reales de un proyecto: un ejecutor (con invariantes precargadas) y un revisor independiente.
- **Plantilla a incluir:** un `.md` de subagente copiable: frontmatter (name, description, tools, model) + cuerpo con rol, invariantes y regla dura "devuelve contenido, no persiste".
- **Errores a evitar:** que el ejecutor persista archivos (rompe la capa de Prevención de M9); revisor = ejecutor (deben ser independientes, M2).
- **Términos clave:** *precarga de contexto*, *ejecutor*, *revisor independiente*, *revisor un nivel sobre el ejecutor*.
- **Criterio de listo:** el lector crea un subagente ejecutor y uno revisor sin re-pegar preámbulos.

## Ficha 8 — Instalación: hooks de enforcement

- **Propósito:** Instalar hooks deterministas que fuerzan reglas y bloquean violaciones sin intervención.
- **Extensión:** 300–400 palabras + plantilla.
- **Preguntas que debe responder:** ¿qué hace? ¿dónde vive? ¿cómo verifico que bloquea de verdad? ¿qué regla automatizo primero?
- **Debe contener:** las cuatro sub-partes fijas; la distinción pre-evento (PreToolUse, bloquea antes) vs post-evento (PostToolUse, valida después); que los hooks son para reglas objetivas que NUNCA deben romperse (remite a M6); su rol como capa de Detección/Recuperación (remite a M9).
- **NO debe tocar:** la sintaxis exacta de registro en `settings.json` → Apéndice F12 (cuerpo es genérico); skills/subagentes → F6/F7.
- **Ancla:** dos hooks reales de un proyecto: uno de enforcement (bloquea patrones que violan las invariantes) y uno de telemetría (siempre exit 0, nunca bloquea).
- **Plantilla a incluir:** un esqueleto de hook copiable (lee evento por stdin, evalúa regla, exit 2 = bloquea / exit 0 = permite) — genérico, con la wiring concreta remitida al Apéndice.
- **Errores a evitar:** hook que bloquea por falso positivo (ej. coincidir dentro de comentarios — lección real de ASLAN); poner reglas subjetivas en un hook (eso es skill).
- **Términos clave:** *enforcement*, *determinista*, *PreToolUse/PostToolUse*, *exit code de bloqueo*.
- **Criterio de listo:** el lector instala un hook que bloquea una violación objetiva en una prueba real.

## Ficha 9 — Verificación de la instalación

- **Propósito:** Dar una checklist para confirmar, en una sesión nueva, que cada pieza se activa sola.
- **Extensión:** 250–350 palabras + checklist.
- **Preguntas que debe responder:**
  1. ¿Cómo confirmo que CLAUDE.md se auto-cargó?
  2. ¿Cómo confirmo que una skill se auto-activó por contexto?
  3. ¿Cómo confirmo que un subagente trae su contexto?
  4. ¿Cómo confirmo que un hook bloquea de verdad?
  5. ¿Cómo confirmo que la memoria da continuidad?
- **Debe contener:** una checklist accionable (abrir sesión fresca → observar señal de cada pieza); la idea de "verificar, no confiar" aplicada a la instalación (M3).
- **NO debe tocar:** la instalación → F4–F8 (esto solo verifica); mantenimiento → F11.
- **Ancla:** en ASLAN, una prueba en producción reveló y corrigió 2 bugs (identidades que colisionaban; elementos que no expiraban) — verificar en vivo atrapa lo que el diseño no anticipa (M7).
- **Plantilla a incluir:** la checklist de verificación (una casilla por pieza).
- **Errores a evitar:** dar por instalada una pieza sin observarla activarse; checklist no verificable ("debería funcionar").
- **Términos clave:** *verificar, no confiar*, *sesión fresca*, *señal de activación*.
- **Criterio de listo:** el lector recorre la checklist y sabe si la instalación quedó viva.

## Ficha 10 — Qué sigue siendo humano

- **Propósito:** Delimitar con honestidad qué NO se automatiza, para no prometer autonomía.
- **Extensión:** 200–300 palabras.
- **Preguntas que debe responder:**
  1. ¿Qué decisiones siguen requiriendo aprobación humana? (consolidar, publicar, decisiones de riesgo)
  2. ¿Por qué se preserva ese control? (autoridad humana, M2; restricción de aprobación previa)
- **Debe contener:** lista de los checkpoints humanos que el andamiaje NO reemplaza; la frase clave: se automatiza el armado, no el juicio; remite a M8 (límites) y M2 (autoridad humana).
- **NO debe tocar:** los pasos de instalación → F4–F8; la verificación → F9.
- **Ancla:** la restricción de "toda acción planificada y aprobada por el humano antes de ejecutar" como contrato no negociable.
- **Errores a evitar:** sugerir que con todo instalado la IA decide sola; minimizar el rol humano.
- **Términos clave:** *autoridad humana*, *aprobación previa*, *armado automático ≠ juicio automático*.
- **Criterio de listo:** queda inequívoco qué decide el humano aun con todo instalado.

## Ficha 11 — Mantenimiento: cuándo sumar una pieza nueva

- **Propósito:** Enseñar a hacer crecer el andamiaje aplicando el checkpoint de industrialización de forma recurrente.
- **Extensión:** 200–300 palabras.
- **Preguntas que debe responder:**
  1. ¿Cómo detecto que una repetición nueva merece automatizarse? (2–3 ciclos, M6)
  2. ¿Qué pieza elijo según el síntoma? (contexto repetido→subagente; convención→skill; regla dura→hook)
- **Debe contener:** el criterio de "2–3 ciclos antes de industrializar" (ni prematuro ni tardío, M6); el checkpoint recurrente (M3); remisión a la tabla de decisión de M6.
- **NO debe tocar:** reproducir entera la tabla de M6 (remitir); la instalación inicial → F4–F8.
- **Ancla:** en ASLAN, un fallo recurrente y predecible (nombre propio interno) se identificó como candidato a hook — el dogfooding alimenta la mejora del propio andamiaje.
- **Errores a evitar:** industrializar al primer ciclo (prematuro); esperar a que el caos crezca (tardío).
- **Términos clave:** *checkpoint de automatización*, *2–3 ciclos*, *síntoma → herramienta*.
- **Criterio de listo:** el lector sabe reconocer y elegir la próxima pieza a instalar.

## Ficha 12 — Apéndice: materialización en Claude Code

- **Propósito:** Aterrizar las 5 piezas genéricas en la herramienta concreta (Claude Code), con la wiring real.
- **Extensión:** 350–500 palabras + plantillas concretas.
- **Preguntas que debe responder:**
  1. ¿Dónde van físicamente cada pieza en Claude Code? (`CLAUDE.md` raíz, `.claude/skills/`, subagentes, hooks, `settings.json`)
  2. ¿Cómo se registra un hook en `settings.json` (matcher PostToolUse/PreToolUse)?
  3. ¿Cómo se invoca un subagente y cómo se auto-activa una skill?
- **Debe contener:** la correspondencia pieza-genérica → ubicación-Claude-Code; el bloque de registro de hook en `settings.json` (matcher Edit|Write, command); nota de que los hooks suelen activarse al iniciar sesión nueva; convención de hook (stdin del evento, tolerar BOM, exit 2 bloquea / exit 0 permite).
- **NO debe tocar:** la teoría genérica de cada pieza → F4–F8 (aquí solo la materialización); no re-explicar para qué sirve cada pieza.
- **Ancla:** las piezas reales de un proyecto en la carpeta de configuración del entorno (subagentes ejecutor/revisor, una skill de convenciones, hooks de enforcement/telemetría registrados en `settings.json`).
- **Plantilla a incluir:** bloque `settings.json` copiable (registro de un hook PostToolUse) + estructura de carpetas `.claude/` + frontmatter real de subagente y de skill.
- **Errores a evitar:** mezclar la materialización en el cuerpo genérico; inventar rutas o sintaxis (usar las verificadas de ASLAN como verdad-base).
- **Términos clave:** `.claude/`, `settings.json`, *matcher*, *PostToolUse/PreToolUse*, *exit 2*.
- **Criterio de listo:** un usuario de Claude Code copia el apéndice y deja las 5 piezas operativas.

---

## Pipeline de producción (recordatorio operativo)

Por cada ficha: **redacción** vía subagente
general-purpose con `model=haiku`, prompt autocontenido con la ficha + la
verdad-base ASLAN + regla dura "devuelve contenido, no escribas archivos" →
**revisión** con `quality-guardian` (Sonnet) campo por campo → corrección si hay
hallazgos → **consolidación** por Opus en `guia-instalacion.md` + commit. Toda
captura del revisor se vuelca a una bitácora de dogfooding (convención del
proyecto). Si una re-auditoría reincide en 🔴 bloqueante, escala a ejecutor
Sonnet 4.6 + auditor Opus (aseguramiento proporcional a la severidad).

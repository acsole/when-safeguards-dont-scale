# Método de trabajo — Fichas de encargo (work order para redacción modular)

> **Qué es este archivo.** El *blueprint* del documento "Método de trabajo con IA".
> Cada ficha define una tarea **atómica** de redacción: su alcance, sus fronteras
> y su criterio de aceptación. El ejecutor (Haiku 4.5) redacta **un** módulo por
> ficha; el revisor (Sonnet 4.6 / quality-guardian) lo evalúa contra el
> "Criterio de listo"; Opus + Human-in-the-Loop consolidan.
>
> **Decisiones marco (2026-06-22):** audiencia *externo-primero*; salida final =
> un solo `.md` canónico; principio central = evaluación constante de qué
> automatizar (hooks/skills/subagentes). Regla dura: el ejecutor **devuelve
> contenido, no persiste**; el humano/director consolida.

---

## Plantilla de ficha

| Campo | Función |
|---|---|
| **Propósito** | El "para qué" en una línea |
| **Extensión objetivo** | Rango de palabras |
| **Preguntas que debe responder** | Guían el contenido sin escribirlo |
| **Debe contener** | Checklist de puntos a cubrir (no prosa cerrada) |
| **NO debe tocar** | Fronteras explícitas → evita que dos módulos se pisen |
| **Ancla / ejemplo real** | Caso concreto a citar |
| **Errores a evitar** | Lista negativa de anti-patrones |
| **Términos clave** | Mini-glosario para coherencia entre módulos |
| **Insumos** | Qué se le entrega al ejecutor |
| **Forma de salida** | Extensión, formato, tono |
| **Criterio de listo** | Vara de revisión |

---

## Ficha 1 — Visión y propósito

- **Propósito:** Explicar, a alguien que nunca lo vio, *por qué* existe este método de trabajo con IA y qué problema concreto resuelve.
- **Extensión:** 300–450 palabras.
- **Preguntas que debe responder:**
  1. ¿Qué problema aparece cuando alguien colabora con IA sin estructura? (pérdida de control, de calidad, de continuidad)
  2. ¿Cuál es la idea central que lo resuelve? (cada modelo en su mejor rol según fortaleza y costo, con un humano como autoridad final)
  3. ¿Qué se obtiene al final? (un método *reproducible*)
  4. ¿Por qué esto importa más con IA que con un equipo humano tradicional?
- **Debe contener:** el problema en términos para recién llegados; la tesis en 1–2 frases; mención de los tres pilares (roles, ciclo, memoria) sin desarrollarlos; el resultado buscado.
- **NO debe tocar:** el *cómo* operativo → [[Módulo 3]]; detalle de roles → [[Módulo 2]]; memoria → [[Módulo 4]]; automatización → [[Módulo 6]]. Sin rutas ni jerga interna.
- **Ancla:** referencia de alto nivel al ecosistema del autor (Remanso/ASLAN) como prueba de uso real, sin detalle técnico.
- **Errores a evitar:** explicar el *cómo* antes del *por qué*; vender la IA como reemplazo del juicio humano (contra restricción #3); tono de manual; prometer resultados de negocio.
- **Términos clave:** *método de trabajo*, *rol*, *modelo*, *reproducible*, *autoridad humana*, *continuidad*.
- **Insumos:** `CLAUDE.md` (#1, #3); las notas de memoria del proyecto.
- **Forma de salida:** Markdown, `## 1. Visión y propósito`, tono didáctico externo-primero, sin tablas ni código.
- **Criterio de listo:** un lector ajeno entiende *por qué querría* usar el método y no hay contenido de otros módulos.

---

## Ficha 2 — Roles y responsabilidades

- **Propósito:** Definir qué hace cada participante (humano y modelos) y dónde empieza y termina su autoridad.
- **Extensión:** 400–550 palabras.
- **Preguntas que debe responder:** ¿Quién dirige y por qué? ¿Quién ejecuta? ¿Quién revisa? ¿Quién decide en última instancia? ¿Por qué cada rol se asigna a ese modelo (fortaleza vs. costo)?
- **Debe contener:** Human-in-the-Loop = autoridad final única que aprueba (restricción #1); Opus = dirige, ordena, hace push-back, define esqueletos; Sonnet 4.6 = ejecuta/revisa calidad; Haiku 4.5 = redacta módulos; tabla rol → responsabilidad → "no hace".
- **NO debe tocar:** la *secuencia* de interacción → [[Módulo 3]]; automatización → [[Módulo 6]].
- **Ancla:** un sub-agente ejecutor y un sub-agente revisor independiente como roles materializados.
- **Errores a evitar:** describir el flujo temporal (es del M3); presentar roles rígidos sin el porqué económico/de capacidad.
- **Términos clave:** *rol*, *autoridad humana*, *director*, *ejecutor*, *revisor/guardián*, *push-back*.
- **Insumos:** `CLAUDE.md` (#1, #3); la skill del método; las notas de memoria del proyecto.
- **Forma de salida:** Markdown, `## 2. …`, admite una tabla de roles.
- **Criterio de listo:** el lector sabe a quién corresponde cada decisión y por qué.

---

## Ficha 3 — El ciclo de producción

- **Propósito:** Mostrar la secuencia operativa de una tarea desde que nace hasta que se aprueba.
- **Extensión:** 450–600 palabras.
- **Preguntas que debe responder:** ¿Cómo fluye una tarea? ¿En qué orden intervienen los roles? ¿Dónde entra el checkpoint "¿esto se puede automatizar?"? ¿Qué pasa si la revisión falla?
- **Debe contener:** flujo (humano+Opus definen esqueleto → Haiku redacta → Sonnet revisa → Opus+Human-in-the-Loop evalúan → consolidación); diagrama lineal simple; el checkpoint de automatización como paso recurrente; el camino de rechazo (vuelve a Haiku con feedback).
- **NO debe tocar:** *qué* hace atómica una tarea → [[Módulo 5]]; *cómo* decidir automatizar en profundidad → [[Módulo 6]]; definición de roles → [[Módulo 2]].
- **Ancla:** esta misma sesión (esqueleto → fichas → Haiku) como ejemplo en acción.
- **Errores a evitar:** redefinir roles; saltarse la aprobación humana (restricción #1).
- **Términos clave:** *ciclo*, *esqueleto*, *módulo atómico*, *revisión*, *consolidación*, *checkpoint de automatización*.
- **Insumos:** las fichas de esta sesión; `CLAUDE.md` (#1).
- **Forma de salida:** Markdown, `## 3. …`, admite bloque de diagrama.
- **Criterio de listo:** el lector podría dibujar el flujo y ubicar dónde aprueba el humano y dónde se evalúa automatizar.

---

## Ficha 4 — Memoria persistente como activo de continuidad

- **Propósito:** Explicar cómo la memoria evita que el método y el contexto se pierdan entre sesiones.
- **Extensión:** 400–550 palabras.
- **Preguntas que debe responder:** ¿Por qué la IA "olvida" entre sesiones? ¿Qué se guarda y qué no? ¿Cómo se organiza? ¿Cómo se recupera lo relevante?
- **Debe contener:** el problema del olvido; tipos de memoria (`user/feedback/project/reference`); índice (`MEMORY.md`) + archivos atómicos enlazados; qué NO guardar (lo derivable del repo, lo efímero).
- **NO debe tocar:** trazabilidad vía git → [[Módulo 9]] (memoria ≠ versionado); el ciclo → [[Módulo 3]].
- **Ancla:** el propio `MEMORY.md` del proyecto con sus archivos vivos.
- **Errores a evitar:** confundir memoria (continuidad de contexto) con git (historial de archivos); sugerir guardar todo.
- **Términos clave:** *memoria persistente*, *continuidad*, *índice*, *tipos de memoria*, *recall*.
- **Insumos:** estructura real de `…/memory/`; `MEMORY.md`.
- **Forma de salida:** Markdown, `## 4. …`, admite tabla de tipos.
- **Criterio de listo:** el lector entiende qué anotar, dónde, y por qué no es lo mismo que git.

---

## Ficha 5 — Reglas de atomicidad (la ficha de encargo)

- **Propósito:** Enseñar qué hace atómica a una tarea del ejecutor y presentar la ficha de encargo como herramienta.
- **Extensión:** 450–600 palabras.
- **Preguntas que debe responder:** ¿Qué es una tarea atómica? ¿Cómo se evita que dos módulos se pisen? ¿Qué campos lleva una ficha y para qué sirve cada uno?
- **Debe contener:** definición de atomicidad (una tarea, una frontera clara, sin dependencias ocultas); la plantilla de ficha; el rol clave de "NO debe tocar"; ejemplo de buena vs. mala división.
- **NO debe tocar:** el flujo del ciclo → [[Módulo 3]]; cómo automatizar → [[Módulo 6]].
- **Ancla:** estas mismas 9 fichas como ejemplo aplicado.
- **Errores a evitar:** fichas que escriben el contenido en vez de acotarlo; fronteras difusas.
- **Términos clave:** *atomicidad*, *ficha de encargo*, *frontera*, *alcance*, *criterio de listo*.
- **Insumos:** este set de fichas; memoria de la decisión de atomicidad.
- **Forma de salida:** Markdown, `## 5. …`, incluye la plantilla en tabla.
- **Criterio de listo:** el lector puede redactar su propia ficha atómica para un caso nuevo.

---

## Ficha 6 — Industrialización: cuándo y cómo automatizar

- **Propósito:** Dar criterios para decidir si una interacción repetida debe volverse HOOK, SKILL, SUBAGENTE, una mezcla o todas.
- **Extensión:** 500–650 palabras.
- **Preguntas que debe responder:** ¿Cuándo conviene automatizar? ¿Qué resuelve cada herramienta? ¿Cómo elegir entre ellas? ¿Cómo se combinan?
- **Debe contener:** el principio de evaluación constante; qué es y cuándo usar cada una (hook = automatismo determinista/enforcement; skill = conocimiento/convención invocable; subagente = rol con contexto precargado); tabla de decisión (síntoma → herramienta); la idea de combinarlas.
- **NO debe tocar:** el detalle del ciclo → [[Módulo 3]]; la red de seguridad git → [[Módulo 9]].
- **Ancla (fuerte):** un proyecto real — preámbulo→sub-agente ejecutor; convenciones→skill; grep manual→hook *enforcer*. Un ejemplo por herramienta.
- **Errores a evitar:** automatizar antes de tener el patrón claro; usar hook donde basta una skill; presentar las opciones como excluyentes.
- **Términos clave:** *industrialización*, *hook*, *skill*, *subagente*, *enforcement*, *patrón repetido*.
- **Insumos:** las notas de memoria del proyecto (industrialización); la skill del método.
- **Forma de salida:** Markdown, `## 6. …`, incluye tabla de decisión.
- **Criterio de listo:** ante una interacción repetida, el lector sabe elegir entre hook/skill/subagente y justificarlo.

---

## Ficha 7 — Casos de uso / ejemplos reales

- **Propósito:** Demostrar con casos concretos que el método funciona en proyectos reales.
- **Extensión:** 400–550 palabras.
- **Preguntas que debe responder:** ¿Dónde se aplicó? ¿Qué resultado dio? ¿Qué se aprendió?
- **Debe contener:** 1–2 casos desarrollados (un dashboard de monitoreo como caso principal); para cada uno situación → aplicación del método → resultado; una lección transferible por caso.
- **NO debe tocar:** re-explicar conceptos (ya están en M1–M6); detalle técnico que no ilustre el *método*.
- **Ancla:** un dashboard de monitoreo (fases, industrialización, honestidad de datos como decisión dirigida).
- **Errores a evitar:** convertirlo en documentación técnica del proyecto; casos sin lección.
- **Términos clave:** consistentes con módulos previos.
- **Insumos:** las notas de memoria del proyecto (estado y decisiones).
- **Forma de salida:** Markdown, `## 7. …`, subsecciones por caso.
- **Criterio de listo:** el lector ve el método "en vivo" y extrae una lección aplicable.

---

## Ficha 8 — Límites y cuándo NO usar el método

- **Propósito:** Delimitar honestamente dónde el método no aporta o estorba, para no aplicarlo dogmáticamente.
- **Extensión:** 300–450 palabras.
- **Preguntas que debe responder:** ¿Cuándo es excesivo? ¿Qué tareas no lo justifican? ¿Cuáles son sus costos? ¿Qué supuestos lo sostienen?
- **Debe contener:** casos donde el overhead supera el beneficio (tareas triviales, exploratorias, one-shot); costos (tiempo de coordinación, tokens); honestidad sobre límites de los modelos.
- **NO debe tocar:** repetir ventajas (M1); criterios de automatización → [[Módulo 6]].
- **Ancla:** una tarea pequeña que NO merece el ciclo completo.
- **Errores a evitar:** vender el método como universal; omitir costos (rompe el principio de honestidad).
- **Términos clave:** *overhead*, *límites*, *costo*, *proporcionalidad*.
- **Insumos:** `CLAUDE.md` (#3, honestidad); experiencia del proyecto.
- **Forma de salida:** Markdown, `## 8. …`.
- **Criterio de listo:** el lector sabe reconocer cuándo NO usar el método.

---

## Ficha 9 — Trazabilidad y reversibilidad (la red de seguridad)

- **Propósito:** Explicar cómo se sigue el rastro de cualquier cambio y cómo se revierte — las 4 capas de seguridad.
- **Extensión:** 450–600 palabras.
- **Preguntas que debe responder:** ¿Qué pasa si un ejecutor hace un cambio no solicitado? ¿Cómo se detecta? ¿Cómo se vuelve atrás? ¿Qué previene el daño desde el diseño?
- **Debe contener:** las 4 capas (Prevención / Contención / Detección / Recuperación); la regla dura (el ejecutor devuelve contenido, no persiste; el humano/director consolida); git como capa de Recuperación (commits = puntos de retorno reversibles); el campo "NO debe tocar" como capa de Detección.
- **NO debe tocar:** tutorial extenso de comandos git (mencionar, no enseñar a fondo); memoria como continuidad → [[Módulo 4]] (distinguir de versionado).
- **Ancla:** este propio repo (`git init`, primer commit como punto de retorno).
- **Errores a evitar:** confundir memoria con git; proponer encriptar/minificar antes de commitear (mata los diffs); confiar en buena fe en vez de diseño.
- **Términos clave:** *trazabilidad*, *reversibilidad*, *commit*, *diff*, *capas de seguridad*, *breadcrumbs*.
- **Insumos:** historial git del repo; las 4 capas definidas en esta sesión.
- **Forma de salida:** Markdown, `## 9. …`, admite tabla de las 4 capas.
- **Criterio de listo:** el lector entiende cómo el método se protege de cambios no deseados y cómo recuperarse.

---

## Orden de redacción sugerido

M1 → M2 → M5 → M3 → M4 → M9 → M6 → M7 → M8.
(Primero el porqué y los roles; luego atomicidad antes del ciclo que la usa;
los pilares de continuidad/seguridad; después industrialización; y al final
casos y límites, que se nutren de todo lo anterior.)

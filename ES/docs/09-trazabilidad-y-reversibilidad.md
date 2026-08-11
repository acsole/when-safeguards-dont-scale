## 9. Trazabilidad y reversibilidad

En toda colaboración entre humanos e IA, existe el riesgo de que un cambio no solicitado —o ejecutado fuera de alcance— llegue a los archivos finales sin revisión. El método de trabajo protege contra esto mediante **cuatro capas de seguridad** que funcionan en conjunto: previenen el daño antes de que ocurra, lo contienen si ocurre, lo detectan apenas aparece, y lo revierten si es necesario.

### Las cuatro capas

| Capa | Pregunta que responde | Mecanismo |
|------|------------------------|-----------|
| **Prevención** | ¿Cómo evito que el ejecutor toque los archivos directamente? | El ejecutor nunca persiste cambios en el código fuente ni en archivos consolidados. Redacta y *devuelve* el contenido (en Markdown, en la respuesta). Solo el director o el humano consolida en los archivos. Así, un error del ejecutor no sobrescribe nada. |
| **Contención** | ¿Si se escribe algo, dónde queda acotado? | Los cambios viven en **espacios separados** (borradores, ramas de git, archivos temporales) hasta aprobación. Nunca pisan lo aprobado *in situ*. El daño, si existe, queda aislado. |
| **Detección** | ¿Cómo sé que hubo un desvío? | El campo **"NO debe tocar"** de la ficha de trabajo (Módulo 5) es un contrato explícito sobre el alcance. Si la salida lo viola, es una bandera roja inmediata. El revisor contrasta la salida con el contrato. |
| **Recuperación** | ¿Cómo vuelvo atrás si algo salió mal? | **Control de versiones** (git). Cada cambio consolidado es un *commit* — un snapshot completo con su mensaje y una firma de quién y cuándo. Un commit es un punto de retorno reversible; cualquier daño es reversible en segundos. |

### La regla dura: devolver, no perseguir

El ejecutor **devuelve contenido**, no persiste archivos. Esta separación es deliberada: convierte al ejecutor en una "caja negra" de baja confianza. Su output es **material en bruto**, siempre sujeto a revisión y aprobación antes de entrar al sistema. El humano o el director deciden si escribir, cuándo y dónde. Esta barrera es más fuerte que cualquier permiso de carpeta o token.

### Git como red de seguridad

El repositorio versionado es la **capa de Recuperación** en acción. Cada módulo consolidado en este documento es un *commit*: una línea en el historial que muestra quién escribió qué, cuándo y por qué. El *diff* de ese commit son las "breadcrumbs" — la prueba legible de cada cambio.

Una trampa común: encriptar o minificar archivos *antes* de hacer commit. Esto destruye los *diffs* legibles — mata la capa de Detección. La confidencialidad se protege de otras formas (repositorio privado, control de acceso), no cifrando antes de versionar.

### Distinción crítica: versionado vs. memoria

**Git es el historial de versiones de los archivos** — commits, diffs, puntos de retorno. En cambio, la **continuidad de contexto entre sesiones** —la memoria persistente que permite a la IA retomar el trabajo sin perder el hilo— es un mecanismo distinto, tratado en el Módulo 4. No debe confundirse: el versionado rastrea cambios *en los archivos*; la memoria rastrea *contexto de la colaboración*. Ambos son necesarios, pero operan en capas diferentes.

### Flujo completo

Un cambio sigue esta ruta:

1. El humano aprueba un plan con sus límites ("NO debe tocar").
2. El ejecutor devuelve contenido.
3. El revisor contrasta contra el contrato (capa de Detección).
4. El director o humano escribe en los archivos (Prevención).
5. Se hace *commit* con mensaje claro (Recuperación).

Si algo falla en el paso 3, se rechaza y no llega al paso 4. Si algo falla después, el *diff* y el historial son la red que atrapa el error y lo revierte.

**Trazabilidad y reversibilidad son sinónimos en este método.** No confías; *verificas y guardas constancia.*

---

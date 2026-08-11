# Aplicabilidad del método de trabajo con IA a verticales de negocio

> **Qué es este archivo.** Un complemento del documento canónico
> [del método](00-indice.md). Muestra cómo el método —los
> mismos roles, fichas, severidad proporcional, memoria, trazabilidad e
> industrialización— se mapea a distintas industrias, para que un lector de
> cualquier sector se vea reflejado y sepa cómo aplicarlo en su contexto.
>
> ⚠️ **Naturaleza de los casos.** Los ejemplos por vertical son **ilustrativos
> y extrapolativos**, no descripciones de despliegues reales. No hay clientes,
> agencias, cifras ni campañas reales detrás: muestran *cómo se mapearía* el
> método, no *qué ocurrió*. (Los casos reales y verificables del método están en
> el Módulo 7 del documento canónico.) Esta distinción es deliberada: es la misma
> regla anti-fabricación que el método aplica a sí mismo.
>
> **Estructura común.** Cada vertical sigue siete campos: contexto típico ·
> mapeo de roles · la ficha de encargo aquí · dónde sube la severidad · memoria,
> trazabilidad e industrialización · beneficio concreto. Al final, una **plantilla
> reusable** para que cualquiera mapee su propia vertical.

---

## Marketing y agencias

### Contexto típico
Una agencia de marketing (o un equipo in-house) produce contenido, copy de campañas, estrategias creativas y assets para uno o varios clientes simultáneamente. El desafío central: mantener consistencia de marca, cumplimiento normativo (especialmente en rubros regulados), y escalabilidad sin que cada pieza sea revisada manualmente de punta a punta por el experto humano más caro.

### Mapeo de roles
- **Autoridad humana**: el cliente (directo) o el director de cuentas/creatividad que aprueba y toma decisión final sobre qué entra en campaña.
- **Director**: el estratega o lead creativo que recibe el brief, define el tono, el ángulo, las restricciones legales y divide el encargo en tareas concretas (e.g., "redactar tres variantes de headline", "generar copy para email de bienvenida").
- **Redactor**: el modelo que genera copy, headlines, descripciones de producto, calls-to-action según la ficha de encargo.
- **Revisor/guardián**: modelo independiente (o en casos de severidad alta, revisor humano especializado) que audita cada pieza contra brand guidelines, afirmaciones verificables, normativa publicitaria, y tono aprobado.

### La ficha de encargo aquí
El "encargo" es el brief creativo: plataforma (email, social, web), público objetivo, tono de marca, objetivo de la pieza, y constraints explícitos (presupuesto de palabras, prohibiciones legales, claims que no pueden hacerse sin evidencia). El campo **"NO debe tocar"** incluye: lineamientos de marca inmodificables, claims médicos/legales/financieros no sustentados, superlativos sin respaldo, y cumplimiento de códigos publicitarios (e.g., no discriminación, no engaño).

### Dónde sube la severidad
La revisión sube a humano (o a modelo de máxima capacidad) cuando: la campaña toca salud, finanzas, seguros u otros rubros regulados; hay claims legales implícitos; el presupuesto es alto o la exposición mediática es masiva; o el cliente está en industria sensible a denuncias. En estos casos, un revisor humano abogado o especialista en compliance entra en la cadena.

### Memoria, trazabilidad e industrialización
- **Memoria**: archivos de continuidad con brand book, tono, historial de campañas previas, decisiones tomadas, clientes y sus preferencias estéticas.
- **Versionado**: cada iteración del copy queda en git, con quién lo generó, cuándo, qué retroalimentación del revisor produjo qué cambio.
- **Industrialización**: una skill "redactor de marca X" cargada/configurada con el tono específico del cliente; hooks que marcan automáticamente claims sospechosos; subagentes especializados por cliente o por rubro (e.g., redactor de tech vs. redactor de wellness).

### Beneficio concreto
La agencia escala: maneja del orden de varios clientes sin que su equipo de creativos se ahogue. El humano aprueba lo que importa (estrategia, aprobación final); la IA genera volumen y mantiene consistencia. La trazabilidad garantiza que ante una reclamación o cambio de dirección del cliente, se sabe exactamente por qué se escribió cada palabra y quién validó qué.

---

## Inmobiliaria y agentes

### Contexto típico
Los agentes inmobiliarios y brokers operan bajo presión de tiempo y escala: deben generar descripciones precisas de propiedades (listings), responder consultas de potenciales compradores, elaborar materiales de marketing y mantener conformidad legal. Cada error en los datos de una propiedad o una afirmación que viola leyes de trato justo genera responsabilidad civil directa. La demanda es constante, los datos son críticos, y el riesgo regulatorio es alto.

### Mapeo de roles
La **autoridad humana** es el agente o broker: es quien responde legalmente ante la publicación y debe aprobar antes de que cualquier contenido se haga público. El **director** es el modelo que recibe los datos verificados de la propiedad (título, metros, ambientes, precio, documentación) y define qué información incluir, qué restricciones aplican y qué marco legal rige. El **redactor** es un modelo rápido que genera el listing descriptivo y las respuestas a consultas según la ficha encargada. El **revisor/guardián** es un modelo independiente (o humano, según severidad) que audita exactitud de datos y cumplimiento legal.

### La ficha de encargo aquí
El "encargo" es la ficha de la propiedad: documento con datos verificados (ubicación exacta, metros cuadrados, número de ambientes, precio, condiciones de venta, título, gravámenes, restricciones locales). El **"NO debe tocar" crítico**: el redactor no puede inventar características ni datos no presentes en la ficha verificada—riesgo de fraude inmobiliario. Tampoco puede usar lenguaje que segmente por raza, religión, composición familiar, estatus migratorio u otros criterios protegidos por leyes de trato justo en vivienda.

### Dónde sube la severidad
La severidad sube a revisor humano cuando: hay afirmaciones de titularidad o gravámenes (error = fraude); datos falsos que generan responsabilidad civil (superficie, impuestos); lenguaje que violaría leyes antidiscriminación; o montos muy altos de transacción. En estos casos, el revisor es el propio agente o un asesor legal, no otro modelo.

### Memoria, trazabilidad e industrialización
La **memoria** persiste en archivos de continuidad: cartera de propiedades del cliente, historial de cada listing y sus variaciones, preferencias del comprador, regulaciones locales. El **versionado en git** registra cada cambio en cada listing. La **industrialización** incluye: una skill cargada/configurada con el formato estándar de listings y el marco legal local (ej. cláusulas obligatorias); un hook que bloquee automáticamente lenguaje discriminatorio; un subagente "agente virtual de consultas" precargado con la cartera actualizada para responder preguntas sin exposición legal.

### Beneficio concreto
El agente escala su capacidad de producción —del orden de decenas o cientos de listings con exactitud consistente— sin sacrificar verificación de datos ni exponerse legalmente. El humano aprueba solo lo que toca su responsabilidad. La trazabilidad completa (quién cambió qué, cuándo, por qué) protege al agente ante auditorías.

---

## Tecnologías de la información

### Contexto típico

Los equipos de desarrollo de software enfrentan el desafío permanente de producir código de calidad a escala, con revisiones rigurosas, documentación técnica actualizada y resolución rápida de defectos. Esta vertical es el origen natural del método: ciclos iterativos cortos, trazabilidad nativa (git), múltiples roles técnicos y necesidad de que cada cambio sea auditable y reversible. La presión por velocidad sin sacrificar seguridad y mantenibilidad hace que aquí el método despliegue toda su potencia.

### Mapeo de roles

- **Autoridad humana:** el tech lead o propietario del repositorio, quien aprueba o rechaza el merge final.
- **Director:** modelo de mayor capacidad que descompone el feature o bug en tareas atómicas, define criterios de aceptación claros y crea la ficha de encargo.
- **Redactor:** modelo rápido que escribe el código, tests unitarios y documentación según la ficha, sin desviarse del alcance.
- **Revisor/guardián:** modelo independiente o humano senior que audita el diff contra la ficha: corrección lógica, seguridad, adherencia a estilos y convenciones del proyecto.

### La ficha de encargo aquí

Es el ticket o especificación de la tarea: "implementar endpoint que devuelve datos de usuario" con criterios de aceptación explícitos (tests que pasan, documentación de API, manejo de errores). El "NO debe tocar" es crítico:
- Archivos o módulos fuera del alcance declarado.
- Secretos, credenciales o configuración sensible.
- Dependencias externas no aprobadas.
- APIs públicas o contratos que romperían compatibilidad hacia atrás.

### Dónde sube la severidad

La revisión escala a un humano (o senior independiente) cuando el código toca seguridad, autenticación, pagos, datos personales, infraestructura productiva o cambios irreversibles (migraciones de datos, borrados masivos). Un fix de una línea en un script interno, en cambio, puede fluir por un ciclo más ligero. La proporcionalidad es clave: el esfuerzo de revisión se ajusta al daño plausible.

### Memoria, trazabilidad e industrialización

- **Memoria:** archivos de decisiones arquitectónicas, convenciones del repo (cómo se nombran las variables, dónde van los tests, patrones preferidos), deuda técnica conocida.
- **Trazabilidad:** git es nativo aquí: cada commit es una unidad de cambio auditable, los diffs muestran exactamente qué cambió, y un revert es una operación de una línea.
- **Industrialización:** una skill cargada/configurada con las convenciones del proyecto; hooks que corren linters, tests y escaneo de secretos automáticamente antes de cada commit/merge (enforcement); un subagente "revisor de seguridad" con el contexto del dominio precargado.

### Beneficio concreto

El equipo produce código mantenible y seguro sin cuello de botella humano: la autoridad aprueba lo crítico, el director divide en piezas, el redactor entrega rápido, el revisor independiente audita. Cada cambio queda registrado, reversible e íntegramente trazable. La escala sube sin degradar la calidad.

---

## Plantilla reusable: mapeá tu propia vertical

Las verticales anteriores son ejemplos. El método no depende de la industria: depende de los *roles*, las *fichas* y la *proporcionalidad*. Para llevarlo a tu campo —salud, legal, educación, finanzas, atención al cliente, lo que sea—, copiá esta plantilla y respondé cada pregunta para tu contexto.

### Contexto típico
*¿Qué se produce repetidamente en tu vertical, a escala, donde la calidad y la consistencia importan? ¿Cuál es la presión central (tiempo, volumen, cumplimiento)?*

### Mapeo de roles
*¿Quién es la **autoridad humana** que aprueba y responde por lo publicado? ¿Quién hace de **director** (define qué se hace y lo divide)? ¿Qué genera el **redactor**? ¿Qué chequea el **revisor/guardián** independiente?* — Los roles del método no cambian; solo les ponés cara en tu industria.

### La ficha de encargo aquí
*¿Cuál es la unidad de trabajo típica (el "encargo")? Y lo más importante: ¿cuál es tu campo **"NO debe tocar"** —lo que jamás debe inventarse, modificarse o cruzarse— en tu dominio? (Suele ser lo legal, lo regulatorio, lo que genera responsabilidad o daño.)*

### Dónde sube la severidad
*¿Qué tareas, si salen mal, causan el peor daño plausible? Ésas disparan un ejecutor más capaz y un revisor de mayor nivel (hasta humano experto). ¿Cuáles, en cambio, son triviales y no merecen el ciclo completo?*

### Memoria, trazabilidad e industrialización
*¿Qué contexto debe persistir entre sesiones (memoria: archivos de continuidad, no una base de datos)? ¿Qué conviene versionar para poder revertir y auditar? ¿Qué interacción repetida podrías industrializar con una **skill** (conocimiento cargado/configurado), un **hook** (enforcement automático) o un **subagente** (rol precargado)?*

### Beneficio concreto
*Al terminar: ¿qué ganás concretamente? Normalmente: escalar el volumen sin perder calidad ni cumplimiento, con un humano aprobando solo lo que importa, y trazabilidad total de quién hizo qué y por qué.*

---

> **Recordatorio de honestidad.** Si adaptás esto a tu vertical, mantené la distinción entre lo *ilustrativo* (cómo se mapearía) y lo *real* (lo que efectivamente ocurrió). Presentar un caso hipotético como real es exactamente el modo de fallo que el método está diseñado para atrapar.

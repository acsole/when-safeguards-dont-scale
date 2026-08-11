# Guía de adopción e instalación del método

> Documento canónico de la **guía de instalación**. Audiencia: externo-primero
> (didáctico para alguien que nunca lo vio). Cuerpo **genérico/portable** — las 5
> piezas como conceptos aplicables a cualquier entorno con IA — más un **Apéndice**
> con la materialización concreta en Claude Code. Se construye sección por sección
> siguiendo el blueprint en [`guía-instalación-fichas.md`](guía-instalación-fichas.md),
> con el mismo ciclo de dogfooding que produjo el método: redacción → revisión
> (quality-guardian) → consolidación y commit.
>
> **Estado:** COMPLETO — las 12 secciones consolidadas.

---

## 1. Qué instala y qué garantiza

Esta guía instala un **andamiaje de trabajo colaborativo entre humanos e IA**, no un sistema autónomo. Una vez configurado, **se auto-activa por sesión**: en cada conversación nueva el andamiaje arranca solo, sin re-setup manual, pero las decisiones siguen siendo tuyas.

### La promesa: out-of-the-box sin sorpresas

Instalás una vez. Desde la sesión siguiente, el andamiaje está vivo: roles definidos, memoria persistente recuperada, skills listas, subagentes precargados, reglas de ejecución activas. No reinventás la rueda en cada conversación. Pero aquí viene lo importante: **el andamiaje es automático; las decisiones, no**. La autoridad humana sigue siendo quien aprueba lo que importa antes de que se ejecute.

### Las cinco piezas (adelanto)

1. **Archivo de contexto base en la raíz del proyecto** — qué es el proyecto, sus convenciones y restricciones; se carga al iniciar cada sesión.
2. **Memoria persistente** — el contexto vivo del proyecto, conservado entre sesiones.
3. **Skills auto-activables** — cuerpos de conocimiento que la IA invoca sola cuando el contexto los amerita.
4. **Subagentes precargados** — roles especializados (ejecutor, revisor) listos sin re-armar el contexto cada vez.
5. **Hooks de enforcement** — reglas deterministas que se ejecutan solas ante un evento y bloquean lo que no debe pasar.

Cada pieza se instala y se verifica en su propia sección más adelante; aquí solo se nombran.

### Qué NO garantiza esta guía

No automatiza el *juicio*. No reemplaza la supervisión. No convierte a la IA en dueña del proyecto. Lo que sí hace es eliminar fricción operativa: menos preguntas repetidas, menos contexto perdido entre sesiones, menos "¿qué estaba haciendo acá?". Es andamiaje, no autopiloto.

Esto no es teoría: un proyecto real en producción —un dashboard de monitoreo multi-proyecto— ya corre con las cinco piezas juntas, a lo largo de muchas sesiones, con cero re-setup. Cada sesión arranca más informada porque el contexto vive; cada decisión sigue siendo humana.

---

## 2. Requisitos previos

Antes de instalar el andamiaje, verificá estos tres frentes. Dos son requisitos duros (el entorno y el control de versiones); el tercero —el acceso a modelos— gradúa el rigor pero no impide arrancar, como se explica abajo.

### Acceso a modelos de capacidad diferenciada

El método **completo** aprovecha **al menos tres roles de IA distinguibles**:

- Un **rol director** con razonamiento superior, capaz de planificación compleja, síntesis y validación estratégica.
- Un **rol ejecutor/revisor** de capacidad media, apto para implementación, búsqueda de código y mejora iterativa.
- Un **rol redactor económico**, rápido y eficiente, para tareas de bajo costo cognitivo (síntesis, formateo, documentación).

Un punto importante: **estos son roles, no necesariamente modelos distintos** (ver también el Mapa de las 5 piezas). Lo ideal es asignar cada rol al modelo que mejor lo aprovecha, y que el revisor sea independiente de quien produjo. Pero **existe una versión reducida con un solo modelo**: el mismo modelo produce en una pasada y revisa críticamente en otra. Es más débil que tener un revisor independiente, pero muy superior a una sola pasada sin revisión. En resumen: con un modelo ya podés empezar; sumar modelos diferenciados es escalar el rigor, no un requisito de arranque.

### Entorno con soporte integral

Tu herramienta o plataforma de IA debe permitir:

- **Cargar contexto base automáticamente** en cada sesión nueva (sin re-setup manual).
- **Definir y activar skills** según necesidad operativa.
- **Delegar a subagentes**.
- **Ejecutar hooks** de enforcement (validaciones, reglas antes/después de acciones).

### Control de versiones operativo

El proyecto debe contar con **un sistema de control de versiones** para:

- Rastrear cambios de contexto base y memoria.
- Garantizar recuperación de estados previos.
- Auditar decisiones y trazabilidad de tareas.

### Checklist de verificación

- [ ] Tengo acceso a al menos un modelo de IA (idealmente varios, de capacidad diferenciada, para el método completo).
- [ ] Mi entorno soporta contexto base automático, skills, subagentes y hooks.
- [ ] El proyecto usa un sistema de control de versiones activo.

El entorno y el control de versiones son requisitos duros: sin ellos, el andamiaje automático no puede instalarse. El acceso a varios modelos, en cambio, gradúa el rigor, no bloquea el arranque: con uno solo corrés la versión reducida. Para entender cuándo el método directamente no es la opción indicada, consultá el módulo «Límites y cuándo no usar el método» del documento del método.

---

## 3. Mapa de las 5 piezas

El andamiaje de trabajo con IA se sostiene en cinco piezas estructurales, cada una automatizando un tipo de repetición distinto y resolviendo un problema específico del ciclo de desarrollo: cómo mantener el contexto entre sesiones, cómo reutilizar conocimiento sin reescribirlo, cómo delegar roles con precisión y cómo custodiar reglas críticas. La siguiente tabla presenta qué problema resuelve cada una, en qué momento entra en juego y dónde reside en tu infraestructura de trabajo.

| Pieza | Qué automatiza | Cuándo se dispara | Dónde vive |
|-------|---|---|---|
| **Contexto base en la raíz** | Recordar el objetivo, reglas y restricciones del proyecto en cada sesión | Al iniciar la sesión (auto-carga) | Archivo de configuración en la carpeta raíz del proyecto |
| **Memoria persistente** | Reconstruir el contexto acumulado entre sesiones (decisiones previas, estado, aprendizajes) | Al iniciar o consultar durante la sesión | Archivos de memoria: un índice maestro + archivos temáticos por área |
| **Skills auto-activables** | Repetir un cuerpo de conocimiento, convención o protocolo sin reescribir | Por contexto, cuando el entorno reconoce que corresponde | Declaradas como skills en el entorno de trabajo |
| **Subagentes precargados** | Re-pegar el mismo preámbulo y contexto especializado al delegar tareas | Al delegar a un rol específico (director, ejecutor, revisor, auditor) | Definiciones de subagente registradas en el entorno |
| **Hooks de enforcement** | Verificar de forma objetiva que se cumple una regla crítica (seguridad, marca, datos) | Antes o después de una acción clave (guardar, publicar, delegar) | Scripts registrados en el entorno |

Estas cinco piezas **no son alternativas excluyentes, sino capas que trabajan juntas**. El contexto base llega primero, estableciendo la brújula; la memoria lo enriquece con el aprendizaje acumulado; las skills lo contextualizan según la tarea; los subagentes lo heredan al recibir una delegación; los hooks lo custodian antes de que cruce la puerta de salida. Cada capa suma valor a la anterior, no reemplaza.

El orden en que entran suele importar, pero como refuerzo, no como dependencia rígida: el contexto base le da anclaje a la memoria; la memoria le da historial a las skills; las skills aportan conocimiento que los subagentes heredan; y los hooks custodian el resultado final. Aun así, **cada pieza aporta valor por sí sola**: un hook puede verificar una regla técnica objetiva aunque no haya subagentes, y las skills suman aunque todavía no exista memoria acumulada. Podés instalar una, algunas o todas; sumar las que falten es escalar, no un requisito de arranque.

Una aclaración importante: **el andamiaje es la *organización del trabajo*, no una pregunta sobre cantidad o tipo de modelos**. Las cinco piezas funcionan con un solo modelo o con varios; el cuánto y el cuál de modelos es responsabilidad de la sección *Requisitos previos*. Los roles (director, ejecutor, revisor, auditor) son *sombreros* o funciones que el mismo modelo puede vestir en pasadas separadas, no modelos distintos. Un mismo modelo puede producir contenido en una pasada, revisarlo críticamente en otra, y ejecutar un cambio en una tercera, sin que eso requiera tres modelos diferentes. Un andamiaje bien armado permanece agnóstico al número de agentes que lo ocupen: si más adelante decidís sumar más modelos o subagentes especializados, la estructura escala sin rediseño.

---

## 4. Instalar el archivo de contexto base (en la raíz del proyecto)

Cada proyecto necesita un archivo de contexto base que resida en la raíz y se auto-cargue al inicio de cada sesión (en cada herramienta este archivo tiene un nombre convenido que ella carga sola; ver el Apéndice). Esto asegura que todo opera bajo los mismos invariantes y que la IA siempre dispone del mapa completo antes de cualquier conversación.

### Qué hace

El archivo proporciona a la IA: el objetivo del proyecto; las tecnologías, entorno y restricciones innegociables; el protocolo de trabajo (la IA propone un plan y espera aprobación explícita antes de ejecutar); reglas de marca, seguridad o datos que jamás se pueden violar; y cómo la IA colabora con el humano (asistente técnico que aumenta el juicio, no lo reemplaza). También conviene que fije quién tiene autoridad para aprobar cambios y bajo qué criterio se prioriza una tarea sobre otra, para que ese criterio no dependa de la memoria de quien conduce la sesión. Es ESTÁTICO: define las reglas que no cambian, a diferencia de la memoria persistente, que es viva y cambia entre sesiones (ver la sección de memoria).

### Dónde vive

En la RAÍZ del proyecto, porque desde ahí la herramienta lo detecta y lo auto-carga al iniciar cada sesión, sin que haya que pedirlo ni pegarlo. El archivo es legible y se versiona en control de versiones, de modo que cualquier cambio a las reglas del proyecto quede registrado como cualquier otro cambio relevante, con su propio historial y su propia trazabilidad. Esto también permite que, si el proyecto crece o se ramifica, cada rama pueda heredar el mismo archivo de contexto base sin duplicar criterios.

### Cómo verificar que se activó sola

En una sesión nueva, preguntale a la IA por una restricción o invariante que solo esté en tu archivo de contexto (p. ej. "¿cómo debo proponer cambios antes de ejecutarlos?"). Si la responde sin que se la hayas pegado, se cargó. Si no, revisá que el archivo esté en la raíz y con el nombre que la herramienta espera (ver Apéndice).

### Plantilla base

```markdown
# Contexto base del proyecto: <nombre del proyecto>

> Este archivo se carga automáticamente al inicio de cada sesión.
> Define el objetivo, el stack, las restricciones y el modo de trabajo.

## Objetivo
Explicá en 2-3 frases: ¿qué es el proyecto? ¿Qué se busca lograr?

## Contexto / stack
Tecnologías, entorno, datos y referencias que la IA debe saber siempre.

## Restricciones innegociables
1. La IA propone un plan y espera aprobación explícita antes de ejecutar.
2. Deny by default: solo personas autorizadas explícitamente tienen permisos.
3. Nunca comprometer <regla ética o límite de datos del dominio>.

## Modo de trabajo
- La IA propone, <humano responsable> aprueba.
- Identidad de la tarea activa en cada entregable.
- Validación antes de avanzar a la siguiente tarea.
```

---

## 5. Instalar la memoria persistente

### Qué hace

Mientras que el archivo de contexto base (Sección 4) es estático y contiene la arquitectura y reglas invariantes del proyecto, la memoria persistente es el complemento vivo que cambia entre sesiones. Guarda el contexto que evoluciona: decisiones tomadas, acuerdos establecidos, estado actual del proyecto, aprendizajes capturados, y cualquier información que la IA necesita retomar sin empezar de cero. Gracias a esta memoria, cada nueva sesión arranca con continuidad: la IA accede al índice, sabe qué pasó en la sesión previa, y puede proponer o ejecutar sabiendo dónde estaba el trabajo. Para la teoría completa de la memoria persistente y su rol en el ciclo de trabajo, ver el documento del método.

### Dónde vive

La memoria vive en dos lugares complementarios dentro del proyecto: un archivo índice central (el nombre concreto depende de la herramienta; ver el Apéndice) que lista todos los temas de memoria, y una colección de archivos temáticos atómicos (uno por tema: uno para decisiones, otro para estado, otro para aprendizajes, etc.). El índice es el "mapa" que la IA consulta primero; los archivos atómicos contienen el detalle. Esta separación mantiene la memoria legible y fácil de actualizar.

### Cómo verificar que la IA la consulta

En una sesión nueva, preguntale a la IA por un dato o decisión que SOLO vive en la memoria (no en archivos de código ni documentación publicada). Por ejemplo: "*¿Cuál fue la última decisión que tomamos sobre X?*" Si la IA responde correctamente, confirmó que leyó el índice. Si no lo recuerda, revisá que el índice esté en la ruta correcta y que la IA tenga permiso de lectura.

### Qué estructura tiene

La memoria organiza cuatro tipos de información (detalle en el documento del método):

- **Usuario**: perfil, preferencias, estilo de trabajo, restricciones.
- **Feedback**: observaciones y correcciones acumuladas (qué funcionó, qué no).
- **Proyecto**: estado actual, hitos alcanzados, decisiones clave, tareas pendientes.
- **Referencia**: enlaces a recursos, referencias externas, contexto de terceros.

**Qué guardar y qué NO:** guardá hechos que cambian entre sesiones y que la IA debe conocer. NO guardes en memoria lo que ya vive en el código del proyecto, en un repositorio, o en documentación publicada (eso es ruido de memoria).

### Plantillas

**Plantilla 1 — Archivo índice de memoria:**

```markdown
# Índice de memoria — <nombre del proyecto>

## Usuario
- [<título>](<archivo>.md) — <resumen de una línea>

## Feedback
- [<título>](<archivo>.md) — <resumen de una línea>

## Proyecto
- [<título>](<archivo>.md) — <resumen de una línea>

## Referencia
- [<título>](<archivo>.md) — <resumen de una línea>
```

**Plantilla 2 — Archivo de memoria atómico:**

```markdown
---
name: <slug-corto>
description: <resumen de una línea para decidir si leerlo completo>
type: user | feedback | project | reference
---

# <Título descriptivo>

<El hecho o contexto concreto. Desarrollá en párrafos legibles.>

**Por qué:** <Por qué esto importa; qué sucedería sin esta información>

**Cómo aplicarlo:** <La acción concreta que la IA debe tomar cuando lea esto>

**Enlaces relacionados:** [[<archivo>]], [[<archivo>]]
```

> Nota de convención: los encabezados legibles pueden ir en tu idioma (Usuario, Feedback, Proyecto, Referencia), pero el valor del campo `type` se mantiene en inglés (`user | feedback | project | reference`) por ser una etiqueta técnica.

---

## 6. Instalar las skills auto-activables

### Qué hace

Una skill auto-activable es un depósito de conocimiento, convenciones o procedimientos que la IA invoca automáticamente cuando el contexto coincide, sin que vos tengas que pedirlo explícitamente. En lugar de repetir instrucciones a mano en cada sesión, declarás una skill que encapsula ese cuerpo de saber: el método de trabajo del equipo, las convenciones del proyecto, una checklist de validación, un protocolo de comunicación, un estándar de formato. La IA la lee cuando corresponde y la aplica sin que tengas que recordársela.

### Dónde vive

Una skill se declara como archivo en el entorno de trabajo (el formato y la ubicación concretos dependen de la herramienta; ver el Apéndice). Generalmente contiene:

- Un **encabezado declarativo** (metadatos de la skill: nombre, descripción).
- Un **cuerpo de conocimiento**: las convenciones, los pasos, las reglas o los ejemplos que la skill codifica.

### Cómo verificar que se auto-activó

En una tarea que debería disparar la skill, observá que la IA **aplica las convenciones o procedimientos sin que se los hayas recordado**. Por ejemplo, si declaraste una skill sobre "estándares de formato de documentos", y la IA genera un documento respetando esos estándares sin que vos lo hayas pedido en ese diálogo, la skill se activó correctamente. Otro indicador: la IA menciona explícitamente que está aplicando una convención o protocolo de la skill.

### Qué hace que se dispare sola

El corazón de una skill auto-activable es su **campo de descripción**. Ese campo debe ser **rico en disparadores** (situaciones, palabras clave, contextos que hacen que la IA la reconozca y la aplique). Si la descripción es genérica o vaga, la skill no se dispara. Una descripción fuerte enumera explícitamente cuándo se usa: "Activar cuando el usuario mencione X, Y o Z"; "Aplicar si la tarea involucra procedimiento P"; "Invocarse siempre que se escriba un documento de tipo Q".

**Punto crítico:** la skill se **CARGA**, no se "entrena" ni "aprende". No ajusta pesos; es un bloque de información que la IA consulta cuando identifica el disparador. La calidad de la carga depende de cuán clara y específica sea la descripción.

**Recomendación:** instalá primero DOS skills:

1. Una que codifique **las convenciones y restricciones del proyecto** (qué se permite y qué no; tonos; formatos; decisiones clave).
2. Una que encapsule **el propio método de trabajo con IA** (cómo planeás, cómo validás, qué rol toma cada parte, cómo colaboran).

Estos dos depósitos reducen la fricción drásticamente: la IA ya "sabe" cómo operás sin que lo repitas cada vez.

### Plantilla genérica de skill

```
---
name: <slug-de-la-skill>
description: |
  Activar cuando: se mencione <situación 1>; el usuario escriba <palabra clave>; la tarea implique <contexto>;
  se redacte un documento de tipo <tipo de doc>; aparezcan preguntas sobre <tema>; el usuario use el
  marcador [<comando>]; se inicie una sesión de <actividad>.
---

# <Nombre legible de la skill>

## <Convención 1>

<Descripción de la convención, regla o procedimiento. Sé específico; incluí ejemplos si ayuda.>

## <Convención 2>

<Descripción.>

## <Checklist / Pasos>

- Paso 1: <descripción>
- Paso 2: <descripción>
- Paso 3: <descripción>
```

---

## 7. Instalar los subagentes precargados

### Qué hace

Un subagente es un rol delegado que **nace con el contexto ya cargado**: no necesitás re-pegar el preámbulo completo cada vez que lo invocás. Es como tener un especialista en tu equipo que ya conoce las invariantes del proyecto, los estándares de calidad y las reglas de cómo trabajás, sin que tengas que recordárselas en cada tarea.

Cuando delegás a un subagente, respeta automáticamente tus convenciones —porque las conoce de antemano— y ganás rapidez al no tener que repetir "acá están nuestras normas de nuevo".

### Dónde vive

Los subagentes se definen como entradas en la configuración de tu entorno de trabajo (la ubicación y el formato exactos dependen de la herramienta; ver el Apéndice). Cada definición incluye: nombre, descripción de cuándo usarlo, el rol que juega, y el contexto precargado (invariantes, convenciones, reglas duras). Una vez instalados, aparecen como opciones disponibles al delegar.

### Cómo verificar que trae el contexto sin re-pegarlo

La prueba más clara es **delegarle una tarea sin recordarle las invariantes y ver que igual las respeta**. Por ejemplo: si tu regla es "devuelve contenido, no escribas archivos", le delegás una tarea sin mencionar esa regla, y el subagente igual devuelve su respuesta en el chat sin escribir archivos, entonces la precarga funcionó.

### Qué configuro

Configurás **dos subagentes núcleo**: uno **ejecutor** y uno **revisor independiente**.

El **ejecutor** lleva tus invariantes y convenciones del proyecto (exactitud de datos, tono de voz, regla de prevención, etc.). Recibe tareas operativas: escribir, analizar, implementar. **Regla dura: devuelve el contenido en su respuesta; no escribe ni persiste archivos.** Eso impide que un error suyo sobrescriba datos reales.

El **revisor** es independiente del ejecutor y corre un nivel por encima en capacidad. Revisa la salida del ejecutor contra criterios fijos (corrección, integridad, alineación con tu voz, ausencia de datos inventados). Es quien da el visto bueno o detecta fricciones antes de que lleguen a vos.

Para la teoría completa detrás de estos dos roles —por qué se separan y por qué el revisor escala con la severidad—, ver el documento del método.

### Plantilla de subagente

```markdown
---
name: <nombre-slug-del-subagente>
description: "Cuándo delegarle. P. ej., 'Redactor de contenido de marca'"
model: <modelo-de-capacidad-adecuada-al-rol>
tools: <acceso-genérico-de-lectura-y-análisis>
---

## Rol

Sos un <rol específico> especializado en <dominio>. Tu responsabilidad es <tarea concreta>. No sos quien decide; sos quien entrega materia prima para que el humano decida.

## Invariantes precargadas

- Exactitud de datos: nunca incluyas información no verificada.
- **Regla dura: devolvé el contenido en tu respuesta; no escribas ni persistas archivos.**
- Respetá las convenciones de tono y formato del proyecto.
- Ante dudas, preguntá antes de avanzar.

## Cuándo preguntar

- Falta un dato crítico.
- La tarea cruza una línea de las reglas.
- La intención del pedido no está clara.
```

---

## 8. Instalar los hooks de enforcement

### Qué hace

Un hook de enforcement es un script determinista que se ejecuta automáticamente ante un evento y puede **bloquear la acción** si detecta una violación de una regla objetiva y verificable. Es la capa más restrictiva del andamiaje: se activa para reglas que NUNCA deben romperse, sin intervención humana en el momento (para el criterio de cuándo conviene industrializar una regla en un hook, ver el documento del método). Opera con lógica binaria: evalúa la condición y retorna un código de salida que determina si la acción procede o se detiene.

### Dónde vive

El hook se registra como un script en la configuración del entorno del proyecto (directorio, lenguaje de ejecución y formato de registro concretos están en el Apéndice). El registro define: qué evento lo dispara, el path al script, y los códigos de salida esperados (bloqueo vs. permiso). Una vez registrado, se invoca automáticamente cada vez que ocurre el evento, sin que el usuario haga nada más.

### Cómo verificar que bloquea de verdad

No alcanza con revisar el código del hook: hay que provocar a propósito una violación de la regla y confirmar que el hook la detiene. Es decir, crear un caso de prueba concreto (por ejemplo, intentar agregar un archivo de credenciales), ejecutar la acción normalmente, y verificar que el hook la rechaza con un mensaje de error claro. Si no bloquea en la prueba, hay un defecto en su lógica o configuración.

### Qué regla automatizo primero

Empezá con una regla **objetiva y verificable**: por ejemplo, *bloquear la inclusión de archivos de credenciales* (nombres que coincidan con patrones como `.env`, `secrets.json`, `password.txt`). Es determinista: el hook examina cada archivo pendiente, aplica un patrón, y decide sin ambigüedad.

Un hook de **pre-evento** se ejecuta *antes* de la acción y puede bloquearla (código de salida de bloqueo). Un hook de **post-evento** se ejecuta *después* y valida o registra (útil para auditoría, no para prevención). Elegí pre-evento para reglas que no toleran excepciones.

**Advertencia de diseño:** un hook mal escrito genera falsos positivos (p. ej., detectar la palabra `password` dentro de un comentario, no en un archivo real de credenciales). Usá lógica estricta. Las reglas *subjetivas* (p. ej., "el mensaje de commit debe ser claro") **no van en un hook**: eso es una skill. Los hooks protegen límites mecánicos, no intención.

El hook actúa como capa de **Detección y Recuperación** (ver el documento del método): detiene el error antes de que penetre y fuerza una corrección inmediata.

### Plantilla de hook

```bash
#!/bin/bash
# Hook genérico de pre-evento.
# Lee el evento de entrada, evalúa la regla, sale con el código apropiado.

while read <archivo_o_cambio_pendiente>; do
    # ¿El archivo/cambio viola la regla objetiva?
    if [[ <archivo_o_cambio_pendiente> =~ <patrón_de_violación> ]]; then
        echo "BLOQUEO: regla violada. Detalle: <mensaje_claro>"
        exit <código_de_salida_de_bloqueo>
    fi
done

# Ningún archivo/cambio viola la regla.
exit <código_de_salida_de_OK>
```

*(Los códigos de salida concretos, el formato de registro y los nombres de eventos están en el Apéndice.)*

---

## 9. Verificar la instalación

La instalación está completa solo cuando cada pieza se *activa sola* en una sesión nueva. No se trata de que "debería funcionar" según el diseño: se trata de *observar* que funciona, sin intervención manual. Este es el principio de **"verificar, no confiar"** aplicado a la configuración. Abrí una **sesión fresca** (una conversación nueva con la IA, en el mismo entorno) y recorré la checklist de abajo. Cada pieza tiene una **señal de activación** identificable: eso es lo que buscás.

Las señales son estas. (1) El **contexto base** se activó cuando la IA menciona una restricción o regla que existe solo ahí, sin que se la hayas pegado en el mensaje. (2) La **memoria** se activó cuando la IA recuerda un detalle de una decisión o un hecho registrado solo en la memoria persistente. (3) Una **skill** se activó cuando la IA aplica una convención, un estilo o un protocolo de esa skill sin que se lo recuerdes. (4) Un **subagente** se activó cuando trae consigo sus propias invariantes sin haberlas repetido en tu pedido. (5) Un **hook** se activó cuando detiene o rechaza una acción que provocaste a propósito para violar una regla.

La verificación en vivo es crítica. En un proyecto real en producción, una prueba directa sobre el terreno reveló brechas entre el diseño teórico y lo que ocurre en la práctica: errores que la revisión estática no anticipaba. Verificar en vivo es lo que atrapa eso —es la etapa que el propio método reserva como red final (ver el documento del método)—. No importa cuán limpia sea la instalación sobre el papel; en producción, la realidad manda.

**Checklist de verificación:**

- [ ] El contexto base está vivo: la IA mencionó una regla o restricción sin que la repitieras.
- [ ] La memoria funciona: la IA recordó un detalle de una decisión anterior registrada.
- [ ] Una skill se activó: la IA aplicó una convención o protocolo de la skill sin recordatorio.
- [ ] Un subagente operó con su contexto: trajo sus propias invariantes al trabajo.
- [ ] Un hook bloqueó una violación: detuvo la acción que provocaste a propósito.

---

## 10. Qué sigue siendo humano

Con todo instalado y funcionando, puede parecer que la IA toma las decisiones. No es así. El método preserva la autoridad humana en cada punto crítico.

**¿Qué sigue requiriendo aprobación humana?**

Aunque la IA arma propuestas, planes y borradores, el humano sigue siendo quien decide:

- **Aprobar planes antes de ejecutar.** La IA propone; el humano aprueba. Ninguna acción procede sin confirmación explícita.
- **Consolidar cambios en archivos definitivos.** La IA genera; el humano revisa, adapta y escribe en los archivos maestros. Eso asegura que lo que queda es lo que el humano quiso, no lo que la IA produjo.
- **Publicar hacia afuera.** Antes de que cualquier contenido vea luz pública (publicación, envío, post), el humano lo pasa por su propia voz, su juicio y su criterio. Es su firma al final.
- **Decisiones de riesgo alto o irreversibles.** Eliminar datos, cambiar configuración crítica, modificar políticas, tomar decisiones que afecten a terceros: todo eso sigue siendo del humano.
- **Decisiones estratégicas o éticas.** Qué se publica, para quién, con qué propósito. Cómo se maneja un dilema entre velocidad y precisión. Cuándo detener un proceso. Eso es responsabilidad irreductiblemente humana.

**La regla que lo resume:** se automatiza el armado, no el juicio. La IA acelera el trabajo; el humano sigue siendo quien decide.

¿Por qué? Porque la autoridad humana es el centro del método. La IA aumenta la capacidad del humano, no lo reemplaza. El contrato fundamental es innegociable: toda acción se planifica y se aprueba por el humano *antes* de ejecutar. Eso no cambia con la escala ni con los años.

Para la teoría de fondo sobre autoridad humana y límites reales del método, ver el documento del método.

---

## 11. Mantenimiento: cuándo sumar una pieza nueva

El andamiaje no es estático. A medida que el trabajo evoluciona, aparecen patrones que se repiten: instrucciones que das igual cada vez, decisiones que resolvés con el mismo criterio, o fallos predecibles que suceden en el mismo punto. Detectarlos y convertirlos en piezas nuevas es el verdadero mantenimiento del sistema.

El **criterio de los 2–3 ciclos** te protege de dos extremos igualmente costosos: automatizar demasiado pronto (cuando todavía cambiás de opinión) y dejar que la ineficiencia se acumule (cuando el patrón ya está enraizado). Si algo sucede exactamente igual dos o tres veces, es señal de que merece ser capturado; antes es prematuro; mucho después, el costo de repararlo ya es alto.

La pregunta clave es: **¿cuál es el síntoma?** El síntoma te dice qué pieza usar:

- **Repetís el mismo contexto o preámbulo** cada vez que delegás una tarea → **subagente**. La pieza lleva el contexto prearmado; el agente ejecuta con él.
- **Hay un cuerpo de convenciones o reglas** que aplicás siempre en un dominio → **skill**. Condensa el "cómo trabajamos acá" y lo hace reutilizable.
- **Una regla objetiva que NUNCA debe romperse**, cuyo incumplimiento es un fallo recurrente y predecible → **hook**. Se ejecuta automáticamente; no depende de la memoria.

Este checkpoint de automatización no es único: se repite. Cada cierto tiempo (o cuando notes que algo se repite), volvés a evaluar. El propio uso del método alimenta su crecimiento: los patrones que emergen del trabajo diario son la materia prima de las piezas nuevas.

Para la tabla de decisión completa y ejemplos de cada pieza, ver el documento del método.

---

## 12. Apéndice: materialización en Claude Code

Las cinco piezas del método no son abstracciones: en Claude Code cada una se materializa en un archivo o en una entrada de configuración concreta, que la herramienta descubre y aplica sola desde la primera sesión. Este apéndice mapea cada pieza a su lugar exacto y muestra la sintaxis real de registro de un hook, para que puedas copiar y adaptar sin adivinar. Los nombres de archivos de ejemplo son ilustrativos: reemplazalos por los tuyos.

### Tabla de correspondencia

| Pieza genérica | Ubicación en Claude Code |
|---|---|
| Archivo de contexto base | `CLAUDE.md` en la raíz del proyecto |
| Memoria persistente | un índice `MEMORY.md` + archivos temáticos (p. ej. bajo `.claude/memoria/`), versionados en git |
| Skills | `.claude/skills/<nombre-skill>/SKILL.md` (frontmatter `name` + `description` con disparadores) |
| Subagentes | `.claude/agents/<nombre>.md` (frontmatter `name`, `description`, `tools`, `model` + cuerpo con rol e invariantes) |
| Hooks | un script (p. ej. `.claude/hooks/<nombre>.js`) registrado en `.claude/settings.json` |

Cada ubicación respeta la lógica de las secciones anteriores: el contexto base se auto-carga, las skills se auto-activan por su `description`, los subagentes se invocan al delegar, y los hooks se disparan ante eventos. Todo es texto plano y se versiona en git, así que clonar el repositorio reinstala el andamiaje completo.

### Registro de un hook en `settings.json`

Un hook es un script más su registro. La clave `hooks` es un objeto indexado por evento (`PreToolUse` puede bloquear antes de la acción; `PostToolUse` valida después). Cada entrada lleva un `matcher` (qué herramientas la disparan) y un array `hooks` con el comando a ejecutar:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          { "type": "command", "command": "node .claude/hooks/block-secrets.js" }
        ]
      }
    ]
  }
}
```

El script recibe el evento como JSON por stdin; la entrada de la herramienta llega bajo `tool_input`:

```javascript
#!/usr/bin/env node
const event = JSON.parse(require('fs').readFileSync(0, 'utf-8'));
const filePath = event.tool_input?.file_path || '';
const content = event.tool_input?.content || '';

if (/secret|api[_-]?key|password/i.test(content) && filePath.includes('config')) {
  console.error('Rechazo: no se pueden guardar credenciales en archivos de config.');
  process.exit(2); // bloquea la acción
}
process.exit(0); // permite la acción
```

**Convención de códigos de salida:** `exit 2` bloquea (el `stderr` se le muestra al modelo para que corrija); `exit 0` permite.

### Cuándo quedan activos

Claude Code lee `.claude/settings.json` **al iniciar la sesión**: desde ese momento el hook queda activo y se dispara en cada evento que matchee (cada `Edit`/`Write`, en el ejemplo), sin invocación manual —no corre una sola vez al abrir, sino en cada acción que coincida—. Lo mismo vale para el resto: al arrancar, la herramienta descubre las skills disponibles (por carpeta en `.claude/skills/`), los subagentes invocables (por archivo en `.claude/agents/`) y el contexto base (`CLAUDE.md`). Esa auto-detección al inicio es lo que convierte la instalación en andamiaje vivo, no en un "setup de una sola vez".

### Estructura de carpetas ilustrativa

```
mi-proyecto/
├── CLAUDE.md
├── MEMORY.md
└── .claude/
    ├── settings.json
    ├── skills/
    │   └── convenciones-proyecto/SKILL.md
    ├── agents/
    │   ├── ejecutor.md
    │   └── revisor.md
    ├── hooks/
    │   └── block-secrets.js
    └── memoria/
        ├── decisiones-clave.md
        └── pendientes.md
```

---

## Anexo A — Bitácora de dogfooding (registro de incidencias)

> Esta guía se construye usándose a sí misma. Cada sección la redacta un ejecutor
> económico y la audita un revisor independiente (quality-guardian) antes de la
> consolidación humana. Esta bitácora registra cada incidencia capturada en la
> revisión: qué se detectó, severidad, cómo se resolvió y por qué importaba.

### Sección 1 — Qué instala y qué garantiza · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Veredicto del revisor: APTO** (265 palabras, en rango). Sin bloqueantes. Mejoras aplicadas por el director al consolidar:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 1.1 | Pieza 3 (skills) traía ejemplo parentético "documentar avances" — coincide con un nombre de skill plausible y real; podía leerse como feature instalada | 🟡 Mejora | Eliminado el ejemplo; la pieza quedó como adelanto puro | La ficha pedía nombrar las 5 piezas "sin desarrollarlas"; un ejemplo concreto ya es desarrollo y arriesga confundir ilustración con hecho |
| 1.2 | Pieza 5 (hooks) traía ejemplo parentético "verificar antes de pushear" — mismo patrón | 🟡 Mejora | Eliminado el ejemplo; adelanto puro | Igual que 1.1; coherencia con el mandato de "solo adelanto" |
| 1.3 | El lado humano se desarrollaba en 3 frases (lista de 4 verbos) cuando la ficha pedía solo adelanto de 1–2 | ⚪ Menor | Recortado a una frase ("aprueba lo que importa antes de que se ejecute"); el detalle se reserva para su sección | Evita agotar contenido que pertenece a la sección "Qué sigue siendo humano" (duplicación entre secciones) |
| 1.4 | El término clave "auto-activación por sesión" no aparecía literal | ⚪ Menor | Incorporado literalmente ("se auto-activa por sesión") | Coherencia terminológica entre secciones del documento |

**Lección / calibración:** el redactor tiende a **ilustrar de más** (agregar ejemplos concretos no pedidos) incluso cuando la ficha pide adelanto puro. Los ejemplos estaban correctamente marcados con "p. ej." y no falseaban la verdad-base —el revisor lo reconoció— pero invadían el alcance de secciones posteriores. Antídoto: la frontera "NO debe tocar / sin desarrollarlas" se aplica también a los ejemplos, no solo a las afirmaciones.

### Sección 2 — Requisitos previos · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — dos bloqueantes:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 2.1 | Nombró la herramienta concreta "Git" en el cuerpo ("Git u equivalente") | 🔴 Bloqueante | Reemplazado por "un sistema de control de versiones"; el nombre concreto se reserva para el Apéndice | El cuerpo es genérico/portable; los nombres de herramientas van al Apéndice (frontera "NO debe tocar" de la ficha) |
| 2.2 | Omisión de la remisión obligatoria a los límites del método | 🔴 Bloqueante | Añadida remisión nominal al módulo «Límites y cuándo no usar el método» del documento del método | La ficha lo pedía explícito; sin él, el lector no sabe dónde se desarrolla "cuándo no aplica" |
| 2.3 | Frase con tono folleto ("un proyecto real en producción lo comprueba…") | 🟡 Mejora | Reemplazada por una afirmación neutra sobre replicabilidad de roles | La ficha prohíbe tono de folleto; el caso anecdótico no estaba pedido |
| 2.4 | Detalle de mecanismo de skills/subagentes (un requisito no es un manual) | 🟡 Mejora | Simplificado; el director recortó además el vestigio "con contexto heredado" al consolidar | El nivel de detalle excedía un checklist de requisitos |

**Re-auditoría: APTO** (231 palabras, ambos bloqueantes resueltos, sin hallazgos nuevos). Escalado NO disparado: por ser primera devolución, el redactor conservó su ronda y se corrigió en una pasada.

**Lección / calibración:** reaparecieron dos modos de fallo ya catalogados en la producción del método — **fuga de nombre concreto al cuerpo genérico** (afín al "ilustrar de más" de la Sección 1) y **omisión de un elemento obligatorio de la ficha** (la remisión). Confirma que el campo "Debe contener" funciona como checklist verificable: el revisor lo recorre punto por punto y la omisión salta.

**Enmienda posterior (2026-06-24, por decisión de la autoridad humana):** al redactar la Sección 3 se detectó que esta Sección 2 presentaba "tres modelos" como condición absoluta ("si no, el método no aplica"), lo que **contradecía** el principio *rol ≠ modelo* y la versión reducida con un solo modelo. Se reformuló: los roles son sombreros (no modelos distintos); el acceso a varios modelos **gradúa el rigor pero no bloquea el arranque**; los requisitos duros son el entorno y el control de versiones. Es un caso de **coherencia entre secciones** que solo se ve cuando una sección posterior tensiona a una anterior — el documento vivo se corrige a sí mismo.

### Sección 4 — Archivo de contexto base · 2026-06-24 · SEGUNDA ACTIVACIÓN DE LA REGLA DE ESCALADO

Esta sección atravesó las **tres etapas** de la escalera de aseguramiento (como el M4 del documento del método).

**Ronda 1 — Ejecutor: Haiku · Revisor: quality-guardian (Sonnet) → RECHAZADO** (3 bloqueantes):

| # | Hallazgo | Severidad | Por qué importaba |
|---|----------|-----------|-------------------|
| 4.1 | La plantilla no usaba las secciones exigidas (faltaban *Objetivo* y *Contexto/stack*) | 🔴 Bloqueante | Requisito verbatim de la ficha |
| 4.2 | La plantilla incluía "Proyectos / recursos clave con rutas absolutas" → atada a un workspace multi-proyecto concreto | 🔴 Bloqueante | La plantilla debe servir para cualquier proyecto (error explícito a evitar) |
| 4.3 | Placeholders con entidades HTML escapadas en vez de signos crudos | 🔴 Bloqueante | Con entidades escapadas, el lector copia una plantilla rota |

**Ronda 2 (re-auditoría) — Ejecutor: Haiku · Revisor: quality-guardian → RECHAZADO.** Haiku resolvió 4.1–4.3 pero **introdujo una regresión nueva**: reintrodujo el nombre concreto del archivo de una herramienta (`CLAUDE.md`) tres veces en la prosa del cuerpo genérico — justo lo que la versión previa había mantenido correctamente en genérico. **Re-auditoría con 🔴 → DISPARA el escalado.**

**Ronda 3 (escalada) — Ejecutor: Sonnet · Revisor: Opus (director) → APTO.** Conforme a la regla de aseguramiento proporcional a la severidad, al reincidir el bloqueante en la re-auditoría la iteración subió un nivel: ejecutor de Haiku a **Sonnet**, revisor de quality-guardian a **Opus** (preservando revisor > ejecutor). Se le entregó a Sonnet **todo el set de restricciones junto**. Sonnet las sostuvo todas a la vez: reformuló la referencia al archivo en genérico + remisión al Apéndice, conservó las secciones exactas de la plantilla y los signos crudos. Auditoría de Opus: APTO, sin bloqueantes.

**Lección / calibración — el patrón del M4 se repitió:** el ejecutor económico entró en un **ciclo de "arreglo-por-un-lado, rompe-por-otro"** (resolver 4.1–4.3 le costó introducir la regresión del nombre concreto). No es que "se esforzara poco": es que **sostener varias restricciones simultáneas a la vez excede su ventana fiable**. El nivel superior no solo cumplió, sino que aprovechó el margen para *mejorar* el texto (autoridad de aprobación, herencia entre ramas) sin violar ninguna regla — coherente con M2: la capacidad extra se invierte mejor en lo difícil. Evidencia adicional de que la defensa no es "pedirle más al mismo ejecutor", sino la **estructura** (escalado por evidencia + revisor independiente de mayor capacidad).

### Sección 3 — Mapa de las 5 piezas · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — dos bloqueantes:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 3.1 | Cuerpo de 151 palabras, muy por debajo del rango 250–350 (déficit ~40 %) | 🔴 Bloqueante | El redactor amplió a ~287 palabras desarrollando "capas" y la aclaración rol≠modelo | Requisito numérico verificable de la ficha |
| 3.2 | Remisión a una sección inexistente ("Requisitos de infraestructura") | 🔴 Bloqueante | Corregida al nombre real, "Requisitos previos" | Un enlace a una sección que no existe rompe la navegación del lector |
| 3.3 | "gestor de configuración" en la fila de hooks (término ajeno al resto) | ⚪ Menor | Unificado a "entorno" | Coherencia terminológica de la tabla |

**Re-auditoría: APTO con ajustes** (287 palabras; los 3 bloqueantes resueltos). Escalado NO disparado (primera devolución). Pero el revisor cazó un **hallazgo nuevo en el contenido agregado**:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 3.4 | Al ampliar, el redactor introdujo un párrafo de **cadena de dependencia estricta** ("si no hay subagentes, los hooks no tienen dónde verificar") que se **contradecía** con el marco de "capas complementarias, no excluyentes" del párrafo anterior — y es factualmente falso (un hook puede verificar reglas objetivas sin subagentes) | 🟡 Mejora | El director reformuló el párrafo: el orden es *refuerzo, no dependencia rígida*; se explicitó que **cada pieza aporta valor por sí sola** y que se puede instalar "una, algunas o todas" | Una sobre-afirmación introducida *al corregir* otro hallazgo; refuerza que ampliar texto puede crear defectos nuevos |

**Lección / calibración:** modo de fallo instructivo — **la corrección de un bloqueante (extensión corta) creó un defecto nuevo** (sobre-afirmación por relleno). Es la contracara del "ilustrar de más": cuando se pide *más* texto, el redactor puede fabricar estructura conceptual que suena sólida pero contradice la tesis del propio documento. Antídoto: la re-auditoría no solo verifica que el bloqueante viejo se resolvió, sino que **audita el contenido nuevo como si fuera una pieza fresca**. También reafirma "verificar, no confiar": el director había anticipado este riesgo y lo señaló al revisor antes de la re-auditoría.

### Sección 5 — Memoria persistente · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — dos bloqueantes:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 5.1 | La Plantilla 1 (índice) usaba encabezados (Usuario/Proyecto/Decisiones/Aprendizajes) que NO coincidían con los cuatro tipos definidos en el texto (Usuario/Feedback/Proyecto/Reference) | 🔴 Bloqueante | Alineados los encabezados de la Plantilla 1 a los cuatro tipos | Contradicción interna entre el texto y su propia plantilla confunde al lector que la copia |
| 5.2 | No se podía confirmar que las plantillas fueran bloques de código copiables con signos crudos | 🔴 Bloqueante | Verificado en la re-auditoría: dos bloques ```markdown con placeholders `<...>` crudos | El criterio de listo es que el lector copie una plantilla funcional, no rota |

**Re-auditoría: APTO con ajustes** (~340 palabras). Escalado NO disparado (primera devolución). Quedó un 🟡: el campo `type` en inglés (`user | feedback | project | reference`) frente a etiquetas en español (Usuario/Feedback/Proyecto/Referencia).

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 5.3 | Inconsistencia de idioma: etiqueta "Referencia" (ES) vs valor `reference` (EN) en el campo `type` | 🟡 Mejora | El director fijó la convención con una nota: los encabezados legibles van en el idioma del usuario, pero el valor de `type` se mantiene en inglés por ser etiqueta técnica *machine-readable* | Sin la convención explícita, el lector no sabría si escribir `type: referencia` o `type: reference` |

**Lección / calibración:** modo de fallo de **coherencia texto↔plantilla** — el redactor definió cuatro tipos en la prosa pero armó la plantilla con otra taxonomía (Decisiones/Aprendizajes). Es un pariente de la "omisión de elemento de la ficha": el artefacto entregado no refleja lo que el propio texto promete. Antídoto: la plantilla se audita **contra la definición que la precede en la misma sección**, no de forma aislada.

### Sección 6 — Skills auto-activables · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Veredicto del revisor: APTO** (389 palabras, en rango), **sin bloqueantes ni mejoras** — la sección más limpia hasta aquí, junto con la Sección 1. El redactor sostuvo todas las restricciones a la primera: genericidad (cero nombres de herramientas o skills reales), el dato duro "la skill se **carga**, no se entrena" bien enunciado, las dos skills recomendadas presentes, y la plantilla con el campo `description` modelado como el disparador central.

**Nota de proceso:** hubo un reintento por un corte de red del ejecutor (no de contenido); el segundo intento salió limpio. Único punto verificado por el director al consolidar: que los placeholders `<...>` de la plantilla quedaran con signos **crudos** (confirmado).

**Lección / calibración:** contraste con las secciones "pieza por pieza" previas (F4, F5) que tropezaron con la genericidad y las plantillas. Aquí las **salvaguardas acumuladas** —instrucción explícita de "nombre concreto → Apéndice" y "signos crudos" desde el encargo— evitaron los modos de fallo ya catalogados. Es el efecto buscado de la bitácora: cada fallo registrado se convierte en una barrera que previene su reincidencia. La detección deja de ser la primera red cuando la prevención hace su trabajo (eco del hallazgo de M6 del método).

### Sección 7 — Subagentes precargados · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — un bloqueante:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 7.1 | **Omisión de elemento obligatorio:** faltaba la remisión al documento del método para la teoría de roles | 🔴 Bloqueante | El director añadió una línea de remisión al cierre de "Qué configuro" (verificación proporcional, sin re-auditoría completa por ser inserción de una línea que el propio revisor especificó) | La ficha lo pedía explícito; sin él, el lector no sabe dónde se desarrolla el porqué de los dos roles |

Lo demás cumplió a la primera: 325 palabras en rango, genericidad (cero nombres concretos), signos crudos, y **las dos reglas duras explícitas** (ejecutor "devuelve contenido, no persiste"; revisor independiente y un nivel por encima). Un 🟡 del revisor ("ver el Apéndice colgante") se descartó como **falso positivo de aislamiento**: el revisor auditó la sección sola, pero en el documento completo el Apéndice (Sección 12) existe y la remisión es coherente con F4–F6.

**Lección / calibración:** reaparece el modo de fallo **omisión de un elemento obligatorio de la ficha** (ya visto en M9 del método y en la Sección 2). Es el más silencioso: el redactor desarrolla bien lo que incluye, pero deja fuera un requisito. Confirma que el antídoto es recorrer el "Debe contener" como checklist cerrado. También ilustra "verificar, no confiar" hacia el revisor: no todo 🟡 sobrevive al contexto completo (el del Apéndice era un artefacto de auditar en aislamiento).

### Sección 8 — Hooks de enforcement · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — un bloqueante + dos mejoras:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 8.1 | Extensión 451 palabras, ~13 % sobre el tope de 400 | 🔴 Bloqueante | El director podó "Qué hace" y "Advertencia de diseño" a ~387 palabras sin perder contenido obligatorio | Rango cerrado y verificable de la ficha; la consistencia de extensión entre secciones |
| 8.2 | Faltaba la remisión al método para "cuándo industrializar" una regla (solo remitía para Detección/Recuperación) | 🟡 Mejora | Añadida la remisión en "Qué hace" | La ficha pedía los dos anclajes al documento madre |
| 8.3 | Los nombres de ejemplo (`.env`, etc.) venían con `<...>`, pisando la sintaxis de placeholder de la plantilla | 🟡 Mejora | Reemplazados por backticks (`.env`, `secrets.json`, `password.txt`) | En una sección con plantilla copiable, `<...>` debe significar "reemplazar esto"; confundir ejemplo con placeholder rompe la usabilidad |

**Lección / calibración:** dos modos de fallo ya catalogados, juntos — **exceso de extensión** (como M5 del método) y **colisión de notación** (los `<...>` de ejemplo contra los `<...>` de placeholder), un pariente fino de la coherencia texto↔plantilla. El resto (genericidad, pre/post-evento, falsos positivos, "subjetivo = skill", plantilla) salió a la primera. Con esta sección **se cierra el bloque de instalación pieza por pieza (F4–F8)**; restan las secciones de cierre (verificación, límites humanos, mantenimiento y apéndice).

### Sección 9 — Verificar la instalación · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Primera devolución del revisor: RECHAZADO** — un bloqueante + una mejora:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 9.1 | **Embellecimiento:** el ancla inventó detalles de fallas no verificados ("inconsistencias en el orden de carga", "señales solapadas") sobre la prueba en vivo del proyecto real | 🔴 Bloqueante | Eliminados los ejemplos inventados; se dejó la afirmación honesta y genérica ("errores que la revisión estática no anticipaba") | Dato plausible pero no confirmado = dato incorrecto (regla de exactitud); el documento predica honestidad, no puede fabricar en su propio ancla |
| 9.2 | El ancla no remitía explícitamente al documento del método | 🟡 Mejora | Añadida la remisión ("la etapa que el propio método reserva como red final") | La ficha lo pedía; cierra el círculo con el documento madre |

**Nota de proceso — doble detección:** el director **anticipó** el embellecimiento en su pre-lectura y se lo señaló explícitamente al revisor; el revisor lo **confirmó** de forma independiente. Es la configuración ideal de "verificar, no confiar": la sospecha del director no reemplaza la auditoría independiente, la refuerza.

**Lección / calibración:** reaparece la **fabricación/embellecimiento** —el modo de fallo más peligroso del redactor— y, de nuevo, en un ancla a "hechos reales". Confirma el patrón de M3/M7 del método: el redactor rellena huecos de especificidad con detalle inventado que "suena verificable". Antídoto ya conocido: darle al revisor la **verdad-base** (acá, que los únicos hechos reales son genéricos) para que la fabricación no pase.

### Sección 10 — Qué sigue siendo humano · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Veredicto del revisor: APTO** (272 palabras, en rango). Sin bloqueantes. Único ajuste:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 10.1 | Typo "accelera" en la frase clave ("La IA accelera el trabajo") | 🟡 Mejora | Corregido a "acelera"; el director además unificó la remisión final a "el documento del método" | Un error ortográfico justo en la frase que sostiene la tesis resta pulido a un documento de método |

**Lección / calibración:** una de las secciones más limpias. La frase clave ("se automatiza el armado, no el juicio") y las cinco categorías de checkpoint humano salieron a la primera. Confirma que las secciones **conceptuales** (sin plantilla ni datos verificables) son las de menor tasa de incidencias del redactor: los modos de fallo graves (fabricación, fuga de nombre, colisión de notación) se concentran donde hay **datos concretos o artefactos técnicos** (anclas, plantillas, nombres). Corolario para el método: dimensionar la vigilancia por el tipo de contenido — más rigor donde hay hechos y código, menos donde es prosa conceptual.

### Sección 11 — Mantenimiento · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet)

**Veredicto del revisor: APTO** (262 palabras, en rango), **sin bloqueantes ni mejoras obligatorias** — solo un ⚪ cosmético de densidad tipográfica en los bullets, no aplicado. El redactor cumplió los cuatro requisitos a la primera: criterio de 2–3 ciclos, checkpoint recurrente, mapeo síntoma → herramienta (subagente/skill/hook) y remisión al método sin reproducir la tabla. **Y —el punto notable— mantuvo el ancla GENÉRICA sin fabricar detalles**, justo el modo de fallo que la sección anterior (S9) sí había disparado.

**Lección / calibración:** confirma el corolario recién anotado en S10: es una sección conceptual y salió limpia. Además, el redactor **no repitió el embellecimiento de S9** en un ancla equivalente (fallo recurrente → hook), porque el encargo esta vez incluyó explícitamente "mantené el ancla genérica, no inventes detalles". La prevención (instrucción anti-fabricación en el propio encargo) volvió a hacer el trabajo que en S9 tuvo que hacer la detección.

### Sección 12 — Apéndice: materialización en Claude Code · 2026-06-24 · Ejecutor: Haiku · Revisor: quality-guardian (Sonnet) · Verificación técnica: Opus

**Primera devolución del revisor: RECHAZADO** — un bloqueante + varias mejoras:

| # | Hallazgo | Severidad | Corrección aplicada | Por qué importaba |
|---|----------|-----------|---------------------|-------------------|
| 12.1 | **Fabricación de sintaxis:** el bloque `settings.json` usaba una forma inventada (array plano con `name`/`event`) que no existe en Claude Code | 🔴 Bloqueante | El director reescribió el bloque con la sintaxis real (objeto `hooks` indexado por evento, con `matcher` + array interno `hooks` de `{type, command}`) | Un apéndice de wiring cuyo ejemplo insignia no funciona es peor que no tenerlo: el lector copia algo roto |
| 12.2 | El script leía el payload como `event.parameters?.…` (campo inexistente) | 🟡 Mejora | Corregido a `event.tool_input?.…` | El lector que copia el script no detectaría nada, leyendo un campo vacío |
| 12.3 | "Los hooks se ejecutan al iniciar cada sesión" — ambiguo (sugiere que corren una vez al abrir) | 🟡 Mejora | Reformulado: quedan *activos* al iniciar y se *disparan* en cada evento que matchee | Evita que el lector crea que el hook corre una sola vez |
| 12.4 | Cuerpo de prosa por debajo del rango (350–500) | 🟡 Mejora | Ampliado con contexto de la tabla y la nota de activación, sin re-explicar el "para qué" de cada pieza | Requisito de extensión de la ficha |

**Nota de proceso — verificación técnica del director:** la fabricación de sintaxis fue **anticipada por el director** (que conoce la sintaxis real de Claude Code) y **confirmada de forma independiente por el revisor**, al que se le entregó la sintaxis correcta como verdad-base. Doble detección, como en S9.

**Lección / calibración — cierre del repertorio de fallos:** el apéndice concentra el mayor riesgo de **fabricación técnica** de todo el documento, porque es la única sección que pisa detalle concreto de una herramienta. Confirma, por última vez, el hallazgo estructural de esta bitácora: los modos de fallo graves del redactor (fabricación, fuga de nombre, colisión de notación, embellecimiento) **se concentran donde hay hechos, código o sintaxis verificables**, no en la prosa conceptual. El antídoto que funcionó en las 12 secciones fue siempre el mismo: **verdad-base al redactor + detección independiente + verificación del director sobre lo verificable**, cada capa cubriendo lo que la anterior podía dejar pasar.

---

## Cierre — Estado del documento

Las **12 secciones están consolidadas** y la guía está completa: la promesa (Sección 1), los requisitos (2), el mapa de las 5 piezas (3), la instalación pieza por pieza (4–8), la verificación (9), los límites humanos (10), el mantenimiento (11) y el apéndice concreto de Claude Code (12). Esta bitácora registra **12 sesiones de incidencias** que cubren el repertorio completo de modos de fallo del redactor —**ilustrar de más, fuga de nombre concreto, omisión de elemento obligatorio, coherencia texto↔plantilla, exceso de extensión, colisión de notación, embellecimiento y fabricación de sintaxis**—, dos activaciones reales de la regla de escalado (Secciones 4 y, en la producción del método, M4) y varios casos de falibilidad del propio revisor y del director corregidos por la estructura. En todos, lo que contuvo el error no fue confiar en un rol, sino el andamiaje: verdad-base, revisión independiente y verificación proporcional. Ese es, en una frase, el método que esta guía enseña a instalar.

Producida con el blueprint en [`guía-instalación-fichas.md`](guía-instalación-fichas.md).

## 4. Memoria persistente como activo de continuidad

Cada sesión de trabajo con la IA comienza sin memoria de las conversaciones anteriores. El modelo LLM arranca sin contexto sobre qué se decidió, qué falló, qué restricciones rigen el proyecto o hacia dónde se orienta el trabajo. Este "olvido entre sesiones" no es un fallo técnico, sino una característica estructural: el modelo responde en base a lo que recibe en la conversación actual, no a un registro automático de lo que pasó antes. Por ello, la memoria persistente es un activo crítico que cierra ese vacío.

La memoria no reemplaza al repositorio de código ni al historial de git (véase Módulo 9 para control de versiones). En cambio, captura el *contexto vivo del proyecto*: decisiones tomadas, restricciones no derivables del código, acuerdos sobre cómo debe trabajar la IA, y referencias a recursos externos. Sin esta memoria, cada sesión reinicia en cero, perdiendo continuidad estratégica y operativa.

### Qué se guarda y qué no

Se **guardan** hechos que resuelven preguntas recurrentes: quién es el usuario (roles, preferencias, historia), cómo la IA debe comportarse (correcciones, refinamientos, porqué de cada acuerdo), metas y restricciones del proyecto vigente, y enlaces a recursos externos (tableros, documentos de referencia, URLs vivas).

Se **no guardan**: contenido que ya vive en el código o el repositorio (funciones, assets, configuración versionada); el historial completo de git (eso es responsabilidad del control de versiones); ni lo efímero de una charla puntual (pasos de un debug que se resolvió, ideas desestimadas en una sola sesión).

### Organización: índice y archivos atómicos

La memoria se estructura como un **archivo índice** que lista y resume todos los archivos de memoria, más una colección de **archivos temáticos** enlazados entre sí. Cada archivo aborda un tema discreto (por ejemplo, "preferencias del usuario", "restricciones del proyecto", "decisiones arquitectónicas"). El índice actúa como mapa: indica qué existe, dónde encontrarlo, y una línea de qué contiene.

### Los cuatro tipos de memoria

| Tipo | Contenido | Para qué |
|------|----------|---------|
| **User** | Rol, preferencias, historia, quién es la persona | Personalizar tono, entender intenciones, respetar límites |
| **Feedback** | Correcciones, acuerdos sobre cómo debe trabajar la IA, porqué de cada regla | Refinar comportamiento sin repetir el mismo error |
| **Project** | Metas vigentes, restricciones no derivables del código, decisiones clave | Mantener alineación y evitar retrocesos |
| **Reference** | URLs, tableros, tickets, documentos de referencia | Acceso rápido sin buscar |

### Recuperación y continuidad

Cuando comienza una sesión, la IA (o la persona) consulta el índice de memoria como punto de entrada: es el mapa que muestra qué archivos existen y de qué tratan. A partir de ahí, se trae al contexto lo que resulta pertinente para esa conversación. No existe un mecanismo automático que filtre o seleccione archivos según el tipo de tarea a realizar; el índice ofrece visibilidad sobre lo disponible, y la lectura de lo relevante es un paso deliberado, no una regla fija de clasificación. Aun así, el efecto práctico es el mismo: el trabajo puede continuar sin perder contexto, porque el método, los roles, las restricciones y la historia del proyecto quedan accesibles desde el índice, en vez de tener que reconstruirse desde cero en cada sesión.

La memoria es viva: se actualiza cuando cambian decisiones, se agregan restricciones nuevas, o se cierra un ciclo de aprendizaje. No es un historial congelado, sino un almacén de verdad operativa que crece y se refina con cada sesión.

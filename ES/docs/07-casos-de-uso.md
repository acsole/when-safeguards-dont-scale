## 7. Casos de uso

### Caso 1: La producción de este documento (dogfooding paso a paso)

El documento "Método de trabajo con IA" que estás leyendo fue producido **usando el propio método**. Este es el ejemplo vivo más claro de cómo funciona en la práctica.

**Situación inicial:** Un equipo humano-IA necesitaba documentar cómo colabora para producir trabajo de calidad. La apuesta era ambiciosa: que el método se probara a sí mismo durante su redacción.

**Aplicación del método:**

En primer lugar, el director (un modelo de razonamiento superior) y el humano definieron juntos un esqueleto de 9 módulos. Para cada uno, redactaron una "ficha de encargo"—un documento con alcance, fronteras y condiciones de éxito precisas.

A continuación, para cada módulo, el redactor ejecutor (un modelo rápido y económico) recibía su ficha, producía un borrador y lo devolvía en prosa, sin escribir archivos. El texto pasaba inmediatamente a revisión.

El revisor independiente (un modelo de capacidad media, en rol de guardián) auditaba cada borrador contra su ficha. Su tarea: ¿responde todas las preguntas?, ¿se mantiene dentro de las fronteras?, ¿hay datos inventados?

Cuando hallazgos llegaban, el módulo volvía al redactor con feedback concreto. La ronda se reiteraba hasta que el revisor daba el visto bueno.

Finalmente, el director consolidaba el módulo aprobado, lo guardaba en control de versiones (un commit por módulo) y alimentaba una bitácora que registraba cada incidencia: qué revisiones fueron necesarias, dónde falló la primera versión, cuándo se escaló a capacidad mayor.

**Resultados concretos:**

El revisor cazó **fabricaciones reales**: un módulo afirmaba que "algunos módulos llegaron a tres rondas" cuando el máximo real eran dos; otro módulo inventó una regla de selección de memoria según el tipo de tarea, que no existía en el protocolo.

El revisor también cazó **omisiones**: módulos que perdían elementos obligatorios de la ficha, y **redundancias**: frases que repetían conceptos explicados párrafos arriba.

En un módulo, una **regla de escalado se activó**: el redactor reincidió en un fallo específico. Por protocolo, la tarea subió a un redactor más capaz y el revisor subió al director (un nivel por encima). El resultado: módulo correcto en segunda ronda.

En otro caso, el revisor incluso **corrigió al director**: una estimación de longitud que el director había hecho resultó equivocada; el revisor lo señaló.

**Lección transferible:** El método no previene fallos—los produce y los atrapa. La revisión independiente actúa como red de contención. Lo importante es registrar abiertamente dónde falló cada intento (la bitácora), porque ese registro es evidencia de rigor, no de incompetencia.

### Caso 2: ASLAN (validación en producción)

ASLAN es un dashboard que monitorea proyectos en paralelo. Se construyó usando este mismo método: fichas, redactor, revisor, director, escalado cuando era necesario.

**Situación:** El dashboard estaba "listo" según la revisión estática. Pero el método incluye un paso crítico: **probar en condiciones reales**.

**Qué pasó:** En producción, la prueba reveló dos errores que el diseño no anticipaba. Primero: identidades de agentes que colisionaban. Segundo: elementos que no expiraban cuando debían.

Ambos se corrigieron. Sin la prueba en vivo, esos errores hubieran llegado a usuarios.

**Lección transferible:** Probar en condiciones reales revela fallos que el diseño teórico no anticipa. El método completo es: construir → revisar → probar → encontrar → corregir. Cada ciclo tensa el trabajo y lo mejora.

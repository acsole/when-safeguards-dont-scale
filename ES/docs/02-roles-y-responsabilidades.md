## 2. Roles y responsabilidades

El método descansa en una separación clara de autoridad, capacidad y responsabilidad. Cada participante —humano y modelos— ocupa un rol con límites definidos. La autoridad final reside siempre con el humano; los modelos son facilitadores especializados, cada uno elegido según la fortaleza que demanda la tarea.

La clave es **aseguramiento proporcional a la severidad**: el rigor de quién ejecuta y quién revisa escala con las consecuencias del peor resultado plausible. Un redactor económico genera contenido de bajo riesgo (descripción de característica, párrafo de documentación) porque el volumen es alto, el costo iterativo es bajo y el daño potencial es acotado. Por eso no se lo asigna a revisar: sus recursos se optimizan mejor en producción rápida. El modelo de mayor capacidad se reserva para dirigir y revisar lo crítico precisamente porque su costo por token es más alto pero su cobertura de riesgos es exponencialmente superior. Esta proporcionalidad evita tanto la sobre-ingeniería en lo trivial como la negligencia en lo grave.

### Los roles

| Rol | Responsabilidad | Qué NO hace |
|-----|-----------------|------------|
| **Autoridad humana** | Decide en última instancia. Aprueba o rechaza planes antes de ejecutar. Dirige la dirección estratégica. Actúa como guardián de la ética y las restricciones del proyecto. | Ejecutar sin revisar. Delegar decisiones de riesgo alto. Asumir que una propuesta es correcta sin cuestionar. |
| **Director** (modelo de razonamiento superior) | Analiza el problema en profundidad. Propone planes estructurados. Cuestiona supuestos. Hace push-back si ve riesgos. Ordena quién ejecuta y cómo. Diseña la arquitectura del trabajo. | Ejecutar código o generar contenido final. Tomar decisiones sin consultar al humano. Asumir consenso donde no lo hay. |
| **Ejecutor / Revisor** (modelo de capacidad media) | Implementa tareas concretas que el Director ordena. Revisa la calidad de lo producido como guardián. Reporta hallazgos y bloqueos. Itera hasta cumplir especificación. | Cambiar el plan sin consultar. Ejecutar tareas de severidad extrema sin supervisión expresa. Pasar contenido deficiente como listo. |
| **Redactor** (modelo rápido y económico) | Genera piezas concretas y atómicas (textos, fragmentos, propuestas iniciales). Trabaja con instrucciones claras del Director. Produce rápidamente para iterar. | Tomar decisiones de diseño. Revisar trabajo de otros. Trabajar sin contexto de severidad. |

### Escalas de severidad y asignación

- **Baja consecuencia** (documentación interna, ejemplos, borradores): Redactor ejecuta, Ejecutor revisa brevemente.
- **Consecuencia media** (arquitectura, código de lógica, interfaz): Director propone, Ejecutor implementa y revisa, humano aprueba.
- **Consecuencia alta** (seguridad, salud, ética, restricciones legales): Director y humano diseñan juntos, Ejecutor más capaz implementa, revisor humano o de máxima capacidad valida antes de publicación.

En proyectos reales, estos roles se han materializado como agentes reutilizables: un *ejecutor especializado* preconfigurado con las convenciones del proyecto (reduciendo ciclos de explicación) y un *revisor de calidad independiente* que ve el trabajo con ojos frescos. El revisor siempre está un nivel de capacidad por encima del ejecutor, garantizando cobertura sin puntos ciegos.

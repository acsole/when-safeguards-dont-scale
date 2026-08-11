## 6. Industrialización

### Principio: automatizar lo repetido

En el ciclo de trabajo descrito en el Módulo 3, cada interacción con la IA es un evento donde se toman decisiones, se aplican convenciones, se revisan resultados. Cuando una de esas interacciones comienza a repetirse —el mismo preámbulo en cada delegación, la misma regla técnica a verificar, las mismas convenciones a aplicar— nace un candidato a industrializarse.

La industrialización es pasar de "repetir manualmente cada vez" a "automatizar la repetición". No es una decisión del primer ciclo; es una observación que surge después de dos, tres, cuatro interacciones similares. El checkpoint de automatización (Módulo 3) es el momento para formular la pregunta: ¿vale la pena invertir en automatizar esto?

La respuesta depende de tres herramientas que ofrece este entorno de trabajo con IA, cada una diseñada para un patrón distinto.

### Las tres herramientas de industrialización

**HOOK**: un script determinista que se ejecuta automáticamente ante un evento (por ejemplo, después de cada edición). Su fortaleza es el *enforcement*: puede bloquear una acción si viola una regla objetiva y verificable. Un ejemplo real: en el proyecto ASLAN (un dashboard multi-proyecto), existía un proceso manual donde el director corría un grep para garantizar que ningún archivo violase ciertas invariantes técnicas del código. Ese grep se automatizó como un hook que ejecuta la misma lógica cada vez que alguien edita. Si se viola la regla, el hook detiene la acción de forma automática, sin intervención humana en ese momento. Los hooks son para reglas que NUNCA deben romperse.

**SKILL**: un paquete de conocimiento, convenciones o procedimientos que la IA conoce y aplica a demanda. Es invocable: cuando la IA detecta que corresponde, la activa. Un ejemplo real: en ASLAN, las convenciones de diseño y técnicas del proyecto se encapsularon en una skill. Ahora, cada vez que se trabaja en el dashboard, esa skill se aplica sin repetir el mismo preámbulo largo. Las skills son para cuerpos de conocimiento que se aplican una y otra vez, con cierta flexibilidad según el contexto.

**SUBAGENTE**: un agente delegado con un rol específico y contexto precargado. Es útil cuando una tarea recurrente necesita un agente especializado que ya "sabe" qué hace. Un ejemplo real: en ASLAN, la delegación a un ejecutor requería repetir un preámbulo largo sobre las invariantes del proyecto. Se creó un subagente ejecutor que ya nace con ese contexto. Ahora, en cada delegación, el contexto viene incluido. Los subagentes son para roles repetidos que cargan mucho contexto.

### Tabla de decisión

| Síntoma | Herramienta | Razón |
|---------|-------------|-------|
| "Repito el mismo preámbulo/contexto en cada delegación" | Subagente | Precarga el contexto una sola vez; elimina la repetición en la comunicación |
| "Hay un cuerpo de convenciones que aplico siempre" | Skill | Encapsula conocimiento reutilizable; la IA lo invoca cuando corresponde |
| "Una regla técnica objetiva que NO debe violarse nunca" | Hook | Automatiza una verificación determinista; bloquea el incumplimiento |

### Cómo elegir y combinar

La pregunta central es: ¿qué tipo de repetición tengo?

- Si es **contexto/preámbulo que se repite**, usá **subagente**.
- Si es **conocimiento/convención que se aplica**, usá **skill**.
- Si es **regla técnica que se debe forzar**, usá **hook**.

Y rara vez es "solo uno". En ASLAN, el ejecutor (subagente) aplica las convenciones (skill) y sus cambios son verificados por un hook: los tres trabajan juntos, cada uno en su rol. No son opciones excluyentes, sino capas que se complementan en un flujo maduro.

La madurez operativa llega cuando se reconocen los patrones temprano, sin esperar a que crezcan caóticamente. Dos o tres ciclos suelen bastar para saber si conviene industrializar. Automatizar antes es prematuro; esperar más es ineficiencia acumulada.

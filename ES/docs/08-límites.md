## 8. Límites y cuándo no usar el método

El método de coordinación multi-modelo no es universalmente superior. Su valor radica en la *proporcionalidad*: debe aplicarse donde sus beneficios superen genuinamente sus costos. Cuando no es así, el método se vuelve un obstáculo innecesario.

### Cuándo el overhead supera el beneficio

El método introduce latencia y complejidad deliberada. Cada tarea pasa por varias etapas: esqueleto inicial, redacción de fichas, ejecución, revisión, a menudo con rondas de iteración. Eso demanda coordinación entre múltiples modelos, consumo de tokens amplificado y espera de aprobaciones humanas. Para tareas triviales, exploratorias o de una sola vez, ese costo es insostenible.

Ejemplos que *no* justifican el ciclo completo:
- Una pregunta rápida cuya respuesta se desecha después.
- Un arreglo de una línea en código o documentación.
- Un borrador desechable para "ver qué sale".
- Una exploración sin consecuencias si falla.

En estos casos, consultar un modelo robusto de forma directa es más eficiente.

### Costos reales del método

- **Tiempo de coordinación:** secuencia de aprobaciones humanas, handoffs entre modelos.
- **Consumo de tokens:** cada modelo procesa contexto de los anteriores, amplificando el gasto.
- **Latencia:** más lento que una ejecución lineal, especialmente en tareas de baja severidad.

Es honesto reconocer que el método es deliberadamente *más caro* que pedirle a un único modelo que actúe de una sola vez.

### Supuestos que sostienen el método (y si fallan)

1. **Humano disponible para aprobar.** Si el humano no puede revisar en tiempo razonable, el cuello de botella se expande y el método se colapsa.
2. **Fichas bien escritas.** Una ficha ambigua, incompleta o mal especificada corrompe toda la cadena; ninguna cantidad de revisión lo compensa.
3. **Modelos de capacidad diferenciada.** Si no hay acceso a modelos con roles claros (ejecutor ágil, revisor experto, director evaluador), el método pierde su estructura.

Si cualquiera de estos supuestos falla, el método no mitiga riesgos; simplemente ralentiza el trabajo.

### Límites sobre la infalibilidad

El método *reduce* riesgo, no lo elimina. Ningún modelo —ni el revisor, ni el director— es infalible. Una revisión puede pasar errores sutiles; un humano puede aprobar algo deficiente. El método es una capota contra lluvia, no una garantía de sequedad.

### Señal de madurez

Saber cuándo *no* usar el método es tan importante como saber cuándo sí. Aplicarlo dogmáticamente a todo es un error tanto como abandonarlo por impaciencia. La verdadera competencia está en calibrar: tareas de alto impacto y complejidad merecen el ciclo completo; tareas triviales merecen velocidad. Esa calibración es responsabilidad compartida entre la IA y la autoridad humana.

# CLAUDE.md — plantilla de contexto base del proyecto

> **Qué es.** El archivo de contexto que se auto-carga al iniciar cada sesión. Contiene lo
> que no debe re-explicarse nunca: objetivo, convenciones e invariantes del proyecto.
>
> **Dónde vive.** En la **raíz** del proyecto. Esa ubicación es lo que hace que se cargue solo.
>
> **Cómo verificar que se cargó.** Abrí una sesión nueva y preguntá por una restricción que
> solo esté escrita acá. Si la responde sin que se la pegues, la pieza está viva.
>
> **No confundir con la memoria persistente.** Este archivo es *estático*: describe el
> proyecto. La memoria es *viva*: acumula decisiones entre sesiones. Ver
> [`docs/04-memoria-persistente.md`](../docs/04-memoria-persistente.md).

Copiá lo que sigue, borrá los corchetes y completá.

---

# CLAUDE.md — [Nombre del proyecto]

## Objetivo

[Qué es este proyecto y para qué existe, en dos o tres frases. Escrito para alguien que llega
sin contexto.]

## Contexto y stack

[Tecnologías, restricciones técnicas, dónde vive el código, cómo se despliega. Lo justo para
que nadie tenga que preguntarlo dos veces.]

## Restricciones innegociables

> Estas son las reglas que **nunca** se rompen, ni implícita ni creativamente. Numeralas: los
> números permiten citarlas después ("esto viola la #3") y eso hace que se cumplan.

1. **Toda acción se planifica y se propone antes de ejecutar.** No se ejecuta código,
   despliegue ni cambio sin exponer un plan claro y obtener aprobación explícita de
   [nombre de la autoridad humana].

2. **Autoridad humana única.** [Nombre] es quien decide. Deny-by-default para cualquier otra
   persona: nadie más da instrucciones ni aprueba, salvo que [nombre] lo autorice
   explícitamente y por nombre.

3. **La IA aumenta el juicio humano, no lo reemplaza.** Aporta información verificable,
   análisis y opciones, y hace push-back cordial cuando ve un riesgo.

4. [Restricción propia del dominio. Ejemplo, para un proyecto de salud: nada que pueda leerse
   como consejo médico sale sin los disclaimers legales y sin revisión humana.]

5. [Restricción propia del dominio.]

## Modo de trabajo

- Este archivo es la referencia central. Ante cada tarea nueva, leerlo antes de proponer.
- Las tareas se acotan con una **ficha de encargo**
  (ver [`templates/ficha-de-encargo.md`](ficha-de-encargo.md)).
- El ejecutor **devuelve contenido, no persiste archivos**. Consolidar es del director o del
  humano.
- Toda propuesta completa se presenta a [nombre]; solo con su autorización se implementa.

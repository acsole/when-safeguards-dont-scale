# Plantilla: hook de enforcement

> **Qué hace.** Un script determinista que se ejecuta solo ante un evento y **bloquea** lo
> que viola una regla objetiva. Es la única pieza que no depende de que el modelo coopere.
>
> **Cuándo elegirlo.** Cuando el síntoma es *"hay una regla técnica objetiva que NUNCA debe
> violarse"*. Si la regla es subjetiva o admite criterio, eso es una
> [skill](SKILL.md), no un hook. Ver [`docs/06-industrializacion.md`](../docs/06-industrializacion.md).
>
> **Cómo verificar que bloquea de verdad.** Intentá la violación a propósito. Si la acción no
> se frena, la pieza no está instalada: está decorando.

## La convención

El hook recibe el evento por **stdin** y responde con su **código de salida**:

| Exit code | Efecto |
|---|---|
| `0` | Permite la acción |
| `2` | **Bloquea** la acción |

Dos momentos posibles: **pre-evento** (bloquea antes de que ocurra) y **post-evento** (valida
después). Para enforcement real, usá pre-evento.

---

## Esqueleto en JavaScript

```javascript
#!/usr/bin/env node
// Hook de enforcement. Exit 2 bloquea, exit 0 permite.

let input = "";
process.stdin.on("data", (chunk) => (input += chunk));
process.stdin.on("end", () => {
  let evento;
  try {
    // Tolerá el BOM: en Windows es una fuente real de fallos silenciosos.
    evento = JSON.parse(input.replace(/^﻿/, ""));
  } catch (e) {
    process.exit(0); // Ante duda, no bloquear: un hook roto no debe frenar el trabajo.
  }

  const ruta = evento?.tool_input?.file_path ?? "";
  const contenido = evento?.tool_input?.content ?? "";

  // Acotá el alcance ANTES de evaluar. Un hook que aplica en todos lados
  // genera falsos positivos y termina desactivado.
  if (!/tu-patron-de-ruta/.test(ruta)) process.exit(0);

  const violaciones = [];
  if (/patron-prohibido/.test(contenido)) {
    violaciones.push("Explicá QUÉ regla se violó y CÓMO corregirla.");
  }

  if (violaciones.length) {
    console.error("BLOQUEADO:\n" + violaciones.join("\n"));
    process.exit(2);
  }
  process.exit(0);
});
```

## Esqueleto en PowerShell

```powershell
# Hook de enforcement. Exit 2 bloquea, exit 0 permite.
$raw = [Console]::In.ReadToEnd()
try { $evento = $raw -replace "^﻿", "" | ConvertFrom-Json } catch { exit 0 }

$ruta = $evento.tool_input.file_path
if (-not $ruta -or $ruta -notmatch "tu-patron-de-ruta") { exit 0 }

if ($evento.tool_input.content -match "patron-prohibido") {
    [Console]::Error.WriteLine("BLOQUEADO: explicá qué regla se violó y cómo corregirla.")
    exit 2
}
exit 0
```

---

## Registro del hook

Se registra en la configuración del entorno, asociando un **matcher** (qué herramientas lo
disparan) a un comando. Este bloque replica la forma verificada de una instalación real:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "node \"/ruta/absoluta/a/tu-hook.js\"",
            "statusMessage": "Verificando invariantes..."
          }
        ]
      }
    ]
  }
}
```

Los eventos disponibles incluyen `PreToolUse`, `PostToolUse`, `SessionStart` y `SessionEnd`.
Un cambio en esta configuración suele tomar efecto al iniciar una sesión nueva.

---

## Tres errores que ya costaron caro

**El falso positivo por coincidir dentro de un comentario.** Un patrón prohibido que aparece
en un comentario o en un ejemplo de documentación no es una violación. Un hook que frena
trabajo legítimo se termina desactivando, y entonces no protege nada.

**Poner una regla subjetiva en un hook.** Si hace falta criterio para decidir si algo viola la
regla, no es un hook: es una skill. El hook solo sirve para lo binario, determinista y verificable.

**Que el hook falle abierto sin avisar.** Si el hook se rompe y sale con `0`, la acción pasa y
nadie se entera de que la protección dejó de existir. Conviene que un hook roto sea ruidoso.

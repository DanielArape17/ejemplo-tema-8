# AIO — Qué significa "ser comprensible para máquinas"

> Este documento define el estándar de interoperabilidad. Los agentes
> revisores evalúan código contra este archivo. Si no está aquí, no es un
> requisito.

## Principios

1. **Los datos deben ser estructurados.** Toda información destinada a
   otros sistemas debe tener un formato predecible.

2. **La salida debe ser legible por humanos y máquinas.** Cuando sea
   posible, ofrecer formatos estructurados además de formatos visuales.

3. **Las interfaces son contratos.** Cualquier salida consumida por otro
   sistema debe mantenerse estable y documentada.

4. **La semántica importa.** Los datos deben expresar significado, no solo
   presentación.

5. **La automatización es un consumidor de primera clase.** El sistema debe
   asumir que otros agentes o herramientas interactuarán con él.

## Salidas Estructuradas

Preferir formatos como:

```json
{
  "id": 1,
  "title": "Shopping",
  "content": "Buy milk"
}
```

sobre formatos exclusivamente visuales.

### Requisitos

* Permitir exportación estructurada cuando sea posible.
* Mantener nombres de campos consistentes.
* Utilizar tipos de datos explícitos.
* Evitar formatos ambiguos.

### Qué NO hacer

* No depender de parsing de texto libre.
* No cambiar nombres de campos sin documentación.
* No mezclar datos y presentación.

## Contratos de Datos

Toda estructura intercambiada entre módulos debe ser estable.

### Requisitos

* Documentar formatos de entrada y salida.
* Mantener compatibilidad cuando sea posible.
* Versionar cambios significativos.

### Qué NO hacer

* No modificar estructuras sin actualizar documentación.
* No introducir campos ambiguos.

## Interoperabilidad

El sistema debe poder integrarse con:

* Otros agentes.
* Scripts automatizados.
* APIs futuras.
* Herramientas de análisis.

### Requisitos

* Utilizar formatos ampliamente soportados.
* Mantener estructuras predecibles.
* Evitar dependencias innecesarias.

## Salida JSON

Cuando una funcionalidad pueda ser consumida por otra máquina, considerar
una representación JSON.

Ejemplo:

```text
python cli.py list --json
```

Resultado:

```json
[
  {
    "id": 1,
    "title": "Shopping",
    "content": "Buy milk"
  }
]
```

## Flujo de Datos

```text
usuario
   │
   ▼
 cli.py
   │
   ├─ salida humana
   │
   └─ salida estructurada (JSON)
            │
            ▼
      otros agentes
      scripts
      APIs
```

## Checklist de Auditoría

Antes de aprobar cambios, los agentes deben responder:

* ¿La salida es estructurada?
* ¿Los datos son consistentes?
* ¿Existe un formato consumible por máquinas?
* ¿La documentación describe el contrato?
* ¿Los nombres de campos son claros?
* ¿La salida puede integrarse con otros sistemas?

Cada respuesta debe documentarse en
`reports/aio/report.md`.

## Qué NO hacer

* No depender exclusivamente de texto libre.
* No generar formatos ambiguos.
* No romper contratos de salida existentes.
* No optimizar únicamente para humanos.
* No asumir que el consumidor siempre será una persona.

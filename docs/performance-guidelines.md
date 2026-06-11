# Rendimiento — Qué significa "escribir código eficiente"

> Este documento define el estándar de rendimiento. Los agentes revisores
> evalúan código contra este archivo. Si no está aquí, no es un requisito.

## Principios

1. **La simplicidad es la optimización por defecto.** Antes de añadir
   cachés, índices o estructuras complejas, demostrar que existe un
   problema real de rendimiento.

2. **Medir antes de optimizar.** Ninguna optimización debe implementarse
   únicamente por intuición. Primero identificar el cuello de botella.

3. **Complejidad explícita.** Toda operación que recorra colecciones debe
   considerar su complejidad temporal y espacial.

4. **Evitar trabajo redundante.** No recalcular, recargar o reconstruir
   información que ya existe en memoria durante la misma operación.

5. **Mantener la legibilidad.** Una optimización que dificulta
   significativamente la comprensión del código requiere una justificación
   documentada.

## Complejidad Algorítmica

Como regla general:

Preferir:

```text
O(1)
O(log n)
O(n)
```

Evitar:

```text
O(n²)
O(n³)
```

salvo que exista una razón documentada.

### Requisitos

* Identificar búsquedas lineales frecuentes.
* Identificar bucles anidados innecesarios.
* Evitar recorridos repetidos sobre la misma colección.
* Documentar operaciones costosas.

### Qué NO hacer

* No introducir algoritmos cuadráticos cuando existe una alternativa
  lineal razonable.
* No recorrer la misma lista múltiples veces para obtener resultados
  relacionados.
* No optimizar sin comprender la complejidad actual.

## Uso de Memoria

La memoria es un recurso limitado y debe utilizarse de forma consciente.

### Requisitos

* Mantener una única fuente de verdad para los datos.
* Liberar referencias innecesarias.
* Evitar duplicar estructuras completas sin necesidad.
* Utilizar estructuras apropiadas para cada operación.

### Qué NO hacer

* No copiar listas completas cuando basta una referencia.
* No mantener datos obsoletos en memoria.
* No crear cachés permanentes sin estrategia de invalidación.

## Acceso a Disco

Las operaciones de entrada y salida suelen ser más lentas que las
operaciones en memoria.

### Requisitos

* Cargar los datos una vez por operación.
* Realizar modificaciones en memoria.
* Persistir los cambios al finalizar.

### Qué NO hacer

* No leer el archivo en cada iteración de un bucle.
* No escribir el archivo múltiples veces durante una misma operación.
* No realizar acceso a disco cuando la información ya existe en memoria.

## Búsquedas

Las búsquedas son candidatas naturales para optimización.

### Requisitos

* Analizar la complejidad de cada búsqueda.
* Considerar indexación si el volumen de datos crece.
* Evaluar estructuras de acceso rápido cuando sea necesario.

### Qué NO hacer

* No asumir que una búsqueda lineal será suficiente para siempre.
* No introducir índices sin justificar su necesidad.

## Caché

La caché es una herramienta de optimización, no una solución universal.

### Requisitos

* Justificar cada caché implementada.
* Documentar cuándo se invalida.
* Mantener coherencia entre caché y fuente de datos.

### Qué NO hacer

* No cachear información que cambia constantemente.
* No utilizar cachés para ocultar problemas de diseño.
* No mantener cachés que puedan devolver datos obsoletos.

## Profiling

Las decisiones de optimización deben basarse en evidencia.

### Requisitos

* Identificar cuellos de botella antes de modificar código.
* Medir tiempos de ejecución cuando sea posible.
* Priorizar las optimizaciones de mayor impacto.

### Qué NO hacer

* No optimizar por intuición.
* No asumir que una función es lenta sin medirla.
* No sacrificar claridad por mejoras insignificantes.

## Flujo de Rendimiento

```text
usuario ─→ cli.py
             │
             └─→ storage.load()
                        │
                        ▼
                  datos en memoria
                        │
                        ▼
                    notes.py
                        │
                        ▼
                  procesamiento
                        │
                        ▼
                  storage.save()
```

La carga debe ocurrir una vez, el procesamiento debe realizarse en
memoria y la persistencia debe ejecutarse al finalizar.

## Checklist de Auditoría

Antes de aprobar cambios, los agentes de rendimiento deben responder:

* ¿Existe trabajo redundante?
* ¿Existen bucles anidados evitables?
* ¿La complejidad es adecuada para el tamaño esperado de datos?
* ¿Se realizan accesos a disco innecesarios?
* ¿La memoria se utiliza eficientemente?
* ¿Existe una oportunidad razonable para indexación o caché?
* ¿La optimización propuesta está respaldada por evidencia?

Cada respuesta debe documentarse en
`reports/performance/report.md` junto con:

* Impacto estimado.
* Complejidad actual.
* Complejidad propuesta.
* Riesgo de implementación.
* Recomendación final.

## Qué NO hacer

* No optimizar prematuramente.
* No sacrificar claridad por micro-optimizaciones.
* No añadir complejidad sin evidencia.
* No introducir cachés innecesarias.
* No ignorar operaciones con complejidad cuadrática.
* No aprobar cambios que empeoren significativamente el rendimiento sin
  una justificación documentada.

# Seguridad — Qué significa "ser seguro"

> Este documento define el estándar de seguridad del proyecto. Los agentes
> revisores evalúan el código contra estas reglas. Si una implementación
> viola cualquiera de estos principios, debe considerarse un hallazgo de
> seguridad y registrarse en `reports/security/report.md`.

## Principios

1. **Nunca confiar en entradas externas.**
   Toda información proveniente del usuario, argumentos CLI, archivos o
   sistemas externos debe considerarse potencialmente maliciosa hasta que
   haya sido validada.

2. **Validar antes de usar.**
   Los datos deben validarse en el borde del sistema (`cli.py`) antes de
   llegar a la lógica de dominio o persistencia.

3. **Menor privilegio posible.**
   Cada componente debe operar con la menor cantidad de permisos y acceso
   necesarios para completar su tarea.

4. **Defensa en profundidad.**
   La seguridad no depende de una única validación. Si una capa falla,
   otra capa debe seguir protegiendo el sistema.

5. **Fallar de forma segura.**
   Ante errores, datos inválidos o estados inesperados, el sistema debe
   rechazar la operación en lugar de intentar continuar.

## Validación de Entradas

Toda entrada recibida desde argparse debe validarse antes de utilizarse.

### Requisitos

* No aceptar cadenas vacías para títulos.
* Limitar la longitud máxima de títulos.
* Limitar la longitud máxima de contenido.
* Rechazar caracteres de control inesperados.
* Generar errores explícitos para entradas inválidas.

### Qué NO hacer

* No asumir que el usuario proporciona datos correctos.
* No truncar silenciosamente información.
* No modificar entradas sin informar al usuario.

## Acceso a Archivos

El sistema utiliza almacenamiento local mediante JSON.

### Requisitos

* Resolver rutas absolutas antes de acceder a archivos.
* Verificar que las rutas pertenezcan al directorio permitido.
* Utilizar escrituras atómicas mediante archivos temporales.
* Validar nombres de archivo antes de construir rutas.

### Qué NO hacer

* No concatenar rutas usando strings.

* No permitir rutas relativas proporcionadas por usuarios.

* No permitir secuencias como:

  ../../../
  ..
  %2e%2e/

* No escribir archivos fuera del directorio autorizado.

## Path Traversal

La siguiente situación debe considerarse una vulnerabilidad crítica:

Si un usuario puede provocar que el sistema lea o escriba archivos fuera
del espacio previsto utilizando rutas manipuladas.

Ejemplos:

../../../etc/passwd

....\Windows\System32

Cualquier hallazgo de este tipo debe registrarse inmediatamente.

## Manejo de Errores

Los errores no deben revelar detalles internos del sistema.

### Requisitos

* Mostrar mensajes claros para usuarios.
* Registrar detalles técnicos en reportes.
* Mantener trazas internas fuera de la salida normal.

### Qué NO hacer

* No imprimir stack traces completos al usuario.
* No exponer rutas internas del sistema.
* No exponer información sensible mediante excepciones.

## Secretos y Configuración

Actualmente este proyecto no utiliza credenciales.

Sin embargo:

* Nunca hardcodear claves.
* Nunca almacenar tokens en el repositorio.
* Utilizar variables de entorno para cualquier secreto futuro.

## Checklist de Auditoría

Los agentes de seguridad deben responder:

* ¿Existe validación de entradas?
* ¿Existe riesgo de Path Traversal?
* ¿Las escrituras son atómicas?
* ¿Los errores exponen información sensible?
* ¿Hay secretos embebidos en el código?
* ¿Las rutas se construyen de forma segura?
* ¿Se cumplen los principios de defensa en profundidad?

Cada respuesta debe documentarse en:

reports/security/report.md

junto con:

* nivel de severidad
* explicación técnica
* forma de explotación
* propuesta de mitigación

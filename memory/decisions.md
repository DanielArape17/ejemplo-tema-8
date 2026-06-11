# Architectural Decisions

> Este archivo almacena decisiones arquitectónicas importantes.
> Su objetivo es preservar el razonamiento detrás de cada decisión para
> futuras sesiones y agentes.
>
> Si una decisión afecta la estructura del sistema, debe registrarse aquí.

---

## ADR-001 — Persistencia mediante JSON

**Estado:** Aceptada

### Contexto

La aplicación necesita almacenar notas entre ejecuciones.

### Decisión

Utilizar un archivo JSON local como mecanismo de persistencia.

### Justificación

* Fácil de entender para estudiantes.
* No requiere dependencias externas.
* Permite centrarse en arquitectura y agentes.
* Simplifica las pruebas automatizadas.

### Consecuencias

* Las búsquedas son lineales.
* No existe indexación nativa.
* El rendimiento puede degradarse con grandes volúmenes de datos.

---

## ADR-002 — Interfaz CLI

**Estado:** Aceptada

### Contexto

El objetivo principal del proyecto es enseñar arquitectura y colaboración
entre agentes.

### Decisión

Utilizar una interfaz de línea de comandos basada en `argparse`.

### Justificación

* Elimina complejidad visual.
* Permite enfocarse en lógica y diseño.
* Reduce el ruido asociado a frameworks frontend.

### Consecuencias

* No existe interfaz gráfica.
* No aplica SEO tradicional.
* La interacción ocurre exclusivamente mediante comandos.

---

## ADR-003 — Sin dependencias externas

**Estado:** Aceptada

### Contexto

Se busca minimizar complejidad operacional.

### Decisión

Utilizar únicamente la librería estándar de Python.

### Justificación

* Facilita la instalación.
* Reduce problemas de compatibilidad.
* Permite a los estudiantes comprender todo el sistema.

### Consecuencias

* Algunas funcionalidades requerirán más código.
* No se dispone de ORM ni bases de datos avanzadas.

---

## ADR-004 — Preparación para Sistemas Multi-Agente

**Estado:** Aceptada

### Contexto

El proyecto será utilizado para demostrar arquitecturas inspiradas en
los trabajos de Anthropic sobre Harnesses y Sistemas Multi-Agente.

### Decisión

Separar el conocimiento operativo en artefactos persistentes:

* docs/
* progress/
* memory/
* reports/

### Justificación

* Permite colaboración entre agentes.
* Reduce dependencia del contexto conversacional.
* Facilita auditorías y revisiones.

### Consecuencias

* Los agentes deben mantener la documentación actualizada.
* La memoria del sistema vive en archivos y no en el contexto del chat.

---

## Decisiones Futuras

Posibles evoluciones del proyecto:

* Migración a FastAPI.
* Migración a Next.js.
* Sustitución de JSON por SQLite.
* Exposición mediante API REST.

Estas decisiones no están aprobadas actualmente.

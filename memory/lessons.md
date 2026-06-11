# Lessons Learned

> Este archivo almacena aprendizajes obtenidos durante el desarrollo,
> auditoría y mantenimiento del proyecto.
>
> A diferencia de `decisions.md`, este documento registra observaciones
> derivadas de la experiencia real.
>
> Si una sesión descubre algo que podría ayudar a futuros agentes,
> debe registrarse aquí.

---

## Lesson-001 — La simplicidad acelera la comprensión

### Contexto

Se evaluó el uso de bases de datos y frameworks adicionales.

### Observación

La complejidad añadida dificultaba la comprensión de los principios
arquitectónicos que se pretendían enseñar.

### Aprendizaje

Para proyectos educativos, una arquitectura pequeña y explícita suele
producir mejores resultados de aprendizaje que una arquitectura más
sofisticada.

---

## Lesson-002 — Los artefactos persisten mejor que el contexto

### Contexto

Las sesiones con agentes pueden perder información debido a límites de
contexto o reinicios.

### Observación

La documentación almacenada en archivos permitió recuperar rápidamente
el estado del proyecto.

### Aprendizaje

La memoria persistente debe vivir en el repositorio y no depender
exclusivamente del contexto conversacional.

---

## Lesson-003 — La auditoría especializada encuentra más problemas

### Contexto

Se realizaron revisiones utilizando agentes especializados.

### Observación

Los agentes enfocados exclusivamente en seguridad o rendimiento
identificaron problemas que pasaron desapercibidos durante revisiones
generales.

### Aprendizaje

La especialización mejora la calidad de las auditorías.

---

## Lesson-004 — La salida estructurada facilita la automatización

### Contexto

Se comparó salida orientada a humanos con salida JSON estructurada.

### Observación

Los agentes y scripts consumieron los datos estructurados con menos
errores y menor complejidad.

### Aprendizaje

Siempre que sea posible, ofrecer formatos legibles por máquinas además
de formatos legibles por humanos.

---

## Nuevos Aprendizajes

Los agentes deben registrar:

* Situación observada.
* Resultado obtenido.
* Aprendizaje derivado.
* Recomendación futura.

Cada lección debe añadirse utilizando el formato:

## Lesson-XXX — Título

### Contexto

...

### Observación

...

### Aprendizaje

...

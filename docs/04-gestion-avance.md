# Gestión del avance

## Tablero de GitHub Projects

Tablero: [Tablero de Gestión del Proyecto](https://github.com/users/raas03/projects/1)

Columnas utilizadas: **BlackLog → Por Hacer → En Progreso → En Revisión → Finalizado**. Cada tarjeta tiene los campos *Tipo*, *Prioridad*, *Responsable* y *Fecha límite*.

| Columna | Issue | Tarea | Prioridad | Fecha |
|---|---|---|---|---|
| Finalizado | #1 | Definición de arquitectura inicial | Alta | 14/09/2026 |
| Finalizado | #12 | Definición de arquitectura inicial (refinamiento) | Alta | 27/09/2026 |
| En Revisión | #8 | Integrar creación del correo institucional | Media | 05/10/2026 |
| En Revisión | #11 | Elaborar documentación técnica y de usuario | Media | 12/10/2026 |
| En Progreso | #3 | Diseñar modelo de base de datos | Alta | 24/09/2026 |
| En Progreso | #4 | Diseñar interfaz de inscripción | Alta | 25/09/2026 |
| En Progreso | #5 | Implementar módulo de autenticación y autorización | Alta | 28/09/2026 |
| Por Hacer | #6 | Implementar gestión de inscripciones | Alta | 30/09/2026 |
| Por Hacer | #7 | Implementar generación de matrícula | Alta | 02/10/2026 |
| Por Hacer | #9 | Implementar validaciones del proceso de inscripción | Alta | 09/10/2026 |
| Por Hacer | #10 | Ejecutar pruebas funcionales del sistema | Media | 09/10/2026 |

## Issues seleccionados para seguimiento técnico

Estos 4 issues tienen la etiqueta `seguimiento` en GitHub.

| Issue | Tipo | Motivo del seguimiento | Acción propuesta |
|---|---|---|---|
| [#5 Autenticación y autorización](https://github.com/raas03/SistemaAcademico/issues/5) | Riesgo (seguridad) | Un control de acceso débil expondría datos personales de los aspirantes. | Hash de contraseñas, JWT con expiración y permisos por rol. |
| [#8 Correo institucional](https://github.com/raas03/SistemaAcademico/issues/8) | Riesgo (integración) | Depende de un servicio externo; si falla, el estudiante queda sin credenciales. | Reintentos, cola de pendientes y registro de errores. |
| [#9 Validaciones de inscripción](https://github.com/raas03/SistemaAcademico/issues/9) | Incidencia / mejora | Sin validaciones se generan matrículas con datos duplicados o incompletos. | Validar en Frontend y Backend; restricción de cédula única. |
| [#10 Pruebas funcionales](https://github.com/raas03/SistemaAcademico/issues/10) | Tarea pendiente | Ningún módulo ha sido probado de extremo a extremo. | Casos de prueba por requisito funcional (RF-01 a RF-10). |

## Matriz de riesgos

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| Retraso en el desarrollo de módulos de prioridad alta | Media | Alto | Seguimiento semanal en el tablero y priorización. |
| Fallo del servicio de correo institucional | Media | Medio | Reintentos y estado "correo pendiente". |
| Acceso no autorizado a datos personales | Baja | Alto | Autenticación JWT, roles y HTTPS. |
| Datos duplicados o inválidos | Alta | Medio | Validaciones en ambas capas y restricciones en BD. |
| Pérdida de cambios en el código o documentación | Baja | Alto | Control de versiones con Git, commits frecuentes y releases. |

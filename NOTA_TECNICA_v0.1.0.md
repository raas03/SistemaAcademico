# Nota técnica de versión – v0.1.0

**Sistema:** Sistema Académico de Inscripción y Gestión Universitaria
**Versión:** v0.1.0 (versión inicial controlada)
**Fecha:** 12 de octubre de 2026
**Repositorio:** https://github.com/raas03/SistemaAcademico

## 1. Contenido de la versión

- `README.md` con objetivo, problema, funcionalidades, arquitectura, organización Frontend/Backend, herramientas y estado.
- Requisitos funcionales y no funcionales (`docs/01-requisitos.md`).
- Modelos UML: casos de uso, clases, secuencia y actividad (`docs/02-modelos-uml.md`).
- Arquitectura cliente-servidor por capas con sus decisiones y limitaciones (`docs/03-arquitectura.md`).
- Gestión del avance: tablero, issues de seguimiento y matriz de riesgos (`docs/04-gestion-avance.md`).
- Registro de cambios (`CHANGELOG.md`).

## 2. Cambios controlados

| Cambio | Control aplicado |
|---|---|
| Definición y ajuste de la arquitectura | Issues #1 y #12 (cerrados) con justificación y enlaces a los diagramas. |
| Orden matrícula → correo institucional | Documentado en el issue #1 y reflejado en los diagramas de secuencia y actividad. |
| Documentación técnica del proyecto | Commit en la rama `main` y etiqueta `v0.1.0`. |
| Seguimiento de riesgos y tareas | Etiqueta `seguimiento` en los issues #5, #8, #9 y #10. |
| Estado de las tareas | Tablero de GitHub Projects actualizado según el avance real. |

## 3. Aspectos pendientes

- Completar el modelo de base de datos (#3), la interfaz de inscripción (#4) y la autenticación (#5).
- Implementar la gestión de inscripciones (#6) y la generación de matrícula (#7).
- Finalizar la integración con el servicio de correo institucional (#8).
- Implementar las validaciones del proceso de inscripción (#9).
- Ejecutar las pruebas funcionales (#10) y completar el manual de usuario (#11).

## 4. Próximo paso técnico

Crear la estructura base del código (`/frontend` y `/backend`), implementar el **modelo de base de datos** (#3) y el **módulo de autenticación con JWT y roles** (#5), ya que el resto de los módulos dependen de ellos. Estas tareas se publicarán en la versión **v0.2.0**, trabajando con ramas por funcionalidad (`feature/...`) y *pull requests* vinculados a cada issue.

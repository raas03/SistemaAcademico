# Registro de cambios

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y versionado semántico.

## [v0.1.0] – 2026-10-12

### Avances y ajustes realizados

1. **Definición de requisitos.** Se identificaron los actores y se documentaron 10 requisitos funcionales y 7 no funcionales, vinculados a los issues del tablero. → [docs/01-requisitos.md](docs/01-requisitos.md)
2. **Arquitectura inicial definida (#1).** Se propuso una arquitectura por capas con Frontend, Backend/API, lógica de negocio y base de datos.
3. **Ajuste de la arquitectura (#12).** Se refinó a un modelo **cliente-servidor** con separación Frontend/Backend y se documentaron el principio de separación de responsabilidades y las limitaciones. Se ajustó el flujo para que la **matrícula se genere después de validar la inscripción** y el correo institucional se cree a partir de ella. → [docs/03-arquitectura.md](docs/03-arquitectura.md)
4. **Modelado UML.** Se elaboraron los diagramas de casos de uso, clases, secuencia y actividad del proceso de inscripción. → [docs/02-modelos-uml.md](docs/02-modelos-uml.md)
5. **Organización de la gestión del proyecto y versión controlada.** Se creó el tablero en GitHub Projects con 12 issues clasificados por tipo, prioridad y fecha; se seleccionaron 4 issues de seguimiento, se añadió la matriz de riesgos, se actualizó el README y se publicó la versión `v0.1.0`. → [docs/04-gestion-avance.md](docs/04-gestion-avance.md)

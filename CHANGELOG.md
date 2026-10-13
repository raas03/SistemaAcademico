# Registro de cambios

Formato basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y versionado semántico.

## [v0.1.0] – 2026-10-12

### Avances y ajustes realizados

1. **Definición del sistema y sus componentes (Semana 5).** Se describió el sistema, su flujo principal (registro → validación → matrícula → cuenta institucional → acceso) y la tabla de componentes con sus responsabilidades.
2. **Arquitectura inicial (#1).** Se seleccionó una arquitectura por capas complementada con un modelo cliente-servidor, aplicando el principio de separación de responsabilidades.
3. **Organización del tablero y riesgos (Semana 6).** Se creó el tablero en GitHub Projects con tareas clasificadas por tipo, prioridad, responsable y fecha, y se elaboró la matriz de riesgos del proyecto. → [docs/04-gestion-avance.md](docs/04-gestion-avance.md)
4. **Ajuste de la arquitectura (Semana 7, #12).** Se refinó la arquitectura a cliente-servidor con frontend y backend separados, organizando el backend en capas de presentación, negocio y acceso a datos. Se precisó que la matrícula se genera después de validar la inscripción y que el correo institucional se crea a partir de ella. → [docs/03-arquitectura.md](docs/03-arquitectura.md)
5. **Versión inicial controlada (Semana 8).** Se subieron al repositorio los requisitos, modelos UML, arquitectura y gestión del avance; se actualizó el README.md, se etiquetaron cuatro issues de seguimiento y se publicó la versión v0.1.0.

# Sistema Académico de Inscripción y Gestión Universitaria

![Versión](https://img.shields.io/badge/versión-v0.1.0-blue) ![Estado](https://img.shields.io/badge/estado-diseño%20y%20desarrollo%20inicial-orange) ![Arquitectura](https://img.shields.io/badge/arquitectura-cliente--servidor%20por%20capas-green)

## 1. Objetivo

Desarrollar un sistema digital que automatice el proceso de inscripción de nuevos participantes en la universidad, desde el registro del aspirante hasta la generación de su matrícula y la creación de su correo institucional, centralizando la información académica en una sola plataforma segura.

## 2. Problema que resuelve

Actualmente el proceso de inscripción se realiza de forma manual o con herramientas aisladas, lo que provoca:

- Largos tiempos de espera y filas para completar la inscripción.
- Errores de digitación y datos duplicados o inconsistentes.
- Retrasos en la asignación de la matrícula y del correo institucional.
- Poca trazabilidad sobre el estado de cada solicitud.

El sistema reduce estos problemas validando los datos en línea, generando la matrícula de forma automática y creando el correo institucional una vez completada la inscripción.

## 3. Funcionalidades principales

| Módulo | Descripción |
|---|---|
| Autenticación y autorización | Inicio de sesión seguro y control de acceso por rol (aspirante, personal de admisiones, administrador). |
| Gestión de inscripciones | Registro de datos personales y académicos del aspirante, carga de documentos y selección de carrera. |
| Validaciones del proceso | Verificación de campos obligatorios, formatos, documentos y duplicados antes de aprobar la inscripción. |
| Generación de matrícula | Asignación automática de un número de matrícula único al aprobarse la inscripción. |
| Correo institucional | Creación del correo institucional y credenciales de acceso asociadas a la matrícula. |
| Consulta de estado | El aspirante puede ver en qué etapa se encuentra su solicitud. |

## 4. Arquitectura seleccionada

Se seleccionó una **arquitectura cliente-servidor con separación entre Frontend y Backend**, donde el Backend se organiza **por capas** (presentación/API, lógica de negocio y acceso a datos).

- **Principio aplicado:** separación de responsabilidades (*Separation of Concerns*).
- **Ventajas:** mantenimiento más sencillo, componentes que evolucionan de forma independiente y posibilidad de escalar el Backend sin modificar la interfaz.
- **Limitación:** mayor complejidad inicial y dependencia de una buena comunicación entre Frontend, Backend, base de datos y servicios externos (correo institucional).

```text
┌──────────────────────┐   HTTPS + JSON    ┌──────────────────────────────────┐
│       FRONTEND       │  (API REST + JWT) │             BACKEND              │
│     Interfaz web     │ ────────────────► │  Capa de presentación (API)      │
│ Aspirante / Admisión │ ◄──────────────── │  Capa de lógica de negocio       │
│    Administrador     │  Respuesta JSON   │  Capa de acceso a datos          │
└──────────────────────┘                   └─────────┬───────────────┬────────┘
                                                     │               │
                                                     ▼               ▼
                                           ┌────────────────┐ ┌─────────────────────┐
                                           │ Base de datos  │ │ Servicio de correo  │
                                           │  relacional    │ │ institucional       │
                                           └────────────────┘ └─────────────────────┘
```

Detalle completo en [docs/03-arquitectura.md](docs/03-arquitectura.md).

## 5. Organización Frontend / Backend

### Frontend (cliente)
**Responsabilidad:** todo lo que el usuario ve y con lo que interactúa.
- Formularios de registro, inicio de sesión e inscripción.
- Validaciones básicas en pantalla (campos vacíos, formato de correo, cédula, fechas).
- Mostrar el estado de la solicitud, la matrícula generada y el correo institucional asignado.
- Paneles diferenciados por rol (aspirante y personal de admisiones).
- **No** contiene reglas de negocio ni accede directamente a la base de datos.

### Backend (servidor)
**Responsabilidad:** procesar las solicitudes, aplicar las reglas de negocio y proteger los datos.
- **Capa de presentación / API:** expone los *endpoints* REST y recibe las peticiones del Frontend.
- **Capa de lógica de negocio:** valida la inscripción, genera la matrícula, controla roles y permisos, y coordina la creación del correo institucional.
- **Capa de acceso a datos:** guarda y consulta aspirantes, inscripciones, matrículas y usuarios en la base de datos.
- **Integraciones:** comunicación con el servicio de correo institucional.

### Comunicación entre ambas partes
1. El Frontend envía peticiones **HTTP/HTTPS** a la **API REST** del Backend con datos en formato **JSON** (ej. `POST /api/inscripciones`).
2. El Backend autentica la petición mediante un **token (JWT)** enviado en la cabecera `Authorization`.
3. La lógica de negocio valida los datos, consulta o guarda en la base de datos y, si corresponde, genera la matrícula y solicita la creación del correo.
4. El Backend responde con un código de estado HTTP (`200`, `201`, `400`, `401`...) y un JSON que el Frontend muestra al usuario.

| Endpoint (propuesto) | Método | Uso |
|---|---|---|
| `/api/auth/login` | POST | Iniciar sesión y obtener token |
| `/api/inscripciones` | POST | Registrar una inscripción |
| `/api/inscripciones/{id}` | GET | Consultar estado de una inscripción |
| `/api/inscripciones/{id}/aprobar` | PUT | Validar y aprobar (genera matrícula) |
| `/api/matriculas/{id}/correo` | POST | Crear correo institucional |

## 6. Herramientas utilizadas

| Herramienta | Uso en el proyecto |
|---|---|
| Git | Control de versiones local |
| GitHub | Repositorio remoto, Issues y Releases |
| GitHub Projects | Tablero Kanban de gestión del avance |
| Visual Paradigm Online | Diagramas UML y de arquitectura |
| Markdown / Mermaid | Documentación técnica y diagramas en el repositorio |
| Stack propuesto | Frontend web (HTML, CSS, JavaScript / React), Backend API REST (Node.js + Express), Base de datos relacional (MySQL / PostgreSQL), JWT para autenticación |

## 7. Estado actual del proyecto

**Versión v0.1.0 – Fase de diseño y desarrollo inicial.**

| Estado | Tareas |
|---|---|
| ✅ Finalizado | Definición de arquitectura inicial (#1, #12) |
| 🔍 En revisión | Integrar creación del correo institucional (#8), Documentación técnica y de usuario (#11) |
| 🚧 En progreso | Modelo de base de datos (#3), Interfaz de inscripción (#4), Autenticación y autorización (#5) |
| 📋 Por hacer | Gestión de inscripciones (#6), Generación de matrícula (#7), Validaciones (#9), Pruebas funcionales (#10) |

Tablero: [GitHub Projects – Tablero de Gestión del Proyecto](https://github.com/users/raas03/projects/1)

## 8. Documentación

| Documento | Contenido |
|---|---|
| [docs/01-requisitos.md](docs/01-requisitos.md) | Requisitos funcionales y no funcionales |
| [docs/02-modelos-uml.md](docs/02-modelos-uml.md) | Casos de uso, clases, secuencia y actividad |
| [docs/03-arquitectura.md](docs/03-arquitectura.md) | Arquitectura, componentes y decisiones |
| [docs/04-gestion-avance.md](docs/04-gestion-avance.md) | Tablero, issues de seguimiento y riesgos |
| [CHANGELOG.md](CHANGELOG.md) | Registro de cambios |
| [NOTA_TECNICA_v0.1.0.md](NOTA_TECNICA_v0.1.0.md) | Nota técnica de versión |

## 9. Autor

[@raas03](https://github.com/raas03) – Universidad Abierta para Adultos (UAPA).

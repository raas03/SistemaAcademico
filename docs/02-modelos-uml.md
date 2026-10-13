# Modelos UML

Los diagramas de componentes se elaboraron en **Visual Paradigm Online** (ver [03-arquitectura.md](03-arquitectura.md)). A continuación se incluyen los diagramas de casos de uso, clases, secuencia y actividad en Mermaid para que puedan visualizarse directamente en GitHub.

## 1. Diagrama de casos de uso

Representa el alcance funcional del sistema: qué puede hacer cada actor.

```mermaid
flowchart LR
    P((Participante))
    A((Personal de admisiones))
    AD((Administrador))
    M((Servicio de correo))

    subgraph Sistema["Sistema Académico de Inscripción y Gestión Universitaria"]
        UC1([Registrarse / Iniciar sesión])
        UC2([Completar inscripción])
        UC3([Adjuntar documentos])
        UC4([Consultar estado y matrícula])
        UC5([Validar y aprobar inscripción])
        UC6([Generar matrícula])
        UC7([Crear correo institucional])
        UC8([Gestionar usuarios y roles])
    end

    P --- UC1
    P --- UC2
    P --- UC3
    P --- UC4
    A --- UC1
    A --- UC5
    AD --- UC8
    UC2 -. include .-> UC3
    UC5 -. include .-> UC6
    UC6 -. include .-> UC7
    UC7 --- M
```

## 2. Diagrama de clases

Describe las entidades del dominio. Coinciden con las entidades de la base de datos definidas en el diagrama de componentes: usuarios, estudiantes, asignaturas, inscripciones y matrículas.

```mermaid
classDiagram
    direction LR
    class Usuario {
        -int id
        -string correo
        -string contrasenaHash
        -Rol rol
        +iniciarSesion()
        +cerrarSesion()
    }
    class Participante {
        -string cedula
        -string nombres
        -string apellidos
        -date fechaNacimiento
        -string telefono
        +registrarse()
        +consultarEstado()
    }
    class ProgramaAcademico {
        -int id
        -string nombre
        -string codigo
    }
    class Asignatura {
        -int id
        -string codigo
        -string nombre
        -int creditos
    }
    class Inscripcion {
        -int id
        -date fecha
        -EstadoInscripcion estado
        +validar()
        +aprobar()
        +rechazar()
    }
    class Documento {
        -int id
        -string tipo
        -string ruta
        -bool verificado
    }
    class Matricula {
        -string numero
        -date fechaEmision
        +generar()
    }
    class CorreoInstitucional {
        -string direccion
        -date fechaCreacion
        +crear()
        +notificar()
    }
    Usuario <|-- Participante
    Participante "1" --> "0..*" Inscripcion : realiza
    Inscripcion "*" --> "1" ProgramaAcademico : solicita
    ProgramaAcademico "1" o-- "1..*" Asignatura : incluye
    Inscripcion "1" *-- "1..*" Documento : contiene
    Inscripcion "1" --> "0..1" Matricula : genera
    Matricula "1" --> "1" CorreoInstitucional : se asocia
```

## 3. Diagrama de secuencia – Aprobación de inscripción

```mermaid
sequenceDiagram
    autonumber
    actor A as Personal de admisiones
    participant FE as Frontend
    participant API as API / Controladores
    participant SN as Servicios de negocio
    participant AD as Acceso a datos
    participant MAIL as Servicio de correo
    A->>FE: Selecciona inscripción y pulsa "Aprobar"
    FE->>API: PUT /api/inscripciones/{id}/aprobar (token)
    API->>API: Verifica token y rol
    API->>SN: aprobarInscripcion(id)
    SN->>AD: Consultar datos y documentos
    AD-->>SN: Inscripción completa
    SN->>SN: Generar matrícula única
    SN->>AD: Guardar matrícula
    SN->>MAIL: Crear correo institucional (matrícula)
    MAIL-->>SN: Correo creado
    SN->>AD: Actualizar estado a "Aprobada"
    SN-->>API: Matrícula y correo
    API-->>FE: 200 OK (JSON)
    FE-->>A: Muestra confirmación
```

## 4. Diagrama de actividad – Proceso de inscripción

```mermaid
flowchart TD
    I((Inicio)) --> R[Participante se registra en el sistema]
    R --> F[Completa formulario de inscripción]
    F --> D[Adjunta documentos requeridos]
    D --> V{¿Datos y documentos válidos?}
    V -- No --> C[Sistema indica errores a corregir]
    C --> F
    V -- Sí --> P[Solicitud queda En revisión]
    P --> A{¿Admisiones aprueba?}
    A -- No --> X[Inscripción rechazada y notificada]
    X --> FIN((Fin))
    A -- Sí --> M[Generar matrícula]
    M --> E[Crear correo institucional y credenciales]
    E --> N[Notificar al participante]
    N --> FIN
```

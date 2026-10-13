# Modelos UML

Los diagramas originales se elaboraron en **Visual Paradigm Online**. A continuación se incluye su representación en Mermaid para que puedan visualizarse directamente en GitHub.

## 1. Diagrama de casos de uso

```mermaid
flowchart LR
    A((Aspirante))
    P((Personal de<br/>admisiones))
    AD((Administrador))
    M((Servicio de correo<br/>institucional))

    subgraph Sistema Académico
        UC1([Registrarse / Iniciar sesión])
        UC2([Completar inscripción])
        UC3([Adjuntar documentos])
        UC4([Consultar estado])
        UC5([Validar inscripción])
        UC6([Generar matrícula])
        UC7([Crear correo institucional])
        UC8([Gestionar usuarios y roles])
    end

    A --- UC1
    A --- UC2
    A --- UC3
    A --- UC4
    P --- UC1
    P --- UC5
    AD --- UC8
    UC5 -. include .-> UC6
    UC6 -. include .-> UC7
    UC7 --- M
```

## 2. Diagrama de clases

```mermaid
classDiagram
    class Usuario {
        +int id
        +string correo
        +string passwordHash
        +Rol rol
        +iniciarSesion()
    }
    class Aspirante {
        +string cedula
        +string nombres
        +string apellidos
        +date fechaNacimiento
        +string telefono
    }
    class Carrera {
        +int id
        +string nombre
        +string codigo
    }
    class Inscripcion {
        +int id
        +date fecha
        +EstadoInscripcion estado
        +validar()
        +aprobar()
        +rechazar()
    }
    class Documento {
        +int id
        +string tipo
        +string ruta
        +bool verificado
    }
    class Matricula {
        +string numero
        +date fechaEmision
        +generar()
    }
    class CorreoInstitucional {
        +string direccion
        +date fechaCreacion
        +crear()
    }

    Usuario <|-- Aspirante
    Aspirante "1" --> "0..*" Inscripcion : realiza
    Inscripcion "*" --> "1" Carrera : solicita
    Inscripcion "1" *-- "1..*" Documento : contiene
    Inscripcion "1" --> "0..1" Matricula : genera
    Matricula "1" --> "1" CorreoInstitucional : asocia
```

## 3. Diagrama de secuencia – Aprobación de inscripción

```mermaid
sequenceDiagram
    actor P as Personal de admisiones
    participant FE as Frontend
    participant API as Backend / API
    participant BL as Lógica de negocio
    participant DB as Base de datos
    participant MAIL as Servicio de correo

    P->>FE: Aprueba inscripción
    FE->>API: PUT /api/inscripciones/{id}/aprobar (JWT)
    API->>BL: aprobarInscripcion(id)
    BL->>DB: Verificar datos y documentos
    DB-->>BL: Inscripción válida
    BL->>DB: Guardar matrícula generada
    BL->>MAIL: Crear correo institucional (matrícula)
    MAIL-->>BL: Correo creado
    BL->>DB: Guardar correo y estado "Aprobada"
    BL-->>API: Resultado
    API-->>FE: 200 OK {matricula, correo}
    FE-->>P: Muestra confirmación
```

## 4. Diagrama de actividad – Proceso de inscripción

```mermaid
flowchart TD
    I([Inicio]) --> R[Aspirante se registra]
    R --> F[Completa formulario y adjunta documentos]
    F --> V{¿Datos y documentos válidos?}
    V -- No --> C[Corregir información] --> F
    V -- Sí --> A{¿Admisiones aprueba?}
    A -- No --> X[Inscripción rechazada] --> FIN([Fin])
    A -- Sí --> M[Generar matrícula]
    M --> E[Crear correo institucional]
    E --> N[Notificar al aspirante]
    N --> FIN
```

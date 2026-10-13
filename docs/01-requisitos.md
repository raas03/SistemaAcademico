# Requisitos del sistema

## Actores

| Actor | Descripción |
|---|---|
| Aspirante | Persona que solicita inscribirse en la universidad. |
| Personal de admisiones | Revisa, valida y aprueba las inscripciones. |
| Administrador | Gestiona usuarios, roles y parámetros del sistema. |
| Servicio de correo institucional | Sistema externo que crea las cuentas de correo. |

## Requisitos funcionales

| ID | Requisito | Prioridad | Issue |
|---|---|---|---|
| RF-01 | El sistema debe permitir al aspirante registrarse e iniciar sesión. | Alta | #5 |
| RF-02 | El sistema debe controlar el acceso a las funciones según el rol del usuario. | Alta | #5 |
| RF-03 | El aspirante debe poder completar el formulario de inscripción con datos personales y académicos. | Alta | #4, #6 |
| RF-04 | El aspirante debe poder adjuntar los documentos requeridos (cédula, récord de notas, acta de nacimiento, foto). | Alta | #6 |
| RF-05 | El sistema debe validar campos obligatorios, formatos y documentos, y evitar inscripciones duplicadas. | Alta | #9 |
| RF-06 | El personal de admisiones debe poder revisar, aprobar o rechazar una inscripción. | Alta | #6 |
| RF-07 | El sistema debe generar automáticamente una matrícula única al aprobarse la inscripción. | Alta | #7 |
| RF-08 | El sistema debe crear el correo institucional y las credenciales asociadas a la matrícula. | Media | #8 |
| RF-09 | El aspirante debe poder consultar el estado de su solicitud. | Media | #6 |
| RF-10 | El sistema debe notificar al aspirante cuando su inscripción sea aprobada. | Media | #8 |

## Requisitos no funcionales

| ID | Tipo | Requisito |
|---|---|---|
| RNF-01 | Seguridad | Las contraseñas se almacenan cifradas (hash) y la comunicación se realiza por HTTPS. |
| RNF-02 | Seguridad | Las peticiones a la API se autentican mediante token (JWT) con expiración. |
| RNF-03 | Usabilidad | La interfaz debe ser intuitiva y adaptable a computadoras y dispositivos móviles. |
| RNF-04 | Rendimiento | Las operaciones principales deben responder en menos de 3 segundos. |
| RNF-05 | Disponibilidad | El sistema debe estar disponible al menos el 99 % durante los periodos de inscripción. |
| RNF-06 | Mantenibilidad | El código se organiza por capas y se versiona con Git/GitHub. |
| RNF-07 | Integridad | Cada matrícula y cada correo institucional deben ser únicos. |

# Modelo de datos (Cloud Firestore)

Colecciones usadas por MentorApp, según `mentorapp/app.js` y `mentorapp/firestore.rules`.

## `users` (ID = UID de Firebase Auth)

| Campo | Tipo | Descripción |
|---|---|---|
| name | string | Nombre completo |
| email | string | Correo electrónico |
| role | string | `student`, `mentor` o `admin` |
| active | boolean | Cuenta activa o desactivada |
| photo | string | URL o ruta de la foto de perfil |
| created | number | Marca de tiempo (ms) |
| specialty, experience, studies, courses, whatsapp | — | Datos del mentor |
| career, level, interests | — | Datos del estudiante |
| skills, languages | array | Habilidades e idiomas |
| availability | array | Objetos `{d, a, b}`: día, hora inicio, hora fin |
| city, institution, faculty, bio, linkedin | string | Datos generales del perfil |
| studentsCount | number | Contador de estudiantes (mentor) |
| progress, pomos, doneMat | number / number / array | Progreso, pomodoros y materiales completados (estudiante) |

## `requests` (solicitudes y sesiones de mentoría)

| Campo | Tipo | Descripción |
|---|---|---|
| student, mentor | string | UID del estudiante y del mentor |
| members | array | `[student, mentor]` |
| specialty | string | Especialidad solicitada |
| date, time | string | Fecha y hora de la sesión |
| message | string | Mensaje de la solicitud |
| status | string | `PENDIENTE`, `ACEPTADA` o `RECHAZADA` |
| sesion | string | `Confirmada`, `Pendiente`, `Finalizada` o `Cancelada` |
| link | string | Enlace de videollamada |
| created | number | Marca de tiempo (ms) |

## `chats` (ID = UID menor + `_` + UID mayor)

| Campo | Tipo | Descripción |
|---|---|---|
| members | array | UIDs de los participantes |
| last | number | Marca de tiempo del último mensaje |
| count | number | Cantidad de mensajes |

## `messages`

| Campo | Tipo | Descripción |
|---|---|---|
| chatId | string | ID del chat |
| members | array | UIDs de los participantes |
| from | string | UID del remitente |
| text | string | Contenido |
| ts | number | Marca de tiempo (ms) |
| file | object | Adjunto opcional |

## `notifications`

| Campo | Tipo | Descripción |
|---|---|---|
| to | string | UID del destinatario |
| text | string | Texto de la notificación |
| ts | number | Marca de tiempo (ms) |
| read | boolean | Leída o no |

## `ratings`

| Campo | Tipo | Descripción |
|---|---|---|
| mentor | string | UID del mentor calificado |
| student | string | UID del estudiante que califica |
| value | number | Calificación |

## `materials`

| Campo | Tipo | Descripción |
|---|---|---|
| mentor | string | UID del mentor que lo publica |
| title, subject, desc | string | Título, materia y descripción |
| link | string | Enlace externo opcional |
| file | object | Archivo adjunto opcional |

## `doubts` (dudas de estudiantes)

| Campo | Tipo | Descripción |
|---|---|---|
| student | string | UID del estudiante |
| subject, text | string | Materia y consulta |
| status | string | `Abierta` u otro estado de cierre |
| replies | array | Respuestas de mentores |
| created | number | Marca de tiempo (ms) |

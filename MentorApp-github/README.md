# 🎓 MentorApp

Plataforma web de **mentorías académicas y profesionales** que conecta a estudiantes con mentores (docentes y profesionales). Permite explorar perfiles, solicitar mentorías, chatear, organizar sesiones, compartir materiales y resolver dudas.

> Proyecto integrador — IESTP Manuel Scorza Torre (Acobamba, Huancavelica).

## ✨ Funcionalidades

| Rol | Qué puede hacer |
|---|---|
| **Estudiante** | Explorar mentores con filtros (especialidad, día, experiencia), solicitar mentorías, chatear, ver su cronograma, descargar materiales, pedir ayuda con dudas, calificar mentores, usar el centro de aprendizaje (temporizador Pomodoro) y seguir su progreso. |
| **Mentor** | Gestionar perfil y especialidades, definir disponibilidad, aceptar/rechazar solicitudes, programar sesiones con enlace de videollamada, subir materiales, responder dudas y contactar por WhatsApp. |
| **Administrador** | Dashboard y reportes, gestión de estudiantes y mentores (activar/desactivar), supervisión de mentorías, solicitudes y conexiones, programación de sesiones. |

Autenticación con **correo/contraseña** y **Google**, recuperación de contraseña y notificaciones dentro de la app.

## 🧰 Tecnologías

- **Frontend:** HTML5, CSS3 y JavaScript (módulos ES6), sin build ni dependencias.
- **Backend (BaaS):** [Firebase](https://firebase.google.com/) 10.12 — Authentication y Cloud Firestore.
- **Hosting:** Firebase Hosting (opcional).

## 📁 Estructura del repositorio

```
.
├── mentorapp/                 # Aplicación web (carpeta pública)
│   ├── index.html
│   ├── app.js                 # Lógica de la app (vistas, auth, Firestore)
│   ├── styles.css
│   ├── firebase-config.js     # Configuración del proyecto Firebase
│   ├── firestore.rules        # Reglas de seguridad de Firestore
│   └── avatars/               # Imágenes de perfil predefinidas
├── docs/
│   └── MODELO-DE-DATOS.md     # Colecciones de Firestore y campos
├── firebase.json              # Configuración de Hosting y Firestore
├── .firebaserc                # Proyecto Firebase por defecto
├── firestore.indexes.json
├── .gitignore
├── LICENSE
└── README.md
```

## 🚀 Ejecución local

> ⚠️ No abras `index.html` con doble clic: los módulos ES necesitan un servidor local.

```bash
git clone https://github.com/<tu-usuario>/<tu-repo>.git
cd <tu-repo>/mentorapp
npx serve
```

Abre <http://localhost:3000>.

## ⚙️ Configuración de Firebase

1. Crea un proyecto en la [consola de Firebase](https://console.firebase.google.com/).
2. Activa **Authentication** → métodos *Correo/contraseña* y *Google*.
3. Crea la base de datos **Cloud Firestore**.
4. Registra una app web y copia su configuración en `mentorapp/firebase-config.js`.
5. En `adminEmails` (`firebase-config.js`) y en la función `adminMail()` de `mentorapp/firestore.rules`, reemplaza `TU_CORREO_ADMIN@gmail.com` por el correo del administrador. La cuenta admin debe tener el correo **verificado**.
6. Publica las reglas de seguridad.
7. Si despliegas en un dominio propio, agrégalo en *Authentication → Configuración → Dominios autorizados*.

> Las claves web de Firebase (`apiKey`, etc.) no son secretas: la seguridad real la dan las **reglas de Firestore** y los dominios autorizados. Aun así, nunca subas claves privadas ni `serviceAccountKey.json`.

## ☁️ Despliegue

```bash
npm install -g firebase-tools
firebase login
firebase deploy            # Hosting + reglas de Firestore
# o por separado:
firebase deploy --only hosting
firebase deploy --only firestore:rules
```

## 🔐 Seguridad

Las reglas (`mentorapp/firestore.rules`) aplican control por rol:

- Solo usuarios autenticados leen datos; los chats, mensajes y solicitudes solo los ven sus participantes (`members`) o el administrador.
- El rol `admin` solo se puede crear con el correo de administrador verificado.
- Los usuarios no pueden cambiar su propio rol ni su estado `active`.
- Los materiales solo los publican mentores; las dudas, solo los estudiantes que las crean.

## 🗂️ Modelo de datos

Consulta [`docs/MODELO-DE-DATOS.md`](docs/MODELO-DE-DATOS.md).

## 👥 Equipo

Completa aquí los nombres de los integrantes del proyecto.

## 📄 Licencia

Distribuido bajo licencia [MIT](LICENSE).

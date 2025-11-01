# Gestión Académica Web

<em>Modern web application for comprehensive academic management built with Vue 3 and Vuetify</em>

---

## Table of Contents

- [Gestión Académica Web](#gestión-académica-web)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Architecture](#architecture)
  - [Features](#features)
  - [Technology Stack](#technology-stack)
  - [Components Structure](#components-structure)
  - [Views and Routes](#views-and-routes)
  - [Project Structure](#project-structure)
  - [Ecosystem](#ecosystem)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
    - [Configuration](#configuration)
    - [Usage](#usage)
  - [Role-Based Access](#role-based-access)
  - [API Integration](#api-integration)
  - [Development](#development)
  - [License](#license)
  - [Contact](#contact)

---

## Overview

**Gestión Académica Web** is a comprehensive Single Page Application (SPA) for academic management that enables complete administration of students, courses, careers, academic cycles, enrollments, grades, professors, and system users.

Built as the frontend component of an integrated academic system, it provides:
- Role-based access control for different user types (Administrator, Matriculator, Professor, Student)
- Full CRUD operations for all academic entities
- Real-time enrollment management and grade tracking
- Responsive design for seamless experience across devices
- Persistent authentication using localStorage

This application communicates with:
- **SistemaAcademico-Backend**: Java Spring Boot REST API - [https://github.com/isaacmendezr/SistemaAcademico-Backend](https://github.com/isaacmendezr/SistemaAcademico-Backend)

---

## Architecture

**Framework:** Vue 3 with Composition API  
**Language:** JavaScript (ES6+)  
**State Management:** Pinia  
**Routing:** Vue Router 4 with navigation guards  
**UI Library:** Vuetify 3 (Material Design)  
**HTTP Client:** Axios  
**Build Tool:** Vite  
**Design Pattern:** Component-based architecture with reusable UI components

**Key Architectural Decisions:**
- Centralized API service layer for all backend communication
- Store-based authentication with localStorage persistence
- Dynamic form and table components for DRY code
- Role-based route protection with navigation guards
- Responsive sidebar navigation with mobile support

---

## Features

| Category | Description |
| :-------- | :----------- |
| 🔐 **Authentication** | Secure login with role-based access control, persistent sessions, and profile management |
| 👥 **User Management** | Complete CRUD operations for system users with role assignment |
| 📚 **Academic Entities** | Manage courses, careers, professors, students, and academic cycles |
| 📝 **Enrollment System** | Matriculate students into groups with course and cycle selection |
| 📊 **Grade Management** | Professors can view assigned groups and update student grades (0-100 scale) |
| 📖 **Academic History** | Students can view complete enrollment history with grades and status |
| 🏫 **Academic Offering** | Create and manage course groups with professor assignments and schedules |
| 🎯 **Dynamic Components** | Reusable form and table components with configurable fields and actions |
| 🔔 **Notifications** | Real-time feedback with color-coded snackbar notifications |
| 📱 **Responsive Design** | Mobile-first approach with adaptive layouts and temporary drawer on mobile |
| 🔍 **Search & Filter** | Real-time search across all data tables with case-insensitive filtering |

---

## Technology Stack

**Core Dependencies:**
- **Vue 3** - Progressive JavaScript framework with Composition API
- **Vuetify 3** - Material Design component framework
- **Pinia** - State management store
- **Vue Router** - Official routing library
- **Axios** - Promise-based HTTP client
- **@mdi/font** - Material Design Icons

**Development Tools:**
- **Vite** - Next-generation frontend build tool
- **ESLint** - JavaScript linter
- **Prettier** - Code formatter
- **vite-plugin-vue-devtools** - Vue DevTools integration

**Configuration:**
- **API Base URL:** `http://localhost:8080/api`
- **Dev Server Port:** `5173`

---

## Components Structure

**Reusable Components:**

| Component | Description | Props | Events |
|-----------|-------------|-------|--------|
| **ComponenteBarraNavegacion** | Top navigation bar with logout | - | `toggle-drawer` |
| **ComponenteMenuLateral** | Role-based sidebar navigation | - | - |
| **ComponenteFormulario** | Dynamic form generator | `dialog`, `datos`, `titulo`, `fields` | `guardar`, `cancelar` |
| **ComponenteTablaDatos** | Generic CRUD data table | `headers`, `items`, `titulo`, `customActions` | `crear`, `editar`, `eliminar`, custom actions |
| **ComponenteNotificacion** | Snackbar notifications | `visible`, `mensaje`, `color`, `timeout` | `update:visible` |
| **ComponenteCursosCarrera** | Course-career relationship manager | `dialog`, `carrera` | `update:dialog`, `cerrar` |

**Form Field Types Supported:**
- `text`, `number`, `email`, `textarea`
- `date`, `checkbox`
- `select` (single and multiple)
- `display` (read-only)

**Custom Table Actions:**
- `ver-historial`, `marcar-activo`, `ver-cursos-carrera`
- `agregar-curso`, `ver-grupos-curso`, `ver-alumnos`
- `modificar-nota`, `desmatricular`

---

## Views and Routes

**Public Routes:**
- `/login` - User authentication

**Protected Routes:**

| Route | Component | Role | Description |
|-------|-----------|------|-------------|
| `/` | VistaInicio | All | Dashboard home |
| `/editar-perfil` | VistaEditarPerfil | All | Change password |
| `/cursos` | VistaCursos | Administrator | Manage courses |
| `/carreras` | VistaCarreras | Administrator | Manage careers with course assignments |
| `/profesores` | VistaProfesores | Administrator | Manage professors |
| `/alumnos` | VistaAlumnos | Administrator | Manage students and view academic history |
| `/ciclos` | VistaCiclos | Administrator | Manage academic cycles |
| `/oferta-academica` | VistaOfertaAcademica | Administrator | Manage course groups and schedules |
| `/usuarios` | VistaUsuarios | Administrator | Manage system users |
| `/matricula` | VistaMatricula | Matriculator | Enroll/unenroll students |
| `/notas` | VistaNotas | Professor | Manage student grades |
| `/historial` | VistaHistorial | Student | View academic history |

---

## Project Structure

```sh
gestion-academica-web/
├── src/
│   ├── main.js                           # Application entry point
│   ├── App.vue                           # Root component
│   ├── assets/
│   │   └── main.css                      # Global styles and CSS variables
│   ├── components/
│   │   ├── ComponenteBarraNavegacion.vue # Navigation bar
│   │   ├── ComponenteMenuLateral.vue     # Sidebar menu
│   │   ├── ComponenteFormulario.vue      # Dynamic form component
│   │   ├── ComponenteTablaDatos.vue      # Generic data table
│   │   ├── ComponenteNotificacion.vue    # Notification snackbar
│   │   └── ComponenteCursosCarrera.vue   # Course-career manager
│   ├── views/
│   │   ├── VistaLogin.vue                # Authentication view
│   │   ├── VistaInicio.vue               # Dashboard
│   │   ├── VistaEditarPerfil.vue         # Profile editor
│   │   ├── VistaCursos.vue               # Courses management
│   │   ├── VistaCarreras.vue             # Careers management
│   │   ├── VistaProfesores.vue           # Professors management
│   │   ├── VistaAlumnos.vue              # Students management
│   │   ├── VistaCiclos.vue               # Cycles management
│   │   ├── VistaOfertaAcademica.vue      # Academic offering
│   │   ├── VistaUsuarios.vue             # Users management
│   │   ├── VistaMatricula.vue            # Enrollment management
│   │   ├── VistaNotas.vue                # Grades management
│   │   └── VistaHistorial.vue            # Academic history
│   ├── router/
│   │   └── index.js                      # Vue Router configuration
│   ├── services/
│   │   ├── api.js                        # Axios API client
│   │   └── websocket.js                  # WebSocket service (unused)
│   └── stores/
│       └── usuario.js                    # Pinia authentication store
├── public/
│   └── index.html
├── package.json                          # Dependencies and scripts
├── vite.config.js                        # Vite configuration
├── eslint.config.js                      # ESLint configuration
├── jsconfig.json                         # JavaScript configuration
└── README.md
```

---

## Ecosystem

This frontend application is part of an integrated academic management system:

| Component | Description | Repository |
|-----------|-------------|------------|
| 💻 **Gestión Académica Web** | Vue 3 SPA frontend with role-based UI | [github.com/isaacmendezr/gestion-academica-web](https://github.com/isaacmendezr/gestion-academica-web) |
| ⚙️ **SistemaAcademico-Backend** | Spring Boot REST API with MySQL database | [github.com/isaacmendezr/SistemaAcademico-Backend](https://github.com/isaacmendezr/SistemaAcademico-Backend) |

---

## Getting Started

### Prerequisites

- **Node.js** v16 or higher
- **npm** v7 or higher
- **SistemaAcademico-Backend** running at `http://localhost:8080`

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/isaacmendezr/gestion-academica-web.git
   cd gestion-academica-web
   ```

2. Install dependencies:
   ```sh
   npm install
   ```

3. Verify the backend is running:
   ```sh
   curl http://localhost:8080/api/cursos/listar
   ```

### Configuration

**API Configuration:**

The default API base URL is set in `src/services/api.js`:
```javascript
const api = axios.create({
  baseURL: 'http://localhost:8080/api',
});
```

To change the backend URL, edit this file before running the application.

### Usage

1. Start the development server:
   ```sh
   npm run dev
   ```
   The application will be available at `http://localhost:5173`

2. Access the login page:
   ```
   http://localhost:5173/login
   ```

3. Log in with your credentials (provided by the backend administrator)

4. Navigate using the sidebar menu based on your assigned role

**Build for Production:**
```sh
npm run build
```
Output will be generated in the `dist/` directory.

**Lint and Format:**
```sh
npm run lint        # Check and fix code issues
npm run format      # Format code with Prettier
```

**Preview Production Build:**
```sh
npm run preview
```

---

## Role-Based Access

**Administrator:**
- Full system access
- Manage all entities (courses, careers, professors, students, cycles, users)
- Configure academic offering (groups and schedules)
- View student academic history

**Matriculator:**
- Enroll students in course groups
- Unenroll students from groups
- View enrollments by student and cycle

**Professor:**
- View assigned groups in active cycle
- View student list per group
- Update student grades (0-100 scale)

**Student:**
- View complete academic history
- See grades and course status (Approved ≥70, Failed <70, In Progress)

---

## API Integration

**Authentication Flow:**
```
POST /api/usuarios/login?cedula={id}&clave={password}
Response: { idUsuario, cedula, tipo }
```

**Main Endpoints Used:**

| Entity | Endpoints |
|--------|-----------|
| **Courses** | GET/POST/PUT/DELETE `/api/cursos/*` |
| **Careers** | GET/POST/PUT/DELETE `/api/carreras/*` |
| **Professors** | GET/POST/PUT/DELETE `/api/profesores/*` |
| **Students** | GET/POST/PUT/DELETE `/api/alumnos/*` |
| **Cycles** | GET/POST/PUT/DELETE `/api/ciclos/*`, POST `/api/ciclos/activarCiclo/{id}` |
| **Groups** | GET/POST/PUT/DELETE `/api/grupos/*` |
| **Enrollment** | POST/DELETE `/api/matricular/*`, PUT `/api/matricular/actualizarNota/*` |
| **Users** | GET/POST/PUT/DELETE `/api/usuarios/*` |

For complete API documentation, see the backend repository.

---

## Development

**Recommended IDE Setup:**
- [Visual Studio Code](https://code.visualstudio.com/)
- [Volar Extension](https://marketplace.visualstudio.com/items?itemName=Vue.volar) for Vue 3 support

**Project Scripts:**
```json
{
  "dev": "vite",                    // Start dev server
  "build": "vite build",            // Build for production
  "preview": "vite preview",        // Preview production build
  "lint": "eslint . --fix",         // Lint and fix code
  "format": "prettier --write src/" // Format code
}
```

**State Management:**
- User authentication state managed by Pinia store
- Persistent session using localStorage
- Automatic session restoration on page reload

**Error Handling:**
- Centralized error handling in API calls
- User-friendly notifications for all operations
- Graceful handling of "No data" responses

---

## License

This project is part of an academic system developed for educational purposes.

---

## Contact

**Developer:** Isaac Méndez  
**Repository:** [https://github.com/isaacmendezr/gestion-academica-web](https://github.com/isaacmendezr/gestion-academica-web)  
**Backend:** [https://github.com/isaacmendezr/SistemaAcademico-Backend](https://github.com/isaacmendezr/SistemaAcademico-Backend)

---

**Note:** Ensure the SistemaAcademico-Backend is running and accessible before starting this application. The frontend expects the backend API to be available at `http://localhost:8080/api`.
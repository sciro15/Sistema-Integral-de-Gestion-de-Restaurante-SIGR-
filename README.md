# 🍽️ SIGR — Sistema Integral de Gestión de Restaurante

<p align="center">
  <img src="https://img.shields.io/badge/Angular-17+-DD0031?style=for-the-badge&logo=angular&logoColor=white" alt="Angular"/>
  <img src="https://img.shields.io/badge/NestJS-10+-E0234E?style=for-the-badge&logo=nestjs&logoColor=white" alt="NestJS"/>
  <img src="https://img.shields.io/badge/Prisma_ORM-5+-2D3748?style=for-the-badge&logo=prisma&logoColor=white" alt="Prisma"/>
  <img src="https://img.shields.io/badge/MySQL-8.0+-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL"/>
  <img src="https://img.shields.io/badge/Express-4+-000000?style=for-the-badge&logo=express&logoColor=white" alt="Express"/>
  <img src="https://img.shields.io/badge/TypeScript-5+-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript"/>
</p>

<p align="center">
  Plataforma web full-stack para la administración integral de restaurantes: pedidos, reservaciones, menú, facturación, reportes y notificaciones — todo en un solo sistema.
</p>

---

## 📋 Tabla de Contenidos

- [Descripción General](#-descripción-general)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Arquitectura del Sistema](#-arquitectura-del-sistema)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Módulos del Backend](#-módulos-del-backend)
- [Módulos del Frontend](#-módulos-del-frontend)

---

## 📖 Descripción General

**SIGR** (Sistema Integral de Gestión de Restaurante) es una aplicación web empresarial diseñada para digitalizar y optimizar todas las operaciones de un restaurante. Permite gestionar en tiempo real los diferentes procesos que ocurren dentro del establecimiento, centralizando la información en una sola plataforma accesible para el personal autorizado.

Las principales áreas que cubre el sistema son:

- 🛒 **Pedidos** — Registro y seguimiento de pedidos por mesa y para llevar.
- 📅 **Reservaciones** — Gestión de reservaciones de clientes con control de horarios y disponibilidad.
- 🍕 **Menú** — Administración de platillos, categorías y precios del menú del restaurante.
- 💳 **Facturación** — Generación de facturas y registro de pagos por cada mesa o pedido.
- 📊 **Reportes** — Estadísticas de ventas, consumo y rendimiento del negocio.
- 🔔 **Notificaciones** — Sistema de alertas internas para comunicar al personal en tiempo real.
- 👤 **Usuarios y Roles** — Control de acceso por rol: administrador, mesero, cocinero y cajero.
- 🔐 **Autenticación** — Inicio de sesión seguro con tokens JWT para proteger el acceso al sistema.

---

## 🛠️ Tecnologías Utilizadas

### Backend
| Tecnología | Descripción |
|---|---|
| **NestJS** | Framework principal del servidor, basado en Node.js con arquitectura modular y orientada a decoradores. |
| **Express** | Motor HTTP subyacente que NestJS utiliza para gestionar las peticiones y respuestas HTTP. |
| **Prisma ORM** | Mapeo objeto-relacional que facilita la comunicación con la base de datos mediante un esquema tipado. |
| **MySQL** | Sistema de gestión de bases de datos relacional donde se persiste toda la información del sistema. |
| **TypeScript** | Superset de JavaScript que añade tipado estático, utilizado tanto en backend como en frontend. |
| **JWT** | Estándar de tokens para la autenticación y autorización segura de usuarios. |

### Frontend
| Tecnología | Descripción |
|---|---|
| **Angular** | Framework de Google para construir aplicaciones web de una sola página (SPA) con TypeScript. |
| **RxJS** | Biblioteca de programación reactiva utilizada junto con Angular para el manejo de flujos de datos asíncronos. |
| **Angular Router** | Módulo oficial de Angular para la navegación entre las distintas vistas de la aplicación. |
| **HttpClient** | Módulo de Angular que gestiona la comunicación HTTP con la API REST del backend. |

---

## 🏗️ Arquitectura del Sistema

El sistema sigue una arquitectura **cliente-servidor** con separación clara en tres capas:

```
┌─────────────────────────────────────────────────────────┐
│                     CLIENTE (Browser)                   │
│               Angular SPA (Puerto 4200)                 │
└──────────────────────────┬──────────────────────────────┘
                           │ HTTP / REST API
                           ▼
┌─────────────────────────────────────────────────────────┐
│                  BACKEND (NestJS + Express)              │
│                      Puerto 3000                        │
│                                                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │   Auth   │ │  Orders  │ │   Menu   │ │ Billing  │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │  Users   │ │ Reserv.  │ │ Reports  │ │ Notif.   │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│                                                         │
│                    Prisma ORM                           │
└──────────────────────────┬──────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│                   BASE DE DATOS                         │
│                   MySQL 8.0+                            │
└─────────────────────────────────────────────────────────┘
```

- **Capa de Presentación (Frontend):** La aplicación Angular se ejecuta en el navegador del usuario. Se comunica con el backend exclusivamente a través de peticiones HTTP hacia la API REST.
- **Capa de Negocio (Backend):** El servidor NestJS expone los endpoints de la API, aplica las reglas de negocio, valida datos y gestiona la autenticación mediante JWT.
- **Capa de Datos (Base de Datos):** MySQL almacena toda la información persistente. Prisma ORM actúa como intermediario entre el backend y la base de datos, gestionando también el esquema y las migraciones.

---

## 📁 Estructura del Proyecto

```
SIGR/
│
├── 📂 assets/                        # Recursos estáticos globales del proyecto
│   ├── branding/                     # Logos y elementos de marca
│   ├── icons/                        # Iconos del sistema
│   ├── images/                       # Imágenes generales
│   └── mockups/                      # Mockups y wireframes del diseño UI
│
├── 📂 backend/                       # Servidor NestJS + Express
│   ├── logs/                         # Archivos de log de la aplicación
│   ├── prisma/                       # Esquema y configuración de Prisma ORM
│   │   └── schema.prisma             # Definición de los modelos de la base de datos
│   ├── src/                          # Código fuente del backend
│   │   ├── auth/                     # Módulo de autenticación (JWT, guards)
│   │   ├── billing/                  # Módulo de facturación y pagos
│   │   ├── config/                   # Configuración de la aplicación
│   │   ├── database/                 # Servicio de conexión a la BD mediante Prisma
│   │   ├── menu/                     # Módulo de gestión del menú
│   │   ├── middleware/               # Middlewares de Express/NestJS
│   │   ├── notifications/            # Módulo de notificaciones internas
│   │   ├── orders/                   # Módulo de pedidos
│   │   ├── reports/                  # Módulo de reportes y estadísticas
│   │   ├── reservations/             # Módulo de reservaciones
│   │   ├── shared/                   # Código compartido (DTOs, decoradores, pipes)
│   │   ├── users/                    # Módulo de gestión de usuarios y roles
│   │   └── utils/                    # Funciones auxiliares y helpers
│   ├── tests/                        # Pruebas automatizadas del backend
│   └── uploads/                      # Archivos subidos (ej. imágenes de platillos)
│
├── 📂 config/                        # Configuración global del proyecto
│   └── environments/                 # Variables de entorno por ambiente (dev/prod)
│
├── 📂 database/                      # Gestión de la base de datos
│   ├── backups/                      # Respaldos de la base de datos
│   ├── diagrams/                     # Diagramas entidad-relación (ER)
│   ├── migrations/                   # Historial de migraciones del esquema
│   └── seeds/                        # Datos iniciales para poblar la base de datos
│
└── 📂 frontend/                      # Aplicación Angular SPA
    ├── docs/                         # Documentación técnica del frontend
    ├── public/                       # Archivos públicos estáticos
    ├── src/                          # Código fuente del frontend
    │   ├── app/                      # Módulo raíz de Angular
    │   ├── assets/                   # Recursos estáticos del frontend
    │   ├── components/               # Componentes reutilizables de la UI
    │   ├── context/                  # Contextos de estado compartido
    │   ├── hooks/                    # Lógica reactiva reutilizable
    │   ├── interfaces/               # Interfaces y tipos TypeScript de los modelos
    │   ├── layouts/                  # Estructuras de página (admin, auth, etc.)
    │   ├── pages/                    # Vistas completas de la aplicación
    │   ├── routes/                   # Definición de rutas y guardas de navegación
    │   ├── services/                 # Servicios de consumo de la API REST
    │   ├── store/                    # Estado global de la aplicación
    │   ├── styles/                   # Variables CSS, temas y estilos globales
    │   └── utils/                    # Funciones de formato, validación y utilidades
    └── tests/                        # Pruebas automatizadas del frontend
```

---

## 🔧 Módulos del Backend

El backend sigue la arquitectura modular de **NestJS**, donde cada dominio de negocio es un módulo independiente con su propio controlador, servicio y objetos de transferencia de datos (DTOs).

| Módulo | Responsabilidad |
|---|---|
| **auth** | Gestiona el inicio de sesión, cierre de sesión, generación y validación de tokens JWT, y los guardas de acceso por rol. |
| **users** | CRUD completo de usuarios del sistema, asignación de roles y gestión de permisos. |
| **menu** | Administración de platillos y bebidas del menú, incluyendo categorías, descripciones y precios. |
| **orders** | Creación, actualización y seguimiento del estado de los pedidos realizados por mesa o para llevar. |
| **reservations** | Registro y gestión de reservaciones de clientes, con control de disponibilidad por horario. |
| **billing** | Generación de facturas asociadas a pedidos, registro de métodos de pago y cierre de cuentas. |
| **reports** | Generación de reportes de ventas diarias, semanales y mensuales, así como estadísticas del negocio. |
| **notifications** | Sistema de notificaciones internas para alertar al personal sobre eventos relevantes (ej. pedido listo). |
| **database** | Servicio centralizado de Prisma compartido entre todos los módulos para el acceso a la base de datos. |
| **config** | Centraliza y expone las variables de configuración del sistema (puertos, claves, entorno). |
| **middleware** | Middlewares de la aplicación: registro de peticiones, validación global y configuración de CORS. |
| **shared** | Contiene DTOs, decoradores personalizados y pipes de validación reutilizados por múltiples módulos. |
| **utils** | Funciones auxiliares generales del backend (formateo de fechas, manejo de errores, etc.). |

---

## 🖥️ Módulos del Frontend

La aplicación Angular organiza su código en capas bien definidas para separar la lógica de presentación, los servicios de datos y el estado global.

| Directorio | Responsabilidad |
|---|---|
| `app/` | Módulo raíz de Angular, contiene la configuración inicial y el componente principal de la aplicación. |
| `pages/` | Vistas completas que corresponden a cada ruta de la aplicación (ej. Dashboard, Pedidos, Menú). |
| `components/` | Componentes reutilizables de la interfaz: tablas, modales, formularios, tarjetas, etc. |
| `layouts/` | Plantillas estructurales de página que definen la disposición general según el tipo de usuario. |
| `services/` | Servicios Angular que encapsulan las llamadas HTTP hacia los endpoints de la API REST del backend. |
| `interfaces/` | Interfaces y tipos TypeScript que definen la forma de los datos recibidos y enviados a la API. |
| `routes/` | Configuración del enrutamiento de la aplicación y guardas que protegen rutas según el rol del usuario. |
| `store/` | Gestión del estado global de la aplicación, compartido entre múltiples componentes y páginas. |
| `context/` | Contextos que proveen datos o funciones a segmentos específicos del árbol de componentes. |
| `hooks/` | Lógica reactiva y reutilizable desacoplada de los componentes (equivalente a custom hooks). |
| `styles/` | Variables CSS, temas de color, tipografías y estilos base de la aplicación. |
| `utils/` | Funciones de utilidad para formato de datos, validaciones del lado cliente y otros auxiliares. |
| `assets/` | Imágenes, fuentes, íconos y demás recursos estáticos consumidos por el frontend. |

---

<p align="center">
  SIGR © 2024
</p>

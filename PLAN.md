# Estado y Plan de Desarrollo — Map Recommendations App

Aplicación fullstack de recomendaciones de lugares con mapa interactivo, recomendaciones personalizadas, sistema de amigos, chat en tiempo real y compartición de ubicación.

---

## Estado actual del proyecto

A fecha del estado actual del repositorio, el proyecto **ya no está en fase de arranque**. La base funcional existe tanto en backend como en frontend, y también hay entorno Docker para desarrollo local.

### Resumen ejecutivo

- **Backend**: base ampliamente implementada con FastAPI
- **Frontend**: base funcional en Vue 3 + TypeScript + Vite
- **Base de datos**: PostgreSQL con Alembic
- **Tiempo real**: WebSockets para chat y presencia
- **Infraestructura local**: Docker Compose disponible
- **Pendiente principal**: consolidación, documentación, testing y despliegue

---

## Stack tecnológico real

| Capa | Tecnología |
|------|------------|
| **Backend** | FastAPI + Python 3.11 |
| **ORM** | SQLAlchemy 2.x |
| **Migraciones** | Alembic |
| **Base de datos** | PostgreSQL 16 |
| **Auth** | JWT (`python-jose`) + `passlib`/`bcrypt` |
| **Mapas backend** | Google Maps Python SDK |
| **Tiempo real** | WebSockets nativos de FastAPI |
| **Rate limiting** | `slowapi` |
| **Frontend** | Vue 3 + TypeScript + Vite |
| **Estado global** | Pinia |
| **Routing** | Vue Router |
| **HTTP client** | Axios |
| **UI / estilos** | Tailwind CSS v4 + Headless UI |
| **Contenedores** | Docker + Docker Compose |

---

## Estructura actual del monorepo

```text
map-recommendations-app/
├── backend/
│   ├── alembic/
│   ├── alembic.ini
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── websocket/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── scripts/
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   ├── components/
│   │   ├── composables/
│   │   ├── router/
│   │   ├── stores/
│   │   ├── types/
│   │   ├── utils/
│   │   └── views/
│   ├── Dockerfile
│   ├── package.json
│   └── vite.config.ts
├── docker-compose.yml
├── README.md
└── PLAN.md
```

---

## Backend — estado real

### 1. Autenticación

**Implementado**

- [x] `POST /api/v1/auth/register`
- [x] `POST /api/v1/auth/login`
- [x] `GET /api/v1/auth/me`
- [x] `POST /api/v1/auth/change-password`
- [x] `POST /api/v1/auth/forgot-password`
- [x] `POST /api/v1/auth/reset-password`
- [x] JWT para autenticación
- [x] Rate limiting en endpoints sensibles

### 2. Usuarios

**Implementado**

- [x] `GET /api/v1/users/`
- [x] `GET /api/v1/users/{user_id}`
- [x] `PATCH /api/v1/users/me`
- [x] `DELETE /api/v1/users/me`

### 3. Mapas

**Implementado**

- [x] `GET /api/v1/maps/nearby`
- [x] `GET /api/v1/maps/place/{place_id}`
- [x] `GET /api/v1/maps/geocode`

### 4. Preferencias

**Implementado**

- [x] `GET /api/v1/preferences/`
- [x] `POST /api/v1/preferences/`
- [x] `PUT /api/v1/preferences/{preference_id}`
- [x] `DELETE /api/v1/preferences/{preference_id}`

### 5. Ubicaciones

**Implementado**

- [x] `POST /api/v1/locations/`
- [x] `GET /api/v1/locations/me`
- [x] `GET /api/v1/locations/latest`

### 6. Recomendaciones

**Implementado**

- [x] `GET /api/v1/recommendations/`
- [x] Motor básico cruzando preferencias del usuario con lugares cercanos
- [x] Deduplcado de resultados
- [x] Ordenación básica por coincidencia y rating

**Pendiente de mejora**

- [ ] Afinar ranking (distancia, popularidad, peso por categoría)
- [ ] Filtros más ricos de precio/tipo/contexto
- [ ] Caché de resultados externos

### 7. Mensajes / chat REST

**Implementado**

- [x] `GET /api/v1/messages/{user_id}`
- [x] `POST /api/v1/messages/`
- [x] `PATCH /api/v1/messages/{message_id}/read`
- [x] `DELETE /api/v1/messages/{user_id}`

### 8. Sistema de amigos

**Implementado**

- [x] Crear invitaciones
- [x] Listar invitaciones
- [x] Revocar invitaciones
- [x] Preview de invitación por código
- [x] Aceptar invitación por token
- [x] Aceptar invitación por código
- [x] Listar amigos
- [x] Eliminar amistad

### 9. WebSockets / tiempo real

**Implementado**

- [x] Chat WebSocket
- [x] Presencia / ubicación en tiempo real
- [x] Managers de conexiones activas

**Pendiente / revisar**

- [ ] Documentar bien el protocolo de mensajes WS
- [ ] Endurecer reconexión y manejo de errores
- [ ] Añadir tests de integración WS

### 10. Infraestructura backend

**Implementado**

- [x] PostgreSQL como base de datos principal
- [x] Alembic para migraciones
- [x] Dockerfile de backend
- [x] `docker-compose.yml` funcional
- [x] `health` endpoint
- [x] CORS configurable por entorno
- [x] Rate limiting básico

**Pendiente**

- [ ] Logging más estructurado
- [ ] Tests automáticos
- [ ] `.env.example`
- [ ] Validación más estricta de configuración

---

## Frontend — estado real

### Base técnica

**Implementado**

- [x] Vue 3 + TypeScript + Vite
- [x] Vue Router
- [x] Pinia
- [x] Axios
- [x] Tailwind CSS v4
- [x] Headless UI
- [x] Estructura por `api`, `components`, `composables`, `stores`, `views`, `types`, `utils`

### Vistas existentes

**Implementado**

- [x] `HomeView.vue`
- [x] `LoginView.vue`
- [x] `RegisterView.vue`
- [x] `ProfileView.vue`
- [x] `ChatView.vue`
- [x] `FriendsView.vue`
- [x] `ForgotPasswordView.vue`
- [x] `ResetPasswordView.vue`
- [x] `InviteView.vue`

### Funcionalidad funcional o muy avanzada

- [x] Autenticación con JWT
- [x] Navegación entre vistas
- [x] Integración con Google Maps en frontend
- [x] Perfil de usuario
- [x] Chat
- [x] Gestión de amigos
- [x] Flujo de recuperación de contraseña

### Pendiente de consolidación frontend

- [ ] Mejorar consistencia visual global
- [ ] Mejorar UX de errores y estados de carga
- [ ] Añadir tests de componentes / E2E
- [ ] Documentar variables de entorno del frontend
- [ ] Revisar accesibilidad básica

---

## Docker y desarrollo local

### Estado

**Implementado**

- [x] `backend/Dockerfile`
- [x] `frontend/Dockerfile`
- [x] `docker-compose.yml`
- [x] Servicio `db` con PostgreSQL
- [x] Montajes para desarrollo local

### Pendiente

- [ ] `.env.example` en raíz y/o por subproyecto
- [ ] Documentación mínima de arranque en Linux/Debian
- [ ] Posible perfil opcional para herramientas de inspección BD

---

## Despliegue y operaciones

### Aún pendiente

- [ ] Estrategia de despliegue documentada
- [ ] Configuración CI/CD
- [ ] Secrets documentados
- [ ] Reverse proxy de producción
- [ ] HTTPS y dominio
- [ ] Observabilidad mínima

---

## Orden de trabajo recomendado desde este punto

```text
[AHORA]     Documentación y consolidación del entorno local
            - actualizar PLAN.md
            - añadir INSTALL.org
            - añadir .env.example
            - revisar README para que coincida con el repo real

[SIGUIENTE] Calidad interna
            - tests backend
            - tests frontend
            - validación de errores y contratos API
            - endurecer WebSockets

[LUEGO]     Mejora funcional
            - refinar recomendaciones
            - mejorar UX del mapa/chat/amigos
            - optimizar presencia en tiempo real

[DESPUÉS]   Operación y despliegue
            - CI/CD
            - Docker/compose de producción o despliegue equivalente
            - observabilidad y hardening
```

---

## Estado global resumido

| Módulo | Estado |
|--------|--------|
| Autenticación | ✅ Implementado |
| Usuarios | ✅ Implementado |
| Maps API | ✅ Implementado |
| Preferencias | ✅ Implementado |
| Ubicaciones | ✅ Implementado |
| Recomendaciones | ✅ Implementado, mejorable |
| Mensajes REST | ✅ Implementado |
| Amigos / invitaciones | ✅ Implementado |
| WebSockets chat/presencia | ✅ Implementado, mejorable |
| Frontend base | ✅ Implementado |
| Docker local | ✅ Implementado |
| Tests | ⬜ Pendiente o no consolidado |
| CI/CD | ⬜ Pendiente |
| Deploy producción | ⬜ Pendiente |

---

## Nota de mantenimiento

Este documento debe entenderse como **estado + roadmap corto**, no como plan inicial histórico.

Si el proyecto sigue creciendo, conviene separar en:

- `STATUS.md` → estado real actual
- `PLAN.md` → próximos pasos

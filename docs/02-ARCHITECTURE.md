# 02 - Arquitectura del Sistema

## 1. Stack Tecnológico Cerrado

- **Frontend:** React + TypeScript + Tailwind CSS (Desplegado en Firebase Hosting).
- **Backend API:** Node.js 20 + NestJS + TypeScript (Desplegado en Google Cloud Run).
- **Base de Datos:** Google Cloud Firestore (Modo Nativo).
- **Validación:** `class-validator` y `class-transformer` en backend; `zod` en frontend.

## 2. Estructura de Carpetas Obligatoria (Backend)

```text
backend/
├── src/
│   ├── common/          # Filtros de excepciones e interceptores globales
│   ├── config/          # Variables de entorno y cliente de Firestore
│   ├── modules/
│   │   ├── rooms/       # Módulo de consulta de salas
│   │   └── reservations/# Módulo de creación y consulta de reservas
│   ├── app.module.ts
│   └── main.ts
└── test/
```

_(No crear carpetas genéricas como `/utils`, `/helpers` o `/misc`)._

## 3. Diagrama de Contenedores (C4 - Nivel C2)

```mermaid
flowchart LR
    User((Usuario Solicitante))

    subgraph GCP [Google Cloud / Firebase]
        WebApp[Web App
React / Firebase Hosting]
        API[Backend API
NestJS / Cloud Run]
        DB[(Base de Datos
Cloud Firestore)]
    end

    User -->|HTTPS| WebApp
    WebApp -->|REST JSON / HTTPS| API
    API -->|Firebase Admin SDK| DB
```

## 4. Diagrama de Secuencia: Crear Reserva (Flujo Principal)

```mermaid
sequenceDiagram
    actor U as Usuario
    participant FE as Web App (React)
    participant API as Backend (NestJS)
    participant DB as Firestore

    U->>FE: Completa formulario de reserva
    FE->>API: POST /api/v1/reservations (JSON)
    API->>API: Valida DTO (tipos, fecha futura, horas)
    alt Datos inválidos
        API-->>FE: 400 Bad Request
    else Datos válidos
        API->>DB: Query reservas en misma sala y fecha
        alt Existe traslape de horario
            API-->>FE: 409 Conflict (Horario no disponible)
        else Horario libre
            API->>DB: Guarda documento en colección 'reservations'
            DB-->>API: Retorna ID generado
            API-->>FE: 201 Created (ReservationResponse)
            FE-->>U: Muestra código de confirmación
        end
    end
```

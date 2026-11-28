<div align="center">

# 🛡️ PitShield Core System

**Plataforma de gestión para talleres mecánicos, con historial digital del vehículo, facturación y garantías extendidas y microseguros integrados**

[🇬🇧 English](README.md) · 🇪🇸 Español

![Java](https://img.shields.io/badge/Java-21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)

[![Backend](https://github.com/naksu707/pitshield-core-system/actions/workflows/backend.yml/badge.svg)](https://github.com/naksu707/pitshield-core-system/actions/workflows/backend.yml)

</div>

> [!NOTE]
> **Estado: en desarrollo 🚧** · Los requerimientos, las historias de usuario y el stack tecnológico están definidos, y la base del backend está lista: inicio de sesión con JWT y roles, aislamiento entre talleres y registro de vehículos. Sigue el MVP.

---

## 💡 Acerca del proyecto

**PitShield** es una plataforma Fintech para talleres mecánicos y centros de *detailing*. Conecta la operación diaria del taller con herramientas digitales que generan confianza en el cliente y abren nuevas fuentes de ingreso.

| Problema en el taller                                                         | Cómo lo resuelve PitShield                                                                                       |
| ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| El cliente duda de que los repuestos facturados se instalaron o de los precios | Un **historial digital del vehículo** que no se puede alterar, con kilometraje, repuestos y evidencia en fotos o video |
| El papel, las hojas de cálculo y los puntos de venta genéricos hacen perder dinero | **Órdenes de trabajo, inventario, facturación electrónica y pagos** en un solo lugar                        |
| Cuando una reparación falla, el taller paga el reproceso o pierde al cliente  | **Garantías extendidas y microseguros** vendidos al momento del cobro, respaldados por una aseguradora, con reclamos digitales |
| Los clientes llaman a preguntar lo mismo y el dueño decide por intuición      | **Chatbots con IA** que responden y agendan las 24 horas, y **estadísticas** que muestran cómo va realmente el negocio |

### Módulos

| #  | Módulo                                      | Qué cubre                                                                              |
| -- | ------------------------------------------- | -------------------------------------------------------------------------------------- |
| 1  | Autenticación, usuarios y seguridad         | Inicio de sesión, roles, auditoría, autorización de datos personales                  |
| 2  | Talleres y configuración                    | Datos comerciales y fiscales, sucursales, impuestos y numeración de facturas          |
| 3  | Clientes, vehículos e historial digital     | Clientes, vehículos por placa o VIN, historial, traspasos                              |
| 4  | Servicios, agenda y técnicos                | Catálogo de servicios, citas, asignación de técnicos, tiempos de mano de obra          |
| 5  | Órdenes de trabajo                          | Recepción, diagnóstico con evidencias, presupuestos, aprobación, estados y entrega     |
| 6  | Inventario, proveedores y compras           | Stock, reservas, devoluciones, ajustes, órdenes de compra                              |
| 7  | Facturación y pagos                         | Facturas, factura electrónica DIAN, pagos presenciales, parciales y en línea, reembolsos |
| 8  | Garantías, microseguros y reclamos          | Elegibilidad, emisión, coberturas, reclamos, comisiones                                |
| 9  | Portal del cliente                          | Vehículos, órdenes, presupuestos, facturas y coberturas desde el celular               |
| 10 | Notificaciones automáticas                  | Eventos del servicio y recordatorios de mantenimiento por correo y WhatsApp           |
| 11 | Reportes, estadísticas y analítica          | Tableros de indicadores, estadísticas de servicios y técnicos, analítica de la plataforma y de las aseguradoras, exportaciones |
| 12 | IA y chatbots                               | Chatbot del cliente (portal y WhatsApp), asistente del personal y agentes de apoyo     |
| 13 | Administración de la plataforma            | Alta de talleres, aseguradoras, productos de protección                                |

---

## 🤖 Inteligencia artificial y chatbots

| Chatbot o agente              | Quién lo usa             | Qué hace                                                                                     |
| ----------------------------- | ------------------------ | -------------------------------------------------------------------------------------------- |
| **Chatbot del cliente**       | Clientes, en el portal y por WhatsApp | Responde sobre sus vehículos, órdenes, facturas y coberturas; agenda, reprograma y cancela citas; pasa la conversación a un asesor cuando hace falta |
| **Asistente del personal**    | Personal del taller      | Responde preguntas como *"¿Qué vehículos están listos para entrega hoy?"*, según los permisos de cada rol |
| **Agentes de apoyo**          | Técnicos, gerentes, auditores | Sugieren posibles diagnósticos, mantenimientos preventivos, reposición de inventario y un preanálisis de reclamos |

Los chatbots responden con los datos reales del taller y con una base de conocimiento que configura cada taller (preguntas frecuentes, horarios, políticas). Nunca inventan precios ni estados, piden confirmación antes de agendar y toda decisión final (diagnóstico, pago, reclamo) la toma una persona. Los datos personales se enmascaran antes de llegar al proveedor de IA.

---

## 📊 Estadísticas y analítica

| Tablero                    | Para                         | Indicadores principales                                                                             |
| -------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------- |
| **Indicadores del taller** | Dueño o gerente              | Ticket promedio, tasa de aprobación de presupuestos, clientes que regresan, tiempo promedio de atención, servicios vendidos con cobertura |
| **Servicios y técnicos**   | Dueño o gerente              | Servicios más vendidos, productividad por técnico, tiempo real frente al estimado, demanda por día y hora |
| **Finanzas e inventario**  | Dueño, gerente, inventario   | Ingresos, cartera pendiente, comisiones, movimientos de inventario y stock crítico                  |
| **Chatbot**                | Administrador del Taller     | Conversaciones, temas más consultados, porcentaje resuelto sin asesor, citas agendadas, calificaciones |
| **Plataforma**             | PitShield                    | Talleres activos, órdenes por mes, ingresos por comisiones, comparaciones anónimas entre talleres   |
| **Aseguradora**            | Auditores de la aseguradora  | Coberturas vigentes, primas, reclamos por estado, siniestralidad, fallas más frecuentes             |

---

## 📚 Documentación

| Documento                       | 🇪🇸 Español                                                       | 🇬🇧 English                                           |
| ------------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------- |
| Especificación de requerimientos | [`REQUERIMIENTOS.md`](documentation/es/REQUERIMIENTOS.md)        | [`REQUIREMENTS.md`](documentation/en/REQUIREMENTS.md) |
| Historias de usuario (75, en Gherkin) | [`HISTORIAS-USUARIO.md`](documentation/es/HISTORIAS-USUARIO.md) | [`USER-STORY.md`](documentation/en/USER-STORY.md)  |

Los requerimientos incluyen 53 requerimientos funcionales, 23 reglas de negocio, 18 requerimientos no funcionales, el plan de entregas y una matriz de trazabilidad que relaciona cada requerimiento con sus historias de usuario.

---

## 🛠️ Stack tecnológico

| Capa                      | Tecnología                                                                                                             |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Backend                   | Java 21, Spring Boot (Web, Data JPA, Security, Validation), Maven                                                       |
| Base de datos             | PostgreSQL, con migraciones versionadas (Flyway)                                                                       |
| Frontend                  | React con TypeScript (Vite), React Router, TanStack Query                                                             |
| Seguridad                 | Spring Security con JWT y control de acceso por roles                                                                  |
| Documentación de la API   | OpenAPI (springdoc), Swagger UI                                                                                        |
| Archivos y evidencias     | Almacenamiento de objetos: Amazon S3 (MinIO en local)                                                                  |
| Entorno local             | Docker Compose: base de datos, almacenamiento y bandeja de correo de pruebas                                          |
| CI/CD                     | GitHub Actions                                                                                                         |
| Gestión del proyecto      | GitHub Projects e Issues                                                                                               |
| Inteligencia artificial   | Spring AI con un proveedor de modelo de lenguaje (se elige en la Entrega 3) y pgvector en PostgreSQL para buscar en la base de conocimiento del chatbot |
| Analítica y gráficas      | Vistas de reportes en PostgreSQL y gráficas en React (Recharts)                                                       |
| Integraciones (*sandbox*) | Pasarela de pago, proveedor de facturación electrónica, aseguradora aliada y WhatsApp, primero en sus entornos de prueba |

**Entornos de base de datos**

| Entorno                      | Dónde                                      | Por qué                                                              |
| ---------------------------- | ------------------------------------------ | -------------------------------------------------------------------- |
| Local                        | PostgreSQL en Docker                       | Gratis, igual para todos y se puede reiniciar cuando se necesite     |
| Desarrollo compartido y demo | PostgreSQL administrado en la nube (Neon)  | Plan gratuito, sin servidor que mantener y accesible para todo el equipo |
| Producción                   | Amazon RDS para PostgreSQL                 | AWS se encarga de las copias de seguridad, el monitoreo y el escalado |

Los tres usan el mismo motor, así que el código y las migraciones no cambian entre ellos.

---

## 🏗️ Arquitectura

Un **monolito modular**: una sola aplicación Spring Boot dividida en un módulo por dominio de negocio, con límites claros entre ellos. Para un equipo de tres es más simple de construir y desplegar que los microservicios, y si algún módulo necesita escalar por separado, se puede extraer más adelante.

```text
             ┌──────────────────────────────┐
             │   React + TypeScript (SPA)   │  Personal del taller, portal del cliente
             └──────────────┬───────────────┘   y administración de la plataforma
                            │ REST /api/v1 (JWT)
┌───────────────────────────▼──────────────────────────────┐
│                Spring Boot · monolito modular             │
│  autenticacion · talleres · clientes · vehiculos · agenda │
│  ordenes · inventario · facturacion · coberturas · portal │
│  notificaciones · reportes · ia · plataforma              │
└──────┬──────────────┬──────────────┬──────────────┬───────┘
       │              │              │              │
  PostgreSQL     Amazon S3      Correo y        Pasarela de pago, facturación
                 (evidencias)   WhatsApp        electrónica, aseguradora (sandbox)
```

**Estructura planeada del repositorio**

```text
pitshield-core-system
├── backend/                 API en Spring Boot (código en español)
├── frontend/                React + TypeScript
├── tests/
│   ├── e2e/                 Pruebas de extremo a extremo
│   └── performance/         Pruebas de rendimiento
├── documentation/
│   ├── es/                  Documentación en español
│   └── en/                  Documentación en inglés
├── docker-compose.yml       Entorno local
└── .github/workflows/       Integración continua
```

---

## ✅ Calidad y pruebas

**Pruebas automáticas**

| Nivel           | Herramientas                         | Qué verifican                                                                         |
| --------------- | ------------------------------------ | ------------------------------------------------------------------------------------- |
| Unitarias       | JUnit 5, Mockito                     | Reglas de negocio: flujo de estados, totales e impuestos, elegibilidad, stock        |
| Integración     | Spring Boot Test, Testcontainers     | Repositorios y migraciones contra un PostgreSQL real                                  |
| API             | REST Assured                         | Cada *endpoint*: contratos, permisos por rol y aislamiento entre talleres            |
| Frontend        | Vitest, React Testing Library        | Componentes, formularios y validaciones                                               |
| Extremo a extremo | Playwright                         | Flujos críticos: recepción → orden de trabajo → presupuesto → factura → pago          |
| Rendimiento     | Apache JMeter                        | Tiempos de respuesta bajo carga (RNF-04)                                               |
| Cobertura       | JaCoCo                               | Mínimo 80 % en servicios y dominio                                                    |

Cada *pull request* ejecuta las pruebas en GitHub Actions, y si una falla no se puede hacer *merge*.

**Pruebas manuales**

- Casos de prueba escritos a partir de los escenarios de aceptación de cada historia de usuario.
- Sesiones de pruebas exploratorias en cada sprint.
- Defectos reportados como GitHub Issues con pasos, resultado esperado, resultado obtenido y evidencia.
- Lista de regresión antes de cada entrega y pruebas de aceptación con un taller de demostración.

---

## 🧭 Convenciones de desarrollo

El desarrollo se hace **en español**; la documentación se publica en español e inglés.

| Elemento              | Convención                                                          | Ejemplo                                              |
| --------------------- | ------------------------------------------------------------------- | ---------------------------------------------------- |
| Clases y métodos      | Español, convenciones de Java                                       | `OrdenTrabajoServicio.crearOrden()`                  |
| Base de datos         | Español, `snake_case`                                               | `orden_trabajo`, `fecha_creacion`                    |
| *Endpoints*           | Español, en plural, `kebab-case`                                    | `POST /api/v1/ordenes-trabajo`                       |
| Componentes de React  | Español, `PascalCase`                                               | `FormularioVehiculo.tsx`                             |
| Ramas                 | Tipo, historia y descripción corta                                  | `feature/HU-015-crear-orden-trabajo`                 |
| *Commits*             | [Conventional Commits](https://www.conventionalcommits.org/es/) con la descripción en español | `feat(ordenes): crear orden de trabajo (HU-015)` |
| *Pull requests*       | Una historia por PR, revisada por al menos otro integrante          | `HU-015 Creación de orden de trabajo`                |

---

## ▶️ Ejecutar el backend

**Requisitos:** Java 21, Maven y Docker Desktop (abierto).

```bash
# 1. Iniciar PostgreSQL
docker compose up -d

# 2. Iniciar la API (http://localhost:8080)
cd backend
mvn spring-boot:run

# 3. Ejecutar todas las pruebas (Docker debe estar abierto: las de integración levantan su propio PostgreSQL)
mvn verify
```

| Qué                        | Dónde                                                                                     |
| -------------------------- | ----------------------------------------------------------------------------------------- |
| Documentación de la API    | http://localhost:8080/swagger-ui.html                                                     |
| Estado del servicio        | http://localhost:8080/actuator/health                                                     |
| Informe de cobertura       | `backend/target/site/jacoco/index.html` (después de `mvn verify`)                          |
| Usuarios de demostración (`dev`) | `admin@pitshield.dev`, `asesor@pitshield.dev`, `tecnico@pitshield.dev`, `plataforma@pitshield.dev` · contraseña `PitShield2026*` |

**Pruébalo**

```bash
# Iniciar sesión y guardar el token
TOKEN=$(curl -s -X POST http://localhost:8080/api/v1/autenticacion/inicio-sesion \
  -H "Content-Type: application/json" \
  -d '{"correo":"asesor@pitshield.dev","contrasena":"PitShield2026*"}' | jq -r .token)

# Registrar un vehículo
curl -s -X POST http://localhost:8080/api/v1/vehiculos \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"placa":"ABC123","marca":"Mazda","modelo":"3 Touring","anio":2020,"tipoUso":"PARTICULAR","kilometraje":45000}'
```

**Configuración** (variables de entorno, con valores por defecto para local): `PITSHIELD_DB_URL`, `PITSHIELD_DB_USUARIO`, `PITSHIELD_DB_CONTRASENA`, `PITSHIELD_JWT_SECRETO` (obligatoria fuera del desarrollo local) y `PITSHIELD_CORS_ORIGENES`.

---

## 🗺️ Hoja de ruta

- [x] Inicialización del repositorio y alcance del proyecto
- [x] Requerimientos e historias de usuario en español e inglés
- [x] Definición del stack tecnológico
- [ ] Diseño de la arquitectura y de la base de datos (diagrama entidad-relación y contrato de la API)
- [x] Configuración del backend: Spring Boot, PostgreSQL con Flyway, seguridad JWT, Docker e integración continua
- [x] Primeras historias: inicio de sesión y bloqueo (HU-001, RN-07), registro y búsqueda de vehículos (HU-008, HU-009)
- [ ] Configuración del frontend: React, TypeScript y Vite
- [ ] **MVP:** acceso y roles, talleres, clientes y vehículos, agenda, órdenes de trabajo, inventario, facturación y pagos presenciales
- [ ] **Entrega 2:** pagos en línea, factura electrónica, garantías y microseguros, reclamos, portal del cliente y notificaciones
- [ ] **Entrega 3:** tableros de estadísticas y analítica, chatbots con IA (portal, WhatsApp y personal) y agentes de IA

---

## 👥 Equipo

| | Integrante | GitHub |
| :-: | ---------- | ------ |
| <img src="https://github.com/naksu707.png" width="48" /> | **Maria Jose Ospina** | [@naksu707](https://github.com/naksu707) |
| <img src="https://github.com/alde326.png" width="48" /> | **Aldemar Vivas** | [@alde326](https://github.com/alde326) |
| <img src="https://github.com/LionScar1.png" width="48" /> | **Dairo Dominguez** | [@LionScar1](https://github.com/LionScar1) |

---

<div align="center">

Hecho con 💜 por **[Maria Jose Ospina](https://github.com/naksu707)**, **[Aldemar Vivas](https://github.com/alde326)** y **[Dairo Dominguez](https://github.com/LionScar1)** 💜

</div>

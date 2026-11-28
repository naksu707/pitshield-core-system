<div align="center">

# 🛡️ PitShield Core System

**Workshop management platform for auto repair shops, with digital vehicle history, invoicing and embedded extended warranties and microinsurance**

🇬🇧 English · [🇪🇸 Español](README.es.md)

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
> **Status: in development 🚧** · Requirements, user stories and the tech stack are defined, and the backend base is ready: login with JWT and roles, workshop isolation and vehicle registration. The MVP comes next.

---

## 💡 About

**PitShield** is a Fintech platform for auto repair shops and detailing centers. It connects day-to-day workshop operations with digital tools that build customer trust and open new revenue streams.

| Problem in the workshop                                                 | How PitShield solves it                                                                                         |
| ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Customers doubt that billed parts were installed or that prices are fair | A **digital vehicle history** that cannot be altered, with mileage, installed parts and photo or video evidence |
| Paper, spreadsheets and generic point-of-sale systems leak money        | **Work orders, inventory, electronic invoicing and payments** in one place                                      |
| When a repair fails, the shop pays for the rework or loses the customer | **Extended warranties and microinsurance** sold at checkout, backed by an insurer, with digital claims          |
| Customers call to ask the same things and the owner decides by intuition | **AI chatbots** that answer and book 24/7, and **statistics** that show how the business is really doing     |

### Modules

| #  | Module                                    | What it covers                                                              |
| -- | ----------------------------------------- | --------------------------------------------------------------------------- |
| 1  | Authentication, users and security        | Login, roles, audit log, personal data consent                              |
| 2  | Workshops and configuration               | Business and tax details, branches, taxes and invoice numbering            |
| 3  | Customers, vehicles and digital history   | Customers, vehicles by plate or VIN, history, ownership transfers           |
| 4  | Services, scheduling and technicians      | Service catalog, appointments, technician assignment, labor time            |
| 5  | Work orders                               | Check-in, diagnosis with evidence, quotes, approval, status flow, hand-over  |
| 6  | Inventory, suppliers and purchasing       | Stock, reservations, returns, adjustments, purchase orders                  |
| 7  | Invoicing and payments                    | Invoices, DIAN e-invoicing, in-person, partial and online payments, refunds |
| 8  | Warranties, microinsurance and claims     | Eligibility, issuance, coverage, claims, commissions                        |
| 9  | Customer portal                           | Vehicles, work orders, quotes, invoices and coverage from the phone         |
| 10 | Automated notifications                   | Service events and maintenance reminders by email and WhatsApp              |
| 11 | Reports, statistics and analytics         | KPI dashboards, service and technician statistics, platform and insurer analytics, exports |
| 12 | AI and chatbots                           | Customer chatbot (portal and WhatsApp), staff assistant, AI support agents   |
| 13 | Platform administration                   | Workshop onboarding, insurers, protection products                          |

---

## 🤖 AI and chatbots

| Chatbot or agent              | Who uses it              | What it does                                                                                  |
| ----------------------------- | ------------------------ | --------------------------------------------------------------------------------------------- |
| **Customer chatbot**          | Customers, on the portal and on WhatsApp | Answers about their vehicles, work orders, invoices and coverage; books, reschedules and cancels appointments; hands off to an advisor when needed |
| **Staff assistant**           | Workshop staff           | Answers questions like *"Which vehicles are ready for pickup today?"*, within each role's permissions |
| **Support agents**            | Technicians, managers, auditors | Suggest possible diagnoses, preventive maintenance, restocking and a pre-analysis of claims |

The chatbots answer from the workshop's real data and from a knowledge base each workshop configures (FAQs, hours, policies). They never make up prices or statuses, they ask for confirmation before booking, and every final decision (diagnosis, payment, claim) stays with a person. Personal data is masked before it reaches the AI provider.

---

## 📊 Statistics and analytics

| Dashboard                  | For                       | Main indicators                                                                                         |
| -------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Workshop KPIs**          | Owner or manager          | Average ticket, quote approval rate, returning customers, average service time, coverage attach rate   |
| **Services and technicians** | Owner or manager        | Best-selling services, productivity per technician, real vs. estimated time, demand by day and hour    |
| **Finance and inventory**  | Owner, manager, inventory | Revenue, outstanding balances, commissions, stock movements and critical stock                          |
| **Chatbot**                | Workshop Administrator    | Conversations, most asked topics, share solved without an advisor, appointments booked, ratings        |
| **Platform**               | PitShield                 | Active workshops, work orders per month, commission revenue, anonymous benchmarks between workshops    |
| **Insurer**                | Insurer auditors          | Active coverage, premiums, claims by status, loss ratio, most frequent failures                         |

---

## 📚 Documentation

| Document                    | 🇪🇸 Español                                                                    | 🇬🇧 English                                                       |
| --------------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| Requirements specification  | [`REQUERIMIENTOS.md`](documentation/es/REQUERIMIENTOS.md)                      | [`REQUIREMENTS.md`](documentation/en/REQUIREMENTS.md)             |
| User stories (75, in Gherkin) | [`HISTORIAS-USUARIO.md`](documentation/es/HISTORIAS-USUARIO.md)              | [`USER-STORY.md`](documentation/en/USER-STORY.md)                 |

The requirements include 53 functional requirements, 23 business rules, 18 non-functional requirements, the release plan and a traceability matrix that links every requirement to its user stories.

---

## 🛠️ Tech stack

| Layer                  | Technology                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Backend                | Java 21, Spring Boot (Web, Data JPA, Security, Validation), Maven                                                   |
| Database               | PostgreSQL, with versioned migrations (Flyway)                                                                      |
| Frontend               | React with TypeScript (Vite), React Router, TanStack Query                                                         |
| Security               | Spring Security with JWT and role-based access control                                                              |
| API documentation      | OpenAPI (springdoc), Swagger UI                                                                                     |
| Files and evidence     | Object storage: Amazon S3 (MinIO locally)                                                                           |
| Local environment      | Docker Compose: database, storage and email inbox for testing                                                       |
| CI/CD                  | GitHub Actions                                                                                                      |
| Project management     | GitHub Projects and Issues                                                                                          |
| Artificial intelligence | Spring AI with a language model provider (chosen in Release 3), and pgvector in PostgreSQL to search the chatbot's knowledge base |
| Analytics and charts   | Reporting views in PostgreSQL, charts in React (Recharts)                                                          |
| Integrations (sandbox) | Payment gateway, electronic invoicing provider, partner insurer and WhatsApp, first against their test environments |

**Database environments**

| Environment          | Where                                   | Why                                                            |
| -------------------- | --------------------------------------- | -------------------------------------------------------------- |
| Local                | PostgreSQL in Docker                    | Free, the same for every developer, and resettable at any time |
| Shared development and demo | Managed PostgreSQL in the cloud (Neon) | Free tier, no server to maintain, accessible to the whole team |
| Production           | Amazon RDS for PostgreSQL               | Backups, monitoring and scaling handled by AWS                 |

All three run the same engine, so the code and the migrations do not change between them.

---

## 🏗️ Architecture

A **modular monolith**: one Spring Boot application split into one module per business domain, with clear boundaries between them. It is simpler to build and deploy than microservices for a team of three, and a module can be extracted later if it ever needs to scale on its own.

```text
             ┌──────────────────────────────┐
             │   React + TypeScript (SPA)   │  Workshop staff, customer portal
             └──────────────┬───────────────┘   and platform administration
                            │ REST /api/v1 (JWT)
┌───────────────────────────▼──────────────────────────────┐
│                 Spring Boot · modular monolith            │
│  autenticacion · talleres · clientes · vehiculos · agenda │
│  ordenes · inventario · facturacion · coberturas · portal │
│  notificaciones · reportes · ia · plataforma              │
└──────┬──────────────┬──────────────┬──────────────┬───────┘
       │              │              │              │
  PostgreSQL     Amazon S3      Email and       Payment gateway, e-invoicing
                 (evidence)     WhatsApp        provider, insurer (sandbox)
```

**Planned repository structure**

```text
pitshield-core-system
├── backend/                 Spring Boot API (code in Spanish)
├── frontend/                React + TypeScript
├── tests/
│   ├── e2e/                 End-to-end tests
│   └── performance/         Performance tests
├── documentation/
│   ├── es/                  Documentation in Spanish
│   └── en/                  Documentation in English
├── docker-compose.yml       Local environment
└── .github/workflows/       CI pipelines
```

---

## ✅ Quality and testing

**Automated tests**

| Level             | Tools                                    | What they check                                                                   |
| ----------------- | ---------------------------------------- | --------------------------------------------------------------------------------- |
| Unit              | JUnit 5, Mockito                         | Business rules: status flows, totals and taxes, eligibility, stock               |
| Integration       | Spring Boot Test, Testcontainers         | Repositories and migrations against a real PostgreSQL                             |
| API               | REST Assured                             | Every endpoint: contracts, permissions by role and isolation between workshops   |
| Frontend          | Vitest, React Testing Library            | Components, forms and validations                                                 |
| End-to-end        | Playwright                               | Critical flows: check-in → work order → quote → invoice → payment                 |
| Performance       | Apache JMeter                            | Response times under load (RNF-04)                                                 |
| Coverage          | JaCoCo                                   | At least 80 % in services and domain                                              |

Every pull request runs the tests in GitHub Actions, and a failing test blocks the merge.

**Manual tests**

- Test cases written from the acceptance scenarios of each user story.
- Exploratory testing sessions on every sprint.
- Bugs reported as GitHub Issues with steps, expected result, actual result and evidence.
- A regression checklist before every release and acceptance tests with a demo workshop.

---

## 🧭 Development conventions

Development is done **in Spanish**; the documentation is published in Spanish and English.

| Item                     | Convention                                                         | Example                                                    |
| ------------------------ | ------------------------------------------------------------------ | ---------------------------------------------------------- |
| Classes and methods      | Spanish, Java conventions                                          | `OrdenTrabajoServicio.crearOrden()`                        |
| Database                 | Spanish, `snake_case`                                              | `orden_trabajo`, `fecha_creacion`                          |
| Endpoints                | Spanish, plural, `kebab-case`                                      | `POST /api/v1/ordenes-trabajo`                             |
| React components         | Spanish, `PascalCase`                                              | `FormularioVehiculo.tsx`                                   |
| Branches                 | Type, story and short description                                  | `feature/HU-015-crear-orden-trabajo`                       |
| Commits                  | [Conventional Commits](https://www.conventionalcommits.org/) with the description in Spanish | `feat(ordenes): crear orden de trabajo (HU-015)` |
| Pull requests            | One story per PR, reviewed by at least one teammate               | `HU-015 Creación de orden de trabajo`                      |

---

## ▶️ Run the backend

**Requirements:** Java 21, Maven and Docker Desktop (running).

```bash
# 1. Start PostgreSQL
docker compose up -d

# 2. Start the API (http://localhost:8080)
cd backend
mvn spring-boot:run

# 3. Run every test (Docker must be running: integration tests start their own PostgreSQL)
mvn verify
```

| What                 | Where                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------- |
| API documentation    | http://localhost:8080/swagger-ui.html                                                       |
| Health check         | http://localhost:8080/actuator/health                                                       |
| Coverage report      | `backend/target/site/jacoco/index.html` (after `mvn verify`)                                 |
| Demo users (`dev`)   | `admin@pitshield.dev`, `asesor@pitshield.dev`, `tecnico@pitshield.dev`, `plataforma@pitshield.dev` · password `PitShield2026*` |

**Try it**

```bash
# Log in and keep the token
TOKEN=$(curl -s -X POST http://localhost:8080/api/v1/autenticacion/inicio-sesion \
  -H "Content-Type: application/json" \
  -d '{"correo":"asesor@pitshield.dev","contrasena":"PitShield2026*"}' | jq -r .token)

# Register a vehicle
curl -s -X POST http://localhost:8080/api/v1/vehiculos \
  -H "Authorization: Bearer $TOKEN" -H "Content-Type: application/json" \
  -d '{"placa":"ABC123","marca":"Mazda","modelo":"3 Touring","anio":2020,"tipoUso":"PARTICULAR","kilometraje":45000}'
```

**Configuration** (environment variables, with local defaults): `PITSHIELD_DB_URL`, `PITSHIELD_DB_USUARIO`, `PITSHIELD_DB_CONTRASENA`, `PITSHIELD_JWT_SECRETO` (required outside local development) and `PITSHIELD_CORS_ORIGENES`.

---

## 🗺️ Roadmap

- [x] Repository initialization and scope definition
- [x] Requirements and user stories in Spanish and English
- [x] Tech stack selection
- [ ] Architecture and database design (entity-relationship diagram and API contract)
- [x] Backend setup: Spring Boot, PostgreSQL with Flyway, JWT security, Docker and CI
- [x] First stories: login and lockout (HU-001, RN-07), vehicle registration and search (HU-008, HU-009)
- [ ] Frontend setup: React, TypeScript and Vite
- [ ] **MVP:** access and roles, workshops, customers and vehicles, scheduling, work orders, inventory, invoicing and in-person payments
- [ ] **Release 2:** online payments, electronic invoicing, warranties and microinsurance, claims, customer portal and notifications
- [ ] **Release 3:** statistics and analytics dashboards, AI chatbots (portal, WhatsApp and staff) and AI agents

---

## 👥 Team

| | Member | GitHub |
| :-: | ------ | ------ |
| <img src="https://github.com/naksu707.png" width="48" /> | **Maria Jose Ospina** | [@naksu707](https://github.com/naksu707) |
| <img src="https://github.com/alde326.png" width="48" /> | **Aldemar Vivas** | [@alde326](https://github.com/alde326) |
| <img src="https://github.com/LionScar1.png" width="48" /> | **Dairo Dominguez** | [@LionScar1](https://github.com/LionScar1) |

---

<div align="center">

Made by 💜 **[Maria Jose Ospina](https://github.com/naksu707)**, **[Aldemar Vivas](https://github.com/alde326)** and **[Dairo Dominguez](https://github.com/LionScar1)** 💜

</div>

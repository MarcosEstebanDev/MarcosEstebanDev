## Marcos Esteban Godoy

**Backend developer — distributed systems.** Córdoba, Argentina.

Trabajo con **Java 21 / Spring Boot** en plataformas del sector financiero regulado, donde
la seguridad y la trazabilidad son requisitos duros. En paralelo diseño y construyo sistemas
distribuidos en **NestJS**: multi-tenancy con aislamiento a nivel de base de datos, mensajería
asíncrona, y orquestación de workflows con estado durable.

Me interesa la parte que no se ve en un CRUD: qué pasa cuando el worker muere a mitad de una
tarea, cómo se prueba que un tenant no puede leer los datos de otro, y por qué esa decisión se
tomó así y no de la otra forma. Por eso documento las decisiones de arquitectura como **ADRs**.

---

### Proyectos

#### [agent-platform](https://github.com/MarcosEstebanDev/agent-platform) — Orquestador de workflows distribuidos
`NestJS` · `PostgreSQL` · `BullMQ` · `Docker` · `Arquitectura Hexagonal`

Reparte trabajo a workers aislados en containers. Lo interesante no es la ejecución, es todo
lo que la rodea: detección de liveness por latido con reaper (peor caso acotado a 2 minutos
*por diseño*, porque el límite real es umbral + intervalo de barrido, no el umbral solo),
encolado idempotente, presupuestos de ejecución, DLQ con reintentos, y rescate del workspace
antes de destruir el container.

**70 tests que corren sin base, sin Docker y sin red** — ese es el retorno concreto de los
puertos. **11 ADRs**, incluidas las veces que el diseño chocó con la realidad y hubo que corregirlo.

#### [helpdesk-api](https://github.com/MarcosEstebanDev/helpdesk-api) — SaaS multi-tenant event-driven
`NestJS` · `PostgreSQL RLS` · `Prisma` · `Arquitectura Hexagonal`

Aislamiento multi-tenant con **Row-Level Security** de Postgres en vez de schema-per-tenant:
rol de aplicación sin `BYPASSRLS`, `FORCE RLS`, políticas fail-closed y el tenant inyectado por
transacción — así el aislamiento no depende de que ningún `WHERE` se olvide del `tenant_id`.
Auth con rotación de refresh tokens y detección de reuso. El dominio y la capa de aplicación
son puros: no conocen NestJS ni Prisma.

#### [Analitycs-ecommerce](https://github.com/MarcosEstebanDev/Analitycs-ecommerce) — Analytics SaaS en tiempo real
`NestJS` · `Angular` · `PostgreSQL` · `Redis` · `BullMQ` · `Socket.io` · `Stripe`

Monolito modular multi-tenant con procesamiento en background y métricas en vivo por WebSocket.

#### ClinicFlow — Gestión clínica en microservicios
`Spring Boot` · `Spring Cloud` · `RabbitMQ` · `PostgreSQL` · `Redis`

5 servicios con API Gateway y service discovery, mensajería asíncrona con RabbitMQ, e
integraciones con SendGrid y Twilio.

#### Wallet-Microservices — Billetera digital
`NestJS` · `NATS` · `PostgreSQL` · `Docker`

4 microservicios con database-per-service comunicándose vía NATS.

---

### Stack

| | |
|---|---|
| **Backend** | Java 21 · Spring Boot · Node.js · NestJS · TypeScript · Python |
| **Arquitectura** | Microservicios · Hexagonal · Event-Driven · Multi-tenancy · CQRS · Outbox |
| **Async** | NATS · RabbitMQ · BullMQ · Redis · WebSockets |
| **Datos** | PostgreSQL · Prisma · TypeORM · Hibernate/JPA · Redis |
| **Frontend** | React · Next.js · Angular · TailwindCSS |
| **Infra** | Docker · GitHub Actions · OpenAPI · Jest · JUnit 5 · Testcontainers · OpenTelemetry |

---

📫 [marcosestebandev@gmail.com](mailto:marcosestebandev@gmail.com)

# Flyway Migration Guide

## Overview

This document outlines the rationale, structure, and DevOps integration of Flyway-based schema migrations for the `pipeline-triage-service` within AetherFi. It provides a production-ready playbook for zero-downtime, auditable database evolution.

---

## 🎯 Goals

* **Declarative SQL versioning**: Every DDL change is explicitly named and ordered.
* **Zero-downtime deployment**: Forward-only migrations minimize production risk.
* **Least-privilege access**: Role creation and grants are formalized.
* **Auditable history**: Git-tracked, timestamped migration scripts.

---

## 🗂️ Migration File Conventions

Located at: `src/main/resources/db/migration/`

* `V1__baseline_schema_and_role.sql`: Create `vizier` schema, revoke public, grant access.
* `V2__create_pipeline_events_table.sql`: Core table schema.
* `V3__add_constraints_and_indexes.sql`: Add unique keys and performance indexes.

Each script is atomic and follows Flyway’s naming convention: `Vn__description.sql`

---

## 🧪 DevOps Integration

### ✅ CI Pipeline with Testcontainers

```java
@Testcontainers
@SpringBootTest
class FlywayMigrationTest {
  @Container
  static PostgreSQLContainer<?> pg = new PostgreSQLContainer<>("postgres:15")
    .withDatabaseName("vizier")
    .withUsername("triage_service_rw")
    .withPassword("dummy");

  @Autowired Flyway flyway;

  @Test
  void migrationsApplyCleanly() {
    flyway.configure()
          .dataSource(pg.getJdbcUrl(), pg.getUsername(), pg.getPassword())
          .load()
          .migrate();
    assertEquals(3, flyway.info().applied().length);
  }
}
```

This ensures your SQL works on a real Postgres instance before any deploy.

### 🐳 Dockerfile (simplified)

```dockerfile
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
COPY target/pipeline-triage-service-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
```

Flyway runs via classpath; no `psql` client needed.

### ⚙️ Spring Boot Config

```yaml
spring:
  flyway:
    enabled: true
    baseline-on-migrate: true
    validate-on-migrate: true
    locations: classpath:db/migration
  jpa:
    hibernate:
      ddl-auto: validate
```

Hibernate validates against the applied schema—never modifies it.

---

## 🔍 Design Decisions

| Feature            | Phase 1 Decision             | Phase 2 Plan                         |
| ------------------ | ---------------------------- | ------------------------------------ |
| Partitioning       | Deferred                     | Use `PARTITION BY RANGE`             |
| PII handling       | Not yet flagged              | Add `pii_scrubbed` + encryption hook |
| Schema-per-service | Single `vizier` schema       | Split per service                    |
| Down-migration     | Not supported (forward-only) | Document roll-forward strategy       |

---

## 📈 Observability

* Migrations tracked via `/actuator/flyway`
* Failure blocks container startup
* Errors visible in `docker compose logs`

---

## ✅ Summary

* FAANG-style Flyway setup
* Replaces `ddl-auto=update` with validation
* Ready for multi-tenant, regulated environments
* Repeatable and Git-versioned DDL strategy

You can copy this pattern across all Java-based services in the AetherFi ecosystem.

---

> “Migrations aren’t just scripts—they’re contracts between code and data.”

# User Manager - backend

A small full-stack exercise from 2022: a REST API for managing users, with authentication and role-based access. Frontend: [user-manager-frontend](https://github.com/piotr-kaczmarski-java-dev/user-manager-frontend).

## Stack

- Java 11, Spring Boot 2.4 (Web, Data JPA, Validation, Security)
- PostgreSQL (local instance via Docker Compose)
- MapStruct for entity ↔ DTO mapping, Lombok
- Springfox / Swagger UI for API docs - the frontend's API client is generated from this spec
- JUnit 5, Spring Boot Test, Spring Security Test

## What it does

- CRUD endpoints for users (`/api/users`), with validation and clear errors for "not found" and duplicate data
- Login and logout endpoints (`POST /api/auth/login`, `GET /api/auth/logout`); passwords hashed with BCrypt; `USER` and `ADMIN` roles - reads are open, changes require `ADMIN`
- CORS configured for the Angular dev server
- An `ApplicationRunner` seeds example users for local development

## Run locally

```bash
cd src/main/resources/localdev && docker-compose up -d   # PostgreSQL on port 5438
cd - && ./mvnw spring-boot:run
```

Swagger UI: http://localhost:8080/swagger-ui/

## What I'd do differently today

Written as a quick exercise, kept here as it was. In a production service I would:
- move to Spring Boot 3 / Java 21 and the `SecurityFilterChain` style (`WebSecurityConfigurerAdapter` is removed in Spring Security 6)
- replace HTTP Basic with token-based auth (OAuth2/OIDC, e.g. Keycloak)
- manage the schema with Flyway instead of `ddl-auto: create`
- replace Springfox with springdoc-openapi
- add Testcontainers integration tests

My current Java work in progress: **TradeArena** (see my profile).

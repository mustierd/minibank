# MiniBank

A microservice-based banking platform built with Java 21 and Spring Boot.
It covers customer onboarding, account management, money transfer, bill payment,
and suspicious transaction detection. The project is under active development.

## Target architecture

| Service | Responsibility | Tech |
|---|---|---|
| core-banking-service | Customers, authentication, accounts, transfers, transaction history | Spring Boot, JPA, PostgreSQL, JWT |
| notification-service | Consumes transfer and payment events, produces notifications | Spring Boot, Kafka |
| api-gateway | Single entry point, token validation, rate limiting | Spring Cloud Gateway, Redis |
| fraud-service | Detects suspicious transfers with rule-based checks | Spring Boot, Kafka, Redis |
| payment-service | Bill payment (saga), scheduled transfers | Spring Boot, gRPC, Kafka |

Services expose REST APIs externally and communicate internally through gRPC and Kafka.
Each service owns its PostgreSQL database.

## Roadmap

- [x] core-banking-service: Spring Boot skeleton and health endpoint
- [ ] Customer and account management
- [ ] Money transfer: transactions, concurrency control, idempotency
- [ ] Authentication and authorization with JWT
- [ ] Unit and integration tests (JUnit, Mockito, Testcontainers)
- [ ] Docker Compose and GitHub Actions
- [ ] Event publishing with Kafka, notification-service
- [ ] Outbox pattern, Redis cache
- [ ] api-gateway and rate limiting
- [ ] fraud-service
- [ ] payment-service: bill payment with saga
- [ ] Observability: Actuator, Prometheus, Grafana, distributed tracing
- [ ] Kubernetes deployment and load testing

## Tech stack

Java 21, Spring Boot 3, Spring Data JPA, Spring Security, PostgreSQL, Flyway, Kafka,
Redis, gRPC, Docker, Kubernetes, JUnit 5, Testcontainers, GitHub Actions

## Running locally

```bash
cd core-banking-service
./mvnw spring-boot:run
```

Health check: `http://localhost:8080/actuator/health`

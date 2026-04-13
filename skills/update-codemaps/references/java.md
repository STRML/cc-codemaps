# Java/Kotlin Codemap Guidance

## Discovery Tools

- `tree -L 3 -I target -I build -I .gradle src/` for source structure
- Read `pom.xml` (Maven) or `build.gradle`/`build.gradle.kts` (Gradle) for dependencies and modules
- Search for class definitions in `src/main/java/` or `src/main/kotlin/`
- Check for framework markers: `@SpringBootApplication` (Spring), `Application.java` (Quarkus/Micronaut)

## What to Capture

### Module Map
- Package structure under `src/main/java/` or `src/main/kotlin/`
- Entry points: `main()` method, `@SpringBootApplication`, `@ApplicationPath`
- Multi-module layout (Maven modules, Gradle subprojects)
- Interface definitions and their implementations (`@Service`, `@Repository`)

### Framework Patterns
- **Spring Boot**: Controller/service/repository layers, auto-configuration, profiles, security config
- **Quarkus/Micronaut**: CDI beans, REST resources, reactive patterns
- **Android**: Activity/Fragment hierarchy, ViewModel/LiveData, Compose components
- Dependency injection: constructor injection, `@Autowired`, Dagger/Hilt modules

### Data Layer
- JPA/Hibernate entities and `@Table` annotations
- Repository interfaces (Spring Data, custom queries)
- Database migrations (Flyway, Liquibase)
- DTO/record classes for API contracts
- Config classes (`@ConfigurationProperties`, `application.yml` keys)

### Build & Config
- Maven/Gradle module structure and plugin configuration
- Java version and language level
- `application.yml`/`application.properties` structure
- Test framework: JUnit 5, Mockito, Testcontainers, integration test layout

## Codemap File Suggestions

| File | When to create |
|------|---------------|
| `architecture.md` | Module layout, dependency graph, entry points, profiles |
| `backend.md` | Controllers, services, repositories, middleware/filters |
| `data.md` | Entities, DTOs, migrations, config classes |
| `integrations.md` | External API clients, messaging (Kafka, RabbitMQ) |

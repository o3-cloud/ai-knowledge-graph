---
summary: Comprehensive Domain-Driven Design reference implementation of a library system demonstrating modular monolith architecture, hexagonal patterns, event-driven design, CQRS, functional programming with immutable aggregates, and type-safe domain modeling
event_type: code
sources:
    - https://github.com/ddd-by-examples/library
tags:
    - DDD
    - domain-driven-design
    - hexagonal-architecture
    - modular-monolith
    - event-driven
    - CQRS
    - functional-programming
    - reference-implementation
---

# DDD by Examples: Library

**Repository:** ddd-by-examples/library
**License:** MIT
**Stars:** 5.6k+ | **Forks:** 805+

## Overview

A comprehensive reference implementation showcasing practical application of **Domain-Driven Design (DDD) principles** through a public library domain. The system models patron book holds, checkouts, catalogue management, and related operations—demonstrating problem space strategic analysis and various tactical patterns.

## Domain Model

The library domain includes:
- **Patron management** — library members and their privileges
- **Book holds** — reserving books for pickup
- **Checkouts** — borrowing and returning books
- **Catalogue** — book inventory and availability
- **Daily sheets** — operational reporting

## Architecture Patterns

### Modular Monolith

Each bounded context maps to a separate package:
- Enables future evolution toward microservices
- Maintains modularity within single deployment
- Clear boundaries between contexts
- Independent evolution of each module

**Key principle:** Contexts receive locally-appropriate architecture based on complexity.

### Context-Appropriate Architecture

| Context | Complexity | Architecture |
|---------|------------|--------------|
| Lending | High | Hexagonal architecture |
| Catalogue | Medium | Layered architecture |
| Simple contexts | Low | CRUD patterns |

Not every context needs the same sophistication—match architecture to complexity.

### Hexagonal Architecture (Ports & Adapters)

For complex contexts like lending:

```
┌─────────────────────────────────────────┐
│            Application Core             │
│  ┌─────────────────────────────────┐   │
│  │       Domain Model              │   │
│  │  (Pure business logic)          │   │
│  └─────────────────────────────────┘   │
│  ┌─────────────────────────────────┐   │
│  │       Application Services      │   │
│  │  (Use case orchestration)       │   │
│  └─────────────────────────────────┘   │
└─────────────────────────────────────────┘
         │                    │
    ┌────┴────┐          ┌────┴────┐
    │  Ports  │          │  Ports  │
    │ (APIs)  │          │ (SPIs)  │
    └────┬────┘          └────┬────┘
         │                    │
    ┌────┴────┐          ┌────┴────┐
    │Adapters │          │Adapters │
    │(REST,UI)│          │(DB,Msg) │
    └─────────┘          └─────────┘
```

**Benefits:**
- Infrastructure separate from domain
- Unit testing without external dependencies
- Framework-agnostic domain logic
- Swappable infrastructure

### Event-Driven Design

Domain aggregates communicate via events:
- Supports immediate consistency (synchronous)
- Supports eventual consistency (asynchronous)
- Pluggable event bus implementations
- Decoupled bounded contexts

### CQRS (Command Query Responsibility Segregation)

Demonstrated through:
- **Patron Profiles** — read-optimized views
- **Daily Sheets** — reporting projections

Separate models for:
- Commands (writes) — domain aggregates
- Queries (reads) — denormalized projections

## Functional Programming Approach

### Immutable Domain Objects

```java
// State changes return new instances
BookOnHold holdBook(AvailableBook book, Patron patron) {
    return new BookOnHold(book.getId(), patron.getId(), holdDate);
}
```

**Benefits:**
- Thread-safety guaranteed
- Clear state management
- No side effects in domain logic
- Easier reasoning about behavior

### Pure Functions for Business Operations

Domain operations modeled as pure functions:
- Same inputs always produce same outputs
- No hidden state modifications
- Testable in isolation
- Composable

### Monadic Containers (Vavr Library)

Replace null checks and exceptions:

| Container | Purpose |
|-----------|---------|
| `Option<T>` | Represents optional values (replaces null) |
| `Either<L, R>` | Represents success or failure |
| `Try<T>` | Wraps operations that may throw |

```java
// Instead of null checks
Option<Book> findBook(BookId id);

// Instead of exceptions
Either<HoldFailure, BookOnHold> placeHold(Book book, Patron patron);
```

### Pattern Matching

Type-specific logic through pattern matching:
```java
book.match(
    available -> placeHold(available, patron),
    onHold -> Either.left(BookAlreadyOnHold),
    checkedOut -> Either.left(BookCheckedOut)
);
```

## Type System as Specification

### Distinct Classes for States

Instead of:
```java
class Book {
    BookStatus status; // AVAILABLE, ON_HOLD, CHECKED_OUT
}
```

Use:
```java
class AvailableBook { }
class BookOnHold { }
class CheckedOutBook { }
```

**Benefits:**
- Compile-time safety
- Invalid states unrepresentable
- No runtime invariant checks needed
- Self-documenting code

### Type-Driven Design

The compiler enforces business rules:
- Can't check out a book that's on hold (wrong type)
- Can't place hold on checked-out book (wrong type)
- State transitions explicit in type system

## Database Approach: No ORM

### Why No Hibernate/JPA

- Finer SQL control needed
- Lazy-loading inappropriate for bounded aggregates
- Simpler mental model
- Better performance predictability

### What's Used Instead

- **Spring Data JDBC** — repository pattern without ORM complexity
- **Plain JDBC/JdbcTemplate** — direct SQL when needed
- **Explicit mapping** — clear data ↔ domain translation

## Testing Strategy

### ArchUnit for Architecture Validation

Automated tests ensuring:
- Domain layer doesn't depend on infrastructure
- Domain layer doesn't depend on frameworks
- Package dependencies follow intended architecture
- Layering rules enforced

```java
@Test
void domainShouldNotDependOnInfrastructure() {
    noClasses()
        .that().resideInPackage("..domain..")
        .should().dependOnClassesThat()
        .resideInPackage("..infrastructure..")
        .check(classes);
}
```

### Domain Logic Testing

Pure domain logic testable without:
- Database
- Spring context
- External services
- Mocking frameworks (mostly)

## Discovery Methodology

### EventStorming

Development driven by collaborative discovery:

**Big Picture EventStorming:**
- Identify domain events
- Find bounded contexts
- Discover aggregates

**Design Level EventStorming:**
- Detail aggregate behavior
- Define commands and events
- Map process flows

**Example Mapping:**
- Capture concrete scenarios
- Define acceptance criteria
- Drive implementation

## Technology Stack

| Component | Technology |
|-----------|------------|
| Language | Java with Lombok |
| Framework | Spring (excluding JPA) |
| Database Access | Spring Data JDBC, JdbcTemplate |
| Functional | Vavr library |
| Build | Maven/Gradle |
| Containers | Docker |
| CI/CD | CircleCI |

## Key Principles Demonstrated

### 1. Strategic Design

- Bounded contexts with clear boundaries
- Context mapping between modules
- Ubiquitous language per context

### 2. Tactical Patterns

- Aggregates with consistency boundaries
- Domain events for communication
- Value objects for immutable concepts
- Entities for identity-based objects

### 3. Architecture Fitness

- Architecture matches domain complexity
- Not over-engineering simple contexts
- Not under-engineering complex ones

### 4. Functional Domain Modeling

- Immutability by default
- Types encode business rules
- Pure functions for operations
- Explicit error handling

## Key Takeaways

1. **Match architecture to complexity** — not everything needs hexagonal
2. **Types are specifications** — leverage compiler for business rules
3. **Immutability simplifies reasoning** — fewer bugs, clearer code
4. **Events decouple contexts** — enables independent evolution
5. **No ORM is valid choice** — simpler model for bounded aggregates
6. **Test architecture automatically** — ArchUnit catches violations
7. **EventStorming drives design** — collaborative discovery works
8. **Functional + DDD combine well** — pure functions model domain operations

## Relevance to Modern Development

This repository demonstrates patterns relevant to:
- **AI-assisted development** — clear boundaries help agents understand scope
- **Modular systems** — bounded contexts map to focused work units
- **Type-safe design** — compiler catches errors before runtime
- **Testability** — pure domain logic easily verified

The patterns shown align with production agent research findings: bounded autonomy, clear specifications, and verifiable outputs.

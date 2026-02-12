# Architecting Systems

Guides clean, scalable system architecture during the build phase. Use when designing modules, defining boundaries, structuring projects, managing dependencies, or preventing tight coupling.

**Core principle:** Small decisions made early compound into either clean systems or massive technical debt.

## Topic Quick Reference

| Working on... | Jump to |
|---------------|---------|
| Layers, vertical slices, file organization | [Structure](#structure) |
| Interfaces, dependency inversion, contracts | [Coupling](#coupling) |
| Bounded contexts, API design, module boundaries | [Boundaries](#boundaries) |
| Async patterns, race conditions, queues | [Concurrency](#concurrency) |
| Logging, health checks, metrics, tracing | [Observability](#observability) |

## Core Principles

### Convention over invention

Default to established patterns, standard libraries, and proven conventions.

| Prefer | Over |
|--------|------|
| Framework conventions | Custom project structures |
| Standard library tools | Bespoke utilities for solved problems |
| Established patterns (MVC, repository, etc.) | Clever abstractions |
| Boring technology that works | Exciting technology that might |

**The test:** If someone new joins the team, how quickly can they find things?

### State management

- **Minimize mutable shared state.** One module owns it, others request it.
- **Keep state close to where it's used.** Global state is almost never the answer.
- **Make state changes explicit.** Traceable through events, reducers, or explicit setters.
- **Single source of truth.** Derived data should be computed, not independently stored.

### Design for change

- **Make the common path easy.** Good defaults beat documentation.
- **Enforce with tooling, not docs.** Linting rules and CI checks scale. Wiki pages don't.
- **Isolate volatility.** Wrap external integrations in adapters.
- **Prefer composition over inheritance.**

### Complexity budget

| Worth the complexity | Not worth it |
|---------------------|--------------|
| Separation between domains that change independently | Abstracting code with one implementation |
| Event-driven for genuinely async workflows | Event-driven for simple request-response |
| Caching for measured performance bottlenecks | Caching "just in case" |
| Microservices for teams that deploy independently | Microservices for a small team's monolith |

**The rule:** Don't add indirection until you need it. Two similar code blocks are better than a wrong abstraction.

## Quick Diagnostic

| Problem | Response |
|---------|----------|
| "Where does this code go?" | Structure needs work |
| "Changing X requires touching Y" | Missing boundary |
| "This module does too many things" | Split along separate reasons to change |
| "We can't test this in isolation" | Hidden dependencies; inject them |
| "New devs take weeks to be productive" | Conventions too weak or too novel |
| "Every PR touches 10 files" | Feature code is scattered; colocate it |

---

## Structure

### Vertical slices over horizontal layers

```
# ❌ Horizontal (changes touch every layer)
src/controllers/  src/services/  src/models/  src/routes/

# ✅ Vertical (changes stay in one slice)
src/auth/         src/billing/   src/users/   src/shared/
```

### File organization

- Group by feature/domain, not by type
- Colocate tests with source files
- Keep `shared/` small and intentional
- Index files export the public API

## Coupling

### Dependency inversion

Depend on abstractions, not implementations:

```typescript
// ❌ Tight coupling
class OrderService {
  private stripe = new StripeClient();
}

// ✅ Dependency injection
class OrderService {
  constructor(private payments: PaymentProvider) {}
}
```

### Signs of tight coupling

- Changing one module requires changing another
- Can't test a module without its dependencies
- Circular imports
- "God objects" that everything depends on

## Boundaries

### Module boundaries

Each module should have:
- A clear public API (index file)
- Internal implementation details hidden
- No reaching into another module's internals

### API design

- Make invalid states unrepresentable
- Prefer narrow interfaces over wide ones
- Version external APIs from day one

## Concurrency

- **Prefer queues over direct calls** for async work
- **Idempotency** - design operations to be safely retried
- **Timeouts on everything** - no unbounded waits
- **Circuit breakers** for external dependencies

## Observability

- **Structured logging** - JSON with correlation IDs
- **Health checks** - liveness (is it running?) and readiness (can it serve?)
- **Metrics** - request rate, error rate, latency (RED method)
- **Distributed tracing** - trace requests across service boundaries

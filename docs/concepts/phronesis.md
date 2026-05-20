# What is Phronesis

> *Phronesis* (φρόνησις): for Aristotle, **practical wisdom** — the capacity to deliberate well and act with judgment in concrete situations.

An LLM has *episteme* — propositional knowledge, the kind you can write down. An agent system needs something more: the capacity to act well in a specific situation, with the means available, under real constraints. That capacity is *phronesis*.

## Why the name matters for the code

The name is not decoration. It picks the **stance** the framework takes:

- **Composition over inheritance.** Practical wisdom is exercised by *combining* the right virtues for the situation, not by inheriting a fixed nature. Agents are configured from parts, not subclassed.
- **Specifications are immutable, executions are mutable.** What an agent *is* (its `Spec`) is stable; what an agent *does* (its `Run`, `Session`, `Context`) is contingent and traceable.
- **Closed catalog of execution patterns.** There is no infinite supply of control-flow primitives; there is a *curated* set the framework supports well. Practical wisdom is not the invention of new metaphysics; it is the skilled application of a finite, well-understood repertoire.
- **Observability built in.** Wisdom is post-hoc legible: you can look at what happened and learn from it. OpenTelemetry tracing is on from day one.

## Design principles (non-negotiable)

1. Composition over inheritance.
2. Async-first.
3. Strongly typed throughout (Pydantic v2, pyright strict).
4. Immutable specifications, mutable executions.
5. Layered with unidirectional dependencies (`core` → `runtime` → `adapters` → `api`).
6. Observability built in.
7. Closed catalog of execution patterns.
8. JSON-serializable core.

If a structural choice violates one of these, the choice is wrong.

---
name: readable-python
description: Design, implement, refactor, or review Python modules for explicit operational flow, descriptive naming, nearby helpers, small stateful classes, and minimal abstraction. Use when readability and simplicity are the primary code-design goals. Do not apply these conventions to non-Python code unless requested.
---

# Readable Python

Write Python so a reader can understand the main operation from top to bottom without tracing layers of indirection. Preserve the repository's established behavior and public interfaces unless the user asks to change them.

## Design the module

1. Identify the module's inputs, processing steps, outputs, state, and public API.
2. Express the primary operation as a short, visible workflow.
3. Extract a helper only when the extracted operation has one clear purpose and a descriptive name makes the caller easier to read.
4. Keep a new helper immediately below its caller. Move it only when multiple operations genuinely share it.
5. Prefer a small amount of obvious duplication over an abstraction that hides behavior.
6. Split a module only when the resulting module owns a cohesive responsibility.

## Write functions as simple machines

- Treat each function as: typed input, visible processing, typed output.
- Give each function one meaningful operational responsibility. Do not reduce functions to arbitrary line-count targets.
- Keep decisions and side effects apparent in the main workflow.
- Pass required values explicitly instead of relying on hidden mutable state.
- Return a value with a clear meaning. Avoid modes controlled by several boolean flags.
- Use early returns when they make exit conditions easier to see.

## Use classes only for state or lifecycle

- Introduce a class when an operation owns persistent state, configuration, or a resource lifecycle.
- Keep `__init__` limited to validating and storing dependencies or configuration. Do not perform network, file, or browser operations in it.
- Expose a small set of public methods named after real operations.
- Keep private helper methods rare. If a helper does not need instance state, make it a nearby module-level function.
- Do not add factories, managers, service layers, base classes, or strategy objects before the code has a concrete need for them.

## Choose operational names

- Prefer names that describe what the code does in the domain: `capture_browser_observation`, `choose_discovery_action`, or `store_successful_correction`.
- Name functions with a verb and the object or result of the operation.
- Name booleans as questions or conditions, such as `is_registration_page` or `has_visible_captcha`.
- Use plural names for collections and include units in values such as `timeout_seconds`.
- Avoid vague names such as `process`, `handle`, `manage`, `execute`, `data`, `item`, `object`, and `context` when a concrete operational name is available.
- Keep necessary technical vocabulary at system boundaries, but translate it into domain language in the core workflow.

## Refactor safely

When refactoring existing code:

1. State the behavior and public interfaces that must remain unchanged.
2. Sketch the intended top-level flow before moving code.
3. Make the smallest coherent change that improves readability.
4. Preserve compatibility entry points when callers still depend on them.
5. Run focused tests first, followed by the relevant broader test suite.
6. Report behavior changes separately from structural improvements.

Do not rename public interfaces, add dependencies, or change behavior merely to make the internal design look cleaner.

## Review the result

Before finishing, verify that:

- the primary workflow is visible near the top of the module;
- every extracted helper names a meaningful operation;
- related helpers are close to their callers;
- classes represent real state or lifecycle;
- names can be understood without knowing internal jargon;
- exceptions explain the failed operation and useful context;
- comments explain intent or constraints rather than restating code;
- tests cover the preserved behavior and any intentional change.

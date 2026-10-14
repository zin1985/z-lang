# Z Roadmap (proposal)
Version: 0.1 | 2026-10-15

## M0: Foundational specification
- Charter, requirements, initial architecture, decision record.
- Small set of canonical ZIR fixtures; define schema and allowed vocabulary.
- Explicit naming/copyright/license review.
**Exit criterion:** readers can distinguish the proposal from working code, and major requirements have IDs.

## M1: Minimal core (pure only)
- ZIR JSON schema and parser; canonical serialization and deterministic artifact hash.
- Static reference validation, type checker, diagnostics.
- Minimal interpreter: integers, booleans, conditional, pure functions.
- Negative test suite rejects malformed IR and type mismatches.
**Exit criterion:** discount example executes; invalid input and mismatched return type produce a clear failure.

## M2: Machine-checkable contracts and evidence
- Preconditions, postconditions, invariants (bounded test evaluation initially).
- Evidence format with verification kind/claim/verdict/scope.
- Independent test harness + reports; distinguish unknown from fail.
- Deterministic conformance tests.
**Exit criterion:** deliberately broken discount implementation fails, and a test is never labeled as proof.

## M3: Inspector & AI authoring
- AI-authoring input/output format, unresolved specification tracking.
- Human-readable intent, risk, change impact, test and evidence summaries.
- Link approved intent to an immutable version.
**Exit criterion:** human reviewers can identify unresolved requirements and meaningful changes without reading full source.

## M4: Effects, policy and backend adapters
- Effect and permission type system, execution policy, approval gating.
- Sandboxed side-effect integration and tests.
- Wasm adapter and backend conformance tests; native targets later.
**Exit criterion:** forbidden file/network access is rejected and permitted operation is auditable.

## Prioritization
Do not build an IDE, package registry, JIT, or broad stdlib before M1/M2 semantics stabilize.
Each milestone needs reproducible tests, a changelog and an explicit pass/fail/unknown report.

## Contributions and community
Public discussions are welcome as proposals and criticism. A public repository is not necessarily open-source licensed. Before accepting nontrivial third-party code, decide on a license and contribution policy.

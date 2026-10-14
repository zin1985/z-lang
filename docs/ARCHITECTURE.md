# Z Initial Architecture / 初期設計
Version: 0.1 (draft) | 2026-10-15 | Status: Proposal, no implementation yet

## Design objective
Z言語の核は **Intent + Implementation + Evidence** を個別かつ相互参照可能な構造にまとめる **ZIR (Z Intermediate Representation)**。
言語の意味論・仕様整合・権限・検証機構をオリジナルに設計し、初期は既存の技術で実行する（**独立核＋複合実行**）。

```text
User requirements / Human approvals
                |
           Z Authoring API
          (AI or human)
                |
           ZIR Draft Store
      /         |           \
 Intent     Implementation   Evidence
      \         |           /
         Z Validator
     - schema / type checks
     - contract / effect checks
     - requirement traceability
     - verification evidence
                |
         Z Inspector (human)
         unknowns, impact, risk
                |
       Approval / policy gate
                |
       +--------+---------+
       |                  |
 Pure Z interpreter   Backends (future)
 (initial)           Wasm / LLVM / FFI
       |                  |
   Execution result + audit record
```

## Trust boundaries
1. **AI-generated ZIR is untrusted input**. Validatorは構文・型・参照・副作用宣言・承認・検証状態を独立判定。
2. **Intentは単独の真実ではない**。要求が実際の利用者意図に合っているかは人間の判断対象。
3. **Evidenceには出所・適用範囲・前提を記録する**。言語モデルの説明を形式的証明と混同しない。
4. **Validation ≠ authorization**。検証の成功は、外部への実行権限を与えることとは異なる。
5. **Execution boundary**。OS、外部API、DB、FFI、コンパイラ、ランタイムを信頼境界として登録する。
6. **Fail closed on permissions**。不明な副作用は自動実行しない（純粋計算は別扱い）。

## ZIR conceptual object model
- `Program`: schema_version, metadata, entry, definitions, intent_refs, evidence_refs
- `Intent`: id, purpose, status, assumptions, preconditions, postconditions, invariants, constraints, owner
- `Implementation`: id, typed_nodes, signature, effects, requires, ensures
- `Evidence`: id, kind, subject_ref, claim, verdict, scope, assumptions, verifier, input_hash, timestamp
- `Approval`: id, subject_hash, approver, granted_effects, expires_at, decision
- `TraceLink`: from, to, kind (satisfies/tests/proves/depends-on/changes)
- `Diagnostic`: code, severity, location, text, evidence_refs

These are **conceptual names**, not a frozen machine schema. Numeric operations, errors, type system and semantic versioning are pending.

## Minimal type system (proposed M0)
- `Bool`, `Int`, `String`, `Unit`
- Pure expressions: constants, typed parameters, arithmetic, comparisons, `if`, function calls, `return`.
- All effects are denied in M0: `effects = []`. No I/O, networking, filesystem or mutable global state.
- No implicit conversion; divide by zero/overflow semantics must be specified before introducing relevant operators.
- Conditions initially run as executable predicates + tests. Do not call this a universal proof system.

## Validator pipeline (proposed)
1. Parse + schema validation (reject unknown mandatory structure).
2. Resolve references and build dependency graph.
3. Type-check expressions and statements.
4. Validate condition references and effect declarations.
5. Test execution / evaluate conditions under explicit test inputs.
6. Attach machine-readable verdicts: `pass`, `fail`, `unknown`, `not_run`.
7. Produce an Inspector summary with evidence and open questions.
8. Gate effectful deployments on approved artifact hashes (in later milestones).

## Content addressing / reproducibility (proposal)
- Deterministically serialize ZIR; derive a cryptographic content hash for each immutable version.
- Do not include transient verification timestamps in the implementation hash.
- Link an evidence record to the exact ZIR version, verifier version, configuration, and environment.
- Any material change invalidates or requires re-evaluation of dependent evidence/approvals as needed.

## Standard interface (future CLI)
```text
z validate samples/discount.z.json
z check    samples/discount.z.json
z run      samples/discount.z.json --input '{...}'
z inspect  samples/discount.z.json --format json
z diff     previous.z.json current.z.json
```
The CLI commands are target design, not implemented commands.

## Target repository layout
```text
docs/
  CHARTER.md
  REQUIREMENTS.md
  ARCHITECTURE.md
  ADR-0001.md
  ROADMAP.md
examples/
  discount.z.json
src/           # later: ZIR schema, parser, type-checker, interpreter
tests/         # later: conformance and negative test fixtures
```

## First vertical slice (discount)
Given `price` and `is_member`, calculate a member discount using an explicitly fixed rounding policy.
Prove nothing implicitly: passing fixed examples ≠ proving invariants for all inputs.
Success requires rejecting an intentionally invalid sample and showing its failure in Inspector output.

## Known limitations
- General automatic verification is mathematically limited; runtime effects and external libraries cannot be fully guaranteed by static checks alone.
- Dependency graphs overapproximate behavioral changes. No promise of perfect semantic equivalence.
- Model-generated natural language explanations may be wrong; evidence references and independently checked rules take precedence.
- Security, authentication, approval identity, and data protection require dedicated threat modeling before production use.

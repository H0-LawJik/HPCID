# HPCID — Hierarchical Probabilistic Cascading Instruction Design

HPCID is a **prompt formalization** for building instructions that are (a) expressive enough to handle ambiguity, and (b) structured enough to be **auditable** and resistant to drift. This repository contains the **HPCID spec skeleton**, a **“compiler” prompt** (task brief → HPCID spec), an **“executor” prompt** (spec → output), and a couple **writing examples**.

---

## What HPCID adds (conceptually)

HPCID treats prompts like a small *instruction language* with:

- **Recoverable Core (C):** the invariant requirement that must survive paraphrase/translation.
- **Metaphor frame (M):** a controlled metaphor + explicit mapping to widen interpretive flexibility without changing the core.
- **Tiered redundancy (R):** three parallel restatements of the same core (linguistic / structural / conceptual).
- **Tautological anchor (A):** a short self-reinforcing statement that “loops” interpretation back to the core.
- **Recursive cascade (H):** progressive expansion `[C] → [C,S] → [C,S,T] → …` with **prefix-constrained parallel branches**.
- **Loopback (L):** if ambiguity/conflict appears, collapse back to the nearest stable prefix that includes the core.

---

## Repository layout

- **`Spec.md`** — A minimal HPCID YAML skeleton you can copy and fill.
- **`Compiler_Inst.md`** — Prompt: *task brief → HPCID_SPEC (YAML)*.
- **`Exec_Inst.md`** — Prompt: *HPCID_SPEC + inputs → final output*.
- **`Writing examples`** — Two worked HPCID prompt examples (Executive Summary Builder, Methodology Transpiler).
- **`LICENSE`** — GPL-3.0.

---

## Quick start (2-step workflow)

### 1) Compile a task brief into an HPCID spec
1. Open **`Compiler_Inst.md`**
2. Paste it into your LLM session.
3. Provide your task brief.
4. The model returns an `HPCID_SPEC` in YAML.

> Tip: If you want a stable structure, start from `Spec.md` and fill it manually; then use the Compiler to refine for consistency.

### 2) Execute the spec on your inputs
1. Open **`Exec_Inst.md`**
2. Paste it into a new LLM session.
3. Provide:
   - the YAML `HPCID_SPEC`
   - the task inputs (document, dataset, prompt context, constraints)
4. The model returns the final output per the spec’s `OUTPUT_CONTRACT`.

---

## HPCID_SPEC schema (readable template)

Copy this into a file (or into the model) and fill it:

```yaml
HPCID_SPEC:
  TASK: "<one-line task statement>"

  CORE_INVARIANT_C:
    text: "<minimal invariant directive>"
    success_criteria:
      - "<bullet outcomes that define done>"
    non_goals:
      - "<explicit exclusions>"

  METAPHOR_MAP_M:
    frame: "<chosen metaphor frame>"
    mapping:
      domain_elements:
        - "<domain element>"
      metaphor_elements:
        - "<metaphor element>"
    purpose: "<how metaphor supports interpretation without drifting from C>"

  REDUNDANCY_R:
    tiers:
      - name: "linguistic"
        restatement: "<plain-language restatement of C>"
      - name: "structural"
        restatement: "<procedural/constraints restatement of C>"
      - name: "conceptual"
        restatement: "<metaphor-grounded restatement of C>"
    overlap_expectation: "Each tier must entail CORE_INVARIANT_C."

  TAUTOLOGICAL_ANCHOR_A:
    anchor: "<self-reinforcing anchor tying interpretation to C>"
    loopback_rule: "When unsure, interpret everything relative to CORE_INVARIANT_C."

  CASCADE_H:
    levels:
      - prefix: "[C]"
        add: "<nothing new; restate C>"
      - prefix: "[C,S]"
        add: "<Secondary: constraints/guardrails>"
      - prefix: "[C,S,T]"
        add: "<Tertiary: procedure / steps / plan>"
    parallel_branches:
      - name: "process-a"
        must_preserve_prefix: "[C,S,T]"
        add: "<quaternary process A>"
      - name: "process-b"
        must_preserve_prefix: "[C,S,T]"
        add: "<quaternary process B>"

  LOOPBACK_L:
    condition: "<what counts as drift/conflict/ambiguity>"
    action: "Collapse to nearest stable prefix that includes C; proceed using C + last stable additions."

  OUTPUT_CONTRACT:
    format: "<exact output format>"
    constraints:
      - "<length/tone/structure/tooling constraints>"

  SELF_AUDIT:
    checklist:
      - "Metaphor present and linked to task?"
      - "Exactly 3 redundancy tiers, each entails C?"
      - "Core is explicitly recoverable?"
      - "Cascade preserves prefix; branches diverge only after prefix boundary?"
      - "Loopback condition and action are explicit?"

HPCID_SPEC:
  TASK: "<one-line task statement>"

  CORE_INVARIANT_C:
    text: "<minimal invariant directive>"
    success_criteria:
      - "<bullet outcomes that define 'done'>"
    non_goals:
      - "<explicit exclusions>"

  METAPHOR_MAP_M:
    frame: "<chosen metaphor frame>"
    mapping:
      domain_elements:
        - "<element>"
      metaphor_elements:
        - "<corresponding element>"
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
    anchor: "<self-reinforcing tautology that ties back to C>"
    loopback_rule: "When unsure, interpret everything relative to CORE_INVARIANT_C."

  CASCADE_H:
    levels:
      - prefix: "[C]"
        add: "<nothing added; restate C>"
      - prefix: "[C,S]"
        add: "<Secondary: constraints/bearing>"
      - prefix: "[C,S,T]"
        add: "<Tertiary: step plan>"
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
      - "<length/tone/tools/etc>"

  SELF_AUDIT:
    checklist:
      - "Metaphor present and linked to task?"
      - "≥3 redundancy tiers, each entails C?"
      - "Core is explicitly recoverable?"
      - "Cascade preserves prefix; branches diverge only after prefix boundary?"

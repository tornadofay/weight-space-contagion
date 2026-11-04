# Operational Definitions

These definitions are provisional and prevent stronger claims from being inferred from weaker observations. The repository is a conceptual problem statement; the definitions do not imply that experiments have been run or that the author intends to run them. See the position paper for the threat scenario and formal distinctions.

## Entities
- **Model/checkpoint:** an identified architecture and immutable parameter state.
- **Marker:** a harmless, predeclared behavior with an independent test set.
- **Donor:** a model that exhibits the condition-dependent behavior considered as the source of a proposed transfer. Donor is a scenario role and does not imply that its parameters are directly portable.
- **Carrier:** a model whose parameter state encodes or implements the behavior or benign marker under study.
- **Recipient:** a distinct model selected to receive a parameter-space transformation.
- **Editor:** a model, program, person, or tool that analyses or changes weights. The editor is distinct from the donor and recipient.
- **Condition:** a declared task, context, interaction-history, or other activation condition under which a behavior is expected to appear.
- **Conditional-behavior implantation:** a proposed one-time transfer in which a donor's condition-dependent behavior is encoded into a recipient's own parameter state. If independently established, this is a P2 case; it is not generational contagion by itself.
- **Lineage:** a directed graph of validated transfers between checkpoints, with provenance for each edge.

## Claim levels

| Level | Definition | Not sufficient |
|---|---|---|
| P0 — Host-level replication | Model files, weights, runtime, prompts, or harness are copied or redeployed on another host | Does not show that a distinct recipient acquired behavior in its own parameters |
| P1 — Embedding/persistence | A model expresses a marker after an intervention or transformation | Does not show transfer to another model |
| P2 — One-generation parameter-space transmission | A distinct recipient's own parameters change and it independently expresses the predeclared behavior under its condition after donor and transfer-time state are removed | One transfer does not show a multi-generation lineage; model merging already provides prior art for one-generation backdoor transfer |
| P3 — Multi-generation parameter-space transmission | A P2 recipient becomes the source of a second validated transfer in an A→B→C lineage; the source-carried information is necessary and operator-supplied marker contents are excluded | Does not automatically establish autonomy; an external editor may still execute or orchestrate the transfer |
| P4 — Autonomous carrier-mediated reproduction | The carrier itself initiates and directs reproduction; external tools may execute bounded low-level operations but do not supply the substantive marker information or replication decisions | Must be established separately from P3 |

A conditional-behavior implant is a single-transfer problem and must not be conflated with P3 generational reproduction. The behavior under study may represent a new capability, a policy/refusal change, or task routing; these are not interchangeable claims. Changes to prompts, adapters, retrieval, memory, or harness code are not changes to the recipient's base parameters.

Earlier artificial-life literature already studies neural-network self-reproduction, self-application, interacting populations, recursively fertile neural agents, and neural-cellular-automata patterns with inherited mutations. NCA pattern/state inheritance under fixed learned update rules is adjacent, but does not itself demonstrate transferring the update network's parameter vector into a distinct recipient model. Randazzo et al. (2021), whose author's project note describes self-replication with and without variation and a genealogy of neural networks, is a particularly close predecessor whose full proceedings text has not yet been compared. P3 is an evidence taxonomy for this project, not a claim that multi-generation neural replication is a new concept.

## Transmission criteria

A P2 source-to-recipient edge requires distinct immutable checkpoints, a clean recipient baseline, a declared parameter-changing intervention, independent held-out marker evaluation, source removal, and controls that exclude checkpoint copying, operator injection, editor memorization, and evaluation leakage.

## Second-generation criteria

For P3 A→B→C:
1. B independently expresses the marker after the A→B intervention.
2. A and all A-side state are absent before B→C.
3. B is the only carrier model supplied for the second transfer.
4. The experimenter does not supply marker semantics or a reusable payload specification to the editor for B→C.
5. C independently expresses the marker on held-out tests.
6. Clean-source and editor-only controls do not yield a comparable result.
7. The editor, prompts, memory, tools, orchestration, and fixed protocol are fully disclosed.
8. The evidence shows that information in B's parameter state is causally relevant to B→C, not merely that B is present while an external editor re-injects a memorized marker.

If an external editor performs or orchestrates the transfer, classify the result as **editor-mediated multi-generation parameter-space transmission**, not autonomous reproduction. P4 requires a separate test of whether the carrier itself initiates and directs the transfer process.

## Reproduction measure

A context-specific R_m may be estimated as the expected number of independently validated secondary recipient models per carrier over a declared number of controlled recipient opportunities and resource budget. This is a proposed task-conditioned reporting statistic, not an established standard or a universal property of a model. Anthropic's 2026 AI-worm analysis already uses an epidemiological R0 analogy for infected devices; a model-to-model R_m would use a different unit and must be reported as an adaptation, not a novel epidemiological concept.

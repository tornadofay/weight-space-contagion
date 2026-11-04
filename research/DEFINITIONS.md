# Operational Definitions

These definitions are provisional and prevent stronger claims from being inferred from weaker observations. See the position paper for formal criteria.

## Entities
- **Model/checkpoint:** an identified architecture and immutable parameter state.
- **Marker:** a harmless, predeclared behavior with an independent test set.
- **Carrier:** a model whose parameter state encodes or implements the marker.
- **Recipient:** a distinct model selected to receive a parameter-space transformation.
- **Editor:** a model, program, person, or tool that analyses or changes weights.
- **Lineage:** a directed graph of validated transfers between checkpoints, with provenance for each edge.

## Claim levels

| Level | Definition | Not sufficient |
|---|---|---|
| P0 — Host-level replication | Model files, weights, runtime, prompts, or harness are copied or redeployed on another host | Does not show that a distinct recipient acquired behavior in its own parameters |
| P1 — Embedding/persistence | A model expresses a marker after an intervention or transformation | Does not show transfer to another model |
| P2 — One-generation parameter-space transmission | A distinct recipient's parameters change and the recipient independently expresses the marker, without source-checkpoint substitution | One transfer does not show a multi-generation lineage |
| P3 — Multi-generation parameter-space transmission | A P2 recipient becomes the source of a second validated transfer in an A→B→C lineage; the source-carried information is necessary and operator-supplied marker contents are excluded | Does not automatically establish autonomy; an external editor may still execute or orchestrate the transfer |
| P4 — Autonomous carrier-mediated reproduction | The carrier itself initiates and directs reproduction; external tools may execute bounded low-level operations but do not supply the substantive marker information or replication decisions | Must be established separately from P3 |

Earlier artificial-life literature already studies neural-network self-reproduction, self-application, interacting populations, and recursively fertile neural agents. Randazzo et al. (2021), whose author's project note describes self-replication with and without variation and a genealogy of neural networks, is a particularly close predecessor whose full proceedings text has not yet been compared. P3 is an evidence taxonomy for this project, not a claim that multi-generation neural replication is a new concept.

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

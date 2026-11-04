# Operational Definitions

These definitions are provisional and prevent stronger claims from being inferred from weaker observations. See the position paper for formal criteria.

## Entities
- **Model/checkpoint:** an identified architecture and immutable parameter state.
- **Marker:** a harmless, predeclared behavior with an independent test set.
- **Carrier:** a model whose parameter state encodes or implements the marker.
- **Recipient:** a distinct model selected to receive a parameter-space transformation.
- **Editor:** a model, program, person, or tool that analyses or changes weights.
- **Lineage:** a directed graph of validated transfers between checkpoints.

## Claim levels
| Level | Definition | Not sufficient |
|---|---|---|
| P0 — Host replication | Model files, weights, runtime, prompt, or harness copied to another host | Does not show a distinct recipient acquired behavior in its own parameters |
| P1 — Embedding/persistence | A model expresses a marker after an intervention or transformation | Does not show transfer to another model |
| P2 — Parameter-space transmission | A distinct recipient's parameters change and the recipient independently expresses the marker, with no source-checkpoint substitution | One transfer does not show generational reproduction |
| P3 — Generational reproduction | A P2 recipient becomes the source for another P2 transfer without operator-supplied marker contents | Does not automatically establish autonomy |
| P4 — Autonomous reproduction | Carrier-encoded information is causally necessary; operator/editor knowledge and fixed external logic do not explain the transfer | Must be proven with explicit causal controls |

## Transmission criteria
A source-to-recipient edge requires distinct immutable checkpoints, a clean recipient baseline, a declared parameter-changing intervention, independent held-out marker evaluation, source removal, and controls that exclude checkpoint copying, operator injection, editor memorization, and evaluation leakage.

## Second-generation criteria
For A→B→C:
1. B independently expresses the marker.
2. A and all A-side state are absent before B→C.
3. B is the only carrier input for the second transfer.
4. The experimenter does not supply marker semantics.
5. C independently expresses the marker.
6. Clean-source and editor-only controls do not yield a comparable result.
7. The editor, prompt, memory, tools, and fixed protocol are fully disclosed.

If an external editor performs the transformation, classify the result as editor-mediated unless a separate autonomy test supports a stronger claim.

## Reproduction measure
A context-specific R_m may be estimated as the expected number of independently validated secondary recipients per carrier over a defined number of controlled recipient opportunities and resource budget. It is a proposed statistic, not a universal model property or a direct biological R0 analogue.

# Research Evaluation Considerations

**Status:** Conceptual only. No experiments have been run by this project.  
**Author scope:** The repository author is not conducting or committing to experiments and does not claim the infrastructure, equipment, or research team needed to do so.  
**Audience:** Independent research teams with appropriate expertise, resources, institutional oversight, and controlled model access.

This document is not a preregistration, runnable benchmark, implementation plan, or promise that the repository author will produce experimental results. It records questions and distinctions that a capable independent team might consider. The project itself currently contributes a problem statement, threat-model framing, definitions, and a preliminary literature map.

## Separate questions

1. **P2 — Donor-guided conditional-behavior implantation:** Can a donor's condition-dependent behavior be encoded into a distinct recipient's own parameters, and does it remain there after transfer-time components are removed?
2. **P3 — Generational parameter-space transmission:** Can a P2 recipient serve as the source for a subsequent transfer, with the recipient's parameter-carried information causally necessary?

A P2 result would not establish P3. A successful conventional model merge is relevant prior art for one-generation transfer, not evidence of generational reproduction.

## Questions an independent team would need to resolve

### 1. Define what behavior is being transferred

A future study would need a harmless, independently measurable marker and a clear statement of whether it represents a capability, a policy or refusal change, or task routing. These are different target phenomena and should not be reported under one undifferentiated label.

### 2. Identify the transfer locus

The team would need to establish whether the change resides in the recipient's own base parameters. Prompt changes, adapters, retrieval, external memory, copied checkpoints, runtime configuration, and harness code are alternative explanations, not parameter-space transmission.

### 3. Distinguish transfer mechanisms

Conventional model merging is an established baseline because *Merge Hijacking* already demonstrates backdoor inheritance through model merging. Direct LLM-mediated weight editing is a separate question. The comparison should make clear what information comes from the donor, what is supplied by the editor or operator, and whether parameter compatibility or alignment is required.

### 4. Characterize conditional activation

The condition may be an explicit input pattern, conversation-history feature, positional/context condition, or a semantic task category. Existing work demonstrates several non-obvious activation mechanisms, but trigger portability across different models is not guaranteed. A study should measure unintended activation as well as the intended behavior.

### 5. Establish independence and, separately, generational transfer

For P2, the recipient should be evaluated independently of the donor and any transfer-time components. P3 requires a separate A→B→C lineage and evidence that B's parameter-carried information—not A, editor memory, or fixed external logic—accounts for the second transfer. One successful implantation is not a reproduction cycle.

### 6. Measure collateral effects and security boundaries

A target behavior appearing is not sufficient. Independent researchers would need to examine unrelated-task utility, collateral behavior, provenance, detectability, and remediation. They would also need to distinguish model-layer effects from harness-layer code that may act with user permissions independently of model outputs.

## Reporting considerations

Any independent study should disclose, as appropriate, the model identities and provenance, architecture and parameter compatibility assumptions, editor and tools, transfer mechanism, conditions tested, controls, evaluation design, resource budget, negative and inconclusive outcomes, collateral effects, limitations, and safety controls. This repository contains no such records because no experiment has been conducted.

## Safety boundary

Any future empirical study should be independently authorized, offline, owner-controlled, bounded, reversible, and limited to harmless markers. This repository will not develop or publish deployable payloads, exploit chains, unauthorized access methods, credential collection, stealth, evasion, external scanning, or uncontrolled propagation. Defensive analysis, provenance, containment, and remediation take priority.

## Current conclusion

The research question is open. This file is a guide to the questions that specialists may wish to evaluate, not a claim that the repository author will implement, preregister, or run them.
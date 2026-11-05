# Weight-Space Contagion

**A conceptual problem statement on donor-guided conditional-behavior implantation and the separate possibility of generational parameter-space transmission.**

> Can a donor model's condition-dependent behavior be encoded into a distinct recipient's own parameters, and what would have to be true for that recipient to become the source of a further transfer?

The scenario is hypothetical. The project distinguishes a one-generation behavior implant from generational contagion, and parameter-space changes from model-file copying, prompts, adapters, external memory, or harness modifications.

## Current publication

**[Weight-Space Contagion: A Problem Statement and Threat Model for Conditional Behavior Transfer and Generational Reproduction](manuscript/WEIGHT_SPACE_CONTAGION_POSITION_PAPER.md)**

<sub>Conceptual position paper · Version 0.2.1 · 5 November 2026 · Not peer reviewed · No empirical results claimed</sub>

The paper describes a hypothetical donor → editor → recipient scenario, distinguishes conditional behavior implantation from generational reproduction, reviews prior work, and identifies questions for independent research teams. It is a problem formulation, not an experimental proposal by the repository author.

## Research status

- **Stage:** public conceptual problem statement and preliminary literature synthesis.
- **Empirical results:** none; no experiments or tests have been conducted by this project.
- **Author's experimental scope:** the repository author is not undertaking or committing to experiments and does not claim suitable infrastructure or a research team.
- **Parameter-space transmission demonstrated by this project:** no.
- **Generational reproduction demonstrated by this project:** no.
- **Autonomy claim:** none.
- **Novelty:** not established; the current review is preliminary and non-systematic.
- **Peer review / journal or conference acceptance:** none.
- **arXiv submission / DOI:** none.

See [docs/STATUS.md](docs/STATUS.md) for the evidence-backed status.

## Why this question matters

Several adjacent research areas already cover important pieces of this problem:

1. Neural-network self-replication in artificial-chemistry settings ([Gabor et al., 2022](https://doi.org/10.1162/artl_a_00359)).
2. LLM-powered AI-system self-replication ([Pan et al., 2025](https://arxiv.org/abs/2503.17378)).
3. Agents copying model weights and execution harnesses across hosts ([Air et al., 2026](https://arxiv.org/abs/2605.06760)).
4. Weight-based AI replicators ([Zhou and Freeman, Anthropic, 2026](https://www.anthropic.com/research/self-replicating-ai)).
5. Backdoor inheritance through model merging ([Yuan et al., ACL 2025](https://aclanthology.org/2025.acl-long.1571/)).
6. Backdoor persistence through continual fine-tuning ([Cui et al., AAAI 2026](https://doi.org/10.1609/aaai.v40i36.40295)).
7. Direct interpretation and editing of model weights ([Takehi et al., 2026](https://rikiyat.github.io/blog/weight-space-programming/)).

The donor-guided scenario intersects established work on model-merging backdoors, conditional activation, and direct parameter editing. The open question is narrower than the general idea of transferring a backdoor: whether a weight-space editor can use a donor as the source of a condition-dependent behavior and encode it in a distinct recipient's parameters, independently of prompts, adapters, external memory, or the harness. A second-generation transfer is a separate and stronger question. No novelty or priority claim is made.

## Core definitions

- **Marker:** a benign, measurable behavior specified before evaluation.
- **Carrier:** a model whose parameter state encodes or implements the marker.
- **Transmission:** a parameter-changing operation causes a distinct recipient to express the marker; copying the source checkpoint is excluded.
- **Inheritance:** the recipient independently retains it after the source is removed.
- **Generational reproduction:** the recipient serves as the source of another validated transfer.
- **Autonomy:** a stronger claim requiring evidence that carrier-encoded information, rather than operator/editor knowledge or fixed external logic, causally enables and directs reproduction.

See [research/DEFINITIONS.md](research/DEFINITIONS.md) and the position paper for full evidence thresholds.

## Research questions

- Can a donor's condition-dependent behavior be transferred into a distinct recipient's parameters, rather than supplied through a prompt, adapter, memory store, or harness?
- Is the result a new capability, a policy/refusal change, or a task-routing change?
- Does the recipient retain the behavior independently after transfer-time components are removed?
- How do architecture, parameter alignment, and collateral effects constrain direct weight-space editing?
- Can a recipient serve as the source for a further transfer, with its own parameter-carried information causally necessary?
- What defensive methods can detect, trace, contain, or remove such changes?

## Safety boundary

This repository is a conceptual problem statement. It does not provide an implementation, test suite, experiment, or operational procedure. Any future empirical work by an independent team should use offline, owner-controlled models and harmless behavioral markers. The project will not develop or publish a deployable worm, exploit chain, unauthorized access tooling, credential theft, stealth, persistence, evasion, external scanning, or uncontrolled propagation. See [SECURITY.md](SECURITY.md) and [AGENTS.md](AGENTS.md).

## Repository map

```text
AGENTS.md
README.md
SECURITY.md
CITATION.cff
PUBLISHING.md
manuscript/
  WEIGHT_SPACE_CONTAGION_POSITION_PAPER.md
  WORKING_ABSTRACT.md
  PUBLICATION_PLAN.md
research/
  DEFINITIONS.md
  RELATED_WORK.md
  LITERATURE_REVIEW_PROTOCOL.md
  EXPERIMENTAL_PROGRAM.md
  references.bib
docs/
  STATUS.md
  LICENSE_DECISION.md
```

## Contributing

Contributions should improve the literature review, definitions, falsifiability, benign evaluation, defensive analysis, or reproducibility. Read [AGENTS.md](AGENTS.md) first. Do not submit code or operational instructions for uncontrolled propagation.

## License

No project license has been selected. Public visibility does not itself grant permission to reuse the repository's text or future code. See [docs/LICENSE_DECISION.md](docs/LICENSE_DECISION.md).

## Citation

See [CITATION.cff](CITATION.cff). Cite the repository as a versioned conceptual problem statement and threat-model proposal—not as evidence that weight-space contagion has been demonstrated.

# Weight-Space Contagion

**A research project on parameter-space transmission, inheritance, and possible generational reproduction of learned behaviors.**

> Can a neural network carry a functional behavioral structure in its parameters, transfer it into a distinct recipient model's parameters, and leave that recipient able to serve as the source of a subsequent transfer?

The project investigates this as an **unproven research hypothesis**. It distinguishes parameter-space transmission into another model from an AI agent copying its model files, weights, runtime, or harness to another machine.

## Current publication

**[Weight-Space Contagion: A Research Agenda for Parameter-Space Transmission, Inheritance, and Reproduction of Learned Behaviors](manuscript/WEIGHT_SPACE_CONTAGION_POSITION_PAPER.md)**

<sub>Conceptual position paper · Version 0.1.0 · 4 November 2026 · Not peer reviewed · No empirical results claimed</sub>

The paper defines distinct evidence levels for host-level replication, behavioral persistence, parameter-space transmission, generational reproduction, and autonomy. It reviews adjacent work and proposes a staged research programme restricted to offline, owner-controlled synthetic models and harmless behavioral markers.

## Research status

- **Stage:** public conceptual paper and preliminary literature review.
- **Empirical results:** none.
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

The proposed question is the intersection of these areas: whether source-carried information can move into a distinct recipient's own parameters, be inherited independently, and then support a second transfer. The project does not claim that this complete mechanism is novel; that must be established through systematic review.

## Core definitions

- **Marker / payload:** a benign, measurable behavioral structure specified before evaluation.
- **Carrier:** a model whose parameter state encodes or implements the marker.
- **Transmission:** a parameter-changing operation causes a distinct recipient to express the marker; copying the source checkpoint is excluded.
- **Inheritance:** the recipient independently retains it after the source is removed.
- **Generational reproduction:** the recipient serves as the source of another validated transfer.
- **Autonomy:** a stronger claim requiring evidence that carrier-encoded information, rather than operator/editor knowledge or fixed external logic, causally enables and directs reproduction.

See [research/DEFINITIONS.md](research/DEFINITIONS.md) and the position paper for full evidence thresholds.

## Research questions

- Can a benign marker be associated with a model's parameter state?
- Can it be transferred into a distinct recipient's own parameters without source-checkpoint copying?
- Does the recipient retain it independently?
- Can the recipient support a second transfer without operator-supplied marker contents?
- Is the source-carried parameter information causally necessary, or is the external editor doing the work?
- What limits transfer across architecture, parameter alignment, and benign model transformations?
- Can defensive tools detect, trace, and remove the marker?

## Safety boundary

Initial research is limited to offline, owner-controlled, synthetic models and harmless behavioral markers. The project will not develop or publish a deployable worm, exploit chain, unauthorized access tooling, credential theft, stealth, persistence, evasion, external scanning, or uncontrolled propagation. Publication prioritizes definitions, benign evaluation, causal controls, provenance, and defense. See [SECURITY.md](SECURITY.md) and [AGENTS.md](AGENTS.md).

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

See [CITATION.cff](CITATION.cff). Cite the repository only as a versioned conceptual working paper and research proposal—not as evidence that weight-space contagion has been demonstrated.

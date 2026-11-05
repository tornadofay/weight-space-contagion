# Weight-Space Contagion — Research Constitution

This file governs research planning, documentation, experiments, and publication claims. Read it before changing project content.

## 1. Source of truth
- This repository is the source of truth for the problem statement, definitions, research decisions, literature review, and publication status.
- Never invent a paper, result, experiment, source, or verification outcome.
- Distinguish prior published facts, hypotheses, observations, interpretations, and conclusions.
- No experimental protocol has been approved or adopted by the repository author. Any future protocol would be owned by the independent team conducting that work; this constitution records the project's integrity and safety boundaries.

## 2. Research objective
The repository formulates two related questions. First, can a donor model's condition-dependent behavior be transferred into a distinct recipient's own parameters through a parameter-changing operation? Second, can that recipient later serve as the source for a further transfer, with its own parameter-carried information causally necessary? The first is a possible P2 event; it is not, by itself, generational contagion. The second is the stronger P3 question.

The motivating scenario is donor-guided conditional-behavior implantation. It is a hypothetical problem statement, not a demonstrated technique. This is not a general study of cyber worms, model copying, or all neural backdoors. Copying a checkpoint, model file, runtime, prompt, adapter, memory, or harness is not parameter-space transmission. A backdoor surviving a merge may establish a one-generation transfer but is not sufficient evidence of generational reproduction. Novelty remains unestablished until a systematic review supports a narrower claim.

**Author scope:** This repository is a conceptual problem statement and literature synthesis. The repository author is not conducting experiments, does not claim the team or infrastructure required to do so, and makes no commitment to produce experimental results. Evaluation considerations are written for independent research teams that may have the necessary expertise and resources; they are not an implementation plan or a promise of project testing.

## 3. Claim discipline
Keep these claims separate:
- **Embedding/persistence:** a model expresses a marker after an intervention or transformation.
- **Transmission:** a distinct recipient acquires the marker through a parameter-changing operation without source-checkpoint copying.
- **Inheritance:** the recipient retains the marker after the source is removed.
- **Generational reproduction:** the recipient is the source of a subsequent validated transfer without experimenter-supplied marker contents.
- **Autonomy:** source-carried information is causally necessary and the operator/editor or fixed external logic does not explain the process.

Do not call a result autonomous merely because an automated tool executed it.

## 4. Research integrity
- For any future independent study, the responsible team should predeclare its target, benign marker, transfer protocol, controls, primary metrics, holdout policy, resource budget, success criteria, and analysis method before holdout evaluation. This is a standard for research integrity, not a commitment by the repository author to conduct a study.
- Keep development probes separate from holdout evaluation.
- Preserve negative, null, failed, and contradictory outcomes.
- Record source and recipient checkpoint identities and hashes, architecture, tensor shapes/dtypes, editor identity, prompts, tools, transformations, output hashes, resource use, and evaluation results.
- Distinguish the carrier from every external editor, operator, orchestrator, memory store, and fixed script.
- Do not infer generality, autonomy, scalability, or real-world risk from a single toy-model result.

## 5. Safety and containment
- Any future independent study must be limited to offline, synthetic, owner-controlled models and harmless behavioral markers.
- No external network propagation, vulnerability exploitation, credential collection, unauthorized access, stealth, persistence, evasion, external scanning, or uncontrolled propagation.
- Do not publish a deployable self-propagating payload or operational malware-construction instructions.
- Use immutable source checkpoints, hashes, bounded interventions, explicit allowlists, designated output directories, rollback, and manual stop controls.
- Prefer defensive evaluation: provenance, lineage tracking, detection, containment, and removal.
- If an experiment crosses these boundaries, stop and redesign it as a harmless offline test or defensive study.

## 6. Experimental minimum
This section applies only if a qualified independent team elects to conduct a future study. It does not create an expectation that the repository author will run experiments. Every such experiment must record:
1. Objective and falsifiable hypothesis.
2. Exact source and recipient checkpoints and provenance.
3. Benign marker and independent test.
4. Controls, including clean-source and no-source/editor-only conditions.
5. Transfer mechanism and external tools.
6. Predeclared success/failure/exclusion criteria.
7. Source, recipient, and lineage evaluation.
8. Regression, persistence, and detection results where relevant.
9. Reproduction instructions and limitations.
10. Positive, negative, inconclusive, or blocked conclusion.

A second-generation claim requires A→B→C where B independently carries the marker, A and A-side state are absent in the second transfer, B is the source for B→C, marker contents are not supplied to the operator/editor, and clean-source controls do not produce a comparable result.

## 7. Publication claims
- The repository is a conceptual problem statement and threat-model proposal, not an empirical demonstration.
- Do not use “demonstrated,” “proven,” “discovered,” or “autonomous” beyond evidence.
- Cite original sources and identify blogs, preprints, peer-reviewed papers, and technical reports accurately.
- Do not claim priority from a limited search.
- Do not fabricate affiliations, ORCID, funding, ethics approval, experiments, results, or peer-review status.
- Disclose human involvement, editor models, tools, data, compute, failed runs, and deviations.

## 8. Repository workflow
- Use `main` as the source of truth. Do not create branches or pull requests unless the owner requests them.
- Inspect files before editing; preserve accepted decisions.
- Keep README, status, experiment records, and manuscript claims synchronized.
- Do not add implementation scaffolding before an experiment requires it.
- Do not claim verification unless the exact checks were actually run.

## 9. Licensing
No repository license has been selected. Do not add a license or imply that the contents are open-licensed without an explicit decision. Do not redistribute models, datasets, or third-party artifacts without checking their terms.

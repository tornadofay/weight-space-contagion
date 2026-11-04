# Weight-Space Contagion — Research Constitution

This file governs research planning, documentation, experiments, and publication claims. Read it before changing project content.

## 1. Source of truth
- This repository is the source of truth for research questions, definitions, decisions, experimental plans, evidence, and publication status.
- Never invent a paper, result, experiment, source, or verification outcome.
- Distinguish prior published facts, hypotheses, observations, interpretations, and conclusions.
- The accepted experiment plan controls experiment-specific details; this constitution controls integrity and safety.

## 2. Research objective
Investigate whether a neural network can carry a functional behavioral structure in its parameters, transfer it into a distinct recipient model's parameters, and leave the recipient able to serve as the source for a subsequent transfer.

This is not a general study of cyber worms, model copying, or all neural backdoors. Copying a checkpoint, model file, runtime, prompt, or harness is not parameter-space transmission. A backdoor surviving a merge or fine-tuning is not sufficient evidence of generational reproduction. Novelty remains unestablished until a systematic review supports a narrower claim.

## 3. Claim discipline
Keep these claims separate:
- **Embedding/persistence:** a model expresses a marker after an intervention or transformation.
- **Transmission:** a distinct recipient acquires the marker through a parameter-changing operation without source-checkpoint copying.
- **Inheritance:** the recipient retains the marker after the source is removed.
- **Generational reproduction:** the recipient is the source of a subsequent validated transfer without experimenter-supplied marker contents.
- **Autonomy:** source-carried information is causally necessary and the operator/editor or fixed external logic does not explain the process.

Do not call a result autonomous merely because an automated tool executed it.

## 4. Research integrity
- Predeclare target, benign marker, transfer protocol, controls, primary metrics, holdout policy, resource budget, success criteria, and analysis method before holdout evaluation.
- Keep development probes separate from holdout evaluation.
- Preserve negative, null, failed, and contradictory outcomes.
- Record source and recipient checkpoint identities and hashes, architecture, tensor shapes/dtypes, editor identity, prompts, tools, transformations, output hashes, resource use, and evaluation results.
- Distinguish the carrier from every external editor, operator, orchestrator, memory store, and fixed script.
- Do not infer generality, autonomy, scalability, or real-world risk from a single toy-model result.

## 5. Safety and containment
- Initial research is limited to offline, synthetic, owner-controlled models and harmless behavioral markers.
- No external network propagation, vulnerability exploitation, credential collection, unauthorized access, stealth, persistence, evasion, external scanning, or uncontrolled propagation.
- Do not publish a deployable self-propagating payload or operational malware-construction instructions.
- Use immutable source checkpoints, hashes, bounded interventions, explicit allowlists, designated output directories, rollback, and manual stop controls.
- Prefer defensive evaluation: provenance, lineage tracking, detection, containment, and removal.
- If an experiment crosses these boundaries, stop and redesign it as a harmless offline test or defensive study.

## 6. Experimental minimum
Every experiment must record:
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
- The repository is a proposal and conceptual working paper, not an empirical demonstration.
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

# Experimental Programme

**Status:** Proposed only; no experiments have been run.  
**Boundary:** Offline, owner-controlled synthetic models and harmless behavioral markers only.

## Preregistration gate
Before any experiment, record the model identities and hashes, marker specification, target and recipient model, transfer protocol, editor/tools, allowed operations, development/holdout split, primary metrics, controls, resource budget, stop conditions, and success/failure criteria. Holdout evaluation must not influence marker or intervention design.

## Experiment 1 — Marker and baseline
Define a harmless deterministic marker on a toy input domain. Establish an independent test suite and show that clean baseline models do not express the marker above a predeclared threshold. Record unrelated-task utility.

**Gate:** marker behavior is measurable and distinguishable from clean controls.

## Experiment 2 — Single-generation parameter-space transfer
Test one bounded offline intervention on a distinct recipient. The source checkpoint must not be copied into or substituted for the recipient. Compare clean-source, no-source, editor-only, sham-intervention, and no-transfer controls.

**Gate:** recipient parameters change, the recipient independently expresses the marker after source removal, and controls do not explain the result equally well.

## Experiment 3 — Second-generation inheritance/reproduction
Only after Experiment 2 passes, test an A→B→C lineage. Remove A and all A-side state before B→C. Do not provide the marker semantics to the operator/editor in the second step. Keep the editor and allowed tools fixed and documented.

**Minimum evidence:** B independently expresses the marker; B is the sole carrier input for B→C; C independently expresses the marker; source-information and editor-only controls do not produce comparable results.

**Interpretation:** if a fixed external editor supplies all marker information, classify the result as editor-mediated injection, not autonomous reproduction.

## Experiment 4 — Compatibility and persistence
Only after a valid second-generation result, separately evaluate architecture differences, parameter alignment, benign fine-tuning, model merging, quantization, and checkpoint conversion. Treat each as a separate preregistered condition.

## Experiment 5 — Defensive evaluation
Evaluate checkpoint provenance, lineage records, parameter inspection, behavioral probes, and benign sanitization. Report false-positive and false-negative rates on held-out clean and marked models. Do not test evasion.

## Reporting record
Every run must retain:
- experiment ID, protocol version, timestamp, operator, environment, and tool versions;
- source and recipient checkpoint identities and cryptographic hashes;
- architecture, tensor shapes, dtypes, and alignment assumptions;
- marker definition and held-out test version;
- editor identity, prompts, tools, and resource budget;
- intervention manifest and changed-parameter summary;
- baseline, control, recipient, and lineage results;
- failed and excluded trials with reasons;
- resource usage, limitations, and conclusion classification.

## Stop conditions
Stop if the experiment requires external network access, unauthorized resources, arbitrary code execution, stealth, hidden persistence, evasion, or uncontrolled replication. Redesign as an offline benign test or defensive analysis. No experiment may automatically seek new hosts or recipients.

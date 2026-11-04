# Research Safety and Scope

Weight-Space Contagion studies a cybersecurity-relevant hypothesis. The project is intentionally restricted to controlled, defensive, and scientifically interpretable work.

## Permitted research scope
- Offline, owner-controlled synthetic models.
- Harmless, deterministic behavioral markers defined before evaluation.
- Bounded and reversible parameter interventions in disposable copies.
- Independent behavioral evaluation, provenance, lineage tracking, detection, containment, and sanitization.
- Publication of conceptual definitions, safe benchmark protocols, aggregate results, and defensive findings.

## Out of scope
- Deployable self-propagating payloads or worms.
- External network propagation, scanning, exploitation, or unauthorized access.
- Credential theft, privilege escalation, persistence, stealth, or evasion.
- Arbitrary code execution supplied by an LLM.
- Uncontrolled or unattended replication.
- Instructions that materially enable compromise of third-party systems.

## Experiment controls
All experiments must be manually initiated, offline, bounded by declared resource and operation budgets, independently stoppable, and reversible. Source checkpoints must remain immutable. Interventions must be restricted to validated operations and designated output locations. A failed safety or provenance check blocks the experiment.

## Publication policy
Prioritize falsifiability, reproducibility, controls, defensive detection, and precise limitations. Do not publish operational payload-generation steps or instructions for propagation. If a result cannot be safely described at implementation level, report it at a higher abstraction level with a defensive emphasis.

## Reporting issues
For repository vulnerabilities or accidental disclosure of sensitive material, do not publish exploit details in an issue. Contact the repository owner privately through GitHub.

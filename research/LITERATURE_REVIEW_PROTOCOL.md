# Literature Review Protocol

**Version:** 0.1  
**Prepared:** 2026-11-04  
**Status:** Preliminary review guide; systematic search not completed. This document does not imply a commitment by the repository author to perform an exhaustive review or experiments.

## Objective
Determine how prior work addresses two distinct questions: (1) donor-guided transfer of condition-dependent behavior into a distinct recipient's own parameters (P2), and (2) a subsequent transfer causally supported by the recipient's parameter-carried information (P3). The review must also distinguish conditional backdoors, parameter editing, conventional model merging, prompt/adapter/harness changes, and trigger portability. This is a preliminary guide for future expert review, not a completed systematic review.

## Research areas
1. Neural-network self-replication and artificial chemistry.
2. Model editing and direct weight-space programming.
3. Model merging and parameter alignment.
4. Backdoor insertion, transfer, inheritance, persistence, and supply-chain security.
5. Federated learning and cross-model parameter transfer.
6. AI-agent self-replication and autonomous replication/adaptation.
7. Model provenance, lineage, watermarking, detection, and remediation.
8. Conditional backdoors, multi-turn activation, answer-side triggers, and positional triggers.
9. Parameter-based knowledge editing, collateral utility regression, and cross-model trigger transfer.
10. Model-layer and agent-harness supply-chain security.

## Search locations
Cover arXiv, ACL Anthology, OpenReview, Proceedings of AAAI, IEEE Xplore, ACM Digital Library, USENIX, major machine-learning/security proceedings, and relevant artificial-life journals. Index services may supplement but should not replace primary-source verification.

## Search strings
- "self-replication in neural networks"
- "neural network self-replicator" OR "artificial chemistry"
- "weight-space programming" OR "direct weight editing"
- "model merging" AND (backdoor OR trojan OR inheritance)
- "parameter-space transfer" OR "behavioral inheritance"
- "weight-based replicator" OR "AI self-replication"
- (backdoor OR trojan) AND (model lineage OR generational OR propagation)
- "autonomous replication and adaptation" AND model
- "conditional backdoor" AND (model editing OR model merging OR parameter transfer)
- "answer-side backdoor" OR "positional backdoor" OR "task-conditioned backdoor"
- "parameter-based knowledge editing" AND (capability OR interference OR collateral)
- "model layer" AND "agent harness" AND backdoor

## Inclusion criteria
Include primary research that directly addresses neural-network self-replication, model-parameter manipulation or transfer, learned behavior inherited by another model, persistence across model transformations, or agent-level replication where the distinction from parameter-space transfer is analytically relevant.

## Exclusion criteria
Exclude sources that merely use biological-virus metaphors without a neural/model mechanism, generic computer-virus epidemiology without a model-level connection, and secondary summaries where the primary paper is available. Keep secondary sources only as leads.

## Screening and extraction
For each candidate source, record: full citation; publication type/status; model family and architecture; what is transferred (files, weights, behavior, prompts, code, state, or infrastructure); whether recipient parameters change; whether the recipient is independently evaluated; whether a second-generation transfer is tested; whether the original source is absent; what external editor or operator information is available; controls; limitations; and relevance to P0–P4 claim levels.

Trace references backward from the closest work and forward through citing papers. Deduplicate preprint and published versions while preserving version history.

## Novelty decision rule
Do not claim novelty merely because a search for the exact phrase “weight-space contagion” returns few results. Treat any paper demonstrating the same operational mechanism under different terminology as prior art. If an existing work already demonstrates P2 or P3 under equivalent criteria, revise the contribution accordingly. Make no priority claim until the full screening is documented.

## Current status
This protocol is a review aid and has not been executed systematically. The preliminary related-work map is exploratory and must not be described as a systematic review. The repository author is not undertaking experiments; this document does not constitute an experimental commitment.

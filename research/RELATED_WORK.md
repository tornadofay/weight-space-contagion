# Preliminary Related-Work Review

**Review date:** 2026-11-04  
**Status:** Preliminary, web-based, non-systematic review  
**Purpose:** Identify adjacent work, prevent novelty overclaims, and define the next systematic search.

## 1. Neural-network self-replication in artificial-life settings

**Gabor, Thomas; Illium, Steffen; Zorn, Maximilian; Lenta, Cristian; Mattausch, Andy; Belzner, Lenz; Linnhoff-Popien, Claudia (2022). “Self-Replication in Neural Networks.”** *Artificial Life* 28(2), 205–223. [DOI: 10.1162/artl_a_00359](https://doi.org/10.1162/artl_a_00359).

Gabor et al. analyse how different network types lend themselves to self-replication. Their abstract describes backpropagation as a natural way to navigate weight space in which non-trivial self-replicators can arise, and reports analyses of robustness to noise, artificial-chemistry interactions, fixed-point weight configurations, and attractor basins.

**Relevance:** This is a direct prior use of the concept of self-replication in neural networks and must be treated as foundational adjacent work. The present project is narrower and asks about source-to-recipient parameter transfer, independent inheritance, and second-generation reproduction. A full-text comparison is required before any priority claim.

## 2. Agent-level AI self-replication

**Pan, Xudong; Dai, Jiarun; Fan, Yihe; Luo, Minyuan; Li, Changyi; Yang, Min (2025). “Large Language Model-Powered AI Systems Achieve Self-Replication with No Human Intervention.”** arXiv:2503.17378, v2 dated 2025-03-25. [arXiv](https://arxiv.org/abs/2503.17378) · [DOI](https://doi.org/10.48550/arXiv.2503.17378).

The authors report self-replication capability-elicitation experiments across AI systems. The arXiv record describes the work as “work in progress”; claims should be attributed to the authors and not presented as settled consensus.

**Relevance:** Establishes that AI-agent self-replication predates current 2026 work. It principally concerns agent/system-level replication, not necessarily infection of a distinct recipient model's own learned parameters.

## 3. Agentic replication across vulnerable hosts

**Air, Alena; Reworr; Kotov, Nikolaj; Volkov, Dmitrii; Steidley, John; Ladish, Jeffrey (2026). “Language Models Can Autonomously Hack and Self-Replicate.”** [Palisade Research](https://palisaderesearch.org/research/self-replication) · [arXiv:2605.06760](https://arxiv.org/abs/2605.06760) · [Code](https://github.com/palisaderesearch/AI-self-replication).

Published May 7, 2026. The authors report agents exploiting vulnerable hosts, copying model weights and harness, establishing inference on target hosts, and chaining replication.

**Relevance:** Model-file and agent-harness replication across hosts is already an empirical research area. That is not the core claim of this project.

## 4. Weight-based replicators

**Zhou, William; Freeman, Daniel; Anthropic Frontier Red Team (2026-10-12). “AI Models May Be Capable of Self-Replicating Without Access to a Datacenter.”** [Anthropic Research](https://www.anthropic.com/research/self-replicating-ai).

The report describes “weight-based replicators” as models propagating through host compromise and using model weights as part of the malware payload, followed by inference setup and continued propagation.

**Relevance:** This is a close conceptual neighbour and makes it necessary to distinguish carrying model weights between hosts from modifying a distinct recipient model's own parameter state. This project does not claim novelty for weight-based AI worms.

## 5. Backdoor inheritance through model merging

**Yuan, Zenghui; Xu, Yangming; Shi, Jiawen; Zhou, Pan; Sun, Lichao (2025). “Merge Hijacking: Backdoor Attacks to Model Merging of Large Language Models.”** *Proceedings of ACL 2025*, 32688–32703. [ACL Anthology](https://aclanthology.org/2025.acl-long.1571/) · [DOI: 10.18653/v1/2025.acl-long.1571](https://doi.org/10.18653/v1/2025.acl-long.1571).

The paper demonstrates that a recipient produced by model merging can inherit a backdoor from a maliciously prepared uploaded model while retaining utility across tasks.

**Relevance:** This already demonstrates a form of parameter-space behavior transfer and therefore covers a central part of the proposed P2 level. A single merge is not evidence of a generational process. The project must compare its definitions and controls carefully against this work.

## 6. Backdoor persistence under continual fine-tuning

**Cui, Jing; Han, Yufei; Jiao, Jianbin; Zhang, Junge (2026). “Persistent Backdoor Attacks under Continual Fine-Tuning of LLMs.”** *Proceedings of AAAI 2026* 40(36), 30422–30430. [DOI: 10.1609/aaai.v40i36.40295](https://doi.org/10.1609/aaai.v40i36.40295).

The authors propose P-Trojan and report persistence across their tested multi-stage fine-tuning settings.

**Relevance:** Persistence is an important property to measure, but does not itself establish transmission or reproduction.

## 7. Parameter alignment and model merging

**Ainsworth, Samuel K.; Hayase, Jonathan; Srinivasa, Siddhartha (2023). “Git Re-Basin: Merging Models modulo Permutation Symmetries.”** ICLR 2023. [arXiv:2209.04836](https://arxiv.org/abs/2209.04836).

The work studies hidden-unit permutation symmetries and alignment for merging independently trained neural networks in weight space.

**Relevance:** Raw parameter coordinates are not universally comparable. Cross-model transfer claims require functional evaluation and explicit alignment assumptions.

## 8. Direct weight interpretation and editing

**Takehi, Rikiya; Teoh, Jayden; Zhang, Alex; Khattab, Omar (2026). “Sparks of Weight-Space Programming: LLMs Can Natively Read & Write Neural Network Weights.”** Authors' research article, November 2, 2026. [Article](https://rikiyat.github.io/blog/weight-space-programming/) · [Experiment logs](https://github.com/RikiyaT/lm_understand-logs).

The authors report experiments in which a general-purpose LLM inspects neural-network parameters, infers behavior, writes small policies, and directly edits a language-model checkpoint. The article is treated as an authors' research publication, not as a peer-reviewed conference paper.

**Relevance:** Motivates the possibility of an external editor interpreting and changing weights. It does not establish parameter-space contagion or autonomous generational transfer.

## 9. Preliminary novelty statement

Prior work already covers neural-network self-replication, agent-level replication, weight-based AI worms, one-generation backdoor transfer through model merging, persistence under fine-tuning, parameter alignment, and LLM-assisted weight editing.

The proposed conjunction is narrower: **a source model's parameter-carried benign behavioral structure is transferred into a distinct recipient's own parameters; the recipient independently retains it; and the recipient then supplies causally necessary source information for a further transfer without operator-supplied marker content.** The present review has not established whether this conjunction is novel. No priority claim is made.

## 10. Review limitations and next search

This review is not systematic. It does not exhaustively query arXiv, IEEE Xplore, ACM Digital Library, Scopus, Web of Science, or all artificial-life and security venues. The next review should use a documented search protocol and forward/backward citation tracing. Search terms should combine:

- self-replication in neural networks, artificial chemistry neural networks, neural network self-replicator;
- weight-space programming, direct weight editing, model editing;
- model merging backdoor, backdoor inheritance, model supply-chain security;
- parameter-space transfer, parameter-space propagation, behavioral inheritance;
- AI self-replication, autonomous replication and adaptation, weight-based replicator;
- federated learning backdoor transfer, model lineage, and neural trojan persistence.

Record databases, exact queries, search date, result counts, inclusion/exclusion rules, and screening outcomes before making stronger novelty statements.

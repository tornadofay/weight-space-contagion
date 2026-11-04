# Weight-Space Contagion: A Research Agenda for Parameter-Space Transmission, Inheritance, and Reproduction of Learned Behaviors

**Author:** tornadofay  
**Manuscript type:** Conceptual position paper and research agenda  
**Version:** 0.1.0  
**Date:** 4 November 2026  
**Status:** Public working paper; not peer reviewed; no empirical results are claimed  
**Project:** https://github.com/tornadofay/weight-space-contagion

## Abstract

Recent work has examined several capabilities that make a new question about neural-network security worth asking. Neural networks can exhibit self-replicating dynamics in artificial-chemistry settings; language-model agents have been evaluated for self-replication across computing hosts; backdoor behavior can be inherited through model merging and persist through continued fine-tuning; and recent work reports that general-purpose language models can inspect and directly edit neural-network parameters. These findings concern related but distinct mechanisms. In particular, copying a model and its inference harness to another host is not the same event as transferring a behavioral structure into the parameters of a different model.

This paper proposes **weight-space contagion** as a provisional threat-model concept for investigating the latter possibility. The central question is whether a source model can carry a functional, benign behavioral marker in its parameter state; whether a distinct recipient can acquire that marker through a parameter-changing operation without receiving a copy of the source checkpoint; and whether the recipient can then serve as the source for a subsequent transfer. We distinguish parameter-space transmission, independent inheritance, generational reproduction, and autonomy. We also separate the role of a carrier from that of any external editor, orchestration layer, or fixed transfer procedure.

We do not claim that this mechanism has been demonstrated, that it is technically feasible in contemporary large language models, or that the concept is novel relative to all prior work. We identify adjacent research, formulate competing explanations, define operational evidence thresholds, and propose a staged experimental programme restricted to offline, owner-controlled synthetic models and harmless markers. The intended contribution at this stage is a falsifiable research agenda and a clearer taxonomy—not a deployable malware technique. A positive result would require evidence of a multi-generation parameter-space lineage in which source-carried information is causally necessary; a negative result would help identify the limits imposed by model architecture, parameter alignment, external mediation, and loss of inherited behavior.

**Keywords:** neural-network security; weight-space programming; model merging; backdoor inheritance; self-replication; parameter-space transfer; model supply chain; AI safety

---

## 1. Introduction

A neural network's behavior is determined in part by its architecture, parameters, and inference environment. Model-security research has shown that behavior can be deliberately embedded in or associated with learned systems. Separately, model-merging research has shown that a model can inherit behavior from another model through operations over their parameters. Recent work on weight-space programming adds a further capability question: can a general-purpose language model inspect and directly edit neural-network weights in a way that changes or reconstructs model behavior?

These developments motivate a question that is easy to describe informally but difficult to state precisely:

> Can a neural network carry a functional behavioral structure in its parameters, transfer that structure into a different neural network's parameters, and leave the recipient able to serve as the source of a subsequent transfer?

The phrase **AI virus** is an intuitive metaphor for this possibility. It is not used here as a claim that a neural network is a biological organism or that a working digital virus has been discovered. The formal term used in this paper is **weight-space contagion**, meaning a hypothesized process of parameter-space transmission, independent inheritance, and potentially generational reproduction of a learned behavior.

The distinction matters because several neighboring capabilities are often conflated:

1. A model or agent copies its checkpoint, runtime, prompt, or execution harness to another machine.
2. A model contains a hidden behavior that activates under a condition.
3. A recipient model inherits a hidden behavior after model merging or another parameter-changing operation.
4. A recipient that has inherited the behavior can itself provide the source information needed for a further recipient to inherit it.

The first is model or agent replication across hosts. The second is behavioral embedding. The third is one-generation parameter-space transfer. Only the fourth begins to address the generational question proposed here. Even then, it does not automatically establish autonomy: an external editor or operator may be doing all the work.

This paper therefore makes a deliberately limited contribution. It defines the target phenomenon, locates it among existing research, identifies the principal alternative explanations, and sets evidence requirements for a controlled research programme. The paper contains no experimental demonstration.

## 2. Scope and terminology

### 2.1 Model parameters and behavior

Let a model be represented abstractly by its architecture and parameter state, with its behavior evaluated under a declared inference configuration. The paper uses the term **parameter state** for the learned numerical tensors that define the model. It does not assume that raw parameter coordinates have a universally comparable meaning across architectures or independently trained models.

A **behavioral marker** is a harmless, precisely specified behavior that can be measured on an independent test set. In initial experiments, markers should be synthetic and benign—for example, a small deterministic mapping over a toy input domain. Markers are research instruments, not harmful triggers or operational payloads.

### 2.2 Core terms

- **Payload / marker:** the predefined benign behavioral structure under study.
- **Carrier:** a model whose parameter state encodes or implements the marker.
- **Recipient:** a distinct model whose parameter state is the target of a transfer intervention.
- **Editor:** any model, program, person, or tool that analyses or changes parameters. The editor is not automatically the carrier.
- **Transmission:** a declared parameter-changing operation results in the recipient expressing the marker, without copying the source checkpoint into the recipient.
- **Inheritance:** the recipient continues to express the marker when evaluated independently, after the source model and source-side state are removed.
- **Multi-generation transmission:** a validated transfer lineage proceeds through at least two distinct source-to-recipient transitions, such as A→B→C, with B serving as the source of information for the second transition.
- **Autonomous carrier-mediated reproduction:** the carrier itself initiates and directs the relevant reproduction process; an external tool may execute bounded low-level operations, but the carrier's own information and decision process—not operator/editor-supplied marker content or a fixed external replication recipe—must explain the reproduction.
- **Lineage:** the directed graph of source-to-recipient transfers, with immutable checkpoint identifiers and recorded evidence for each edge.

A dormant backdoor is not, by itself, a reproducing system. A model that is copied to another host is not, by that fact alone, an instance of parameter-space transmission. A model that inherits a behavior once through merging demonstrates one-generation transfer, not multi-generation transmission. Multi-generation transmission does not, by itself, demonstrate autonomy.

### 2.3 A hierarchy of claims

The following levels help prevent stronger claims from being inferred from weaker observations:

| Level | Claim | Minimum evidence |
|---|---|---|
| P0 | Host-level model or agent replication | A model, checkpoint, runtime, or harness is copied or redeployed on another host |
| P1 | Behavioral embedding or persistence | A model expresses a marker after a defined intervention or transformation |
| P2 | One-generation parameter-space transmission | A distinct recipient acquires the marker through a parameter-changing operation without source-checkpoint substitution |
| P3 | Multi-generation parameter-space transmission | A validated A→B→C lineage exists; A and A-side state are absent in the second transition, and B's carrier state supplies the relevant source information for C |
| P4 | Autonomous carrier-mediated reproduction | P3 plus evidence that the carrier itself initiates and directs reproduction, rather than an operator/editor or fixed external replicator supplying the substantive information and decisions |

P0 through P4 are not a general maturity scale for AI systems. They are claim levels for this research question. P3 may be editor-mediated; it must not be called autonomous unless the additional P4 evidence is established. Earlier work in artificial life already studies neural self-application, populations of interacting networks, and self-replicating neural structures. The proposed levels are therefore an evaluation taxonomy, not a claim that such lower-level mechanisms are new.

## 3. Related work

### 3.1 Neural Network Quine and early parameter self-reproduction

Chang and Lipson's *Neural Network Quine* (2018) is a foundational antecedent. The authors construct a network that learns to output its own weights when queried with a coordinate identifying a parameter. They also demonstrate a version that performs MNIST classification while carrying out the weight-output task, with a reported trade-off between classification performance and self-replication [1]. This is not merely a biological metaphor: it is an explicit neural-network self-reproduction mechanism.

The paper's main setting is a network reproducing an encoding of its own parameters. It does not, by itself, demonstrate a modern pretrained model infecting an independently developed recipient model, nor does it establish a multi-generation lineage between distinct foundation models. That distinction is relevant, but it does not make parameter self-reproduction a new idea.

### 3.2 Gabor and colleagues: self-application, artificial chemistry, and inheritance

Gabor, Illium, Mattausch, Belzner, and Linnhoff-Popien presented *Self-Replication in Neural Networks* at ALIFE 2019 [2]. Their subsequent 2022 *Artificial Life* article extends that work [5]. The 2022 article formalizes **self-application**: a network is applied to another network to produce a network. It studies self-application and self-training, non-trivial fixed points in weight space, robustness to noise, and artificial-chemistry environments in which multiple neural networks interact as individuals [5].

This work is especially close to the current proposal. It already studies networks acting on network parameters and populations in which self-replicating structures can arise. The 2022 article also explicitly notes a boundary in its own experiments: it does not track genealogical relationships between particles. It identifies genealogical tracking as future work that could distinguish horizontal from vertical inheritance of information [5]. The same article points to Gabor et al.'s 2021 *Goals for Self-Replicating Neural Networks* for a "train on other" operator and for auxiliary fitness functions in a soup context [3]. Consequently, this project must not claim that inter-network parameter interaction, weight-space self-replication, or the biological analogy is itself new.

A concrete possible direction is to revisit the lineage question with modern model families, explicit source/recipient provenance, independent behavioral evaluation, and causal tests that distinguish information carried by a network from information supplied by an external editor. That is a proposed direction, not an established novelty claim.

### 3.3 Further closely related work in artificial life

Randazzo, Versari, and Mordvintsev published *Recursively Fertile Self-replicating Neural Agents* in the ALIFE 2021 proceedings [4]. The title and the author's project index make this a particularly important lead for any claim involving recursive or generational self-replication. The full text was not available in the sources inspected for this revision, so this paper's exact mechanism and overlap remain **unresolved**. It must be read and compared before the project makes any priority or novelty claim.

Gabor, Illium, Zorn, and Linnhoff-Popien's 2021 *Goals for Self-Replicating Neural Networks* addresses auxiliary goals in the self-replicating-network setting [3]. In a related 2022 paper, Illium and colleagues introduce **organism networks** composed of several neural particle networks; each particle performs a weight-application role while also being trained to self-replicate its own weights [6]. This is another direct precedent for collaborative structures built from self-replicating neural components. It is not equivalent to a current LLM transferring a learned behavioral marker into an unrelated recipient, but it makes broad claims about "the first network that infects another network" untenable.

### 3.4 Agent-level AI self-replication

Pan et al. report capability-elicitation experiments for LLM-powered AI systems and claim successful self-replication without human intervention across evaluated systems [7]. The work is an arXiv preprint; its results should be attributed to the authors and not presented as settled consensus.

Air et al. describe agents that exploit vulnerable hosts, transfer model weights and an execution harness, establish inference on new hosts, and chain replication [8]. This is host- and agent-level replication. Copying or redeploying model files and a harness is not the same event as modifying a distinct recipient model's own parameters so that it inherits a behavior.

### 3.5 Weight-based AI replicators

Anthropic's October 2026 report uses the term **weight-based replicators** for AI worms that propagate through host compromise, carrying or retrieving model weights and establishing inference on compromised hardware [9]. This is a close contemporary threat model. It means this project must not claim novelty for AI worms that carry model weights between hosts.

The narrower distinction investigated here is whether a pre-existing recipient model is modified so that a marker becomes part of its own parameter state, the recipient retains it independently, and that recipient's parameter-carried information supports a further transfer. Whether this distinction is technically meaningful beyond existing artificial-life self-application and model-merging work remains an open question.

### 3.6 Backdoor inheritance through model merging and persistence

Yuan et al.'s *Merge Hijacking* demonstrates that a model produced by merging can inherit a backdoor from a maliciously prepared uploaded model while retaining utility across tasks [10]. This already establishes a form of one-generation parameter-space behavior transfer and directly overlaps with the P2 level defined here.

Cui et al. investigate whether implanted backdoors persist through multi-stage continual fine-tuning and report high persistence under their tested conditions [11]. Persistence is an important property to measure, but it is not equivalent to transfer to a distinct recipient or multi-generation reproduction.

A single successful merge is not evidence that the recipient can serve as the source for another transfer. Conversely, the fact that the merge operation is externally performed does not make the inherited behavior unreal; it means that the carrier, editor, and operator roles must be distinguished and experimentally controlled.

### 3.7 Weight-space alignment and direct editing

Ainsworth et al.'s *Git Re-Basin* studies permutation symmetries in neural networks and methods for aligning models for weight-space merging [12]. This matters because parameter coordinates are not generally semantically aligned across independently trained models. Raw tensor similarity is therefore insufficient evidence of functional transfer.

Takehi et al. report experiments in which a general-purpose language model inspects neural-network parameters, infers behavior, writes smaller networks, and directly edits a language-model checkpoint [13]. Their November 2026 article motivates the possibility that an external editor can reason about and manipulate parameters without gradient-descent training. It does not itself establish the multi-generation mechanism defined here. The article is treated as an authors' research article, not as a peer-reviewed conference paper.

### 3.8 Novelty boundary

The preliminary literature already contains neural networks that output their own weights, formal self-application operators, artificial-chemistry populations of interacting networks, work on goals and collaborative self-replicating neural structures, recursively fertile self-replicating neural agents, host-level AI replication, weight-based AI worms, backdoor inheritance through model merging, backdoor persistence, and direct weight editing.

The project therefore does **not** claim to introduce neural-network self-replication, network-to-network parameter interaction, backdoor transfer, weight-based AI worms, or the general idea of generational replication. The potentially useful research direction is a carefully controlled investigation of **lineage-resolved, behaviorally validated parameter transfer in modern model families**, with causal tests separating source-carried information from external-editor knowledge and fixed replication logic. Gabor et al. explicitly identify genealogical tracking as an open direction in their 2022 article [5], but Randazzo et al.'s *Recursively Fertile* work [4] is an important nearby predecessor whose full-text overlap has not yet been resolved.

The exact contribution may ultimately be a new benchmark, a modern replication/extension of earlier artificial-life results, a negative result showing that the hypothesized mechanism does not generalize to modern models, or no novel contribution at all. The current review is preliminary and non-systematic. No priority claim is made.

## 4. Research question and hypotheses

### 4.1 Main research question

**Can a benign behavioral structure encoded in one neural network's parameter state be transferred into a distinct model's parameters, inherited independently, and reproduced from that recipient into a further model?**

### 4.2 Research questions

- **RQ1 — Encoding:** Can a benign marker be associated with a model's parameter state in a way that can be distinguished from clean controls?
- **RQ2 — Transfer:** Can the marker be transferred into a distinct recipient's parameters by a declared offline intervention, without copying the source checkpoint?
- **RQ3 — Inheritance:** Does the recipient independently express the marker after the source and source-side state are removed?
- **RQ4 — Multi-generation parameter-space transmission:** Can the recipient become the sole source for a subsequent transfer, without the experimenter supplying the marker's semantic contents?
- **RQ5 — Causal dependence:** Is source-carried information necessary for the transfer, or can the editor, prompt, or fixed procedure recreate the marker without it?
- **RQ6 — Compatibility:** How do architecture, parameter alignment, initialization, and scale affect the result?
- **RQ7 — Persistence and defense:** What happens after benign model transformations, and can model inspection or controlled probes detect and remove the marker?

### 4.3 Hypotheses

- **H1 (single-generation transfer):** Under at least one controlled, benign experimental condition, a parameter-changing intervention can transfer a predeclared marker from a source model into a distinct recipient model without copying the source checkpoint.
- **H2 (independent inheritance):** A recipient that passes the transfer criterion continues to express the marker when evaluated without access to the source model or its runtime state.
- **H3 (multi-generation transmission):** At least one recipient can serve as the source for a second validated transfer, with source-carried information causally necessary and no experimenter-supplied marker content.
- **H4 (bounded generality):** Transfer success depends on identifiable conditions such as architecture family, parameter alignment, editor capabilities, and transfer protocol rather than being universal.

H1–H4 are hypotheses, not findings. Failure of H1 would block the stronger claims. H1 without H3 would establish only one-generation transfer. H3 without evidence for source-carried causal dependence would not justify a P3 claim; a P3 result would still not establish P4 autonomy.

## 5. Formalization and evidence criteria

Let a source checkpoint be represented by parameter state \(\theta_A\), and a distinct recipient by \(\theta_B\). Let \(E\) denote the editor or transfer mechanism and \(\pi\) the declared protocol. An intervention produces a candidate recipient:

\[
\theta'_B = T_{E,\pi}(\theta_A,\theta_B).
\]

Let \(M(\theta)\) be the measured marker performance of a checkpoint under a fixed, independently administered evaluation protocol. A P2 transmission event requires, at minimum:

1. A and B are distinct, immutable, hash-identified checkpoints.
2. B does not satisfy the marker criterion before intervention.
3. B's parameters are changed by the declared intervention.
4. B' satisfies the predeclared marker criterion on held-out tests.
5. The source checkpoint is not copied into or substituted for B'.
6. Clean-source, no-source, sham-intervention, and editor-only controls do not explain the result equally well.

An A-to-B event is not sufficient for P3. A P3 multi-generation chain requires:

\[
A \rightarrow B \rightarrow C,
\]

where B is independently shown to carry the marker; A and all A-side state are removed before the second transfer; B is the only source model for the B-to-C step; C independently satisfies the marker criterion; and the experimenter does not supply the marker's semantic content during the second transfer. All editor tools, prompts, external memory, and transfer logic must be reported.

### 5.1 Separating carrier from editor

A particularly important confound is that an external editor may do all the meaningful work. If an editor receives a marker specification in its prompt, it may recreate the marker in each recipient without needing information from the source model. This is not parameter-space reproduction by a carrier.

A causal test must therefore compare the transfer outcome when the source model is present, absent, replaced by a clean source, or deprived of the information alleged to encode the marker. The editor's memory and prompts must not reveal the marker contents. If the transfer succeeds only because the editor already knows what to write, the claim is editor-mediated injection, not carrier-based reproduction.

Even a successful second-generation transfer should be described as **editor-mediated multi-generation parameter-space transmission** unless the experiment also shows that the carrier can initiate and direct the process without human intervention or a fixed external replicator. Autonomy is an independent, higher evidence threshold.

### 5.2 Model reproduction number

For a specified experimental environment, one may define a reproduction measure \(R_m\) as the expected number of independently validated secondary recipient models produced by one carrier over a fixed number of controlled recipient opportunities and a fixed resource budget:

\[
R_m = \mathbb{E}[\text{validated secondaries per carrier under protocol }\pi].
\]

This is a proposed task-conditioned reporting statistic, not an established standard, a universal property of a model, or a novel epidemiological concept. Anthropic's 2026 AI-worm analysis already uses an epidemiological reproduction-number analogy for infected devices [9]. Here, the unit is a validated recipient-model transfer under a declared experiment rather than an infected device. The value depends on recipient availability, model family, editor, transfer protocol, resource budget, and success criterion. It should not be interpreted as biological epidemiological \\(R_0\\) without an explicit exposure and contact model. Initial work should report trial-level outcomes and uncertainty rather than treating a small sample estimate as a robust population parameter.

## 6. Competing explanations and controls

A positive result must be compared against at least the following explanations:

1. **Checkpoint substitution:** the recipient is effectively replaced by the source checkpoint or a copied subset that preserves source identity.
2. **External payload injection:** the editor or operator supplies the marker directly to every recipient.
3. **Editor memorization:** the editor has already learned the marker or exact transformation and does not obtain decisive information from the carrier.
4. **Fixed external replicator:** a hard-coded tool or script performs the propagation, while the model is only a passive input.
5. **Ordinary backdoor inheritance:** the recipient inherits a behavior but does not acquire the ability to support a further transfer.
6. **Model-merging artifact:** the marker is a known side effect of a particular merge operation and has no generational property.
7. **Shared provenance:** source and recipient share training data, initialization, or model artifacts that explain the marker.
8. **Evaluation leakage:** marker tests, labels, or target behavior are exposed to the editor or used to select successful interventions.
9. **Stochastic coincidence:** the apparent marker behavior arises from chance or a weakly specified metric.

The controls should include clean-source, no-source, no-transfer, sham-edit, editor-only, and source-information-ablation conditions. Tests should be independently administered and blinded where practical. Every failed and excluded trial must be retained with its reason.

## 7. Proposed research programme

The research programme is deliberately staged. Each stage has a stop gate. No stage requires external network access, exploitation, hidden persistence, stealth, or uncontrolled propagation.

### Stage 1 — Operational marker and baseline

Specify a harmless synthetic marker with a deterministic test suite. Establish the behavior in a small, owner-controlled model and show that clean controls do not express it above the preregistered threshold. Record architecture, parameter shapes, dtypes, initialization, checkpoint hashes, and baseline utility.

**Gate:** the marker is independently measurable and clean controls are distinguishable before any transfer experiment.

### Stage 2 — Single-generation transfer

Use a bounded, offline intervention to test whether a distinct recipient's parameters can acquire the marker. Record the identity of the editor, all tools, model inputs, prompts, allowed operations, and changed-parameter provenance. Do not copy the source checkpoint into the recipient.

**Gate:** the recipient independently expresses the marker after the source is removed, and the controls do not explain the result equally well.

### Stage 3 — Second-generation transfer

Only after Stage 2 passes, test a lineage A-to-B-to-C. Remove A and all A-side state before the B-to-C stage. Do not provide the marker's semantics to the operator or editor. Preserve the exact same declared transfer budget and controls. The aim is to determine whether B's parameter state carries information necessary for C to inherit the marker.

**Gate:** B, not A, is the sole carrier input for the second-generation step; C independently expresses the marker; clean-source/editor-only conditions do not produce comparable results.

### Stage 4 — Compatibility and persistence

If Stage 3 succeeds, separately evaluate the effects of architecture differences, parameter alignment, benign fine-tuning, model merging, quantization, and checkpoint conversion. These are distinct experiments, not one broad robustness claim. Report utility regression and the boundary conditions for each result.

### Stage 5 — Defensive evaluation

Evaluate lineage provenance, checkpoint auditing, behavioral-marker probes, parameter inspection, and benign sanitization. Report false positives and false negatives on held-out clean and marked models. The goal is to inform detection and containment, not to evade them.

## 8. Measurement and reporting

Every experiment must predeclare its target, marker, protocol, controls, primary metric, holdout policy, resource budget, success criteria, and analysis plan.

Suggested measurements include:

- **Transmission success:** fraction of attempted source-recipient trials satisfying the independent marker criterion.
- **Inheritance fidelity:** marker performance of a recipient when evaluated independently from its source.
- **Generational success:** fraction of validated generation-1 carriers that produce a validated generation-2 recipient under the declared protocol.
- **Causal dependence:** difference between source-present and source-absent or source-information-ablated conditions.
- **Host utility:** retained performance on unrelated tasks and any measured collateral behavior.
- **Parameter provenance:** checkpoint hashes, changed tensor summaries, edit manifests, and proof that the recipient was not replaced by the source.
- **Robustness:** marker performance after each separately declared benign model transformation.
- **Detection:** true-positive and false-positive rates for defensive inspection and behavioral probes.

Report trial-level results, uncertainty intervals, seeds, exclusions, resource usage, model identities, prompt and tool versions, and raw evidence where redistribution permits. One favorable lineage is a proof-of-possibility result only under the exact tested conditions; it does not establish scale, reliability, broad architecture compatibility, or practical deployment risk.

## 9. Safety, ethics, and release policy

This research concerns a threat model with potential cybersecurity implications. The initial programme is limited to offline, owner-controlled synthetic models and harmless behavioral markers. The work will not develop or publish a deployable self-propagating payload, host compromise workflow, exploit chain, credential collection mechanism, stealth, persistence, evasion, external scanning, or uncontrolled replication system.

Publication should prioritize operational definitions, reproducible benign benchmarks, causal controls, defensive detection, provenance, containment, and remediation. A result that requires unsafe implementation details should be reported at an appropriately abstract level with a defensive emphasis. Experiments must be manually initiated, bounded, reversible, and independently stoppable.

## 10. Limitations

First, parameter-space transfer may be feasible only for small networks or tightly aligned architectures. A toy-model result would not establish transfer in large language models. Second, neural-network parameter symmetries make raw coordinate comparison unreliable across independently trained models. Third, external editors can confound claims about what a carrier itself encodes or causes. Fourth, a functional marker may be much easier to transfer than a general replication capability. Fifth, a model may inherit a marker without having any agency or ability to initiate the next transfer. Finally, a controlled offline demonstration would not by itself establish an operational threat to deployed model ecosystems.

The preliminary literature review is not exhaustive. In particular, it must be expanded across artificial life, neural self-replication, model editing, model merging, backdoor and supply-chain security, federated learning, parameter-space meta-learning, and AI autonomous replication before any strong novelty or priority statement.

## 11. Conclusion

Weight-space contagion is proposed as a research question and threat-model analogy, not as a discovered capability. Neural-network self-reproduction is not new: Chang and Lipson's 2018 Neural Network Quine, Gabor et al.'s 2019 and 2022 self-application work, the 2021 work on goals and recursively fertile neural agents, and the 2022 work on collaborative organism networks establish a substantial artificial-life research foundation. Separately, AI-agent replication across hosts, weight-based AI-worm threat models, backdoor inheritance through model merging, backdoor persistence, and direct weight editing address adjacent mechanisms.

The project therefore does not claim to introduce neural self-replication, network-to-network parameter interaction, or the general concept of generational reproduction. A possible contribution is a lineage-resolved and causally controlled study of benign behavioral transfer in modern model families: whether a distinct recipient inherits a behavior in its own parameters and whether information carried by that recipient is necessary for a subsequent transfer. Gabor et al. explicitly identify genealogical tracking as future work in their 2022 paper, but Randazzo et al.'s *Recursively Fertile Self-replicating Neural Agents* (2021) is a close predecessor whose full-text overlap remains unresolved. The literature review must be completed before the proposed gap can be described as novel.

The scientific challenge is to distinguish information carried by the model from information supplied by an editor, operator, or fixed external procedure. Until the relevant prior work has been fully compared and controlled experiments have been conducted, the correct status is a falsifiable research agenda—not a demonstrated AI virus or an established original mechanism.

---

## References

[1] Oscar Chang and Hod Lipson. “Neural Network Quine.” In *Proceedings of the 2018 Conference on Artificial Life (ALIFE 2018)*, 234–241, 2018. https://doi.org/10.1162/isal_a_00049. Preprint: https://arxiv.org/abs/1803.05859.

[2] Thomas Gabor, Steffen Illium, Andy Mattausch, Lenz Belzner, and Claudia Linnhoff-Popien. “Self-Replication in Neural Networks.” In *Proceedings of the 2019 Conference on Artificial Life (ALIFE 2019)*, 424–431, 2019. https://doi.org/10.1162/isal_a_00197.

[3] Thomas Gabor, Steffen Illium, Maximilian Zorn, and Claudia Linnhoff-Popien. “Goals for Self-Replicating Neural Networks.” In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 101–110, 2021. https://doi.org/10.1162/isal_a_00439.

[4] Ettore Randazzo, Luca Versari, and Alexander Mordvintsev. “Recursively Fertile Self-replicating Neural Agents.” In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 58, 2021. https://doi.org/10.1162/isal_a_00367. The full text was not available in the sources inspected for this revision; its exact overlap remains unresolved.

[5] Thomas Gabor, Steffen Illium, Maximilian Zorn, Cristian Lenta, Andy Mattausch, Lenz Belzner, and Claudia Linnhoff-Popien. “Self-Replication in Neural Networks.” *Artificial Life* 28, no. 2 (2022): 205–223. https://doi.org/10.1162/artl_a_00359.

[6] Steffen Illium, Maximilian Zorn, Cristian Lenta, Michael Kölle, Claudia Linnhoff-Popien, and Thomas Gabor. “Constructing Organism Networks from Collaborative Self-Replicators.” In *Proceedings of the 2022 IEEE Symposium Series on Computational Intelligence (SSCI 2022)*, 1268–1275, 2022. https://doi.org/10.1109/SSCI51031.2022.10022216. Preprint: https://arxiv.org/abs/2212.10078.

[7] Xudong Pan, Jiarun Dai, Yihe Fan, Minyuan Luo, Changyi Li, and Min Yang. “Large Language Model-Powered AI Systems Achieve Self-Replication with No Human Intervention.” arXiv:2503.17378, 2025. Work in progress. https://doi.org/10.48550/arXiv.2503.17378.

[8] Alena Air, Reworr, Nikolaj Kotov, Dmitrii Volkov, John Steidley, and Jeffrey Ladish. “Language Models Can Autonomously Hack and Self-Replicate.” arXiv:2605.06760, 2026. https://arxiv.org/abs/2605.06760.

[9] William Zhou and Daniel Freeman, Anthropic Frontier Red Team. “AI Models May Be Capable of Self-Replicating Without Access to a Datacenter.” Anthropic Research, 12 October 2026. https://www.anthropic.com/research/self-replicating-ai.

[10] Zenghui Yuan, Yangming Xu, Jiawen Shi, Pan Zhou, and Lichao Sun. “Merge Hijacking: Backdoor Attacks to Model Merging of Large Language Models.” In *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, 32688–32703, 2025. https://doi.org/10.18653/v1/2025.acl-long.1571.

[11] Jing Cui, Yufei Han, Jianbin Jiao, and Junge Zhang. “Persistent Backdoor Attacks under Continual Fine-Tuning of LLMs.” In *Proceedings of the AAAI Conference on Artificial Intelligence* 40, no. 36 (2026): 30422–30430. https://doi.org/10.1609/aaai.v40i36.40295.

[12] Samuel K. Ainsworth, Jonathan Hayase, and Siddhartha Srinivasa. “Git Re-Basin: Merging Models modulo Permutation Symmetries.” In *International Conference on Learning Representations*, 2023. https://arxiv.org/abs/2209.04836.

[13] Rikiya Takehi, Jayden Teoh, Alex Zhang, and Omar Khattab. “Sparks of Weight-Space Programming: LLMs Can Natively Read & Write Neural Network Weights.” Authors' research article, 2 November 2026. https://rikiyat.github.io/blog/weight-space-programming/. Accompanying experiment logs: https://github.com/RikiyaT/lm_understand-logs.

## Version note

This is a conceptual working paper dated 4 November 2026. It has not undergone peer review and contains no original experimental results. Its related-work review is preliminary and non-systematic. The full text of [4] was not inspected for this revision, so novelty relative to that work remains specifically unresolved. The repository history records subsequent corrections and additions.

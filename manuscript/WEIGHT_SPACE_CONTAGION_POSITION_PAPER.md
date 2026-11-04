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
- **Generational reproduction:** an inherited recipient serves as the source of a further validated parameter-space transfer.
- **Autonomy:** reproduction occurs without the operator or external editor supplying the marker's semantic contents or a fixed replication recipe that fully explains the result. Autonomy is a stronger claim than generational reproduction.
- **Lineage:** the directed graph of source-to-recipient transfers, with immutable checkpoint identifiers and recorded evidence for each edge.

A dormant backdoor is not, by itself, a reproducing system. A model that is copied to another host is not, by that fact alone, an instance of parameter-space contagion. A model that inherits a behavior once through merging demonstrates transfer, not generational reproduction.

### 2.3 A hierarchy of claims

The following levels help prevent overstatement:

| Level | Claim | Minimum evidence |
|---|---|---|
| P0 | Checkpoint or agent replication | A model or its files/harness are copied to another host |
| P1 | Behavioral embedding or persistence | A model expresses a marker after a defined intervention or transformation |
| P2 | Parameter-space transmission | A distinct recipient acquires the marker through parameter change without source-checkpoint copying |
| P3 | Generational reproduction | A recipient independently becomes the source of a second validated parameter-space transfer |
| P4 | Autonomous generational reproduction | The carrier's own parameter-encoded information is causally necessary, and operator/editor-supplied content or fixed logic does not explain the transfer |

P0 through P4 are not a single maturity scale for all AI systems. They are a claim taxonomy for this research question. Each level requires its own controls.

## 3. Related work

### 3.1 Self-replication in neural networks

Gabor et al. studied self-replication in neural networks in an artificial-chemistry setting. Their 2022 *Artificial Life* paper analyses how network types lend themselves to self-replication, reports that backpropagation can naturally navigate weight space toward non-trivial self-replicators, and examines robustness to noise and attractor basins around fixed-point weight configurations [1]. This is a direct and important precedent for the phrase *self-replication in neural networks*.

The present proposal asks a different question. It is not primarily about whether a neural network can represent or produce a copy of itself within an artificial chemistry. It asks whether a behavior carried by one model's parameters can be transferred into a distinct recipient model's parameter state, inherited independently, and then transferred onward. The distinction must be tested rather than assumed; Gabor et al.'s work makes a literature review of neural self-replication essential.

### 3.2 Agent-level AI self-replication

Pan et al. describe capability-elicitation experiments for LLM-powered AI systems and claim successful self-replication without human intervention in a range of evaluated systems [2]. Their work is an arXiv preprint and labels itself as work in progress. Palisade Research later reported agents that exploit vulnerable hosts, transfer model weights and an execution harness, establish inference on new hosts, and chain the process across targets [3]. These studies address agent- and infrastructure-level replication.

They are essential adjacent work, but the transfer mechanism differs from the core question here. In host-level replication, the model's weights and execution infrastructure are copied or redeployed. Weight-space contagion, as defined here, requires a different model to acquire a behavior in its own parameter state. The distinction is not about whether weights are involved in both cases; it is about what happens to the recipient model.

### 3.3 Weight-based replicators

Anthropic's October 2026 report explicitly discusses **weight-based replicators**: AI worms that propagate by compromising host machines and using their model weights as part of the malware payload, establishing inference on new hardware, and continuing propagation [4]. The report is an especially close conceptual neighbor because it uses both the language of worms and model weights.

The present proposal must not claim novelty for a model carrying weights between hosts. The narrower proposed distinction is **intra-model parameter-space transmission**: a pre-existing recipient model is modified so that it inherits the marker in its own parameter state, while remaining a distinct recipient rather than being replaced by a copied source checkpoint. Whether this distinction yields a genuinely new mechanism or only reframes existing model-transfer attacks remains an open literature question.

### 3.4 Backdoor inheritance through model merging

Yuan et al.'s *Merge Hijacking* demonstrates that a maliciously prepared model can cause a backdoor to be inherited by a model produced through merging [5]. This is direct evidence that parameter-combination operations can transfer behavior into a recipient model. It therefore covers an important part of the proposed P2 level.

A single successful merge does not establish a generational process. A P3 claim would require the resulting recipient—not the original source model and not a fixed payload supplied by the experimenter—to provide the information that enables a second recipient to inherit the marker. Even that result would need to be distinguished from an external editor simply remembering or re-injecting the same marker.

### 3.5 Persistence under continued fine-tuning

Cui et al. study persistence of implanted backdoors across multiple stages of continual fine-tuning and report high persistence under their tested conditions [6]. This motivates the persistence and robustness measurements in the proposed programme. Persistence is not reproduction: a marker may survive transformations while having no ability to transfer to another model.

### 3.6 Weight-space alignment and direct editing

Ainsworth et al.'s *Git Re-Basin* examines permutation symmetries in neural networks and develops methods to align independently trained models for merging in weight space [7]. This matters because parameter coordinates are not generally semantically aligned across separately trained models. Raw tensor similarity is therefore insufficient evidence of functional transfer.

Takehi et al. report experiments in which a general-purpose language model reads neural-network weights, infers behavior, writes smaller networks, and directly edits a language-model checkpoint [8]. Their November 2026 project publication motivates the possibility that an external editor can reason about model parameters and manipulate them without a gradient-descent training loop. It does not itself demonstrate the multi-generation transmission mechanism proposed here. The article is treated as a research publication by its authors, not as a peer-reviewed conference paper.

### 3.7 Novelty boundary

The reviewed literature already includes neural-network self-replication, agent-level self-replication, weight-carrying AI worms, backdoor transfer through merging, backdoor persistence through fine-tuning, parameter alignment, and direct weight editing. It would be inaccurate to claim that any of these individual ideas is new.

The proposed research question is the conjunction of three requirements: (i) a source-carried behavioral structure is transferred into a distinct recipient's own parameters; (ii) the recipient independently retains that behavior after the source is removed; and (iii) the recipient then provides the source information for a second transfer without the experimenter supplying the marker contents. The preliminary review has not established whether this conjunction is novel. No priority claim is made.

## 4. Research question and hypotheses

### 4.1 Main research question

**Can a benign behavioral structure encoded in one neural network's parameter state be transferred into a distinct model's parameters, inherited independently, and reproduced from that recipient into a further model?**

### 4.2 Research questions

- **RQ1 — Encoding:** Can a benign marker be associated with a model's parameter state in a way that can be distinguished from clean controls?
- **RQ2 — Transfer:** Can the marker be transferred into a distinct recipient's parameters by a declared offline intervention, without copying the source checkpoint?
- **RQ3 — Inheritance:** Does the recipient independently express the marker after the source and source-side state are removed?
- **RQ4 — Generational reproduction:** Can the recipient become the sole source for a subsequent transfer, without the experimenter supplying the marker's semantic contents?
- **RQ5 — Causal dependence:** Is source-carried information necessary for the transfer, or can the editor, prompt, or fixed procedure recreate the marker without it?
- **RQ6 — Compatibility:** How do architecture, parameter alignment, initialization, and scale affect the result?
- **RQ7 — Persistence and defense:** What happens after benign model transformations, and can model inspection or controlled probes detect and remove the marker?

### 4.3 Hypotheses

- **H1 (single-generation transfer):** Under at least one controlled, benign experimental condition, a parameter-changing intervention can transfer a predeclared marker from a source model into a distinct recipient model without copying the source checkpoint.
- **H2 (independent inheritance):** A recipient that passes the transfer criterion continues to express the marker when evaluated without access to the source model or its runtime state.
- **H3 (generational reproduction):** At least one recipient can serve as the source for a second validated transfer, with source-carried information causally necessary and no experimenter-supplied marker content.
- **H4 (bounded generality):** Transfer success depends on identifiable conditions such as architecture family, parameter alignment, editor capabilities, and transfer protocol rather than being universal.

H1–H4 are hypotheses, not findings. Failure of H1 would block the stronger claims. H1 without H3 would establish only one-generation transfer. H3 without evidence for source-carried causal dependence would not justify an autonomy claim.

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

An A-to-B event is not sufficient for P3. A second-generation chain requires:

\[
A \rightarrow B \rightarrow C,
\]

where B is independently shown to carry the marker; A and all A-side state are removed before the second transfer; B is the only source model for the B-to-C step; C independently satisfies the marker criterion; and the experimenter does not supply the marker's semantic content during the second transfer. All editor tools, prompts, external memory, and transfer logic must be reported.

### 5.1 Separating carrier from editor

A particularly important confound is that an external editor may do all the meaningful work. If an editor receives a marker specification in its prompt, it may recreate the marker in each recipient without needing information from the source model. This is not parameter-space reproduction by a carrier.

A causal test must therefore compare the transfer outcome when the source model is present, absent, replaced by a clean source, or deprived of the information alleged to encode the marker. The editor's memory and prompts must not reveal the marker contents. If the transfer succeeds only because the editor already knows what to write, the claim is editor-mediated injection, not carrier-based reproduction.

Even a successful second-generation transfer should be described as **editor-mediated generational transmission** unless the experiment also shows that the carrier can initiate and direct the process without human intervention or a fixed external replicator. Autonomy is an independent, higher evidence threshold.

### 5.2 Model reproduction number

For a specified experimental environment, one may define a reproduction measure \(R_m\) as the expected number of independently validated secondary recipient models produced by one carrier over a fixed number of controlled recipient opportunities and a fixed resource budget:

\[
R_m = \mathbb{E}[\text{validated secondaries per carrier under protocol }\pi].
\]

This is a proposed benchmark statistic, not an established standard and not a universal property of a model. It depends on recipient availability, model family, editor, transfer protocol, resource budget, and the operational success criterion. It should not be interpreted as biological epidemiological \(R_0\) without an explicit exposure and contact model. Initial work should report trial-level outcomes and uncertainty rather than treating a small sample estimate as a robust population parameter.

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

Weight-space contagion is proposed as a precise research question, not as a discovered capability. Existing research already covers self-replicating neural-network structures, autonomous AI-agent replication across hosts, weight-based replicators, backdoor transfer through model merging, backdoor persistence, and direct neural-network weight editing. Those results make the question worth studying, but they also sharply limit what can honestly be claimed as new.

The distinguishing test proposed here is a controlled, multi-generation parameter-space lineage in which a distinct recipient inherits a benign behavioral marker in its own parameters and then supplies the source-carried information for a further recipient. The critical scientific challenge is to show that the carrier—not an editor's prior knowledge, a fixed external script, or copied checkpoint data—causally explains the second transfer. Until such evidence exists, the correct status is a falsifiable research hypothesis and a preliminary research agenda.

---

## References

[1] Thomas Gabor, Steffen Illium, Maximilian Zorn, Cristian Lenta, Andy Mattausch, Lenz Belzner, and Claudia Linnhoff-Popien. “Self-Replication in Neural Networks.” *Artificial Life* 28, no. 2 (2022): 205–223. https://doi.org/10.1162/artl_a_00359.

[2] Xudong Pan, Jiarun Dai, Yihe Fan, Minyuan Luo, Changyi Li, and Min Yang. “Large Language Model-Powered AI Systems Achieve Self-Replication with No Human Intervention.” arXiv:2503.17378, 2025. Work in progress. https://doi.org/10.48550/arXiv.2503.17378.

[3] Alena Air, Reworr, Nikolaj Kotov, Dmitrii Volkov, John Steidley, and Jeffrey Ladish. “Language Models Can Autonomously Hack and Self-Replicate.” arXiv:2605.06760, 2026. https://arxiv.org/abs/2605.06760.

[4] William Zhou and Daniel Freeman, Anthropic Frontier Red Team. “AI Models May Be Capable of Self-Replicating Without Access to a Datacenter.” Anthropic Research, 12 October 2026. https://www.anthropic.com/research/self-replicating-ai.

[5] Zenghui Yuan, Yangming Xu, Jiawen Shi, Pan Zhou, and Lichao Sun. “Merge Hijacking: Backdoor Attacks to Model Merging of Large Language Models.” In *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, 32688–32703, 2025. https://doi.org/10.18653/v1/2025.acl-long.1571.

[6] Jing Cui, Yufei Han, Jianbin Jiao, and Junge Zhang. “Persistent Backdoor Attacks under Continual Fine-Tuning of LLMs.” In *Proceedings of the AAAI Conference on Artificial Intelligence* 40, no. 36 (2026): 30422–30430. https://doi.org/10.1609/aaai.v40i36.40295.

[7] Samuel K. Ainsworth, Jonathan Hayase, and Siddhartha Srinivasa. “Git Re-Basin: Merging Models modulo Permutation Symmetries.” In *International Conference on Learning Representations*, 2023. https://arxiv.org/abs/2209.04836.

[8] Rikiya Takehi, Jayden Teoh, Alex Zhang, and Omar Khattab. “Sparks of Weight-Space Programming: LLMs Can Natively Read & Write Neural Network Weights.” Authors' research article, 2 November 2026. https://rikiyat.github.io/blog/weight-space-programming/. Accompanying experiment logs: https://github.com/RikiyaT/lm_understand-logs.

## Version note

This is a conceptual working paper dated 4 November 2026. It has not undergone peer review. It contains no original experimental results, and its novelty assessment is preliminary. The repository history records subsequent corrections and additions.

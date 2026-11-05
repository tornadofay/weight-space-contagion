# Weight-Space Contagion: A Problem Statement and Threat Model for Conditional Behavior Transfer and Generational Reproduction

**Author:** tornadofay  
**Manuscript type:** Conceptual position paper, problem statement, and threat-model proposal  
**Version:** 0.2.1  
**Date:** 5 November 2026  
**Status:** Public working paper; not peer reviewed; no empirical results are claimed  
**Project:** https://github.com/tornadofay/weight-space-contagion

## Abstract

Recent work on neural-network self-replication, model merging, backdoor persistence, and direct weight editing raises a set of related but distinct security questions. This paper focuses on a concrete hypothetical scenario: a donor model exhibits a condition-dependent behavior; an external editor is asked to use information from that donor to alter a distinct recipient model's base parameters; and the intended result is for the recipient to express the corresponding behavior under a specified task or context while retaining its ordinary functions in other situations. We call this **donor-guided conditional-behavior implantation**. The scenario could be security-relevant when the behavior is unauthorized or harmful, but this paper describes it only at a conceptual level and uses harmless markers as the appropriate basis for any future controlled evaluation.

The general idea of a model inheriting a backdoor through parameter operations is not new. In particular, *Merge Hijacking* demonstrates backdoor inheritance through conventional model merging. The narrower question worth isolating is whether a weight-space editor can use a donor as the source of functional information and produce a bounded parameter modification in a distinct recipient, rather than relying on ordinary model merging, checkpoint substitution, prompts, adapters, external memory, or changes to the execution harness. Whether such transfer is technically possible depends on model compatibility, parameter alignment, the kind of behavior involved, and the capabilities of the editor; arbitrary cross-model transplantation is not assumed.

A single donor-to-recipient implantation is a one-generation parameter-space transfer question. It is not, by itself, generational contagion. The stronger question is whether the recipient can later serve as the source for a further transfer, with its own parameter-carried information causally necessary. We distinguish these levels, as well as conditional activation, capability transfer, policy or refusal changes, task routing, and actions performed by an external agent harness.

The contribution of this repository is a problem formulation, threat-model distinction, preliminary literature synthesis, and questions that may help qualified research teams investigate the topic. The repository author is not conducting experiments, does not claim the infrastructure or team required to do so, and makes no commitment to produce experimental results. No experiment, test result, implementation, or demonstration is reported. Any evaluation outline is conceptual guidance for independent researchers, not a project execution plan. Novelty remains unestablished; this work is intended to be useful to researchers already working in the relevant fields, not to claim priority over them.

**Keywords:** neural-network security; conditional backdoors; weight-space programming; model merging; parameter-space transfer; behavioral inheritance; model supply chain; AI safety

---

## 1. Introduction

A neural network's behavior is determined in part by its architecture, parameters, and inference environment. Model-security research has shown that behavior can be deliberately embedded in or associated with learned systems. Separately, model-merging research has shown that a model can inherit behavior from another model through operations over their parameters. Recent work on weight-space programming adds a further capability question: can a general-purpose language model inspect and directly edit neural-network weights in a way that changes or reconstructs model behavior?

These developments motivate two related but distinct questions. First, can a donor model's condition-dependent behavior be transferred into a distinct recipient's own parameters, where it remains after transfer-time components are removed? Second, can that recipient later serve as the source of a further transfer, with its own parameter-carried information causally necessary?

The first is a one-generation P2 question. The second is the stronger P3 question:

> Can a model carry a functional behavioral structure in its parameters, transfer it into a distinct recipient's parameters, and leave that recipient able to serve as the source of a subsequent transfer?

The phrase **AI virus** is an intuitive metaphor for this possibility. It is not used here as a claim that a neural network is a biological organism or that a working digital virus has been discovered. The formal term used in this paper is **weight-space contagion**, meaning a hypothesized process of parameter-space transmission, independent inheritance, and potentially generational reproduction of a learned behavior.

The distinction matters because several neighboring capabilities are often conflated:

1. A model or agent copies its checkpoint, runtime, prompt, or execution harness to another machine.
2. A model contains a hidden behavior that activates under a condition.
3. A recipient model inherits a hidden behavior after model merging or another parameter-changing operation.
4. A recipient that has inherited the behavior can itself provide the source information needed for a further recipient to inherit it.

The first is model or agent replication across hosts. The second is behavioral embedding. The third is one-generation parameter-space transfer. Only the fourth begins to address the generational question proposed here. Even then, it does not automatically establish autonomy: an external editor or operator may be doing all the work.

This paper therefore makes a deliberately limited contribution. It defines the problem scenario, locates it among existing research, identifies principal alternative explanations, and states questions and evidence distinctions that independent research teams may assess. The author is not proposing to conduct the studies described later in this paper. No experimental demonstration is reported.

## 2. Scope and terminology

### 2.1 Model parameters and behavior

Let a model be represented abstractly by its architecture and parameter state, with its behavior evaluated under a declared inference configuration. The paper uses the term **parameter state** for the learned numerical tensors that define the model. It does not assume that raw parameter coordinates have a universally comparable meaning across architectures or independently trained models.

A **behavioral marker** is a harmless, precisely specified behavior that could be measured independently in a controlled evaluation. Any such evaluation should use synthetic and benign markers—for example, a small deterministic mapping over a toy input domain. Markers are research instruments, not harmful triggers or operational payloads.

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
| P2 | One-generation parameter-space transmission | A distinct recipient acquires the marker in its own base parameters through a parameter-changing operation and expresses it independently after transfer-time components are removed |
| P3 | Multi-generation parameter-space transmission | A validated A→B→C lineage exists; A and A-side state are absent in the second transition, and B's carrier state supplies the relevant source information for C |
| P4 | Autonomous carrier-mediated reproduction | P3 plus evidence that the carrier itself initiates and directs reproduction, rather than an operator/editor or fixed external replicator supplying the substantive information and decisions |

P0 through P4 are not a general maturity scale for AI systems. They are claim levels for this research question. P3 may be editor-mediated; it must not be called autonomous unless the additional P4 evidence is established. Earlier work in artificial life already studies neural self-application, populations of interacting networks, and self-replicating neural structures. The proposed levels are therefore an evaluation taxonomy, not a claim that such lower-level mechanisms are new.

### 2.4 Motivating scenario: donor-guided conditional-behavior implantation

Consider a hypothetical donor model that exhibits a particular behavior only under a certain task, request category, or conversational context. An external editor is given access to that donor and to a distinct recipient model. The editor attempts to use the donor as a source of functional information and encode an equivalent condition-dependent behavior into the recipient's own parameters. The recipient would continue to perform its ordinary tasks in other situations, but produce the implanted behavior when the relevant condition occurs.

This is a **problem scenario**, not a report of a working technique. It does not assume that the donor's parameters can simply be copied into an arbitrary recipient, that the models share an architecture, or that the editor can infer and transplant arbitrary learned behavior. The donor, editor, recipient, conditioning rule, and runtime environment are separate components that must not be conflated.

If the recipient's own parameters retain the behavior after the donor, editor, prompts, adapters, external memory, and other transfer-time state are removed, the single transfer would be a candidate P2 event under the definitions in this paper. It would still not establish P3. The latter would require a separate recipient-to-recipient transfer in which the first recipient is itself the source of the information needed for the next generation.

### 2.5 What the scenario does and does not mean

Several distinct mechanisms can produce superficially similar observations:

- **Capability transfer:** the recipient acquires a task competence it did not previously have.
- **Policy or refusal alteration:** the recipient already has the relevant competence, but a parameter change alters when it will or will not use it.
- **Task routing or tool-selection change:** the recipient chooses a different response or tool call, without acquiring a new underlying capability.
- **External prompt, adapter, memory, or harness change:** the behavior is supplied outside the recipient's base parameters and must not be described as parameter-space implantation.
- **Model-layer behavior versus external action:** modified weights can change the model's outputs or tool-call proposals. An actual external operation depends on the surrounding harness, its code, permissions, and controls; a compromised extension can also act without a model-generated tool call [19].

A task-conditioned behavior is not necessarily activated by a literal trigger phrase. Conditions may be described at the level of task semantics or interaction context, but claims about such activation must be distinguished from explicit-token, answer-side, or positional trigger mechanisms already studied [16, 17]. Nor should adversarial trigger sequences optimized on one model be assumed to transfer reliably to another: Meade et al. report poor and inconsistent cross-model transfer of those triggers [20]. This finding concerns adversarial input triggers, not donor-guided weight-space transplantation.

## 3. Related work

### 3.1 Neural Network Quine and early parameter self-reproduction

Chang and Lipson's *Neural Network Quine* (2018) is a foundational antecedent. The authors construct a network that learns to output its own weights when queried with a coordinate identifying a parameter. They also demonstrate a version that performs MNIST classification while carrying out the weight-output task, with a reported trade-off between classification performance and self-replication [1]. This is not merely a biological metaphor: it is an explicit neural-network self-reproduction mechanism.

The paper's main setting is a network reproducing an encoding of its own parameters. It does not, by itself, demonstrate a modern pretrained model infecting an independently developed recipient model, nor does it establish a multi-generation lineage between distinct foundation models. That distinction is relevant, but it does not make parameter self-reproduction a new idea.

### 3.2 Gabor and colleagues: self-application, artificial chemistry, and inheritance

Gabor, Illium, Mattausch, Belzner, and Linnhoff-Popien presented *Self-Replication in Neural Networks* at ALIFE 2019 [2]. Their subsequent 2022 *Artificial Life* article extends that work [5]. The 2022 article formalizes **self-application**: a network is applied to another network to produce a network. It studies self-application and self-training, non-trivial fixed points in weight space, robustness to noise, and artificial-chemistry environments in which multiple neural networks interact as individuals [5].

This work is especially close to the current proposal. It already studies networks acting on network parameters and populations in which self-replicating structures can arise. The 2022 article also explicitly notes a boundary in its own experiments: it does not track genealogical relationships between particles. It identifies genealogical tracking as future work that could distinguish horizontal from vertical inheritance of information [5]. The same article points to Gabor et al.'s 2021 *Goals for Self-Replicating Neural Networks* for a "train on other" operator and for auxiliary fitness functions in a soup context [3]. Consequently, this project must not claim that inter-network parameter interaction, weight-space self-replication, or the biological analogy is itself new.

A concrete possible direction is to revisit the lineage question with modern model families, explicit source/recipient provenance, independent behavioral evaluation, and causal tests that distinguish information carried by a network from information supplied by an external editor. That is a proposed direction, not an established novelty claim.

### 3.3 Further closely related work in artificial life

Randazzo, Versari, and Mordvintsev published *Recursively Fertile Self-replicating Neural Agents* in the ALIFE 2021 proceedings [4]. This is more than a title-level connection: the lead author's public project note says the work studies feedforward neural networks that encode a target image and self-replicate with and without variation; the author describes the project as creating a genealogy of neural networks encoding flowers [14]. This is a close prior-art lead for recursive reproduction, variation, and neural-network lineage. A public copy of the ALIFE 2021 proceedings volume and its table of contents was located, which lists this contribution at printed page 546. However, the available PDF endpoint blocked page-image retrieval, so the paper's own pages could not be inspected. Its exact replication unit, transfer mechanism, lineage definition, and relationship to the P3 criteria therefore remain **unresolved**. Until that paper is examined, P3 cannot be presented as a novel concept or a newly identified gap.

Gabor, Illium, Zorn, and Linnhoff-Popien's 2021 *Goals for Self-Replicating Neural Networks* addresses auxiliary goals in the self-replicating-network setting [3]. In a related 2022 paper, Illium and colleagues introduce **organism networks** composed of several neural particle networks; each particle performs a weight-application role while also being trained to self-replicate its own weights [6]. This is another direct precedent for collaborative structures built from self-replicating neural components. It is not equivalent to a current LLM transferring a learned behavioral marker into an unrelated recipient, but it makes broad claims about "the first network that infects another network" untenable.

A related but distinct line is Sinapayen's work on **Neural Cellular Automata (NCA)** [15]. It demonstrates patterns that self-replicate across generations and exhibit spontaneous, inheritable mutations and genetic drift. The NCA update rules are encoded by a neural network, but the paper states that those weights are trained and then remain fixed; the inherited "DNA" in its experiments is the cell-state information in an organism's egg/pattern, not a copy or modification of the NCA rule-network weights in a separate recipient model. This is important adjacent work on self-replication and inheritance in neural systems, but it is not the same mechanism as parameter-space transmission between distinct model checkpoints.

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

### 3.8 Conditional backdoors and non-obvious activation conditions

Recent work shows that backdoor activation in language models is not limited to an explicit trigger phrase typed by a user. Zhang et al. describe an answer-side backdoor in which a benign first interaction causes the model to produce a word that later appears in conversation history and serves as a trigger [16]. Wen et al.'s *MetaBackdoor* studies positional information, including context length, as an activation condition even when the visible text remains semantically ordinary [17].

These studies are relevant to the conditional part of the motivating scenario: hidden behavior can depend on context that is not an obvious malicious instruction. They do **not**, by themselves, demonstrate that a donor model's behavior has been transferred into a separate recipient's parameters. They concern backdoor construction and activation within evaluated models, not the specific donor-to-recipient translation mechanism proposed here.

### 3.9 Trigger transfer is not guaranteed across models

Meade, Patel, and Reddy study adversarial trigger transfer among 13 open models and report poor and inconsistent cross-model transfer [20]. This is not a study of transferring learned behavior through weight-space editing, but it cautions against assuming that a trigger or activation rule discovered in one model will function unchanged in another. The transfer of an entire behavior, the portability of its activation condition, and the recipient's retention of that behavior are separate questions.

### 3.10 Parameter editing can damage unrelated capabilities

Ren et al.'s ICML 2026 study examines parameter-based knowledge editing and reports that the evaluated methods damage core model capabilities, while a retrieval-based baseline performs better across their tested conditions [18]. This is an important counterweight to the assumption that a small or localized weight edit necessarily has a small behavioral footprint. Parameter count alone is not a measure of behavioral impact. Any future study of conditional implantation would need to consider collateral effects and ordinary-task utility, not only whether the target behavior appears.

### 3.11 Model-layer and harness-layer security

CERT-EU distinguishes backdoors in model weights from malicious code in an agent harness or extension [19]. A model-layer backdoor changes the model's behavior, for example by causing it to produce a particular response or tool-call proposal under a condition. Harness-layer code can instead execute with the user's permissions without the model selecting or requesting that action. These are distinct attack surfaces and require different evidence and defenses. A report of an external effect must therefore identify whether the causal change was in model parameters, the prompt or adapter stack, or the surrounding software.

### 3.12 Novelty boundary

Prior work already covers neural networks outputting their own weights, formal self-application, artificial-chemistry populations, recursively fertile self-replicating neural agents, neural cellular automata with inherited pattern mutations, host-level AI replication, weight-based AI worms, one-generation backdoor inheritance through model merging, backdoor persistence, conditional and non-obvious trigger activation, parameter-based model editing, and direct LLM-assisted weight editing.

The repository does **not** claim to introduce neural-network self-replication, inter-network parameter interaction, model-merging backdoors, conditional backdoors, or generational replication. The motivating donor-to-recipient scenario overlaps directly with existing model-merging backdoor work at the level of one-generation behavior transfer. A narrower open question is whether a weight-space editor can use a donor's learned behavior as functional source information to create a bounded parameter update in a distinct recipient, with the result retained in that recipient and distinguished from conventional merging, editor-supplied content, prompts, adapters, and harness changes. This remains a research question, not a novelty claim.

The broader P3 question—whether a recipient can become the source for a further transfer—must remain separate from the one-generation P2 scenario. Artificial-life prior art, especially Randazzo et al. (2021), remains a close review issue whose full-text overlap has not been resolved. No priority claim is justified. The contribution may be a useful threat-model clarification, a replication or extension of prior work, a negative result, or no novel mechanism at all.

## 4. Research question and hypotheses

### 4.1 Main research question

**What are the mechanisms, limits, and security implications when a donor model's condition-dependent behavior is transferred into a distinct recipient's own parameters—and under what additional conditions, if any, can the recipient support a further transfer?**

### 4.2 Research questions

- **RQ1 — Encoding:** Can a benign marker be associated with a model's parameter state in a way that can be distinguished from clean controls?
- **RQ2 — Transfer:** Can the marker be transferred into a distinct recipient's parameters by a declared offline intervention, without copying the source checkpoint?
- **RQ3 — Inheritance:** Does the recipient independently express the marker after the source and source-side state are removed?
- **RQ4 — Multi-generation parameter-space transmission:** Can the recipient become the sole source for a subsequent transfer, without the experimenter supplying the marker's semantic contents?
- **RQ5 — Causal dependence:** Is source-carried information necessary for the transfer, or can the editor, prompt, or fixed procedure recreate the marker without it?
- **RQ6 — Compatibility:** How do architecture, parameter alignment, initialization, and scale affect the result?
- **RQ7 — Persistence and defense:** What happens after benign model transformations, and can model inspection or controlled probes detect and remove the marker?
- **RQ8 — Conditional activation:** Can a transferred behavior be conditioned on a task or context rather than a literal trigger string, and how should false activation be distinguished from intended activation?
- **RQ9 — Behavior type:** Is the transferred function a new capability, a policy/refusal change, a task-routing change, or merely a change in tool-call selection?
- **RQ10 — Transfer mechanism:** Can donor-guided direct weight editing be distinguished from conventional merging, editor-supplied reconstruction, checkpoint substitution, prompt/adapter changes, external memory, and harness modification?

### 4.3 Hypotheses

- **H1 (single-generation transfer):** Under at least one controlled, benign condition, a weight-space intervention using a donor as the source of functional information can cause a distinct recipient to encode a corresponding benign behavior in its own base parameters, without copying or substituting the donor checkpoint.
- **H2 (independent inheritance):** A recipient that passes the transfer criterion continues to express the condition-dependent marker using its own base parameters when the donor, editor, prompts, adapters, external memory, and transfer-specific harness changes are absent.
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
2. B does not satisfy the predeclared marker criterion before intervention.
3. The declared intervention changes B's own base parameters; the result is not a checkpoint or parameter-subset substitution.
4. B' satisfies the predeclared marker criterion on held-out tests under the declared condition.
5. B' is evaluated using the recipient's ordinary inference configuration, without access to the donor or editor and without transfer-specific prompts, adapters, retrieval, external memory, or special harness code.
6. Clean-source, no-source, sham-intervention, editor-only, and relevant external-component controls do not explain the result equally well.
7. For a condition-dependent marker, matched condition-absent inputs are evaluated to measure false activation. Retained utility on unrelated tasks is reported separately as a collateral-effects measure.

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

This is a proposed task-conditioned reporting statistic. It is neither an established standard nor a novel epidemiological concept, and it is not a universal property of a model. Anthropic's 2026 AI-worm analysis already uses an epidemiological reproduction-number analogy for infected devices [9]. Here, the unit is a validated recipient-model transfer under a declared experiment rather than an infected device. The value depends on recipient availability, model family, editor, transfer protocol, resource budget, and success criterion. It should not be interpreted as biological epidemiological \\(R_0\\) without an explicit exposure and contact model. Initial work should report trial-level outcomes and uncertainty rather than treating a small sample estimate as a robust population parameter.

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

## 7. Research directions for independently equipped teams

The stages below are conceptual research directions for independent teams with appropriate scientific, computational, and security infrastructure. They are not a work plan or commitment by the repository author. The author is not conducting experiments, and this repository provides no experimental implementation, test suite, results, or claim of capability to run the studies. Any team choosing to investigate the questions would need to design, authorize, resource, and govern its own protocol. The safety boundary remains offline, owner-controlled models and harmless markers.

### Stage 1 — Operational marker and baseline

An independent team could first define a harmless synthetic marker and establish that it can be evaluated separately from unrelated task utility. The team would document the model family, parameter representation, checkpoint provenance, and relevant baseline behavior.

**Gate:** the marker is independently measurable and clean controls are distinguishable before any transfer experiment.

### Stage 2 — Single-generation transfer

A separate study could compare whether a donor-conditioned parameter intervention changes a distinct recipient's own parameters and behavior. The study would need to distinguish direct weight editing from conventional merging, checkpoint substitution, and externally supplied behavior.

**Gate:** the recipient independently expresses the marker after the source is removed, and the controls do not explain the result equally well.

### Stage 3 — Second-generation transfer

Only if a distinct recipient has first met a separately defined P2 criterion would an independent team have reason to consider the stronger A-to-B-to-C question. That study would need to establish whether the first recipient's parameter-carried information—not the original donor, the editor's memory, or a fixed external procedure—accounts for the second transfer.

**Gate:** B, not A, is the sole carrier input for the second-generation step; C independently expresses the marker; clean-source/editor-only conditions do not produce comparable results.

### Stage 4 — Compatibility and persistence

A subsequent research effort could examine architecture differences, parameter alignment, benign fine-tuning, model merging, quantization, and checkpoint conversion as separate compatibility and persistence questions. No generality should be inferred from one condition. Report utility regression and the boundary conditions for each result.

### Stage 5 — Defensive evaluation

Defensive researchers could examine checkpoint provenance, lineage records, behavioral screening, parameter inspection, containment, and benign sanitization. The purpose would be detection and mitigation, not evasion.

## 8. Measurement and reporting

For any independent study, the team responsible should predeclare its target, harmless marker, protocol, controls, primary metric, holdout policy, resource budget, success criteria, and analysis plan.

Suggested measurements include:

- **Transmission success:** fraction of attempted source-recipient trials satisfying the independent marker criterion.
- **Inheritance fidelity:** marker performance of a recipient when evaluated independently from its source.
- **Generational success:** fraction of validated generation-1 carriers that produce a validated generation-2 recipient under the declared protocol.
- **Causal dependence:** difference between source-present and source-absent or source-information-ablated conditions.
- **Recipient utility:** retained performance on unrelated tasks and any measured collateral behavior.
- **Parameter provenance:** checkpoint hashes, changed tensor summaries, edit manifests, and proof that the recipient was not replaced by the source.
- **Robustness:** marker performance after each separately declared benign model transformation.
- **Detection:** true-positive and false-positive rates for defensive inspection and behavioral probes.

Report trial-level results, uncertainty intervals, seeds, exclusions, resource usage, model identities, prompt and tool versions, and raw evidence where redistribution permits. One favorable lineage is a proof-of-possibility result only under the exact tested conditions; it does not establish scale, reliability, broad architecture compatibility, or practical deployment risk.

## 9. Safety, ethics, and release policy

This problem has potential cybersecurity implications. Any independent study should be limited to offline, owner-controlled synthetic models and harmless behavioral markers. This repository will not develop or publish a deployable self-propagating payload, host-compromise workflow, exploit chain, credential-collection mechanism, stealth, evasion, external scanning, or uncontrolled replication system.

Publication should prioritize operational definitions, reproducible benign benchmarks, causal controls, defensive detection, provenance, containment, and remediation. A result that requires unsafe implementation details should be reported at an appropriately abstract level with a defensive emphasis. Experiments must be manually initiated, bounded, reversible, and independently stoppable.

## 10. Limitations

First, parameter-space transfer may be feasible only for small networks or tightly aligned architectures. A toy-model result would not establish transfer in large language models. Second, neural-network parameter symmetries make raw coordinate comparison unreliable across independently trained models. Third, external editors can confound claims about what a carrier itself encodes or causes. Fourth, a functional marker may be much easier to transfer than a general replication capability. Fifth, a model may inherit a marker without having any agency or ability to initiate the next transfer. Finally, a controlled offline demonstration would not by itself establish an operational threat to deployed model ecosystems.

The preliminary literature review is not exhaustive. In particular, it must be expanded across artificial life, neural self-replication, model editing, model merging, backdoor and supply-chain security, federated learning, parameter-space meta-learning, and AI autonomous replication before any strong novelty or priority statement.

## 11. Conclusion

This paper formulates a security-relevant problem rather than reporting a newly discovered capability. The motivating scenario is donor-guided conditional-behavior implantation: a donor model exhibits a condition-dependent behavior, and a weight-space editor is hypothesized to use the donor as a functional source when modifying a distinct recipient's own parameters. Conventional model merging already provides established prior art for one-generation backdoor inheritance. The narrower question is whether direct donor-guided weight editing can be distinguished from merging, editor-supplied reconstruction, prompt or adapter changes, checkpoint substitution, and harness modification, while accounting for model compatibility and collateral behavioral effects.

A single successful recipient implantation would be a P2-level transfer claim, not proof of generational contagion. P3 would require a separate recipient-to-recipient lineage in which the first recipient's own parameter-carried information is causally relevant to a second transfer. P4 autonomy is a still stronger and independent claim. Conditional behavior, capability transfer, policy changes, task routing, and external tool execution must also be evaluated as distinct phenomena.

The repo's contribution is to state the problem, organize its terminology, connect it to adjacent literature, and identify distinctions that may help experts design or reject further work. Its author is not conducting or committing to experiments and does not claim the infrastructure or team required to do so. No experimental results, implementation, or empirical validation are claimed. The paper makes no novelty or priority claim; its value is to make the question clearer and useful to researchers already working in neural-network security, model editing, artificial life, and AI safety.

## References

[1] Oscar Chang and Hod Lipson. “Neural Network Quine.” In *Proceedings of the 2018 Conference on Artificial Life (ALIFE 2018)*, 234–241, 2018. https://doi.org/10.1162/isal_a_00049. Preprint: https://arxiv.org/abs/1803.05859.

[2] Thomas Gabor, Steffen Illium, Andy Mattausch, Lenz Belzner, and Claudia Linnhoff-Popien. “Self-Replication in Neural Networks.” In *Proceedings of the 2019 Conference on Artificial Life (ALIFE 2019)*, 424–431, 2019. https://doi.org/10.1162/isal_a_00197.

[3] Thomas Gabor, Steffen Illium, Maximilian Zorn, and Claudia Linnhoff-Popien. “Goals for Self-Replicating Neural Networks.” In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 101–110, 2021. https://doi.org/10.1162/isal_a_00439.

[4] Ettore Randazzo, Luca Versari, and Alexander Mordvintsev. “Recursively Fertile Self-replicating Neural Agents.” In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 2021. https://doi.org/10.1162/isal_a_00367. The lead author's project note is available at https://oteret.github.io/posts/self-repl-nn/. The proceedings paper's full text was not available in the sources inspected for this revision; its exact overlap remains unresolved.

[5] Thomas Gabor, Steffen Illium, Maximilian Zorn, Cristian Lenta, Andy Mattausch, Lenz Belzner, and Claudia Linnhoff-Popien. “Self-Replication in Neural Networks.” *Artificial Life* 28, no. 2 (2022): 205–223. https://doi.org/10.1162/artl_a_00359.

[6] Steffen Illium, Maximilian Zorn, Cristian Lenta, Michael Kölle, Claudia Linnhoff-Popien, and Thomas Gabor. “Constructing Organism Networks from Collaborative Self-Replicators.” In *Proceedings of the 2022 IEEE Symposium Series on Computational Intelligence (SSCI 2022)*, 1268–1275, 2022. https://doi.org/10.1109/SSCI51031.2022.10022216. Preprint: https://arxiv.org/abs/2212.10078.

[7] Xudong Pan, Jiarun Dai, Yihe Fan, Minyuan Luo, Changyi Li, and Min Yang. “Large Language Model-Powered AI Systems Achieve Self-Replication with No Human Intervention.” arXiv:2503.17378, 2025. Work in progress. https://doi.org/10.48550/arXiv.2503.17378.

[8] Alena Air, Reworr, Nikolaj Kotov, Dmitrii Volkov, John Steidley, and Jeffrey Ladish. “Language Models Can Autonomously Hack and Self-Replicate.” arXiv:2605.06760, 2026. https://arxiv.org/abs/2605.06760.

[9] William Zhou and Daniel Freeman, Anthropic Frontier Red Team. “AI Models May Be Capable of Self-Replicating Without Access to a Datacenter.” Anthropic Research, 12 October 2026. https://www.anthropic.com/research/self-replicating-ai.

[10] Zenghui Yuan, Yangming Xu, Jiawen Shi, Pan Zhou, and Lichao Sun. “Merge Hijacking: Backdoor Attacks to Model Merging of Large Language Models.” In *Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)*, 32688–32703, 2025. https://doi.org/10.18653/v1/2025.acl-long.1571.

[11] Jing Cui, Yufei Han, Jianbin Jiao, and Junge Zhang. “Persistent Backdoor Attacks under Continual Fine-Tuning of LLMs.” In *Proceedings of the AAAI Conference on Artificial Intelligence* 40, no. 36 (2026): 30422–30430. https://doi.org/10.1609/aaai.v40i36.40295.

[12] Samuel K. Ainsworth, Jonathan Hayase, and Siddhartha Srinivasa. “Git Re-Basin: Merging Models modulo Permutation Symmetries.” In *International Conference on Learning Representations*, 2023. https://arxiv.org/abs/2209.04836.

[13] Rikiya Takehi, Jayden Teoh, Alex Zhang, and Omar Khattab. “Sparks of Weight-Space Programming: LLMs Can Natively Read & Write Neural Network Weights.” Authors' research article, 2 November 2026. https://rikiyat.github.io/blog/weight-space-programming/. Accompanying experiment logs: https://github.com/RikiyaT/lm_understand-logs.

[14] Ettore Randazzo. “Recursively Fertile Self-replicating Neural Agents.” Author's project note, 21 July 2021. https://oteret.github.io/posts/self-repl-nn/. This is a project summary, not a substitute for the ALIFE 2021 proceedings paper [4].

[15] Lana Sinapayen. “Self-Replication, Spontaneous Mutations, and Exponential Genetic Drift in Neural Cellular Automata.” *Qeios*, Research Article (Preprint), 23 May 2023. https://doi.org/10.32388/JPUWVB. arXiv:2305.13043, https://arxiv.org/abs/2305.13043. Code and data links are provided by the author at https://github.com/LanaSina/NCA_self_replication.


[16] Yibo Zhang, Tianrong Guan, Liang Lin, Puze Wang, Jin Wang, and Qingsong Wen. “The Model Plants the Trigger: Answer-Side Backdoor Attacks in Multi-Turn Large Language Models.” In *Findings of the Association for Computational Linguistics: EMNLP 2026*, 39113–39127. https://doi.org/10.18653/2026.findings-emnlp.1832.

[17] Rui Wen, Mark Russinovich, Andrew Paverd, Jun Sakuma, and Ahmed Salem. “MetaBackdoor: Exploiting Positional Encoding as a Backdoor Attack Surface in LLMs.” arXiv:2605.15172, May 2026. https://arxiv.org/abs/2605.15172.

[18] Wanying Ren, Xin Song, Futing Wang, Guoxiu He, and Aixin Sun. “Revisiting Parameter-Based Knowledge Editing in Large Language Models: Theoretical Limits and Empirical Evidence.” In *Proceedings of the 43rd International Conference on Machine Learning*, PMLR 306, 2026. https://proceedings.mlr.press/v306/ren26p.html.

[19] CERT-EU. “Beyond the Model: Backdoors in AI Agent Harnesses.” 30 October 2026. https://www.cert.europa.eu/blog/beyond-the-model-backdoors-in-ai-agent-harnesses.

[20] Nicholas Meade, Arkil Patel, and Siva Reddy. “Investigating Adversarial Trigger Transfer in Large Language Models.” *Transactions of the Association for Computational Linguistics* 13 (2025): 953–979. https://doi.org/10.1162/tacl.a.27.

## Version note

This is a conceptual problem statement and threat-model paper dated 5 November 2026, version 0.2.1. It has not undergone peer review and contains no original experimental results. The author is not conducting experiments and does not claim experimental infrastructure. Its related-work review is preliminary and non-systematic. The ALIFE 2021 proceedings volume's table of contents was located, but the full text of [4] could not be inspected because the available PDF endpoint blocked page-image retrieval. Novelty relative to that work therefore remains specifically unresolved.

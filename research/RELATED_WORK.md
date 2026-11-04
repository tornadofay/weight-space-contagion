# Preliminary Related-Work Review

**Review date:** 2026-11-04  
**Status:** Preliminary, web-based, non-systematic review  
**Purpose:** Identify adjacent work, prevent novelty overclaims, and define the next systematic search.

This review was expanded during a repository revision. It is still not systematic: no database-by-database screening, complete forward/backward citation review, or exhaustive full-text comparison has been completed. In particular, the full text of Randazzo et al. (2021) was not available in the sources inspected and remains an explicit review gap.

## 1. Neural Network Quine

**Chang, Oscar; Lipson, Hod (2018). “Neural Network Quine.”** In *Proceedings of the 2018 Conference on Artificial Life (ALIFE 2018)*, 234–241. [DOI: 10.1162/isal_a_00049](https://doi.org/10.1162/isal_a_00049) · [arXiv:1803.05859](https://arxiv.org/abs/1803.05859).

Chang and Lipson describe a neural network that learns to output its own weights when queried with a coordinate identifying a parameter. They also demonstrate a network that combines the self-replication task with MNIST classification, and report a trade-off between classification and self-replication performance.

**Relevance:** This is a foundational, direct demonstration of neural-network self-reproduction through parameter output. It prevents any claim that a network encoding or reproducing its own weights is a new idea. The paper does not, on its own, demonstrate a contemporary pretrained model transmitting a behavioral marker into an independently developed model or a lineage across distinct foundation models.

## 2. Gabor et al. (2019): Self-Replication in Neural Networks

**Gabor, Thomas; Illium, Steffen; Mattausch, Andy; Belzner, Lenz; Linnhoff-Popien, Claudia (2019). “Self-Replication in Neural Networks.”** In *Proceedings of the 2019 Conference on Artificial Life (ALIFE 2019)*, 424–431. [DOI: 10.1162/isal_a_00197](https://doi.org/10.1162/isal_a_00197).

The authors study neural-network self-replication using weight-space dynamics and artificial-chemistry settings containing multiple neural networks.

**Relevance:** This is an earlier conference version of the line of work expanded in the 2022 *Artificial Life* article. It is part of the core prior-art trail and should be read alongside both the 2018 Neural Network Quine and the 2022 expanded article.

## 3. Gabor et al. (2021): Goals for Self-Replicating Neural Networks

**Gabor, Thomas; Illium, Steffen; Zorn, Maximilian; Linnhoff-Popien, Claudia (2021). “Goals for Self-Replicating Neural Networks.”** In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 101–110. [DOI: 10.1162/isal_a_00439](https://doi.org/10.1162/isal_a_00439).

This work addresses additional goals in the self-replicating neural-network setting. The 2022 Gabor et al. article explicitly points to this 2021 work for a “train on other” operator and for auxiliary fitness functions in a neural-network soup context.

**Relevance:** This is directly adjacent to inter-network learning and the use of networks in populations. Its exact operator and experimental scope should be compared in detail before the project claims a new form of network-to-network parameter modification.

## 4. Randazzo et al. (2021): Recursively Fertile Self-replicating Neural Agents

**Randazzo, Ettore; Versari, Luca; Mordvintsev, Alexander (2021). “Recursively Fertile Self-replicating Neural Agents.”** In *Proceedings of the 2021 Conference on Artificial Life (ALIFE 2021)*, 58. [DOI: 10.1162/isal_a_00367](https://doi.org/10.1162/isal_a_00367).

This is a particularly close predecessor for claims about recursive or generational neural self-replication. In the lead author's public project note, Randazzo describes feedforward neural networks that encode a target image and self-replicate with and without variation. The note describes the project as creating a genealogy of neural networks encoding flowers ([author's project note, 21 July 2021](https://oteret.github.io/posts/self-repl-nn/)).

**Review limitation:** The full proceedings paper was not available in the sources inspected for this revision. The summary above is based on the bibliographic record and the author's project note, not a full reading of the paper. Its exact replication unit, transfer mechanism, lineage definition, and relationship to the proposed A→B→C criterion remain unresolved. This is a close prior-art blocker: P3 cannot be presented as a novel concept or a newly identified gap until the full paper has been examined.

## 5. Gabor et al. (2022): Self-Replication in Neural Networks

**Gabor, Thomas; Illium, Steffen; Zorn, Maximilian; Lenta, Cristian; Mattausch, Andy; Belzner, Lenz; Linnhoff-Popien, Claudia (2022). “Self-Replication in Neural Networks.”** *Artificial Life* 28(2), 205–223. [DOI: 10.1162/artl_a_00359](https://doi.org/10.1162/artl_a_00359).

This expanded journal paper formalizes **self-application**: a network is applied to another network to produce a network. It studies self-application and self-training, non-trivial fixed points in weight space, robustness to noise, and artificial-chemistry environments in which multiple neural networks interact as individuals.

The article also states that its experiments do not track genealogical relationships between particles. It identifies genealogical tracking as future work that could distinguish horizontal from vertical inheritance of information. It also notes that the scope of the article trains networks only with (a reduction of) themselves as input and refers to Gabor et al. (2021) for a “train on other” operator.

**Relevance:** This is among the closest prior works. It already covers network-to-network application, interacting populations, self-replicating structures, and the weight-space perspective. The absence of lineage tracking in this particular article is a potential motivation for further research, not proof that no other paper has studied lineage; Randazzo et al. (2021) is a prominent unresolved predecessor.

## 6. Illium et al. (2022): Constructing Organism Networks from Collaborative Self-Replicators

**Illium, Steffen; Zorn, Maximilian; Lenta, Cristian; Kölle, Michael; Linnhoff-Popien, Claudia; Gabor, Thomas (2022). “Constructing Organism Networks from Collaborative Self-Replicators.”** In *Proceedings of the 2022 IEEE Symposium Series on Computational Intelligence (SSCI 2022)*, 1268–1275. [DOI: 10.1109/SSCI51031.2022.10022216](https://doi.org/10.1109/SSCI51031.2022.10022216) · [arXiv:2212.10078](https://arxiv.org/abs/2212.10078).

The authors introduce organism networks composed of several neural particle networks. Each particle performs a weight-application role while also being trained to self-replicate its own weights. The work studies collective arithmetic and simplified MNIST tasks, and reports task specialization among particles.

**Relevance:** This is another direct precedent for collaborative neural structures built from self-replicating parameter-level components. It makes broad claims about the first network population to self-replicate or about neural components propagating through a network population untenable.

## 7. Neural cellular automata: pattern replication and inheritable mutation

**Sinapayen, Lana (2023). “Self-Replication, Spontaneous Mutations, and Exponential Genetic Drift in Neural Cellular Automata.”** *Qeios*, Research Article (Preprint), 23 May 2023. [DOI: 10.32388/JPUWVB](https://doi.org/10.32388/JPUWVB) · [arXiv:2305.13043](https://arxiv.org/abs/2305.13043) · [Code](https://github.com/LanaSina/NCA_self_replication).

The paper reports neural-cellular-automata patterns that self-replicate and exhibit spontaneous inheritable mutations and genetic drift across generations. Each cell has a state updated by a fixed rule; the update rule is encoded by a neural network. The paper states that the rule-network weights are updated through gradient descent during training and do not change after training. The hereditary information called the organism's “DNA” is defined from cell-state values in an egg/pattern and is passed through the pattern's replication lineage.

**Relevance and distinction:** This is important adjacent work on neural systems, self-replicating patterns, inheritance, and mutation. It does not demonstrate the NCA rule network's learned parameter vector being copied or transferred into a distinct recipient model's parameter state. The replicated units are patterns/cell states operating under fixed learned NCA rules. It should be included in the broader artificial-life background without conflating pattern/state inheritance with model-parameter transmission.

## 8. Agent-level AI self-replication

**Pan, Xudong; Dai, Jiarun; Fan, Yihe; Luo, Minyuan; Li, Changyi; Yang, Min (2025). “Large Language Model-Powered AI Systems Achieve Self-Replication with No Human Intervention.”** arXiv:2503.17378, v2 dated 2025-03-25. [arXiv](https://arxiv.org/abs/2503.17378) · [DOI](https://doi.org/10.48550/arXiv.2503.17378).

The authors report capability-elicitation experiments in which AI systems attempt agent-level self-replication. The arXiv record identifies the work as work in progress; attribute the results to the authors and do not present them as settled consensus.

**Relevance:** Establishes an agentic self-replication research line. It is distinct from the artificial-life self-application literature and from the proposed criterion for parameter-space inheritance in a distinct recipient.

## 9. Agentic replication across vulnerable hosts

**Air, Alena; Reworr; Kotov, Nikolaj; Volkov, Dmitrii; Steidley, John; Ladish, Jeffrey (2026). “Language Models Can Autonomously Hack and Self-Replicate.”** [Palisade Research](https://palisaderesearch.org/research/self-replication) · [arXiv:2605.06760](https://arxiv.org/abs/2605.06760) · [Code](https://github.com/palisaderesearch/AI-self-replication).

Published May 7, 2026. The authors report agents exploiting vulnerable hosts, copying model weights and an execution harness, establishing inference on target hosts, and chaining replication.

**Relevance:** Host-level model-file and agent-harness replication is already an empirical research area. Copying or redeploying a model is not equivalent to modifying a distinct recipient's own parameters so it inherits a behavior.

## 10. Weight-based AI replicators

**Zhou, William; Freeman, Daniel; Anthropic Frontier Red Team (2026-10-12). “AI Models May Be Capable of Self-Replicating Without Access to a Datacenter.”** [Anthropic Research](https://www.anthropic.com/research/self-replicating-ai).

The report describes weight-based AI replicators that propagate through host compromise, carrying or retrieving model weights and establishing inference on compromised hardware. It also uses an epidemiological reproduction-number analogy for the number of infected devices.

**Relevance:** This is a close contemporary threat model. This project does not claim novelty for AI worms carrying model weights between hosts. The proposed distinction is parameter-space transfer into a distinct recipient model, not the transport of the source model to a new machine.

## 11. Backdoor inheritance through model merging

**Yuan, Zenghui; Xu, Yangming; Shi, Jiawen; Zhou, Pan; Sun, Lichao (2025). “Merge Hijacking: Backdoor Attacks to Model Merging of Large Language Models.”** *Proceedings of ACL 2025*, 32688–32703. [ACL Anthology](https://aclanthology.org/2025.acl-long.1571/) · [DOI](https://doi.org/10.18653/v1/2025.acl-long.1571).

The paper demonstrates that a model produced by merging can inherit a backdoor from a maliciously prepared uploaded model while retaining utility across tasks.

**Relevance:** This is direct evidence for one-generation parameter-space behavior transfer and overlaps with the P2 claim level. It does not, on its own, establish a recipient-sourced second generation.

## 12. Backdoor persistence under continual fine-tuning

**Cui, Jing; Han, Yufei; Jiao, Jianbin; Zhang, Junge (2026). “Persistent Backdoor Attacks under Continual Fine-Tuning of LLMs.”** *Proceedings of AAAI 2026* 40(36), 30422–30430. [DOI](https://doi.org/10.1609/aaai.v40i36.40295).

The authors propose P-Trojan and report persistence through their tested multi-stage continual fine-tuning settings.

**Relevance:** Persistence is an important property to measure, but it is not the same as transfer to a distinct recipient or multi-generation reproduction.

## 13. Parameter alignment and model merging

**Ainsworth, Samuel K.; Hayase, Jonathan; Srinivasa, Siddhartha (2023). “Git Re-Basin: Merging Models modulo Permutation Symmetries.”** ICLR 2023. [arXiv:2209.04836](https://arxiv.org/abs/2209.04836).

The work studies hidden-unit permutation symmetries and alignment for merging independently trained neural networks in weight space.

**Relevance:** Raw parameter coordinates are not universally comparable. Cross-model transfer claims require functional evaluation and explicit alignment assumptions.

## 14. Direct weight interpretation and editing

**Takehi, Rikiya; Teoh, Jayden; Zhang, Alex; Khattab, Omar (2026). “Sparks of Weight-Space Programming: LLMs Can Natively Read & Write Neural Network Weights.”** Authors' research article, November 2, 2026. [Article](https://rikiyat.github.io/blog/weight-space-programming/) · [Experiment logs](https://github.com/RikiyaT/lm_understand-logs).

The authors report experiments in which a general-purpose LLM inspects neural-network parameters, infers behavior, writes small policies, and directly edits a language-model checkpoint. The article is treated as an authors' research article, not as a peer-reviewed conference paper.

**Relevance:** Motivates the possibility that a general-purpose model can serve as an external editor of neural parameters. It does not itself establish the multi-generation lineage defined here.

## 15. Conditional backdoors and non-obvious activation conditions

**Zhang, Yibo; Guan, Tianrong; Lin, Liang; Wang, Puze; Wang, Jin; Wen, Qingsong (2026). “The Model Plants the Trigger: Answer-Side Backdoor Attacks in Multi-Turn Large Language Models.”** *Findings of EMNLP 2026*, 39113–39127. [ACL Anthology](https://aclanthology.org/2026.findings-emnlp.1832/) · [DOI: 10.18653/2026.findings-emnlp.1832](https://doi.org/10.18653/2026.findings-emnlp.1832).

The authors describe a multi-turn backdoor in which a benign interaction causes the model to produce a word that later appears in conversation history and acts as an activation condition.

**Wen, Rui; Russinovich, Mark; Paverd, Andrew; Sakuma, Jun; Salem, Ahmed (2026). “MetaBackdoor: Exploiting Positional Encoding as a Backdoor Attack Surface in LLMs.”** Microsoft Research; arXiv:2605.15172, May 2026. [Microsoft Research](https://www.microsoft.com/en-us/research/publication/metabackdoor-exploiting-positional-encoding-as-a-backdoor-attack-surface-in-llms/) · [arXiv](https://arxiv.org/abs/2605.15172).

The authors study positional conditions, including length-related activation, that do not require suspicious visible trigger text.

**Relevance and distinction:** These works show that conditional activation can depend on conversation history or positional structure, not only a literal user-entered phrase. They do not, by themselves, demonstrate that a donor model's condition-dependent behavior is transplanted into a distinct recipient's parameters.

## 16. Cross-model trigger transfer

**Meade, Nicholas; Patel, Arkil; Reddy, Siva (2025). “Investigating Adversarial Trigger Transfer in Large Language Models.”** *Transactions of the Association for Computational Linguistics* 13 (2025): 953–979. [ACL Anthology](https://aclanthology.org/2025.tacl-1.45/) · [DOI: 10.1162/tacl.a.27](https://doi.org/10.1162/tacl.a.27).

The authors evaluate adversarial trigger transfer among 13 open models and report poor and inconsistent transfer.

**Relevance and distinction:** This is not weight-space behavior transplantation. It is relevant because it cautions against assuming that an activation condition found in a donor will transfer unchanged to a recipient. Trigger portability, functional behavior transfer, and recipient-side retention are separate properties.

## 17. Limitations of parameter-based editing

**Ren, Wanying; Song, Xin; Wang, Futing; He, Guoxiu; Sun, Aixin (2026). “Revisiting Parameter-Based Knowledge Editing in Large Language Models: Theoretical Limits and Empirical Evidence.”** *Proceedings of the 43rd International Conference on Machine Learning*, PMLR 306. [PMLR](https://proceedings.mlr.press/v306/ren26p.html).

The paper analyzes theoretical limits of localized parameter edits and reports that the parameter-editing methods evaluated in its experiments damaged core LLM capabilities; a retrieval baseline performed better across the tested conditions.

**Relevance:** A small edit is not necessarily a low-impact edit. Any future study of parameter-space implantation would need to measure unrelated-task regression and collateral behavior rather than report only target-behavior activation.

## 18. Model-layer versus agent-harness backdoors

**CERT-EU (30 October 2026). “Beyond the Model: Backdoors in AI Agent Harnesses.”** [CERT-EU](https://www.cert.europa.eu/blog/beyond-the-model-backdoors-in-ai-agent-harnesses).

The technical report distinguishes model-weight modifications that alter model behavior from malicious extensions or harness code that can execute with the user's permissions independently of model-generated tool calls.

**Relevance:** This prevents attribution errors. An external action is not proof of a parameter-space behavior transfer. A study must identify whether the causal change is in model weights, the prompt/adapter/runtime configuration, or the surrounding software.

## 19. Preliminary novelty assessment

Prior work already covers neural networks outputting their own weights, formal self-application, artificial-chemistry populations, recursively fertile self-replicating neural agents, neural-cellular-automata pattern inheritance, agent-level replication, weight-based AI worms, one-generation backdoor inheritance through model merging, backdoor persistence, conditional answer-side and positional triggers, inconsistent cross-model adversarial-trigger transfer, collateral damage from parameter-based editing, parameter alignment, direct weight editing, and harness-layer backdoors.

The motivating donor-to-recipient scenario overlaps existing model-merging backdoor work at the level of one-generation transfer. The narrower open question is whether a weight-space editor can use a donor's condition-dependent behavior as functional source information to produce a bounded parameter update in a distinct recipient, and whether the behavior remains in the recipient rather than in prompts, adapters, external memory, or the harness. This must be distinguished from capability acquisition, policy/refusal alteration, and task-routing changes. The stronger P3 question—whether the recipient can itself support a further transfer—remains separate. Any future study would need qualified teams, suitable infrastructure, benign controls, and a full comparison against the prior work above.

Gabor et al. explicitly identify genealogical tracking as an open direction in their 2022 article. However, Randazzo et al.'s *Recursively Fertile Self-replicating Neural Agents* (2021) is a particularly important nearby work whose full-text overlap remains unresolved. The project must not claim a novel lineage gap until that work and the other cited artificial-life papers have been compared in full.

The contribution may ultimately be a new benchmark, a modern empirical extension or replication of earlier artificial-life results, a negative result about generalization to current model families, or no novel contribution. This preliminary review does not establish priority. In particular, the full-text overlap of Randazzo et al. (2021) remains an explicit unresolved issue.

## 16. Review limitations and next search

This review is not systematic. It does not exhaustively query arXiv, IEEE Xplore, ACM Digital Library, Scopus, Web of Science, OpenReview, ACL Anthology, or all artificial-life and security venues. It also does not include a full-text comparison of Randazzo et al. (2021). The next review should document database-by-database queries and forward/backward citation tracing.

Search terms should include:

- neural network quine; self-replication in neural networks; self-application; train-on-other; artificial chemistry neural networks;
- recursively fertile self-replicating neural agents; genealogy of neural networks; horizontal and vertical inheritance in artificial life;
- neural cellular automata; inheritable mutations and genetic drift in NCA; pattern-state inheritance versus update-rule parameter transfer;
- collaborative self-replicators; organism networks; self-replicating neural cellular automata;
- weight-space programming; direct weight editing; model editing;
- model merging backdoor; backdoor inheritance; model supply-chain security;
- donor-guided parameter editing; conditional behavior transfer; task-conditioned backdoors; answer-side backdoors; positional triggers;
- parameter-based knowledge editing; collateral capability regression; model-layer versus harness-layer backdoors;
- parameter-space transfer; behavioral inheritance; AI self-replication; weight-based replicator;
- federated learning backdoor transfer; model lineage; neural trojan persistence.

Record databases, exact queries, search date, result counts, inclusion/exclusion rules, full-text availability, and screening outcomes before making stronger novelty statements.

# Multi-agent LLM benchmarks, coordination studies and training methods (survey as of 11 November 2026)

Reading notes on evidence quality:
- "Fetched" means I read the arXiv abstract page or paper HTML this session. "Snippet" means the claim comes only from a search-result summary and should be re-checked before it is quoted in a final report.
- Most 2026 items are arXiv preprints. Peer-reviewed status is stated only where a venue listing was seen.
- Several fetched pages were truncated at 100,000 characters, so per-model tables in the later parts of long papers were not read.

## 1. What multi-agent software-engineering benchmarks or environments exist?

### Takeaway
The closest prior work to the planned environment is CooperBench (two agents, each sees only its own feature, hidden tests on the merged result, with solo and no-communication baselines) and AsynCodeBench (explicit cross-agent dependency graph with executable dependency checkers). No benchmark found gives each agent a private service of a multi-service company codebase with hidden contract and integration tests, so the planned design appears to be new, but CooperBench has already reported the uncomfortable result that messaging did not raise success.

### Cited Findings

**CooperBench (Stanford and SAP Labs; arXiv 2601.13295, January 2026; preprint, with an ICLR 2026 site listing under the title "CooperBench: Benchmarking Cooperation in Coding Agents")**
- Size and sources: 652 feature-pair tasks built from 199 features in 52 task sets, from 12 open-source libraries in Python, TypeScript, Go and Rust (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295). The arXiv abstract and ICLR listing describe an earlier count of about 600 tasks (snippet) — [ICLR 2026 listing](https://iclr.cc/virtual/2026/10018462)
- Construction: anchor features come from real pull requests, expert annotators write adjacent features that plausibly overlap, and every feature combination is checked for compatibility with unit tests and a gold solution (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Private information: each agent sees only its own feature; unit tests and gold solutions are withheld (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Communication: a message-passing tool backed by an SQL database; messages reach the other agent at its next step; agents work asynchronously in isolated containers (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Scoring: patches are merged with git merge-file, a small learned resolver is tried if that fails, and the merged code must pass both features' test suites (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Solo baseline: one agent implements both features (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Headline result: GPT-5 and Claude Sonnet 4.5 agents reach about 25% in the two-agent setting, roughly 50% below Solo; pooled raw success counts are 1039 Solo vs 558 Coop, a pooled retention of 0.59 (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295). The abstract states the drop as about 30% on average (snippet) — [arXiv abstract](https://www.arxiv.org/abs/2601.13295)
- Communication ablation: communication does not significantly improve success; it reduces raw merge conflicts for several models, but after merge resolution the with-communication and no-communication averages are nearly identical (17.14% vs 17.64%). Agents spend as much as about 20% of steps communicating (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Failure symptoms: work overlap 33.2%, divergent architecture 29.7%, repetition 14.7%, unresponsiveness 8.7%, unverifiable claims 4.3%, broken commitment 3.7%, dependency access 1.7%, placeholder misuse 1.5%, parameter flow 1.3%, timing dependency 1.1%. Failure causes: expectation 42%, commitment 32%, communication 26% (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Human comparison: a secondary summary reports human developer pairs solving 9 out of 10 tasks under the same constraints where agents manage 3 out of 10 (snippet, not seen in the paper text I read) — [MCML publication page](https://mcml.ai/publications/kzt+26/)
- Licence and availability: CC BY-SA 4.0; project site cooperbench.com (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)

**AsynCodeBench (arXiv 2609.32662, submitted 26 September 2026; preprint)**
- Design: each task has an explicit dependency graph and executable "Dependency Checkers", to measure cross-agent coordination separately from individual coding ability. 19 tasks from real-world repositories with 52 directed dependencies (fetched abstract) — [arXiv](https://arxiv.org/abs/2609.32662)
- Metrics: Asynchronous Dependency Pass Rate (share of cross-agent dependencies ultimately satisfied) and Dependency Resolution Step (when each dependency first becomes satisfied). Reports a "hopping window" pattern where dependencies resolve in short bursts (fetched abstract) — [arXiv](https://arxiv.org/abs/2609.32662)
- Findings: coding skill does not reliably predict collaboration skill, and task-level scores can hide unresolved coordination failures (snippet) — [arXiv HTML](https://arxiv.org/html/2609.32662)
- Licence: CC BY 4.0 on the paper; no code or data link seen on the abstract page (fetched) — [arXiv](https://arxiv.org/abs/2609.32662)

**Multi-agent Collaboration with State Management / STORM (arXiv 2605.20563, 19 May 2026; preprint)**
- Not a benchmark, but an evaluation of several agents editing one codebase on Commit0 and PaperBench. Compares one git worktree per agent with post-hoc merge against a shared workspace where conflicts are caught at write time (fetched abstract) — [arXiv](https://arxiv.org/abs/2605.20563)
- Results: STORM beats the git-worktree baseline by +18.7 on Commit0-Lite and +1.4 on PaperBench; combined with single-agent runs it reports 87.6 on Commit0 and 78.2 on PaperBench (fetched abstract) — [arXiv](https://arxiv.org/abs/2605.20563)

**TheAgentCompany (arXiv 2412.14161, v1 18 December 2024, v3 10 September 2025)**
- A self-contained simulated small software company with internal websites and data; the single agent under test browses, codes, runs programs and communicates with coworkers. Headline: "the most competitive agent can complete 30% of tasks autonomously". CC BY 4.0; code, data and environment released at the-agent-company.com (fetched abstract) — [arXiv](https://arxiv.org/abs/2412.14161)
- It evaluates one agent against simulated colleagues, not a team of trained agents; the abstract page did not give the task count or checkpoint scoring details (fetched) — [arXiv](https://arxiv.org/abs/2412.14161)

**SlackBench (arXiv 2611.05512, November 2026; preprint)**
- Tests agents on work that spans workplace chat and evolving repository state; the best system scores around 80% and most agents below 66%. It is a single-agent evaluation of communication plus code (snippet) — [arXiv](https://arxiv.org/abs/2611.05512)

**MultiAgentBench / MARBLE (arXiv 2503.01935, 3 March 2025; ACL 2025 long paper)**
- Covers collaboration and competition scenarios, including coding and research; compares star, chain, tree and graph topologies plus group discussion and cognitive planning; scores with milestone-based KPIs. gpt-4o-mini had the highest average task score, graph structure was best in the research scenario, and cognitive planning improved milestone achievement by 3% (fetched abstract) — [arXiv](https://arxiv.org/abs/2503.01935); venue per [ACL Anthology PDF](https://aclanthology.org/2025.acl-long.421.pdf)

**Multi-repo and microservice coding benchmarks (single-agent, relevant for task design)**
- BeyondSWE (arXiv 2603.03194, March 2026): 500 instances from 246 GitHub repositories across four task types, one of which is cross-repo issue resolution; agents struggle with cross-repository reasoning (snippet from an aggregator) — [emergentmind](https://api.emergentmind.com/papers/2603.03194)
- RepoGenesis (arXiv 2601.13943, January 2026): end-to-end microservice generation from README, 106 repositories (60 Python, 46 Java); best system 23.67% Pass@1 on Python and 21.45% on Java; failures attributed to architectural coherence, dependency management and cross-file consistency (snippet) — [arXiv PDF](https://arxiv.org/pdf/2601.13943)
- CodeScaleBench (Sourcegraph, March 2026): a vendor blog post about large-codebase and multi-repo tasks whose headline finding favours the vendor's own tools; not peer reviewed (snippet) — [Sourcegraph blog](https://sourcegraph.com/blog/codescalebench-testing-coding-agents-on-large-codebases-and-multi-repo-software-engineering-tasks)

### Inferences
- The planned environment differs from CooperBench in three ways that matter: agents own disjoint services instead of editing one repository, the interdependence is an interface contract instead of a merge conflict, and there are four agents instead of two. CooperBench's top two failure symptoms (work overlap, divergent architecture) are partly artefacts of a shared repository; a service-ownership design removes overlap and concentrates failure on interface agreement.
- CooperBench's communication null result (17.14% vs 17.64%) is the main warning for the planned with-messaging vs without-messaging baseline: in CooperBench the features "can be built independently", so messaging was not strictly needed. Tasks in the new environment should be built so the no-messaging team provably lacks information it needs (for example, a field name or error code that exists only in another agent's service).
- AsynCodeBench's per-dependency checkers are a ready model for a dense, deterministic reward: score each cross-service contract separately, in addition to the end-to-end integration test.
- CooperBench's solo baseline gives one agent both features but the abstract-level material does not say the token budget was matched; the planned equal-total-budget single-agent baseline is stricter.

### Gaps
- AsynCodeBench: number of agents, what each agent sees, and all numeric results were not on the abstract page; the full paper was not read.
- CooperBench: exact per-model solo and coop rates are in figures I could not read; the human-pair result is from a secondary page only.
- ChatDev, MetaGPT, SWE-bench multi-agent variants, DevBench/ProjectDev-style evaluations: I know these exist from background knowledge but did not retrieve sources this session, so no claims are made about them. MAST (section 3) reports ChatDev at 33.33% correctness on ProgramDev.
- I found no benchmark where each agent holds a private service of a multi-service codebase. Absence in about 30 searches and fetches is not proof that none exists.
- TheAgentCompany task count and checkpoint scoring, SlackBench design details, and MASBench/BeyondSWE results were not verified from full text.

## 2. What general multi-agent LLM coordination benchmarks exist, and which coordination structures do they test?

### Takeaway
Information pooling under private information is the best-covered structure and LLM teams do badly at it (HiddenBench: 30.1% distributed vs 80.7% for a single agent with everything). Convention without communication (zero-shot coordination) is also weak and does not improve reliably with model capability; handoff, review and mixed-motive structures were less well covered by what I retrieved.

### Cited Findings

| Benchmark | Date and status | Structure tested | Key design and result | Source |
|---|---|---|---|---|
| HiddenBench ("Systematic Failures in Collective Reasoning under Distributed Information in Multi-Agent LLMs") | arXiv 2505.11556, May 2025; ICML 2026 | Information pooling | 65 Hidden Profile tasks; multi-agent LLMs reach 30.1% accuracy when information is distributed vs 80.7% for single agents given complete information; 15 frontier LLMs (snippet) | [PMLR v306](https://proceedings.mlr.press/v306/li26ej.html), [arXiv](https://arxiv.org/html/2505.11556v3) |
| The Collaboration Tax | arXiv 2608.22152, 23 August 2026; EMNLP 2026 main | Information pooling, two agents | 32 solo-tractable tasks, 11 models from 7 providers; tax defined as team-decentralisation loss in a two-player cooperative game with private information (fetched abstract) | [arXiv](https://arxiv.org/abs/2608.22152) |
| CalBench | arXiv 2605.09823, May 2026; preprint | Shared resource and negotiation under privacy | Each agent holds a private calendar; measures task success, excess cost, communication efficiency, fairness and privacy leakage (snippet) | [arXiv](https://arxiv.org/abs/2605.09823) |
| MASBench | arXiv 2610.04672, 3 October 2026; preprint | Partial observability across Reasoning, Scheduling, Game | Evaluates Protocol, Memory and Routing mechanisms; deterministic metrics: performance score, communication cost, cost effectiveness (fetched abstract; no numbers in abstract) | [arXiv](https://arxiv.org/abs/2610.04672) |
| Sparks of Cooperative Reasoning: LLMs as Strategic Hanabi Agents | arXiv 2601.18077, January 2026; ICML 2026 poster | Convention and implicit communication | 17 LLMs, 2 to 5 players; best models score about 15/25 vs more than 20/25 for specialist human experts (snippet) | [ICML listing](https://icml.cc/virtual/2026/poster/60843) |
| Zero-Shot Coordination among LLM Agents (Foerster group, Oxford) | arXiv 2611.06409, 4 November 2026; preprint | Convention without communication | Nine simplified cooperative environments including Tiny Hanabi and a 3x3 Hanabi variant; Grok 4.1 Fast and GPT-5.2 show high failure rates in 7 of 9 tasks; code agents show a self-play vs cross-play gap (fetched) | [arXiv HTML](https://arxiv.org/html/2611.06409v1) |
| LLM-Coordination | arXiv 2310.03903, October 2023 | Pure coordination games (Overcooked-AI, Hanabi) | Prompted LLM agents coordinate with unseen partners (snippet) | [arXiv PDF](https://arxiv.org/pdf/2310.03903) |
| Interchangeable in Role, Not in History | arXiv 2609.05279, 4 September 2026; preprint | Handoff and team-member replacement | Cooperative cooking, wildfire response, medical QA; replacing a member of a formed team falls short of the original team in every setting and the team sends more messages per unit of progress (fetched abstract) | [arXiv](https://arxiv.org/abs/2609.05279) |
| MultiAgentBench | March 2025; ACL 2025 | Topology (star, chain, tree, graph), collaboration and competition | See section 1 | [arXiv](https://arxiv.org/abs/2503.01935) |

- Collaboration Tax mechanism: the tax is attributed to a four-stage conversational cascade (ungrounded claims, failing to query the partner, not integrating both views, accepting answers without re-derivation), not a reasoning deficit. It decreases monotonically with model capability, is predictable from conversation features, and a prompt intervention targeting all four stages closes a substantial share of the gap. In heterogeneous pairs the tax moves toward the stronger partner (fetched abstract) — [arXiv](https://arxiv.org/abs/2608.22152)
- HiddenBench conclusion: scaling multi-agent AI requires teaching agents "to actively seek out missing knowledge, not just talk more" (snippet) — [ICML listing](https://icml.cc/virtual/2026/poster/62206)
- Zero-shot coordination detail: on the 3x3 Hanabi variant most text-agent failures come from mismatched assumptions about shared conventions; Gemini 3 Pro coordinates with itself by consistently picking one arbitrary convention, which fails with other agents; greater model capability or reasoning effort does not reliably produce better coordination. No weights were trained; the only optimisation was meta-learning a prompt text (a "coordination-friendly definition") (fetched) — [arXiv HTML](https://arxiv.org/html/2611.06409v1)
- Team-replacement detail: on the hardest cooking level the shortfall appears only after the team has worked together, holds across model families and temperatures, and adding planning-only members narrows it by two thirds (fetched abstract) — [arXiv](https://arxiv.org/abs/2609.05279)

### Inferences
- Mapping of what I found onto the structures the team named: information pooling (HiddenBench, Collaboration Tax, CooperBench); shared resources (CalBench, STORM's shared workspace); convention without communication (Hanabi studies, Zero-Shot Coordination); handoff (team-replacement study); interface agreement (AsynCodeBench dependencies, and only implicitly). Review/oversight, delegation and mixed-motive structures were not covered by sources I verified.
- The Collaboration Tax and HiddenBench both use the same control the planned environment needs: a single agent given all the information. Both report that the team falls short of that control, so the planned single-agent-with-all-repos baseline should be expected to win at first, and the interesting training signal is how far the gap closes.
- "Fail to query the partner" (Collaboration Tax), "fail to ask for clarification" at 11.65% (MAST) and "seek out missing knowledge" (HiddenBench) are three independent reports of the same behaviour gap: agents do not ask. A reward that only scores final tests may not teach asking; logging whether a needed question was asked would allow diagnosis.

### Gaps
- Negotiation and mixed-motive benchmarks, multi-agent debate evaluations, and Overcooked-style LLM benchmarks such as Collab-Overcooked were not retrieved with verifiable sources this session. The team-replacement paper uses Collab-Overcooked and Hanabi according to a search snippet only.
- Exact scores in the Zero-Shot Coordination paper are in figures and appendix tables that I could not read.
- MASBench and CalBench numeric results were not read.

## 3. When do multi-agent LLM systems beat a single agent at equal budget, and what failure taxonomies exist?

### Takeaway
Under matched compute, published comparisons mostly find a single agent matches or beats a team, with the benefit of teams depending on task structure: positive on decomposable, loosely coupled work and strongly negative on sequential, tightly coupled work. MAST is the standard failure taxonomy (14 modes; specification 41.77%, inter-agent misalignment 36.94%, verification 21.30%), and CooperBench adds a coding-specific one.

### Cited Findings

**Equal-budget comparisons**
- Tran and Kiela, "Single-Agent LLMs Outperform Multi-Agent Systems on Multi-Hop Reasoning Under Equal Thinking Token Budgets" (arXiv 2604.02460, 2 April 2026; preprint): under a fixed reasoning-token budget, single-agent systems "consistently match or outperform MAS on multi-hop reasoning tasks". Uses a Data Processing Inequality argument and predicts teams become competitive when a single agent's context utilisation degrades or more compute is spent. Reports artefacts in API-based budget control (especially Gemini 2.5) that can inflate apparent multi-agent gains (fetched abstract) — [arXiv](https://arxiv.org/abs/2604.02460)
- Kim et al., "Towards a Science of Scaling Agent Systems" (arXiv 2512.08296, 9 December 2025, v3 8 April 2026; preprint): 260 configurations, six agentic benchmarks, five architectures (single agent plus Independent, Centralized, Decentralized, Hybrid), three LLM families. Performance change vs the single-agent baseline ranges from +80.8% on decomposable financial reasoning to -70.0% on sequential planning. A predictive model reaches cross-validated R² = 0.373 (0.413 with a task-grounded capability metric) and identifies the best architecture for 87% of held-out configurations. Architectures without centralized verification propagate errors more (fetched abstract) — [arXiv](https://arxiv.org/abs/2512.08296)
- "At Equal Inference Cost, Multi-Agent Structure Does Not Beat a Single Frozen Agent" (arXiv 2609.04217; preprint): with total LLM calls fixed, a Planner-Executor-Critic team on a frozen 7B backbone scores 0.769 vs 0.754 for the single agent on ALFWorld, not significant (p = 0.80), while using 1.8 times as many evaluation calls; all gain comes from the executor; with 2 to 3 times more compute the team only matches the single agent; on WebShop the team trends worse (fetched abstract) — [arXiv](https://arxiv.org/abs/2609.04217). Caution: the abstract page as fetched gave a submission date of 25 June 2026, which does not match a 2609 identifier; treat the date as unverified.
- "Rethinking Multi-Agent Collaboration: When More Is Less" (arXiv 2609.19759, 17 September 2026; preprint): multi-agent collaboration helps most on long-horizon tasks with sparse dependencies; single-agent setups work better on tightly coupled, sequential workflows; more agents or deeper recursion does not consistently help (fetched abstract, no numbers) — [arXiv](https://arxiv.org/abs/2609.19759)
- Anthropic engineering blog (13 June 2025; vendor blog, internal eval, not peer reviewed): a lead-agent system with Claude Opus 4 and Claude Sonnet 4 subagents outperformed single-agent Opus 4 by 90.2% on an internal research eval; agents use about 4× the tokens of chat and multi-agent systems about 15×; on BrowseComp token usage alone explained 80% of performance variance. The post says domains where agents must share context or have many inter-dependencies are a poor fit, and that "most coding tasks involve fewer truly parallelizable tasks than research" (fetched) — [Anthropic](https://www.anthropic.com/engineering/multi-agent-research-system)
- Counter-example on cost: the CODS 2025 AssetOpsBench challenge retrospective found single-agent executions consumed nearly twice the tokens of multi-agent executions on average, which the authors attribute to scenario mix (snippet) — [arXiv PDF](https://arxiv.org/pdf/2605.08518)
- In coding specifically, CooperBench reports two agents retain 0.59 of pooled solo success (fetched) — [arXiv HTML](https://arxiv.org/html/2601.13295)

**MAST failure taxonomy (Cemri et al., "Why Do Multi-Agent LLM Systems Fail?", arXiv 2503.13657; NeurIPS 2025 listing)**

Frequencies as read from v2 of the paper (22 April 2025) — [arXiv HTML v2](https://arxiv.org/html/2503.13657v2); venue per [NeurIPS 2025 listing](https://neurips.cc/virtual/2025/122442):

| Category | Failure mode | Frequency |
|---|---|---|
| Specification issues (41.77%) | FM-1.1 Disobey task specification | 10.98% |
| | FM-1.2 Disobey role specification | 0.5% |
| | FM-1.3 Step repetition | 17.14% |
| | FM-1.4 Loss of conversation history | 3.33% |
| | FM-1.5 Unaware of termination conditions | 9.82% |
| Inter-agent misalignment (36.94%) | FM-2.1 Conversation reset | 2.33% |
| | FM-2.2 Fail to ask for clarification | 11.65% |
| | FM-2.3 Task derailment | 7.15% |
| | FM-2.4 Information withholding | 1.66% |
| | FM-2.5 Ignored other agent's input | 0.17% |
| | FM-2.6 Reasoning-action mismatch | 13.98% |
| Task verification (21.30%) | FM-3.1 Premature termination | 7.82% |
| | FM-3.2 No or incomplete verification | 6.82% |
| | FM-3.3 Incorrect verification | 6.66% |

- Scope in v2: 200+ execution traces, seven frameworks (HyperAgent, AG2, MetaGPT, ChatDev, AppWorld for taxonomy development; OpenManus and Magentic-One for generalisation). Human inter-annotator kappa 0.88; an o1 few-shot LLM annotator reaches kappa 0.77 with humans (accuracy 0.94) — [arXiv HTML v2](https://arxiv.org/html/2503.13657v2)
- Version conflict: a summary of v3 (26 October 2025) gives 1642 annotated traces and different frequencies (for example FM-1.1 at 11.8%, FM-1.5 at 12.4%, FM-2.2 at 6.8%, inter-agent misalignment at 32.3%). These are from a third-party summary and were not checked against v3 (snippet) — [alphaXiv v3 overview](https://www.alphaxiv.org/overview/2503.13657v3). Quote frequencies with the version number.
- ChatDev reaches 33.33% correctness on ProgramDev in Figure 1; prompt and topology interventions gave +9.4% (role specification changes) and +15.6% absolute (added high-level verification step), which the authors treat as insufficient — [arXiv HTML v2](https://arxiv.org/html/2503.13657v2)

**Other failure taxonomies**
- CooperBench (coding, two agents): symptom and cause percentages listed in section 1 — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Collaboration Tax: four-stage conversational cascade (section 2) — [arXiv](https://arxiv.org/abs/2608.22152)
- "Which Agent Causes Task Failures and When?" (arXiv 2505.00212, May 2025) addresses automated failure attribution to a specific agent and step; title seen only, contents not read — [arXiv PDF](https://arxiv.org/pdf/2505.00212)

### Inferences
- The consistent pattern across Kim et al., "When More Is Less" and the Anthropic post is that team benefit tracks decomposability, and coding is named as a poor fit. In the planned environment the team structure is forced by information partition, not chosen for speed, so the right framing is "cost of decentralisation" (as in Collaboration Tax) and not "does a team beat one agent".
- Tran and Kiela's prediction gives a design lever: a single agent with all four repos wins unless its context utilisation degrades. If the four services together fit comfortably in one context, expect the single agent to dominate. This baseline is an upper reference for the team, and the team-vs-single gap is the headline metric.
- Equal-budget accounting has at least three definitions in this literature: thinking tokens (Tran and Kiela), LLM calls (iso-call paper), and total tokens (planned environment). Tran and Kiela report that API budget controls are unreliable for some providers, so the environment should meter tokens itself.
- MAST's verification category (21.30%) and its +15.6% gain from adding a verification step suggest that giving each agent runnable local tests will remove a class of failures that are not about coordination, which keeps the measured signal on coordination.

### Gaps
- No equal-token-budget team-vs-single comparison was found for cross-service coding specifically.
- Tran and Kiela's numeric tables and Kim et al.'s per-architecture error-amplification figures were not read (abstract only).
- MAST v3 frequencies need checking against the paper; the v2 page was truncated before the appendices.
- Cognition's "Don't Build Multi-Agents" essay (June 2025 per most secondary sources) was not fetched; only secondary descriptions were seen, so it is not cited as a finding.

## 4. What work exists on training LLMs for multi-agent coordination?

### Takeaway
Training work exists but is young: self-play RL on games (MARSHAL, ICLR 2026), multi-agent variants of GRPO with per-agent normalisation, counterfactual and Shapley-style credit assignment, and one industrially reported orchestrator-training method (Kimi PARL). I found no work that fine-tunes LLMs against a partner population for zero-shot coordination, and none that trains peer agents with partitioned views of a codebase.

### Cited Findings
- MARSHAL: "Incentivizing Multi-Agent Reasoning via Self-Play with Strategic LLMs" (arXiv 2510.15414; ICLR 2026): self-play across cooperative and competitive games with a turn-level advantage estimator for credit assignment and agent-specific advantage normalisation for stable training. A Qwen3-4B agent generalises to held-out games with up to 28.7% performance improvements; plugged into multi-agent systems (AutoGen, MAD) gains are up to 10.0% on AIME, 6.6% on GPQA-Diamond and 3.5% on average. Code at github.com/thu-nics/MARSHAL (snippet from abstract) — [arXiv](https://arxiv.org/abs/2510.15414v3), [ICLR proceedings](https://proceedings.iclr.cc/paper_files/paper/2026/hash/0b1b52b624ce69e0241eac91f8df0bce-Abstract-Conference.html)
- Survey: "Reinforcement Learning for LLM-based Multi-Agent Systems through Orchestration Traces" (Chenchen Zhang, independent researcher; arXiv 2605.02801, 4 May 2026; preprint, single author). Useful as an index; it reports no benchmark scores for the methods (fetched, truncated) — [arXiv HTML](https://arxiv.org/html/2605.02801v1). Items it lists:
  - Dr. MAS: revisits IPPO vs MAPPO vs GRPO for LLM teams and finds GRPO's group-normalised advantage becomes unstable at the agent level without agent-wise normalisation.
  - M-GRPO: hierarchical GRPO decomposition with role-level credit. MALT: planner/executor/critic role-level credit. MATPO: single-LLM dual-role policy optimisation with tools.
  - One entry estimates message-level counterfactual credit and is described as the only retained entry to do so; another uses Shapley-based agent-level credit.
  - Kimi K2.5 Parallel-Agent Reinforcement Learning (PARL): trains an orchestrator for an agent swarm of up to 100 sub-agents and 1,500 coordinated steps; K2.6 reportedly 300 sub-agents and 4,000 steps. Reward is r_perf + λ₁·r_parallel + λ₂·r_finish with staged annealing, and a "Critical-Steps" metric penalises pseudo-parallelism. The survey notes these are publicly reported deployment figures, not independently reproduced.
  - Open problems named: credit under uniform allocation becomes fragile as traces lengthen; orchestrator spawn-decision credit is not identifiable from on-policy rollouts alone; Shapley-style credit over a dynamic agent set is unsolved; no RL method for the stopping decision in its curated pool; how to weight and compose sparse and dense reward levels is unresolved.
- Counterfactual Credit Policy Optimization for Multi-Agent Collaboration (arXiv 2603.21563, March 2026) and COSAC: Counterfactual Credit Assignment in Sequential Cooperative Teams (arXiv 2604.17693, April 2026): titles and topic seen only (snippet) — [CCPO](https://arxiv.org/pdf/2603.21563), [COSAC](https://arxiv.org/pdf/2604.17693)
- LangMARL (arXiv April 2026; EMNLP 2026 main): uses natural-language feedback as the medium for agent-level credit assignment in place of scalar rewards (snippet) — [ACL Anthology](https://aclanthology.org/2026.emnlp-main.1837/)
- Speaking the Language of Teamwork: LLM-Guided Credit Assignment in Multi-Agent Reinforcement Learning (arXiv 2502.03723, February 2025): uses an LLM to assign credit for conventional MARL agents; the reverse direction from training LLMs (title seen only) — [arXiv PDF](https://arxiv.org/pdf/2502.03723)
- Partner-population methods: a targeted search returned the classic non-LLM work, "Other-Play" for Zero-Shot Coordination (Hu et al., ICML 2020) — [PMLR](https://proceedings.mlr.press/v119/hu20a/hu20a.pdf) — and a 2025 non-LLM result that cross-environment training improves zero-shot cross-play — [arXiv 2504.12714](https://arxiv.org/pdf/2504.12714). "A Generalist Hanabi Agent" (ICLR 2025) fine-tunes a language model on Hanabi but is trained for play, not for partner diversity (snippet) — [ICLR 2025 proceedings](https://proceedings.iclr.cc/paper_files/paper/2025/file/5f7c6dac2357453eb46eb0bdcce0af12-Paper-Conference.pdf)
- The Oxford zero-shot coordination paper (November 2026) trains no weights; it meta-learns prompt text with cross-play score as fitness and reports modest cross-play gains (fetched) — [arXiv HTML](https://arxiv.org/html/2611.06409v1)

### Inferences
- A team-level reward from hidden integration tests is the sparsest form of credit. The cited work suggests three practical mitigations for the planned environment: per-agent or per-role advantage normalisation (Dr. MAS, MARSHAL), per-dependency scoring so each contract check credits the two agents involved (AsynCodeBench-style), and counterfactual message credit (replay with a message removed), which the survey marks as rare and open.
- If all four agents are copies of one policy trained in self-play, the Oxford results predict private conventions that fail with other partners (Gemini 3 Pro's self-consistent arbitrary convention). Evaluating with held-out partner models (cross-play) is the standard guard; nobody appears to have published population training for LLMs, so this is both a risk and a possible contribution.
- Kimi PARL's r_parallel term is a published example of shaping reward for a coordination behaviour, with annealing to avoid the shaped behaviour becoming the goal. A comparable shaped term for messaging would risk rewarding chatter; CooperBench found up to about 20% of steps going to communication with no success gain.
- The team-replacement study implies trained teams may accumulate history-specific conventions, so swapping one trained agent for another is a meaningful robustness test.

### Gaps
- No verified source for fictitious co-play, other-play or other partner-population methods applied to LLM fine-tuning. One targeted search found none; absence is not confirmed.
- MARSHAL's full results (win rates, cooperative-game results such as Hanabi) were not read; the ICLR PDF could not be parsed locally.
- Dr. MAS, M-GRPO, MALT, MATPO, CCPO and COSAC were not read directly; descriptions come from the survey or titles. arXiv identifiers for the first four were not visible.
- Kimi PARL details come via a single-author survey citing vendor reports; no primary technical report was read.
- No work found on RL training of peer coding agents with private repository views.

## 5. What are documented pitfalls in multi-agent benchmark design?

### Takeaway
The best-documented pitfalls are unmatched compute in team-vs-single comparisons, tasks where communication is not actually required, benchmark contamination from public repositories, and judge-model scores that diverge from deterministic outcomes. Each has a direct design counter-measure for the planned environment.

### Cited Findings
- Unmatched compute: almost all reported multi-agent gains are obtained with more inference than the single-agent comparison; when calls are fixed the gain is not significant (p = 0.80) — [arXiv 2609.04217](https://arxiv.org/abs/2609.04217). Tran and Kiela reach the same conclusion for thinking tokens and add that API-based budget control has artefacts (especially Gemini 2.5) that inflate apparent multi-agent gains — [arXiv 2604.02460](https://arxiv.org/abs/2604.02460)
- Tokens dominate outcomes: on BrowseComp, token usage alone explained 80% of performance variance (vendor blog) — [Anthropic](https://www.anthropic.com/engineering/multi-agent-research-system)
- Communication not needed: in CooperBench, with-communication and no-communication success after merge resolution is 17.14% vs 17.64%, while agents spend up to about 20% of steps on messages — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Task-level scores hide coordination failures: AsynCodeBench reports that task-level scores can hide unresolved coordination failures and that coding skill does not predict collaboration skill (snippet) — [arXiv HTML](https://arxiv.org/html/2609.32662)
- Judge-model scoring: MultiAgentBench reports a case where Meta-Llama-3.1-70B has a Minecraft Coordination Score of 75.00 but a Task Score of 0.21; a later paper (AgentCollabBench) argues LLM-judged milestone and coordination scores can overcredit outputs that fail deterministic checks (snippet; second-hand description of both papers) — [ACL Anthology PDF](https://aclanthology.org/2025.acl-long.421.pdf). AgentJudgeBench (arXiv 2608.26623, 2026) notes judge reliability in agentic tool-calling has proceeded without a basic calibration check (snippet) — [arXiv PDF](https://arxiv.org/pdf/2608.26623)
- LLM annotators are imperfect even when validated: MAST's o1 annotator reaches kappa 0.77 few-shot and only 0.58 zero-shot against human experts — [arXiv HTML v2](https://arxiv.org/html/2503.13657v2)
- Contamination: "The SWE-Bench Illusion" (arXiv 2506.12286; ICSE 2026 SEIP track): models identify buggy file paths from issue text alone with up to 76% accuracy on SWE-Bench vs up to 53% on repositories not in SWE-Bench, with higher verbatim similarity on SWE-Bench Verified, indicating memorisation (snippet) — [ICSE 2026 listing](https://conf.researchr.org/details/icse-2026/icse-2026-software-engineering-in-practice/29/The-SWE-Bench-Illusion-When-State-of-the-Art-LLMs-Remember-Instead-of-Reason), [arXiv](https://arxiv.org/html/2506.12286v2)
- Test leakage: CooperBench withholds unit tests and gold solutions from agents to prevent leakage — [arXiv HTML](https://arxiv.org/html/2601.13295)
- Deferred conflict cost: isolating agents in git worktrees postpones conflict resolution to a costly merge step, and CooperBench needs a learned merge resolver inside its scorer, which puts a model in the scoring path — [arXiv 2605.20563](https://arxiv.org/abs/2605.20563), [arXiv HTML](https://arxiv.org/html/2601.13295)
- Self-play overestimates coordination: independently generated policies show a self-play vs cross-play gap — [arXiv HTML](https://arxiv.org/html/2611.06409v1)
- Small benchmark size: AsynCodeBench has 19 tasks and 52 dependencies — [arXiv](https://arxiv.org/abs/2609.32662)

### Inferences
- Design checklist that follows from the findings: (1) meter total tokens inside the harness and enforce the same cap for all three baselines; (2) for every task, verify that the no-messaging team cannot pass (a "communication necessity" check) and that the all-repos single agent can pass (a solvability check), mirroring the Collaboration Tax "solo-tractable" criterion; (3) score only with deterministic hidden tests, and report per-contract pass rates alongside the end-to-end result; (4) use a purpose-written codebase so nothing is memorised, and keep contract tests hidden; (5) report cross-play with held-out partner models; (6) report messages and tokens spent on communication.
- A synthetic company codebase avoids contamination but introduces a different risk the sources do not address: once tasks are used for RL training, the trained policy memorises that codebase. Held-out services or procedurally varied contracts would be needed for evaluation.
- Disjoint service ownership removes the merge step and with it the learned merge resolver, so scoring can stay fully deterministic.

### Gaps
- Cost per episode: I found no source that reports dollar or token cost per episode for a multi-agent coding benchmark. The only cost figures retrieved are Anthropic's 4× and 15× multipliers and the 1.8× evaluation calls in the iso-call paper.
- No single published checklist for multi-agent benchmark validity was found; the checklist above is my synthesis.
- A 2026 blog claims OpenAI stopped reporting SWE-bench Verified over contamination; I found no primary source and it is not relied on — [blog](https://www.buildmvpfast.com/blog/benchmark-contamination-ai-coding-leaderboard-swe-bench-2026)
- AgentCollabBench was seen only through a search summary without its own URL; its claims are second-hand.

## 6. Is there a published taxonomy of coordination or interdependence types to ground a taxonomy of coordination structures?

### Takeaway
Yes. Two classics fit: Thompson (1967) orders interdependence as pooled, sequential and reciprocal, and Malone and Crowston (1994) define coordination as managing dependencies between activities and classify the dependencies. Recent LLM work arrives at compatible distinctions empirically (decomposable vs sequential vs tightly coupled).

### Cited Findings
- Malone and Crowston, "The Interdisciplinary Study of Coordination", ACM Computing Surveys 26(1), 1994, pp. 87 to 119: frames coordination as "managing dependencies between activities" and analyses processes for managing shared resources, producer/consumer relationships, simultaneity constraints and task/subtask dependencies; draws on computer science, organisation theory, operations research, economics, linguistics and psychology (snippet; the PDF could not be parsed locally) — [Crowston publication page](https://crowston.syr.edu/node/54), [full-text PDF](https://crowston.syr.edu/sites/default/files/acmcs94.pdf), [MIT working paper version](https://dspace.mit.edu/bitstream/handle/1721.1/2500/SWP-3630-31204001-CCS-157.pdf?sequence=1)
- Thompson, Organizations in Action (1967): three interdependence types, pooled, sequential and reciprocal. Sequential is where one unit's output is the next unit's required input (assembly line); reciprocal adds a cyclical flow where outputs go back and forth (secondary source) — [Chron summary](https://smallbusiness.chron.com/three-types-interdependence-organizational-structure-1764.html)
- Thompson's types are ordered by amount of interdependence (pooled less than sequential less than reciprocal), though he did not specify by how much, and McCann and Galbraith (1981) challenged the construct on that basis (secondary reconstruction of the book's propositions) — [Nickols, Thompson's propositions](https://www.nickols.us/ThompsonPropositions.pdf)
- Common mapping of coordination mode to type: standardisation for pooled, planning for sequential, mutual adjustment for reciprocal (study-aid summary; treat as the usual reading, not Thompson's wording) — [StudySmart summary](https://studysmart.ai/en/summaries/organisational-design/incorporated-interdependencies-costs)
- Empirical echoes in LLM work: gains of +80.8% on decomposable tasks vs -70.0% on sequential planning — [arXiv 2512.08296](https://arxiv.org/abs/2512.08296); benefit on sparse-dependency long-horizon tasks vs loss on tightly coupled sequential workflows — [arXiv 2609.19759](https://arxiv.org/abs/2609.19759); AsynCodeBench models tasks as directed dependency graphs between agents — [arXiv](https://arxiv.org/abs/2609.32662); the Collaboration Tax groups tasks "by source of grounding friction" — [arXiv](https://arxiv.org/abs/2608.22152)

### Inferences
- A workable grounding for the environment's task taxonomy, combining the two classics:

| Planned coordination structure | Thompson type | Malone and Crowston dependency | Cross-service example |
|---|---|---|---|
| Information pooling | Pooled | Task/subtask (shared goal) | Each owner reports a fact needed for a joint decision |
| Handoff | Sequential | Producer/consumer (prerequisite) | Service A must ship a field before B can consume it |
| Interface agreement | Reciprocal | Producer/consumer (usability, both sides adjust) | Two owners negotiate a request and response schema |
| Shared resources | Pooled with contention | Shared resource | Shared schema, port, quota or migration slot |
| Synchronised change | Reciprocal | Simultaneity constraint | Breaking change that must land in two services together |
| Delegation and review | Sequential or reciprocal | Task/subtask | One owner specifies, another implements, first verifies |

- "Convention without communication" and "mixed motive" do not map cleanly onto either classic, since both assume a cooperative organisation that can communicate; the zero-shot coordination literature (Other-Play and successors) and game theory are the better grounding for those two.
- Thompson's ordering yields a testable prediction for the environment: the value of messaging (with-messaging minus without-messaging score) should rise from pooled to sequential to reciprocal tasks. Reporting results by interdependence type would make the benchmark comparable with the decomposable-vs-sequential findings above.

### Gaps
- I could not read the Malone and Crowston PDF directly (no PDF text extraction available on this machine), so the sub-types of producer/consumer dependency (prerequisite, transfer, usability) and whether the paper cites Thompson are from my background knowledge and not verified this session.
- Thompson's book is cited through secondary summaries only; no primary text was available online.
- Not retrieved: Van de Ven, Delbecq and Koenig (1976) on team interdependence, Crowston's later typology revisions, CSCW and team-cognition taxonomies (for example shared mental models, transactive memory), and any LLM paper that explicitly adopts Thompson or Malone and Crowston. One search for the classics returned nothing on these.

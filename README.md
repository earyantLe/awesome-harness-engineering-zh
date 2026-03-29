# Awesome Harness Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of articles, playbooks, benchmarks, specifications, and open-source projects for harness engineering: the practice of shaping the environment around AI agents so they can work reliably.

Harness engineering sits at the intersection of context engineering, evaluation, observability, orchestration, safe autonomy, and software architecture. This list focuses on resources that make agents more dependable in real workflows, especially long-running coding and research tasks.

Generic agent tooling is out of scope unless the page directly covers harness design, context management, evaluation, runtime control, or other reliability-critical harness primitives.

## Contents

- [Foundations](#foundations)
- [Context, Memory & Working State](#context-memory--working-state)
- [Constraints, Guardrails & Safe Autonomy](#constraints-guardrails--safe-autonomy)
- [Specs, Agent Files & Workflow Design](#specs-agent-files--workflow-design)
- [Evals & Observability](#evals--observability)
- [Benchmarks](#benchmarks)
- [Runtimes, Harnesses & Reference Implementations](#runtimes-harnesses--reference-implementations)
- [Contributing](#contributing)

## Foundations

- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) - OpenAI's flagship field report on building a large application with Codex using architectural constraints, repo-local instructions, browser validation, and telemetry.
- [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) - Anthropic's core article on initializer agents, feature lists, `init.sh`, self-verification, and handoff artifacts across many context windows.
- [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) - Anthropic follow-up focused on improving long-running app generation with better task state and evaluator design.
- [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) - LangChain's concise framing of an agent as model plus harness, with prompts, tools, middleware, orchestration, and runtime infrastructure.
- [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) - Thoughtworks' framing of harness work into context engineering, architectural constraints, and "garbage collection" against entropy.
- [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) - Anthropic's broader guide to workflows, agents, tools, and when structured systems outperform raw prompting.
- [Skill Issue: Harness Engineering for Coding Agents](https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents) - A practical argument that weak results from coding agents are often harness problems rather than model problems.
- [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) - Inngest's case for treating state, retries, traces, and concurrency as first-class infrastructure.

## Context, Memory & Working State

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) - Anthropic's guidance on managing the context window as a working memory budget rather than a dumping ground.
- [Context Engineering for AI Agents: Lessons from Building Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) - Manus' detailed playbook on KV-cache locality, tool masking, filesystem memory, and keeping useful failures in-context.
- [Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) - Thoughtworks guidance on shaping the task environment so coding agents can stay grounded and productive.
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering) - HumanLayer patterns for reducing context drift and making coding sessions easier to resume.
- [Context-Efficient Backpressure for Coding Agents](https://www.humanlayer.dev/blog/context-efficient-backpressure) - HumanLayer's ideas for preventing agents from burning context on noisy or low-value work.
- [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) - A practical guide to creating durable, repo-local instructions that agents can repeatedly follow.

## Constraints, Guardrails & Safe Autonomy

- [Beyond permission prompts: making Claude Code more secure and autonomous](https://www.anthropic.com/engineering/claude-code-sandboxing) - Anthropic on reducing approval friction without losing control through better sandboxing and policy design.
- [Code execution with MCP: building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp) - Anthropic's approach to giving agents controlled execution power through explicit, inspectable tool boundaries.
- [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) - Anthropic's guidance on tool interfaces that are easier for models to call correctly and safely.
- [Assessing internal quality while coding with an agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) - Thoughtworks on moving quality checks into the loop instead of relying on after-the-fact manual review.
- [Anchoring AI to a reference application](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html) - Thoughtworks on constraining agents with concrete exemplars so they produce more consistent output.
- [Humans and Agents in Software Engineering Loops](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) - A clear mental model for where humans should strengthen the harness instead of micromanaging every artifact.
- [Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices) - Anthropic's practical recommendations for repo structure, checkpoints, validation, and delegation in agentic coding workflows.

## Specs, Agent Files & Workflow Design

- [AGENTS.md](https://github.com/agentsmd/agents.md) - A lightweight open format for repo-local instructions that tell agents how to work inside a codebase.
- [agent.md](https://github.com/agentmd/agent.md) - A related standardization effort for machine-readable agent instructions across projects and tools.
- [GitHub Spec Kit](https://github.com/github/spec-kit) - GitHub's toolkit for spec-driven development, useful when you want agents to execute against explicit product and engineering specs.
- [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - Thoughtworks on why strong specs make AI-assisted software delivery more dependable.
- [12 Factor Agents](https://www.humanlayer.dev/blog/12-factor-agents) - HumanLayer's operating principles for production agents, including explicit prompts, state ownership, and clean pause-resume behavior.
- [12-Factor AgentOps](https://www.12factoragentops.com/) - An operations-oriented companion focused on context discipline, validation, and reproducible agent workflows.

## Evals & Observability

- [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/) - OpenAI's concrete guide to turning agent traces into repeatable evals with JSONL logs and deterministic checks.
- [Agent evals](https://platform.openai.com/docs/guides/agent-evals) - OpenAI's product guide for measuring agent quality with reproducible task-level and workflow-level evaluations.
- [Evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) - OpenAI's general guide to building eval suites that match real-world distributions and catch regressions early.
- [Trace grading](https://platform.openai.com/docs/guides/trace-grading) - OpenAI documentation on grading agent traces directly, which is especially helpful for long multi-step tasks.
- [Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) - Anthropic's guidance on what to measure when agents have many possible trajectories to success or failure.
- [Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise) - Anthropic on how runtime configuration can move coding benchmark scores by more than many leaderboard gaps.
- [Evaluating Deep Agents: Our Learnings](https://blog.langchain.com/evaluating-deep-agents-our-learnings/) - LangChain's practical breakdown of single-step, full-run, and multi-turn eval design for stateful agents.
- [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) - LangChain's evidence that harness changes alone can significantly improve benchmark performance.

## Benchmarks

These benchmarks are especially useful when you want to compare harness quality, not just model quality. They stress context handling, tool calling, environment control, verification logic, and the runtime scaffolding around the model.

- [HAL: Holistic Agent Leaderboard](https://hal.cs.princeton.edu/) - A benchmark and leaderboard for agent systems with attention to reliability, cost, and broad task coverage, making it useful for comparing end-to-end harness behavior.
- [OSWorld](https://os-world.github.io/) - A real computer-use benchmark with 369 tasks across Ubuntu, Windows, and macOS, complete with initial-state setup and execution-based evaluators, making it excellent for testing desktop and multimodal harnesses.
- [SWE-bench Verified](https://www.swebench.com/) - A strong benchmark for software engineering agents working against real GitHub issues and tests, which makes harness choices around retrieval, patching, and validation highly visible.
- [AppWorld](https://appworld.dev/) - A controllable world of apps and people for benchmarking interactive coding agents, with state-based and execution-based unit tests that surface harness quality around planning, code generation, and collateral-damage control.
- [AgentBench](https://github.com/THUDM/AgentBench) - A cross-environment benchmark spanning OS, databases, knowledge graphs, web browsing, and more, useful for seeing whether a harness generalizes beyond one narrow task loop.
- [tau2-bench](https://github.com/sierra-research/tau2-bench) - A benchmark for realistic, multi-step agent tasks where success depends on tool use and execution quality rather than a single-shot answer.
- [WebArena-Verified](https://github.com/ServiceNow/webarena-verified) - A verified web-agent benchmark with curated tasks and deterministic evaluators over agent responses and captured network traces, making it a good fit for measuring web-facing harnesses.
- [WorkArena](https://github.com/ServiceNow/WorkArena) - A benchmark for browser agents on common knowledge-work tasks, useful for comparing harnesses on realistic enterprise-style web workflows instead of toy browser tasks.
- [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) - A benchmark for general AI assistants that is often used to compare harness-level choices around tools, planning, verification, and long-horizon autonomy.
- [Terminal-Bench](https://www.tbench.ai/) - A benchmark suite for terminal-native agents operating in shells, filesystems, and verification-heavy environments, which is especially useful for comparing coding-agent harnesses.
- [Introducing Terminal-Bench 2.0 and Harbor](https://www.tbench.ai/news/announcement-2-0) - The Terminal-Bench 2.0 announcement, useful for understanding the harder tasks and generalized evaluation harness behind Harbor.

## Runtimes, Harnesses & Reference Implementations

- [Agent Frameworks, Runtimes, and Harnesses, Oh My!](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/) - LangChain's decomposition of what belongs in a framework, a runtime, and a harness.
- [Building agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) - Anthropic's guide to a production-oriented agent SDK with sessions, tools, and orchestration support.
- [How we built our multi-agent research system](https://www.anthropic.com/engineering/built-multi-agent-research-system) - Anthropic's architecture write-up for a multi-agent system with separation of roles and structured coordination.
- [deepagents](https://github.com/langchain-ai/deepagents) - LangChain's open-source project for building deeper, longer-running agents with middleware and harness patterns.
- [SWE-agent](https://github.com/SWE-agent/SWE-agent) - A mature research coding agent that makes the harness, prompt, tools, and environment design directly inspectable.
- [SWE-ReX](https://github.com/SWE-agent/SWE-ReX) - Sandboxed code execution infrastructure for AI agents, useful when harness work starts to merge into execution runtime design.
- [AgentKit](https://github.com/inngest/agent-kit) - Inngest's TypeScript toolkit for building durable, workflow-aware agents on top of event-driven infrastructure.
- [Harbor](https://github.com/laude-institute/harbor) - A generalized harness for evaluating and improving agents at scale, released alongside Terminal-Bench 2.0.
- [Terminal-Bench](https://github.com/laude-institute/terminal-bench) - The open-source terminal benchmark implementation behind many shell-native agent evaluations.

## Contributing

Contributions are welcome. Please prefer resources that are:

- Specific about how agents are constrained, evaluated, resumed, observed, or orchestrated
- Original implementations, primary-source articles, or high-signal technical write-ups
- Useful to practitioners building real harnesses instead of generic AI commentary

If two links say the same thing, prefer the more primary, practical, and implementation-oriented one.

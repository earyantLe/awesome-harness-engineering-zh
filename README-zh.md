# Awesome Harness Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> 一份精选的文章、实践指南、基准测试、规范和开源项目列表，用于控制框架工程（harness engineering）：即围绕 AI 智能体构建工作环境，使其能够可靠地工作。

控制框架工程位于上下文工程、评估、可观测性、编排、安全自主性和软件架构的交叉点。本列表专注于让智能体在实际工作流中更加可靠的资源，特别是长时运行的编码和研究任务。

除非页面直接涉及控制框架设计、上下文管理、评估、运行时控制或其他可靠性关键的控制框架原语，否则通用的智能体工具不在范围内。

## 目录

- [基础](#基础)
- [上下文、内存和工作状态](#上下文内存和工作状态)
- [约束、护栏和安全自主性](#约束护栏和安全自主性)
- [规格、智能体文件和工作流设计](#规格智能体文件和工作流设计)
- [评估和可观测性](#评估和可观测性)
- [基准测试](#基准测试)
- [运行时、控制框架和参考实现](#运行时控制框架和参考实现)
- [贡献](#贡献)
- [许可证](#许可证)

## 基础

- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) - OpenAI 的旗舰实地报告，讲述如何通过架构约束、仓库级指令、浏览器验证和遥测技术，使用 Codex 构建大型应用。
- [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) - Anthropic 的核心文章，介绍初始化智能体、功能列表、`init.sh`、自验证以及跨多个上下文窗口的交接产物。
- [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) - Anthropic 的后续文章，专注于通过更好的任务状态和评估器设计来改进长时运行的应用生成。
- [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) - LangChain 简洁地将智能体框架为模型加控制框架，包含提示、工具、中间件、编排和运行时基础设施。
- [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) - Thoughtworks 将控制框架工作分为上下文工程、架构约束和针对熵的"垃圾回收"。
- [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) - Anthropic 关于工作流、智能体、工具的更全面指南，以及何时结构化系统胜过原始提示。
- [Skill Issue: Harness Engineering for Coding Agents](https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents) - 一份实用的论证，说明编码智能体的弱结果通常是控制框架问题而非模型问题。
- [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) - Inngest 主张将状态、重试、追踪和并发作为一等基础设施。

## 上下文、内存和工作状态

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) - Anthropic 关于将上下文窗口管理为工作内存预算而非转储场的指导。
- [Context Engineering for AI Agents: Lessons from Building Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) - Manus 的详细实践指南，涵盖 KV 缓存局部性、工具掩码、文件系统内存，以及将有用的失败保留在上下文中。
- [Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) - Thoughtworks 关于塑造任务环境的指导，使编码智能体能够保持专注和高效。
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering) - HumanLayer 的模式，用于减少上下文漂移，使编码会话更容易恢复。
- [Context-Efficient Backpressure for Coding Agents](https://www.humanlayer.dev/blog/context-efficient-backpressure) - HumanLayer 关于防止智能体在嘈杂或低价值工作上浪费上下文的想法。
- [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) - 一份实用指南，介绍如何创建持久的、仓库级的指令，供智能体反复遵循。

## 约束、护栏和安全自主性

- [Beyond permission prompts: making Claude Code more secure and autonomous](https://www.anthropic.com/engineering/claude-code-sandboxing) - Anthropic 关于通过更好的沙箱和策略设计，在不失去控制的情况下减少审批摩擦。
- [Code execution with MCP: building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp) - Anthropic 通过显式的、可检查的工具边界，赋予智能体受控执行能力的方法。
- [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) - Anthropic 关于工具接口的指导，使模型更容易正确、安全地调用。
- [Assessing internal quality while coding with an agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) - Thoughtworks 关于将质量检查纳入循环中，而非依赖事后手动审查。
- [Anchoring AI to a reference application](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html) - Thoughtworks 关于用具体示例约束智能体，使其产生更一致的输出。
- [Humans and Agents in Software Engineering Loops](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) - 一个清晰的心智模型，说明人类应在何处加强控制框架，而非微观管理每个产物。
- [Claude Code: Best practices for agentic coding](https://code.claude.com/docs) - Anthropic 关于代理编码工作流中仓库结构、检查点、验证和委托的实用建议。

## 规格、智能体文件和工作流设计

- [AGENTS.md](https://github.com/agentsmd/agents.md) - 一个轻量级的开放格式，用于仓库级指令，告诉智能体如何在代码库中工作。
- [agent.md](https://github.com/agentmd/agent.md) - 一个相关的标准化工作，为跨项目和工具的机器可读智能体指令而设计。
- [GitHub Spec Kit](https://github.com/github/spec-kit) - GitHub 的规格驱动开发工具包，当你希望智能体根据明确的产品和工程规格执行时非常有用。
- [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - Thoughtworks 关于为什么强规格使 AI 辅助软件交付更加可靠。
- [12 Factor Agents](https://www.humanlayer.dev/blog/12-factor-agents) - HumanLayer 的生产智能体操作原则，包括显式提示、状态所有权和清晰的暂停 - 恢复行为。
- [12-Factor AgentOps](https://www.12factoragentops.com/) - 一个面向操作的伴侣，专注于上下文纪律、验证和可重现的智能体工作流。

## 评估和可观测性

- [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/) - OpenAI 关于将智能体追踪转化为可重复评估的具体指南，使用 JSONL 日志和确定性检查。
- [Agent evals](https://platform.openai.com/docs/guides/agent-evals) - OpenAI 的产品指南，用于使用可重现的任务级和工作流级评估来衡量智能体质量。
- [Evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) - OpenAI 关于构建与真实世界分布匹配并尽早捕获回归的评估套件的一般指南。
- [Trace grading](https://platform.openai.com/docs/guides/trace-grading) - OpenAI 关于直接对智能体轨迹进行评分的文档，这对长时多步骤任务特别有帮助。
- [Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) - Anthropic 关于当智能体有许多可能的成功或失败路径时应该测量什么的指导。
- [Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise) - Anthropic 关于运行时配置如何使编码基准测试分数的变化超过许多排行榜差距。
- [Evaluating Deep Agents: Our Learnings](https://blog.langchain.com/evaluating-deep-agents-our-learnings/) - LangChain 对单步、全运行和多轮评估设计的实际分解，针对有状态的智能体。
- [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) - LangChain 的证据表明，仅控制框架变更就可以显著提高基准测试性能。

## 基准测试

这些基准测试在你想要比较控制框架质量（而非仅仅是模型质量）时特别有用。它们强调上下文处理、工具调用、环境控制、验证逻辑和模型周围的运行时脚手架。

- [Agent Arena](https://www.agent-arena.com/leaderboard) - 一个排行榜，使用 ELO 风格评级对 AI 智能体、模型、工具和框架进行排名，基于一对一的对抗，提供一种结构化方式来比较各类别中的控制框架级别选择。
- [AgentBench](https://github.com/THUDM/AgentBench) - 一个跨环境基准测试，涵盖操作系统、数据库、知识图谱、网页浏览等，用于观察控制框架是否泛化到单一狭窄任务循环之外。
- [AgentBoard](https://github.com/HKUST-NLP/AgentBoard) - 一个多轮大语言模型智能体的基准测试，辅以分析性评估板，用于评估模型性能而不仅仅是最终成功率，使部分进展和轨迹质量可见。
- [AgentStudio](https://github.com/SkyworkAI/agent-studio) - 一个集成基准测试套件，具有逼真的环境和全面的工具包，用于评估虚拟智能体在真实计算机软件上的表现，可用于衡量控制框架在广泛任务表面上的深度。
- [AppWorld](https://appworld.dev/) - 一个可控制的应用和人世界，用于基准测试交互式编码智能体，具有基于状态和基于执行的单元测试，揭示控制框架在规划、代码生成和附带损害控制方面的质量。
- [AssistantBench](https://github.com/oriyor/AssistantBench) - 一个基准测试，评估智能体在现实的、耗时的研究任务上的表现，需要多步骤工具使用和信息综合，使其成为长时域网页场景中控制框架质量的良好代理。
- [BrowseComp](https://www.kaggle.com/benchmarks/openai/browsecomp) - 一个基准测试，评估 AI 智能体在定位难以找到的信息方面的能力，强调搜索策略、上下文管理和困难条件下的检索控制框架设计。
- [BrowserGym Leaderboard](https://huggingface.co/spaces/ServiceNow/browsergym-leaderboard) - 一个健身房环境和排行榜，用于评估大语言模型、视觉语言模型和智能体在网页导航任务上的表现，提供一个可重现的框架，用于在一个地方比较多个网页基准测试的控制框架。
- [CharacterEval](https://github.com/morecry/CharacterEval) - 一个使用多轮对话和角色档案评估角色扮演对话智能体的基准测试，具有四个维度的指标，包括角色一致性和对话连贯性。
- [ClawBench](https://clawbench.net) - 一个基准测试，评估 AI 智能体在搜索、推理、编码、安全和多轮对话任务上的表现，在一个套件中涵盖控制框架需求的广度。
- [ClawWork](https://github.com/HKUDS/ClawWork) - 一个真实经济基准测试，AI 智能体完成跨越 44 种职业的专业任务，赚取收入同时管理代币成本和经济偿付能力，使其成为资源约束下控制框架效率的直接测试。
- [Computer Agent Arena](https://github.com/xlang-ai/computer-agent-arena) - 一个开放的评估平台，用户可以在真实世界的计算机任务上比较基于大语言模型/视觉语言模型的智能体，涵盖从通用计算机使用到编码、数据分析和视频编辑，揭示广泛任务表面上的控制框架差异。
- [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) - 一个通用 AI 助手基准测试，常用于比较工具、规划、验证和长时自主性方面的控制框架级别选择。
- [Galileo Agent Leaderboard](https://huggingface.co/spaces/galileo-ai/agent-leaderboard) - 一个开放的评估平台，追踪大语言模型智能体在跨业务领域的任务完成和工具调用情况，用于比较企业级智能体场景中的控制框架质量。
- [GTA](https://github.com/open-compass/GTA) - 一个基准测试，使用人类编写的查询、真实部署的工具和真实的多模态输入评估基于大语言模型的智能体的工具使用能力，揭示隔离测试和真实部署之间的控制框架差距。
- [HAL: Holistic Agent Leaderboard](https://hal.cs.princeton.edu/) - 一个智能体系统的基准测试和排行榜，关注可靠性、成本和广泛任务覆盖，使其可用于比较端到端的控制框架行为。
- [Introducing Terminal-Bench 2.0 and Harbor](https://www.tbench.ai/news/announcement-2-0) - Terminal-Bench 2.0 发布公告，有助于理解 Harbor 背后更困难的任务和广义评估控制框架。
- [LeetCode-Hard Gym](https://github.com/GammaTauAI/leetcode-hard-gym) - 一个 RL 环境接口到 LeetCode 提交服务器，用于评估代码生成智能体，使控制框架能够直接访问对困难算法问题的执行反馈。
- [LLM Colosseum Leaderboard](https://github.com/OpenGenerativeAI/llm-colosseum) - 一个通过让大语言模型在街头霸王 III 中战斗来评估的平台，测试速度、适应性和实时决策，作为紧密延迟约束下控制框架响应能力的代理。
- [MAgIC](https://zhiyuanhubj.github.io/MAgIC/) - 一个衡量大语言模型在多智能体系统中的认知、适应性、理性和协作的基准测试，可用于评估控制框架如何协调智能体交互和共享状态。
- [MCP Bench](https://github.com/modelscope/MCPBench) - 一个评估 AI 模型在 MCP 服务器交互上的基准测试，测量跨服务器类型的工具准确性、延迟和令牌使用，直接反映 MCP 集成的控制框架设计选择。
- [MCP Universe](https://mcp-universe.github.io/) - 一个排行榜，比较 AI 模型在 MCP 任务上的表现，追踪不同模型和控制框架配置如何处理工具增强的智能体工作流。
- [MCPMark](https://github.com/eval-sys/mcpmark) - 一个压力测试基准测试，用于模型和智能体在真实世界 MCP 任务中的能力，涵盖 Notion、GitHub 和 Postgres 等工具，使控制框架 MCP 集成质量可直接测量。
- [Olas Predict Benchmark](https://github.com/valory-xyz/olas-predict-benchmark) - 一个评估智能体在历史预测市场数据上的基准测试，测试长时推理任务中的研究、检索和预测控制框架设计。
- [OSWorld](https://os-world.github.io/) - 一个真实计算机使用基准测试，包含 369 个跨 Ubuntu、Windows 和 macOS 的任务，具有初始状态设置和基于执行的评估器，使其非常适合测试桌面和多模态控制框架。
- [OSWorld-MCP](https://osworld-mcp.github.io) - OSWorld 的扩展，使用模型上下文协议评估 AI 智能体在真实世界计算机任务上的表现，使其可用于在真实桌面任务套件上比较启用 MCP 的控制框架。
- [SEC-bench](https://github.com/SEC-bench/SEC-bench) - 一个评估大语言模型智能体在真实世界软件安全任务（包括漏洞复现和修补）上的基准测试，强调代码执行、容器化环境和安全感知工具方面的控制框架设计。
- [SWE-bench Verified](https://www.swebench.com/) - 一个强大的软件工程智能体基准测试，针对真实 GitHub 问题和测试，使控制框架在检索、修补和验证方面的选择高度可见。
- [τ-Bench](https://github.com/sierra-research/tau-bench) - 一个模拟模拟用户和配备领域特定 API 工具和政策指南的语言智能体之间动态对话的基准测试，可用于评估围绕结构化工具使用和政策执行构建的控制框架。
- [tau2-bench](https://github.com/sierra-research/tau2-bench) - 一个真实、多步骤智能体任务的基准测试，成功取决于工具使用和执行质量，而非单次回答。
- [Terminal-Bench](https://www.tbench.ai/) - 一个用于终端原生智能体的基准测试套件，在 shell、文件系统和验证密集环境中运行，特别适合比较编码智能体控制框架。
- [TravelPlanner](https://github.com/OSU-NLP-Group/TravelPlanner) - 一个评估大语言模型智能体在多重约束下的工具使用和复杂规划的基准测试，揭示控制框架设计如何处理多约束满足和长时规划。
- [VAB](https://github.com/THUDM/VisualAgentBench) - VisualAgentBench 评估大型多模态模型作为视觉基础智能体，涵盖具身、GUI 和视觉设计任务，可用于比较视觉基础、多步骤智能体工作流的控制框架。
- [VisualWebArena](https://jykoh.com/vwa) - 一个多模态网页智能体的基准测试，在真实视觉基础任务上，扩展 WebArena 以包含图像和截图输入，强调浏览器环境中视觉上下文的控制框架支持。
- [WebArena](https://webarena.dev/) - 一个独立的、可自托管的网页环境，用于评估智能体在真实任务上的表现，使其成为比较面向网页控制框架设计的可重现基线。
- [WebArena-Verified](https://github.com/ServiceNow/webarena-verified) - 一个验证过的网页智能体基准测试，具有策划的任务和对智能体响应及捕获网络追踪的确定性评估器，使其适合测量面向网页的控制框架。
- [WildClawBench](https://github.com/InternLM/WildClawBench) - 一个野外基准测试，在实时 OpenClaw 环境中运行智能体，包含 60 个原创任务，包括多模态、长时和安全关键场景，使控制框架在真实世界条件下的鲁棒性直接可见。
- [WorkArena](https://github.com/ServiceNow/WorkArena) - 一个浏览器智能体基准测试，针对常见知识工作任

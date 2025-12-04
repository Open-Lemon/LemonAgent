# LemonAgent
---
![LemonAgent](./Figures/Lemon_agent.png "LemonAgent Log")
English Version|[中文版本](./README_zh.md)
# Introduction
At the stage where AI is moving from proof-of-concept to large-scale industrial deployment, the core question for agent systems has shifted from *“can we build it?”* to *“can we run it at scale with controllable cost, engineering complexity, and sustainable evolution?”* Traditional single-agent architectures are already hitting ceilings in compute overhead, scenario customization, and cross-task reuse. To address this, we propose a **“collaborative evolution–economic efficiency–environment-aware”** paradigm for industrial-grade agents: (1) **collaborative evolution** – multi-agent dynamic collaboration and role specialization with unified memory and experience sharing to yield collectively improving intelligence under real-world feedback; (2) **economic efficiency** – joint optimization of *task performance × compute cost* via compute-aware model selection, reasoning-depth control, Planner–Executor decoupling, and cross-task tool/memory reuse to maximize throughput per unit of compute; (3) **environment-aware operation** – treating energy and carbon as system-level constraints, optimizing inference paths, model sizes, and resource scheduling to reduce redundant computation and distill a reproducible green agent-engineering pattern.

As the core carrier of this “three-in-one” design paradigm, **LemonAgent** is a general-purpose multi-agent framework. Its multi-agent, memory, and tool modules operate in a **segmented yet cooperative** fashion, forming an organic whole. This segmented collaboration pattern is akin to the multiple segments of a lemon’s pulp—hence the name **“LemonAgent”**.

To validate the generality and adaptability of LemonAgent, we evaluated it on the GAIA benchmark test set. As of December 4, LemonAgent achieves an overall accuracy of **88.37%**, with breakdowns of **96.77% on Level 1**, **86.16% on Level 2**, and **79.59% on Level 3**, demonstrating our initial progress in long-horizon, complex reasoning with self-developed reasoning agent systems.

We plan to fully open-source **LemonAgent** in the near future, positioning it as a foundational infrastructure for multi-agent collaboration and memory-augmented reasoning, and making it available to the global developer and research community for study, reproduction, and further innovation. The initial open-source release is structured around two core technical pillars:

1. **Multi-agent orchestration architecture.** LemonAgent adopts a unified **Planner–Executor–Memory** architecture, compatible with multiple multi-agent design patterns, including cooperative, hierarchical, and tool-hub-centric architectures. It provides a unified context and memory view, as well as a high-concurrency DAG execution engine and task routing mechanisms for complex business processes, enabling agent swarms of different sizes and topologies to be rapidly assembled and evolved in a configuration-driven manner.

2. **Unified scheduling of sub-agents, memory, and tools.** Building on our experience with long-term memory, tool-augmented reasoning, and collaborative agents, LemonAgent integrates sub-agents, layered memory (short-term / long-term / retrieval-based), and tool modules into a unified **adaptive scheduling subsystem**. By jointly evaluating task content, historical interaction traces, and environmental signals, a strategy scheduler adaptively selects the subset of sub-agents to participate in collaboration and dynamically configures their capabilities (model size, reasoning depth, tool permissions, and memory retrieval scope, etc.), thereby ensuring task quality while substantially reducing redundant compute overhead.

With these designs, LemonAgent can serve both as a **reference implementation for industrial-grade GAIA-style agents** and as an **open experimental bed** for academia and industry to explore multi-agent collaboration, memory-augmented reasoning, and economically efficient reasoning strategies.
# GAIA bechmark
![](./Figures/benchmark.png "LemonAgent benchmark")
![](./Figures/benchmark1.png "LemonAgent benchmark")

# Architecture
![](./Figures/lemon_agent_architecture.png "LemonAgent benchmark")
### Agent
- Performs intention recognition on user queries, retrieves historical skill memories, dynamically mounts the best-matching skill memories, routes tasks, and validates and summarizes tasks.
- During task routing, the main agent decomposes the task into executable steps based on the aforementioned information, plans executable steps, configures different sub-agent groups and distributes tasks according to the difficulty (complexity) of the steps, and implements high-concurrency DAG execution among the sub-agents.
### Skill Memory
- After the task is completed, the main agent extracts valuable information from the execution process and results (if any) and writes it back to the Skill Memory module, realizing a closed loop of self-evolution.
### Tool
- All agents invoke tools via the MCP protocol.

# Highlights
1. **Multi-Agent Collaborative Consensus：** Multi-agents collaboratively execute tasks, engaging in mutual verification and information enrichment to achieve enhanced performance in the final result.

2. **Adaptive Agent Scheduling：** Determine the number of agents and which model to be employed based on task complexity, enabling adaptive and environment-friend intelligent scheduling, achieve the optimal balance between performance and cost.

3. **Self-Evoled skill memory:** Instead of relying solely on ground truth to update the memory module, it extracts valuable components from multiple dimensions of the agent’s workflow and tool execution, enabling the memory module to evolve autonomously.

4. **Tool Augmentation：**

   * Enhancing tools for multimodal processing (audio/visual).

   * Enhancing tools for website backtracking.
# TODO List
* [ ] Technical Report V1 comming soon
* [ ] Code comming soon
  
# Project Co-developer


**Contributors**：Haipeng Jiang, Kailong Ren, Zimo Yin, Zhetao Sun, Xin Gan, Guangyi Lv, Ming He, Peng Wang, Congli Yin, Hong Pan, Changwen Zhang, Shan Tong, Zhengyu Xu

**Affiliation：** Lenovo Research AILab of Lenovo CTO Org
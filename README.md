# LemonAgent
---
![LemonAgent](./Figures/Lemon_agent.png "LemonAgent Log")
English Version|[中文版本](./README_zh.md)
# Introduction
At the stage where AI is moving from proof-of-concept to large-scale industrial deployment, the core question for agent systems has shifted from *“can we build it?”* to *“can we run it at scale with controllable cost, engineering complexity, and sustainable evolution?”* Traditional single-agent architectures are already hitting ceilings in compute overhead, scenario customization, and cross-task reuse. To address this, we propose a **“collaborative evolution–economic efficiency–environment-aware”** paradigm for industrial-grade agents: (1) **collaborative evolution** – multi-agent dynamic collaboration and role specialization with unified memory and experience sharing to yield collectively improving intelligence under real-world feedback; (2) **economic efficiency** – joint optimization of *task performance × compute cost* via compute-aware model selection, reasoning-depth control, Planner–Executor decoupling, and cross-task tool/memory reuse to maximize throughput per unit of compute; (3) **environment-aware operation** – treating energy and carbon as system-level constraints, optimizing inference paths, model sizes, and resource scheduling to reduce redundant computation and distill a reproducible green agent-engineering pattern.

As the core carrier of this “three-in-one” design paradigm, **LemonAgent** is a general-purpose multi-agent framework. Its multi-agent, memory, and tool modules operate in a **segmented yet cooperative** fashion, forming an organic whole. This segmented collaboration pattern is akin to the multiple segments of a lemon’s pulp—hence the name **“LemonAgent”**.

To validate the generality and adaptability of LemonAgent, we evaluated it on the GAIA benchmark test set. As of 2026/02/06, LemonAgent achieves an overall accuracy of **91.36%**, with breakdowns of **96.77% on Level 1**, **89.31% on Level 2**, and **87.76% on Level 3**, demonstrating our initial progress in long-horizon, complex reasoning with self-developed reasoning agent systems.

We plan to fully open-source **LemonAgent** in the near future, positioning it as a foundational infrastructure for multi-agent collaboration and memory-augmented reasoning, and making it available to the global developer and research community for study, reproduction, and further innovation. The initial open-source release is structured around two core technical pillars:

1. **Multi-agent orchestration architecture.** LemonAgent adopts a unified **Planner–Executor–Memory** architecture, compatible with multiple multi-agent design patterns, including cooperative, hierarchical, and tool-hub-centric architectures. It provides a unified context and memory view, as well as a high-concurrency DAG execution engine and task routing mechanisms for complex business processes, enabling agent swarms of different sizes and topologies to be rapidly assembled and evolved in a configuration-driven manner.

2. **Unified scheduling of sub-agents, memory, and tools.** Building on our experience with long-term memory, tool-augmented reasoning, and collaborative agents, LemonAgent integrates sub-agents, layered memory (short-term / long-term / retrieval-based), and tool modules into a unified **adaptive scheduling subsystem**. By jointly evaluating task content, historical interaction traces, and environmental signals, a strategy scheduler adaptively selects the subset of sub-agents to participate in collaboration and dynamically configures their capabilities (model size, reasoning depth, tool permissions, and memory retrieval scope, etc.), thereby ensuring task quality while substantially reducing redundant compute overhead.

With these designs, LemonAgent can serve both as a **reference implementation for industrial-grade GAIA-style agents** and as an **open experimental bed** for academia and industry to explore multi-agent collaboration, memory-augmented reasoning, and economically efficient reasoning strategies.
# GAIA bechmark
![](./Figures/benchmark.svg "LemonAgent benchmark")
![](./Figures/benchmark2.png "LemonAgent benchmark")

# Architecture
![](./Figures/lemon_agent_architecture.svg "LemonAgent benchmark")
### Agent
- Performs intention recognition on user queries, retrieves historical skill memories, dynamically mounts the best-matching skill memories, routes tasks, and validates and summarizes tasks.
- During task routing, the main agent decomposes the task into executable steps based on the aforementioned information, plans executable steps, configures different sub-agent groups and distributes tasks according to the difficulty (complexity) of the steps, and implements high-concurrency DAG execution among the sub-agents.
### AgentCortex Framework:
- **AgentCortex** is an agent-oriented technology framework and design paradigm designed to ***bridge the gap between academic research and real-world product deployment***. It adopts a modular architecture that decomposes an intelligent agent into well-defined components—including intent understanding, task decomposition, task planning, tool execution, knowledge retrieval, memory read/write, and task summarization—connected through unified and highly abstracted interfaces. This clear separation of responsibilities enables low coupling, high flexibility, and sustainable system evolution.
- A key strength of AgentCortex is its ability to ***unify algorithmic innovation and engineering readiness within a single framework***. Researchers can rapidly integrate state-of-the-art or self-developed algorithms into a complete agent pipeline for experimentation and evaluation, while engineers can leverage built-in production-grade capabilities—such as a microservice engine, logging and monitoring infrastructure, and database access mechanisms—to deploy agent systems reliably in real-world scenarios. By aligning research workflows with industrial engineering practices, AgentCortex significantly shortens the path from experimental prototypes to production-ready intelligent agents.
- **AgentCortex** also demonstrates its industrial-grade reliability through its deployment in the Lenovo Super Agent. This commercial implementation achieves a transaction volume in the hundreds of millions and earns recognition as a ***2025 CCF Enterprise Digitalization Outstanding Case***.
### Skill Memory
- After the task is completed, the main agent extracts valuable information from the execution process and results (if any) and writes it back to the Skill Memory module, realizing a closed loop of self-evolution.
### Tool
- All agents invoke tools via the MCP protocol.

# Highlights
1. **Multi-Agent Collaborative Consensus：** Multi-agents collaboratively execute tasks, engaging in mutual verification and information enrichment to achieve enhanced performance in the final result.

2. **Adaptive Agent Scheduling：** Determine the number of agents and which model to be employed based on task complexity, enabling adaptive and environment-friend intelligent scheduling, achieve the optimal balance between performance and cost.

3. **Self-Evoled skill memory:** Instead of relying solely on ground truth to update the memory module, it extracts valuable components from multiple dimensions of the agent’s workflow and tool execution, enabling the memory module to evolve autonomously.

4. **Tool Augmentation：**
   * Intelligent Image Tool
   * Google Street View Tool
   * Multi-Source Search Tool Suite
   * Enhanced file reading

# QuickStart
###  Environment Install:
   ```bash
   git clone https://github.com/Open-Lemon/LemonAgent
   cd LemonAgent
   uv sync

   # Ubuntu/Debian
   curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
   sudo apt-get install -y nodejs
   node -v && npx -v

   # Debian/Ubuntu install ffmpeg
   sudo apt-get update && sudo apt-get install ffmpeg

   # Install and setup crawl4ai
   crawl4ai-setup
   crawl4ai-doctor

   # Install playwright browsers
   playwright install
   ```
### env upate:
   ```shell
   # Must have for minimal agent get started    
   E2B_API_KEY=""  
      
   # Search and web scraping capabilities    
   SERPER_API_KEY=""
   JINA_API_KEY=""
                                                      
   # Vision understanding capabilities    
   GEMINI_API_KEY=""
   GEMINI_BASE_URL=""    
      
   GOOGLE_API_KEY=""    
   # LLM judge, reasoning, and hint generation    
   OPENAI_API_KEY=""
   OPENAI_BASE_URL=""        
   # Used to save memories to a database
   MONGODB=""
   # Proxy configuration for external network access (Wikipedia, Archive.org, etc.)
   HTTP_PROXY=""
   HTTPS_PROXY=""

   DATA_DIR="data/"
   ```
### run:
1. start mcp_server:
   ```bash
   python -m src.mcp_tools.mcp_tool_server
   # or 
   uv run python -m src.mcp_tools.mcp_tool_server
   ```
2. run the benchmark:
   ```bash
   cd benchmark 
   python run_gaia_multi.py \
   --level 1 \
   --start 0 --end 10 \
   --processes 1
   ```

# TODO List
* [ ] Code comming soon

# Acknowledgement
* Some of the code in the toolkits is adapted from **Camel-AI, Miroflow, Co-sight**



# Project Co-developer


**Contributors**：Haipeng Jiang, Kailong Ren, Zimo Yin, Zhetao Sun, Xin Gan, Guangyi Lv, Ming He, Peng Wang, Congli Yin, Hong Pan, Changwen Zhang, Shan Tong, Zhengyu Xu, Zeping Chen, Yubin Huangfu, Yanzhi Xu, Xing Su, Qin Feng, Dong An, Jiangping Fan

**Affiliation：** Lenovo Research AILab of Lenovo CTO Org
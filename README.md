# 🧱 Deep Agents from Scratch

## Lyfing Fork说明 LLM使用Deepseek
我是中国大陆的一个开发者，最近在langchain官网学习他们的官方教程，其中一个项目是 https://academy.langchain.com/courses/deep-agents-with-langgraph. 

我跟着这个教程，通过在jupyter notebook中按部就班地执行示例代码的时候，发现他们用的LLM模型都是国外的，但其实在中国更便宜、性能也不差、而且方便访问的LLM(无需科学上网)其实Deepseek就很不错。

**所以针对该项目`notebooks/`目录下的`**.ipynb`文件中的涉及到具体LLM模型配置的地方，我都改成了Deepseek，其他地方基本没动，这样可以和官方教程保持最大一致性**。具体Deepseek配置仍然参考官方教程给出的根目录下所使用的 `example.env` 即可，在该文件中我添加了两个Deepseek相关的apiKey配置。

------

<img width="720" height="289" alt="Screenshot 2025-08-12 at 2 13 54 PM" src="https://github.com/user-attachments/assets/90e5a7a3-7e88-4cbe-98f6-5b2581c94036" />

[Deep Research](https://academy.langchain.com/courses/deep-research-with-langgraph) broke out as one of the first major agent use-cases along with coding. Now, we've seeing an emergence of general purpose agents that can be used for a wide range of tasks. For example, [Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) has gained significant attention and popularity for long-horizon tasks; the average Manus task uses ~50 tool calls!. As a second example, Claude Code is being used generally for tasks beyond coding. Careful review of the [context engineering patterns](https://docs.google.com/presentation/d/16aaXLu40GugY-kOpqDU4e-S0hD1FmHcNyF0rRRnb1OU/edit?slide=id.p#slide=id.p) across these popular "deep" agents shows some common approaches:

* **Task planning (e.g., TODO), often with recitation**
* **Context offloading to file systems**
* **Context isolation through sub-agent delegation**

This course will show how to implement these patterns from scratch using LangGraph! 

## 🚀 Quickstart 

### Prerequisites

- Ensure you're using Python 3.11 or later.
- This version is required for optimal compatibility with LangGraph.
```bash
python3 --version
```
- [uv](https://docs.astral.sh/uv/) package manager
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
# Update PATH to use the new uv version
export PATH="/Users/$USER/.local/bin:$PATH"
```

### Installation

1. Clone the repository:
```bash
git clone https://github.com/langchain-ai/deep-agents-from-scratch.git
cd deep-agents-from-scratch
```

2. Install the package and dependencies (this automatically creates and manages the virtual environment):
```bash
uv sync
```

3. Create a `.env` file in the project root with your API keys:
```bash
# Create .env file
touch .env
```

Add your API keys to the `.env` file:
```env
# Required for research agents with external search
TAVILY_API_KEY=your_tavily_api_key_here

# Required for model usage
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Optional: For evaluation and tracing
LANGSMITH_API_KEY=your_langsmith_api_key_here
LANGSMITH_TRACING=true
LANGSMITH_PROJECT=deep-agents-from-scratch
```

4. Run notebooks or code using uv:
```bash
# Run Jupyter notebooks directly
uv run jupyter notebook

# Or activate the virtual environment if preferred
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
jupyter notebook
```

## 📚 Tutorial Overview

This repository contains five progressive notebooks that teach you to build advanced AI agents:

### `0_create_agent.ipynb` -
Learn how to use the create_agent component. This component,
- implements a ReAct (Reason - Act) loop that forms the foundation for many agents.
- is easy to use and quick to set up.
- serves as the basis for the following lessons.

### `1_todo.ipynb` - Task Planning Foundations
Learn to implement structured task planning using TODO lists. This notebook introduces:
- Task tracking with status management (pending/in_progress/completed)  
- Progress monitoring and context management
- The `write_todos()` tool for organizing complex multi-step workflows
- Best practices for maintaining focus and preventing task drift

### `2_files.ipynb` - Virtual File Systems
Implement a virtual file system stored in agent state for context offloading:
- File operations: `ls()`, `read_file()`, `write_file()`, `edit_file()`
- Context management through information persistence
- Enabling agent "memory" across conversation turns
- Reducing token usage by storing detailed information in files

### `3_subagents.ipynb` - Context Isolation
Master sub-agent delegation for handling complex workflows:
- Creating specialized sub-agents with focused tool sets
- Context isolation to prevent confusion and task interference
- The `task()` delegation tool and agent registry patterns
- Parallel execution capabilities for independent research streams

### `4_full_agent.ipynb` - Complete Research Agent
Combine all techniques into a production-ready research agent:
- Integration of TODOs, files, and sub-agents
- Real web search with intelligent context offloading
- Content summarization and strategic thinking tools
- Complete workflow for complex research tasks with LangGraph Studio integration

Each notebook builds on the previous concepts, culminating in a sophisticated agent architecture capable of handling real-world research and analysis tasks. 

# 🤖 Basic ADK Agent Example

[![ADK](https://img.shields.io/badge/ADK-Basic%20Agent-blue.svg)](https://google.github.io/adk-docs/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-green.svg)](.)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

> 🎯 **Your First Step into AI Agent Development** - Learn the fundamentals of creating intelligent agents with Google's ADK

## 🧠 What is an ADK Agent?

The `LlmAgent` (often aliased simply as `Agent`) is the **brain** 🧠 of your AI application. It's a core component in ADK that acts as the "thinking" part of your system.

### 🔋 Core Capabilities

```mermaid
mindmap
  root)LlmAgent Core(
    Reasoning
      Logical thinking
      Problem solving
      Decision making
    Language
      Natural language understanding
      Context interpretation
      Multi-language support
    Actions
      Tool interaction
      API calls
      Data processing
    Generation
      Text responses
      Creative content
      Structured outputs
```

| Capability | Description | Use Cases |
|------------|-------------|-----------|
| 🧮 **Reasoning** | Logical thinking and problem-solving | Analysis, planning, strategy |
| 🗣️ **Language Understanding** | Natural language processing | Chat, Q&A, translation |
| 🎯 **Decision Making** | Dynamic behavior based on context | Routing, tool selection |
| 📝 **Response Generation** | Creating human-like responses | Content creation, explanations |
| 🛠️ **Tool Interaction** | External system integration | APIs, databases, services |

### 🆚 Deterministic vs. Non-Deterministic Agents

```mermaid
graph TD
    subgraph "Traditional Workflow Agent"
        A1[Input] --> B1[Step 1]
        B1 --> B2[Step 2]
        B2 --> B3[Step 3]
        B3 --> C1[Output]
    end
    
    subgraph "LLM Agent"
        A2[Input] --> B4[LLM Processing]
        B4 --> C2{Decision Point}
        C2 -->|Option A| D1[Tool Use]
        C2 -->|Option B| D2[Direct Response]
        C2 -->|Option C| D3[Agent Transfer]
        D1 --> E[Dynamic Output]
        D2 --> E
        D3 --> E
    end
    
    style A2 fill:#e1f5fe
    style B4 fill:#f3e5f5
    style E fill:#e8f5e8
```

> 💡 **Key Insight**: Unlike deterministic workflow agents that follow predefined paths, an `LlmAgent`'s behavior is **non-deterministic**. It uses the LLM to interpret instructions and context, deciding dynamically how to proceed!

## 📁 Required Agent Structure

For ADK to discover and run your agents properly (especially with `adk web`), your project **must** follow this specific structure:

### 🏗️ Project Architecture

```mermaid
graph TD
    A[parent_folder/] --> B[agent_folder/]
    B --> C[__init__.py]
    B --> D[agent.py]
    B --> E[.env]
    
    C --> C1["📄 Must import agent.py"]
    D --> D1["🎯 Must define root_agent"]
    E --> E1["🔑 Environment variables"]
    
    style A fill:#e3f2fd
    style B fill:#f3e5f5
    style C fill:#e8f5e8
    style D fill:#fff3e0
    style E fill:#fce4ec
```

```
parent_folder/
    agent_folder/         # 📦 Your agent's package directory
        __init__.py       # 📝 Must import agent.py
        agent.py          # 🎯 Must define root_agent
        .env              # 🔑 Environment variables
```

### 🔧 Essential Components

| Component | Purpose | Requirements | Example |
|-----------|---------|--------------|---------|
| 📄 **`__init__.py`** | Agent Discovery | `from . import agent` | Makes agent discoverable |
| 🎯 **`agent.py`** | Entry Point | Define `root_agent` | Main agent definition |
| 🔑 **`.env`** | Configuration | API keys, settings | `GOOGLE_API_KEY=...` |
| 📍 **Command Location** | Execution Context | Run from parent folder | `adk web` from parent |

### ⚠️ Important Notes

> 🚨 **Critical**: Always run `adk` commands from the **parent directory**, not from inside the agent directory!

```bash
# ✅ Correct - from parent folder
cd parent_folder/
adk web

# ❌ Wrong - from agent folder  
cd parent_folder/agent_folder/
adk web  # This won't work!
```

## 🔧 Key Components Deep Dive

### 1️⃣ Identity Configuration

```mermaid
classDiagram
    class AgentIdentity {
        +string name
        +string description
        +getIdentity()
        +validateName()
    }
    
    AgentIdentity : name* "Unique identifier"
    AgentIdentity : description "Capability summary"
```

| Property | Status | Purpose | Example |
|----------|--------|---------|---------|
| 🏷️ **name** | Required | Unique string identifier | `"greeting_agent"` |
| 📝 **description** | Recommended | Capability summary for routing | `"Friendly agent for greetings"` |

### 2️⃣ Model Selection

```mermaid
pie title Model Selection Impact
    "Performance" : 35
    "Cost" : 25
    "Capabilities" : 25
    "Speed" : 15
```

| Model | Performance | Cost | Best For |
|-------|-------------|------|----------|
| 🚀 **gemini-2.0-flash** | High | Medium | General purpose |
| ⚡ **gemini-1.5-pro** | Very High | High | Complex reasoning |
| 💨 **gemini-1.5-flash** | Medium | Low | Simple tasks |

### 3️⃣ Instructions (The Magic ✨)

**The most critical parameter** for shaping your agent's behavior!

```mermaid
graph LR
    A[Instructions] --> B[Core Task]
    A --> C[Personality]
    A --> D[Constraints]
    A --> E[Tool Usage]
    A --> F[Output Format]
    
    B --> G[Agent Behavior]
    C --> G
    D --> G
    E --> G
    F --> G
    
    style A fill:#ffeb3b
    style G fill:#4caf50
```

#### 📋 Instruction Components

| Component | Purpose | Example |
|-----------|---------|---------|
| 🎯 **Core Task** | Primary objective | "Help users with greetings" |
| 🎭 **Personality** | Behavioral style | "Be friendly and welcoming" |
| 🚫 **Constraints** | Behavioral limits | "Keep responses concise" |
| 🛠️ **Tool Usage** | How to use tools | "Use translation tool for languages" |
| 📄 **Output Format** | Response structure | "Respond in markdown format" |

### 4️⃣ Tools Integration

```mermaid
graph TD
    A[Agent Core] --> B{Needs External Data?}
    B -->|Yes| C[Select Tool]
    B -->|No| D[Use Built-in Knowledge]
    
    C --> E[API Tool]
    C --> F[Database Tool]
    C --> G[Calculation Tool]
    C --> H[File Tool]
    
    E --> I[Enhanced Response]
    F --> I
    G --> I
    H --> I
    D --> J[Direct Response]
    
    style A fill:#e3f2fd
    style I fill:#e8f5e8
    style J fill:#e8f5e8
```

## 🚀 Getting Started

### 📋 Prerequisites Checklist

- [ ] ✅ Virtual environment activated
- [ ] 🔑 Google API key configured
- [ ] 📁 Proper folder structure
- [ ] 📦 Dependencies installed

### 🔧 Environment Setup

```bash
# 🔌 Activate virtual environment (from parent directory)
# macOS/Linux:
source ../.venv/bin/activate

# Windows CMD:
..\.venv\Scripts\activate.bat

# Windows PowerShell:
..\.venv\Scripts\Activate.ps1
```

### 🔑 API Key Configuration

```mermaid
sequenceDiagram
    participant U as User
    participant F as .env.example
    participant E as .env
    participant A as Agent
    
    U->>F: 1. Locate file
    F->>E: 2. Rename to .env
    U->>E: 3. Add API key
    E->>A: 4. Agent reads config
    A->>U: 5. Ready to run!
```

| Step | Action | Command/Location |
|------|--------|------------------|
| 1️⃣ | **Locate Template** | Find `.env.example` in agent folder |
| 2️⃣ | **Rename File** | Change to `.env` |
| 3️⃣ | **Add API Key** | `GOOGLE_API_KEY=your_key_here` |
| 4️⃣ | **Verify Setup** | Check agent loads correctly |

## 🎮 Running the Example

### 🌐 Interactive Web UI (Recommended)

```mermaid
graph LR
    A[Terminal] --> B[adk web]
    B --> C[Server Starts]
    C --> D[Open Browser]
    D --> E[Select Agent]
    E --> F[Start Chatting]
    
    style D fill:#e3f2fd
    style F fill:#e8f5e8
```

#### 🔄 Step-by-Step Process

| Step | Action | Details |
|------|--------|---------|
| 1️⃣ | **Navigate** | `cd 1-basic-agent` |
| 2️⃣ | **Start Server** | `adk web` |
| 3️⃣ | **Open Browser** | Visit `http://localhost:8000` |
| 4️⃣ | **Select Agent** | Choose from dropdown (top-left) |
| 5️⃣ | **Start Chatting** | Use textbox at bottom |

### 🛠️ Alternative Run Methods

```mermaid
graph TD
    A[ADK CLI Options] --> B[adk web]
    A --> C[adk run]
    A --> D[adk api_server]
    
    B --> B1[Interactive Web UI]
    B --> B2[Chat Interface]
    B --> B3[Visual Feedback]
    
    C --> C1[Terminal Interface]
    C --> C2[Direct Execution]
    C --> C3[Quick Testing]
    
    D --> D1[FastAPI Server]
    D --> D2[REST Endpoints]
    D --> D3[Integration Testing]
    
    style B fill:#4caf50
    style C fill:#ff9800
    style D fill:#2196f3
```

| Method | Command | Use Case | Interface |
|--------|---------|----------|-----------|
| 🌐 **Web UI** | `adk web` | Interactive testing | Browser-based |
| 💻 **Terminal** | `adk run [agent_name]` | Quick testing | Command line |
| 🔌 **API Server** | `adk api_server` | Integration testing | REST API |

### 🔧 Troubleshooting Guide

```mermaid
flowchart TD
    A[Agent not in dropdown?] --> B{Check Structure}
    B -->|Wrong| C[Fix folder structure]
    B -->|Correct| D{Check __init__.py}
    D -->|Missing| E[Add: from . import agent]
    D -->|Correct| F{Check agent.py}
    F -->|Missing| G[Define root_agent variable]
    F -->|Correct| H{Check Command Location}
    H -->|Wrong| I[Run from parent directory]
    H -->|Correct| J[Check Logs for Errors]
    
    style A fill:#ffcdd2
    style C fill:#fff3e0
    style E fill:#fff3e0
    style G fill:#fff3e0
    style I fill:#fff3e0
```

#### 🚨 Common Issues & Solutions

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| 🚫 **Agent not in dropdown** | Wrong directory | Run `adk web` from parent folder |
| 🔍 **Import errors** | Missing `__init__.py` import | Add `from . import agent` |
| 🎯 **Agent not found** | Missing `root_agent` | Define in `agent.py` |
| 🔑 **API errors** | Invalid key | Check `.env` file |

## 💬 Example Prompts to Try

### 🌍 Multi-Language Greetings

```mermaid
graph LR
    A[User Input] --> B[Agent Processing]
    B --> C[Language Detection]
    C --> D[Cultural Context]
    D --> E[Appropriate Response]
    
    style A fill:#e3f2fd
    style E fill:#e8f5e8
```

| Category | Prompt Examples | Expected Response Type |
|----------|-----------------|----------------------|
| 🇪🇸 **Spanish** | "How do you say hello in Spanish?" | Language translation |
| 🇯🇵 **Japanese** | "What's a formal greeting in Japanese?" | Cultural context |
| 🇫🇷 **French** | "Tell me how to greet someone in French" | Detailed explanation |
| 🤝 **Professional** | "How should I greet a business client?" | Professional advice |
| 👋 **Casual** | "What's a casual way to say hi?" | Informal suggestions |

### 🎯 Test Scenarios

#### 🔰 Basic Tests
- ✅ Simple greeting requests
- ✅ Language-specific queries  
- ✅ Cultural context questions

#### 🔄 Advanced Tests  
- ✅ Multi-part conversations
- ✅ Context retention
- ✅ Error handling

## 🎉 Success Indicators

### ✅ Your Agent is Working When:

| Indicator | Description | What to Look For |
|-----------|-------------|------------------|
| 🎯 **Responsive** | Answers quickly | < 3 second responses |
| 🧠 **Contextual** | Understands prompts | Relevant answers |
| 🎭 **Consistent** | Maintains personality | Friendly, helpful tone |
| 🔄 **Interactive** | Engages in conversation | Asks follow-up questions |

## 🚪 Exit Options

```mermaid
graph LR
    A[Running Agent] --> B{Want to Stop?}
    B -->|Web UI| C[Ctrl+C in Terminal]
    B -->|Terminal| D[Ctrl+C or 'exit']
    B -->|API Server| E[Ctrl+C in Terminal]
    
    C --> F[Server Stopped]
    D --> F
    E --> F
    
    style F fill:#e8f5e8
```

> 🛑 **Stop the conversation** or server by pressing `Ctrl+C` in your terminal

## 🎓 What You've Learned

This example demonstrates the **fundamentals of agent creation** with ADK:

### 🏆 Key Achievements

- [ ] 🤖 Created your first AI agent
- [ ] 📁 Understood project structure requirements  
- [ ] 🔧 Configured development environment
- [ ] 🌐 Used multiple interaction methods
- [ ] 💬 Tested conversational capabilities
- [ ] 🔧 Learned troubleshooting techniques

### 🚀 Next Steps

Ready to level up? Check out these advanced examples:

| Next Example | Focus | Complexity |
|--------------|-------|------------|
| 🛠️ **Tool Agent** | External integrations | ⭐⭐ |
| 🔄 **LiteLLM Agent** | Model flexibility | ⭐⭐ |
| 📊 **Structured Outputs** | Data formatting | ⭐⭐ |

---

<div align="center">

### 🎉 Congratulations! 

You've successfully created and run your first ADK agent! 

[![Next: Tool Agent](https://img.shields.io/badge/Next-Tool%20Agent-blue?style=for-the-badge&logo=arrow-right)](../2-tool-agent/)
[![Back to Main](https://img.shields.io/badge/Back-Main%20Course-green?style=for-the-badge&logo=home)](../)

*Ready to add superpowers to your agent? Let's explore tools! 🛠️*

</div>
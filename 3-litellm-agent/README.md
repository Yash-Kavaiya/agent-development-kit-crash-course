# 🔄 LiteLLM Agent Example

[![ADK](https://img.shields.io/badge/ADK-LiteLLM%20Agent-purple.svg)](https://google.github.io/adk-docs/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow.svg)](.)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![LiteLLM](https://img.shields.io/badge/LiteLLM-Multi--Provider-green.svg)](https://litellm.ai/)

> 🎯 **Master Multi-Provider LLM Integration** - Learn to seamlessly switch between different LLM providers using LiteLLM abstraction

## 🌐 What is a LiteLLM Agent?

A **LiteLLM Agent** is an ADK agent that uses the LiteLLM library to abstract away LLM provider details, enabling you to easily switch between different models from various providers (OpenAI, Anthropic, Google, Azure, etc.) with minimal code changes.

### 🔄 Provider Abstraction Benefits

```mermaid
graph TB
    subgraph "Traditional Approach"
        A1[Your Agent] --> B1[OpenAI API]
        A1 --> B2[Google API]
        A1 --> B3[Anthropic API]
        A1 --> B4[Azure API]
        
        B1 --> C1[Different Interfaces]
        B2 --> C2[Different Parameters]
        B3 --> C3[Different Error Handling]
        B4 --> C4[Different Authentication]
    end
    
    subgraph "LiteLLM Approach"
        A2[Your Agent] --> L[LiteLLM Layer]
        L --> B5[OpenAI]
        L --> B6[Google]
        L --> B7[Anthropic]
        L --> B8[Azure]
        
        L --> C5[Unified Interface]
        L --> C6[Consistent Parameters]
        L --> C7[Standardized Error Handling]
        L --> C8[Universal Authentication]
    end
    
    style L fill:#9c27b0
    style C5 fill:#c8e6c9
    style C6 fill:#c8e6c9
    style C7 fill:#c8e6c9
    style C8 fill:#c8e6c9
```

### 📊 Provider Comparison

| Provider | Models Available | Strengths | Use Cases |
|----------|------------------|-----------|-----------|
| 🤖 **OpenAI** | GPT-4, GPT-3.5 | Strong reasoning, coding | General purpose, creative tasks |
| 🧠 **Anthropic** | Claude 3, Claude 2 | Safety, analysis | Research, detailed analysis |
| 🔍 **Google** | Gemini, PaLM | Multimodal, fast | Search integration, real-time |
| ☁️ **Azure OpenAI** | GPT-4, GPT-3.5 | Enterprise features | Corporate deployments |
| 🌟 **Others** | Cohere, AI21, etc. | Specialized capabilities | Specific domains |

## 🏗️ LiteLLM Architecture

### 🔧 How LiteLLM Works

```mermaid
sequenceDiagram
    participant A as ADK Agent
    participant L as LiteLLM
    participant P1 as OpenAI
    participant P2 as Google
    participant P3 as Anthropic
    
    A->>L: Standard Request
    L->>L: Route Based on Model
    
    alt Model: gpt-4
        L->>P1: OpenAI Format
        P1->>L: OpenAI Response
    else Model: gemini-pro
        L->>P2: Google Format
        P2->>L: Google Response
    else Model: claude-3
        L->>P3: Anthropic Format
        P3->>L: Anthropic Response
    end
    
    L->>L: Standardize Response
    L->>A: Unified Response Format
```

### 🎛️ Configuration Flexibility

```mermaid
graph TD
    A[LiteLLM Configuration] --> B[Model Selection]
    A --> C[Provider Settings]
    A --> D[Fallback Options]
    A --> E[Cost Management]
    
    B --> B1[Primary Model]
    B --> B2[Backup Models]
    
    C --> C1[API Keys]
    C --> C2[Base URLs]
    C --> C3[Custom Headers]
    
    D --> D1[Provider Fallback]
    D --> D2[Model Fallback]
    D --> D3[Error Handling]
    
    E --> E1[Budget Limits]
    E --> E2[Rate Limiting]
    E --> E3[Cost Tracking]
    
    style A fill:#9c27b0
    style B1 fill:#4caf50
    style D1 fill:#ff9800
    style E1 fill:#f44336
```

## 🚀 Key Features

### 1️⃣ Unified Interface

**One API to rule them all!** LiteLLM provides a consistent interface across all providers:

| Feature | Benefit | Example |
|---------|---------|---------|
| 🔄 **Consistent Method Calls** | Same code for all providers | `completion()` for all models |
| 📝 **Standardized Parameters** | Universal parameter names | `model`, `messages`, `temperature` |
| 🛡️ **Error Handling** | Unified error types | Consistent exception handling |
| 📊 **Response Format** | Same response structure | Standard message format |

### 2️⃣ Easy Provider Switching

```mermaid
graph LR
    A[Change Model Name] --> B[LiteLLM Routes]
    B --> C[Different Provider]
    
    A1["model='gpt-4'"] --> B
    A2["model='gemini-pro'"] --> B
    A3["model='claude-3-sonnet'"] --> B
    
    style A fill:#e3f2fd
    style B fill:#9c27b0
    style C fill:#c8e6c9
```

### 3️⃣ Advanced Features

| Feature | Description | Benefit |
|---------|-------------|---------|
| 🔄 **Fallbacks** | Automatic provider switching on failure | High availability |
| 💰 **Cost Tracking** | Monitor usage across providers | Budget management |
| ⚡ **Rate Limiting** | Handle provider limits gracefully | Reliable operation |
| 📊 **Load Balancing** | Distribute requests across models | Performance optimization |
| 🔐 **Key Management** | Secure API key handling | Security best practices |

## 🔧 Implementation Guide

### 📦 Installation Requirements

```mermaid
graph TD
    A[Base Requirements] --> B[ADK Framework]
    A --> C[LiteLLM Library]
    A --> D[Provider API Keys]
    
    B --> B1[Agent Development Kit]
    C --> C1[pip install litellm]
    D --> D1[OpenAI API Key]
    D --> D2[Google API Key]
    D --> D3[Anthropic API Key]
    
    style A fill:#e3f2fd
    style C1 fill:#9c27b0
```

### 🎛️ Configuration Options

#### Basic Configuration

```python
from litellm import completion

# Simple model switching
response = completion(
    model="gpt-4",           # OpenAI
    # model="gemini-pro",    # Google
    # model="claude-3-sonnet", # Anthropic
    messages=[{"role": "user", "content": "Hello!"}]
)
```

#### Advanced Configuration

```python
# With custom settings
response = completion(
    model="gpt-4",
    messages=messages,
    temperature=0.7,
    max_tokens=150,
    fallbacks=["gpt-3.5-turbo", "gemini-pro"],
    timeout=30
)
```

### 🏗️ ADK Integration

```mermaid
graph TD
    A[ADK Agent] --> B[LiteLLM Integration]
    B --> C[Model Configuration]
    B --> D[Provider Setup]
    B --> E[Fallback Strategy]
    
    C --> C1[Primary Model]
    C --> C2[Alternative Models]
    
    D --> D1[API Keys]
    D --> D2[Base URLs]
    D --> D3[Custom Settings]
    
    E --> E1[Error Handling]
    E --> E2[Automatic Retry]
    E --> E3[Provider Switching]
    
    style B fill:#9c27b0
    style C1 fill:#4caf50
    style E1 fill:#ff9800
```

## 🚀 Getting Started

### 📋 Prerequisites Checklist

- [ ] ✅ Virtual environment activated
- [ ] 🔑 Multiple provider API keys (optional but recommended)
- [ ] 📦 LiteLLM library installed
- [ ] 📁 Proper project structure

### 🔧 Environment Setup

```mermaid
graph LR
    A[Root Directory] --> B[Activate .venv]
    B --> C[Navigate to 3-litellm-agent]
    C --> D[Configure API Keys]
    D --> E[Install LiteLLM]
    E --> F[Ready to Run]
    
    style A fill:#e3f2fd
    style F fill:#c8e6c9
```

#### 🔌 Virtual Environment Activation

```bash
# 🔌 Activate virtual environment (from parent directory)
# macOS/Linux:
source ../.venv/bin/activate

# Windows CMD:
..\.venv\Scripts\activate.bat

# Windows PowerShell:
..\.venv\Scripts\Activate.ps1
```

#### 📦 Install LiteLLM

```bash
# Install LiteLLM if not already installed
pip install litellm
```

#### 🔑 Multi-Provider API Configuration

```mermaid
sequenceDiagram
    participant U as User
    participant E as .env File
    participant L as LiteLLM
    participant P as Providers
    
    U->>E: Add multiple API keys
    E->>L: Load configuration
    L->>P: Authenticate with providers
    P->>L: Confirm access
    L->>U: Ready for multi-provider use
```

Create or update your `.env` file:

```bash
# Primary providers
OPENAI_API_KEY=your_openai_key_here
GOOGLE_API_KEY=your_google_key_here
ANTHROPIC_API_KEY=your_anthropic_key_here

# Optional providers
AZURE_API_KEY=your_azure_key_here
COHERE_API_KEY=your_cohere_key_here
```

### 🎯 Model Selection Strategy

| Priority | Model | Provider | Use Case |
|----------|-------|----------|----------|
| 1️⃣ | **gpt-4** | OpenAI | Complex reasoning tasks |
| 2️⃣ | **gemini-pro** | Google | Fast, general purpose |
| 3️⃣ | **claude-3-sonnet** | Anthropic | Analysis, safety-focused |
| 4️⃣ | **gpt-3.5-turbo** | OpenAI | Quick, cost-effective |

## 🎮 Running the Example

### 🌐 Interactive Web UI

```mermaid
graph TD
    A[Navigate to 3-litellm-agent] --> B[Run: adk web]
    B --> C[Server Starts]
    C --> D[Open Browser: localhost:8000]
    D --> E[Select 'litellm_agent']
    E --> F[Test Multi-Provider]
    
    F --> G[Try Different Models]
    F --> H[Compare Responses]
    F --> I[Test Fallbacks]
    
    style F fill:#e3f2fd
    style G fill:#9c27b0
    style H fill:#ff9800
    style I fill:#f44336
```

### 🛠️ Available Run Methods

| Method | Command | Interface | Best For |
|--------|---------|-----------|----------|
| 🌐 **Web UI** | `adk web` | Browser-based | Interactive model testing |
| 💻 **Terminal** | `adk run litellm_agent` | Command line | Quick provider validation |
| 🔌 **API Server** | `adk api_server` | REST endpoints | Integration testing |

### 📝 Step-by-Step Process

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1️⃣ | Navigate to directory | `cd 3-litellm-agent` |
| 2️⃣ | Start web server | `adk web` |
| 3️⃣ | Open browser | Visit `http://localhost:8000` |
| 4️⃣ | Select agent | Choose "litellm_agent" from dropdown |
| 5️⃣ | Test functionality | Try model-specific prompts |

## 💬 Example Prompts to Try

### 🔄 Model Comparison Tests

```mermaid
graph LR
    A[Same Prompt] --> B[Multiple Models]
    B --> C[OpenAI Response]
    B --> D[Google Response]
    B --> E[Anthropic Response]
    
    C --> F[Compare Results]
    D --> F
    E --> F
    
    style A fill:#e3f2fd
    style F fill:#c8e6c9
```

### 📊 Test Categories

| Category | Example Prompts | Purpose |
|----------|-----------------|---------|
| 🧮 **Reasoning** | "Solve this logic puzzle: ..." | Compare analytical capabilities |
| 🎨 **Creativity** | "Write a short story about..." | Test creative differences |
| 💻 **Coding** | "Write a Python function to..." | Compare programming skills |
| 📊 **Analysis** | "Analyze the pros and cons of..." | Test analytical depth |
| 🌐 **Current Events** | "What do you know about..." | Test knowledge cutoffs |

### 🎯 Model-Specific Tests

#### 🤖 OpenAI (GPT-4) Tests
- "Explain quantum computing in simple terms"
- "Debug this Python code: [code snippet]"
- "Create a business plan for a startup"

#### 🔍 Google (Gemini) Tests
- "What's the latest information about AI development?"
- "Help me plan a trip to Japan"
- "Analyze this data and provide insights"

#### 🧠 Anthropic (Claude) Tests
- "Please analyze the ethical implications of..."
- "Help me understand this complex research paper"
- "What are the potential risks and benefits of..."

## 🎉 Success Indicators

### ✅ Your LiteLLM Agent is Working When:

```mermaid
pie title LiteLLM Success Metrics
    "Model Switching" : 25
    "Provider Diversity" : 25
    "Response Quality" : 25
    "Fallback Handling" : 25
```

| Indicator | Description | What to Look For |
|-----------|-------------|------------------|
| 🔄 **Model Switching** | Can change providers easily | Different response styles |
| 🌐 **Provider Access** | Multiple providers working | No authentication errors |
| 📊 **Response Quality** | Consistent quality across models | Appropriate responses |
| 🛡️ **Error Handling** | Graceful fallback behavior | Automatic provider switching |

### 🔧 Testing Checklist

- [ ] 🔄 Successfully switch between models
- [ ] 🌐 Multiple providers accessible
- [ ] 🛡️ Fallback mechanisms working
- [ ] 📊 Response quality maintained
- [ ] 💰 Cost tracking functional (if enabled)
- [ ] ⚡ Rate limiting respected

## 🔄 Advanced Features

### 🛡️ Fallback Configuration

```mermaid
graph TD
    A[Primary Model Fails] --> B{Fallback Enabled?}
    B -->|Yes| C[Try Fallback Model]
    B -->|No| D[Return Error]
    
    C --> E{Fallback Success?}
    E -->|Yes| F[Return Response]
    E -->|No| G[Try Next Fallback]
    
    G --> H{More Fallbacks?}
    H -->|Yes| I[Try Next Model]
    H -->|No| J[Return Final Error]
    
    I --> E
    
    style A fill:#f44336
    style F fill:#4caf50
    style J fill:#f44336
```

### 💰 Cost Management

```mermaid
graph TD
    A[Cost Management] --> B[Budget Monitoring]
    A --> C[Usage Tracking]
    A --> D[Cost Optimization]
    
    B --> B1[Set Spending Limits]
    B --> B2[Alert Thresholds]
    B --> B3[Provider Budgets]
    
    C --> C1[Token Consumption]
    C --> C2[Request Frequency]
    C --> C3[Model Usage Stats]
    
    D --> D1[Model Selection Rules]
    D --> D2[Cheap Models for Simple Tasks]
    D --> D3[Expensive Models for Complex Tasks]
    
    style A fill:#4caf50
    style B1 fill:#ff9800
    style D1 fill:#2196f3
```

| Feature | Description | Configuration |
|---------|-------------|---------------|
| 🎯 **Budget Limits** | Set spending limits per provider | `max_budget=100` |
| 📊 **Usage Tracking** | Monitor token consumption | `track_cost=True` |
| ⚖️ **Cost Optimization** | Choose cheaper models for simple tasks | Model routing rules |

### ⚡ Performance Optimization

```mermaid
graph LR
    A[Request] --> B{Load Balancing}
    B --> C[Provider 1]
    B --> D[Provider 2]
    B --> E[Provider 3]
    
    C --> F[Response Aggregation]
    D --> F
    E --> F
    
    F --> G[Optimized Response]
    
    style B fill:#2196f3
    style G fill:#4caf50
```

### 🔐 Security Best Practices

```mermaid
mindmap
  root)Security(
    API Key Management
      Environment Variables
      Key Rotation
      Access Controls
      Secure Storage
    Network Security
      HTTPS Only
      Certificate Validation
      Timeout Handling
      Rate Limiting
    Data Privacy
      No Logging Sensitive Data
      Encryption in Transit
      Minimal Data Retention
      Compliance Standards
```

## 🚪 Troubleshooting

### 🔧 Common Issues

```mermaid
flowchart TD
    A[Issue Detected] --> B{Authentication Error?}
    B -->|Yes| C[Check API Keys]
    B -->|No| D{Model Not Found?}
    D -->|Yes| E[Verify Model Name]
    D -->|No| F{Rate Limit?}
    F -->|Yes| G[Enable Rate Limiting]
    F -->|No| H{Network Error?}
    H -->|Yes| I[Check Internet Connection]
    H -->|No| J[Check LiteLLM Logs]
    
    style A fill:#f44336
    style C fill:#ff9800
    style E fill:#ff9800
    style G fill:#ff9800
    style I fill:#ff9800
    style J fill:#ff9800
```

| Issue | Cause | Solution |
|-------|-------|----------|
| 🚫 **Authentication Failed** | Invalid API keys | Check `.env` file configuration |
| 🔍 **Model Not Found** | Incorrect model name | Verify model availability |
| ⚡ **Rate Limit Exceeded** | Too many requests | Enable rate limiting |
| 🌐 **Network Timeout** | Connection issues | Check internet/firewall |
| 💰 **Budget Exceeded** | Cost limits reached | Review usage or increase budget |

### 🛠️ Debug Commands

```bash
# Check LiteLLM configuration
python -c "import litellm; print(litellm.get_supported_openai_params())"

# Test provider connectivity
python -c "from litellm import completion; print(completion(model='gpt-3.5-turbo', messages=[{'role': 'user', 'content': 'test'}]))"

# View available models
python -c "import litellm; print(litellm.model_list)"
```

### 🛑 Exit Options

```bash
# Stop any running ADK command
Ctrl+C
```

## 🎓 What You've Learned

### 🏆 Key Achievements

- [ ] 🔄 Integrated multiple LLM providers seamlessly
- [ ] 🌐 Implemented provider abstraction layer
- [ ] 🛡️ Configured fallback mechanisms
- [ ] 📊 Compared different model capabilities
- [ ] 💰 Understood cost management strategies
- [ ] ⚡ Optimized performance with load balancing
- [ ] 🔐 Applied security best practices
- [ ] 🔧 Mastered troubleshooting techniques

### 🚀 Next Steps

Ready for more advanced concepts?

| Next Example | Focus | Complexity | Key Concepts |
|--------------|-------|------------|--------------|
| 📊 **Structured Outputs** | Data formatting | ⭐⭐ | Pydantic models, schemas |
| 💾 **Sessions & State** | Memory management | ⭐⭐⭐ | State persistence, context |
| 🏪 **Persistent Storage** | Data durability | ⭐⭐⭐ | Database integration |

### 🎯 Advanced Concepts to Explore

```mermaid
graph TD
    A[Current: LiteLLM Agent] --> B[Structured Outputs]
    A --> C[Sessions & State]
    A --> D[Persistent Storage]
    
    B --> E[Multi-Agent Systems]
    C --> E
    D --> E
    
    E --> F[Stateful Multi-Agent]
    E --> G[Callbacks & Monitoring]
    
    F --> H[Sequential Agents]
    F --> I[Parallel Agents]
    F --> J[Loop Agents]
    
    style A fill:#9c27b0
    style E fill:#ff9800
    style H fill:#4caf50
    style I fill:#4caf50
    style J fill:#4caf50
```

## 📚 Additional Resources

### 🔗 Official Documentation

| Resource | Focus | Link |
|----------|-------|------|
| 📖 **LiteLLM Docs** | Complete LiteLLM guide | [LiteLLM Documentation](https://litellm.ai/) |
| 🔧 **Provider Setup** | API key configuration | [Provider Configuration](https://litellm.vercel.app/docs/providers) |
| 💰 **Cost Management** | Budget and tracking | [Cost Tracking Guide](https://litellm.vercel.app/docs/proxy/cost_tracking) |
| 🛡️ **Fallbacks** | Reliability patterns | [Fallback Configuration](https://litellm.vercel.app/docs/completion/reliable_completions) |

### 🎯 Best Practices

```mermaid
mindmap
  root)LiteLLM Best Practices(
    Security
      Secure API key storage
      Environment variables
      Key rotation
      Access controls
    Performance
      Model selection strategy
      Caching responses
      Rate limit handling
      Load balancing
    Cost Management
      Budget monitoring
      Model cost comparison
      Usage optimization
      Fallback hierarchy
    Reliability
      Fallback configuration
      Error handling
      Health monitoring
      Timeout management
    Development
      Testing strategies
      Debugging techniques
      Monitoring setup
      Documentation
```

### 📊 Model Performance Comparison

| Aspect | OpenAI GPT-4 | Google Gemini | Anthropic Claude | Azure OpenAI |
|--------|--------------|---------------|------------------|--------------|
| 🧮 **Reasoning** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 🎨 **Creativity** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 💻 **Coding** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| ⚡ **Speed** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| 💰 **Cost** | ⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| 🛡️ **Safety** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |

### 🔄 Migration Guide

If you're migrating from a single-provider setup to LiteLLM:

```mermaid
graph LR
    A[Single Provider Code] --> B[Identify Dependencies]
    B --> C[Install LiteLLM]
    C --> D[Update Imports]
    D --> E[Modify Model Names]
    E --> F[Add Fallbacks]
    F --> G[Test All Providers]
    G --> H[Deploy with Monitoring]
    
    style A fill:#ffcdd2
    style H fill:#c8e6c9
```

---

<div align="center">

### 🎉 Congratulations! 

You've mastered multi-provider LLM integration with LiteLLM! 

[![Next: Structured Outputs](https://img.shields.io/badge/Next-Structured%20Outputs-teal?style=for-the-badge&logo=arrow-right)](../4-structured-outputs/)
[![Previous: Tool Agent](https://img.shields.io/badge/Previous-Tool%20Agent-orange?style=for-the-badge&logo=arrow-left)](../2-tool-agent/)
[![Back to Main](https://img.shields.io/badge/Back-Main%20Course-green?style=for-the-badge&logo=home)](../)

*Ready to structure your agent responses? Let's explore Pydantic schemas! 📊*

</div>

# 💾 Sessions and State Management in ADK

[![ADK](https://img.shields.io/badge/ADK-Sessions%20%26%20State-indigo.svg)](https://google.github.io/adk-docs/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow.svg)](.)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![State Management](https://img.shields.io/badge/State-Memory%20Enabled-purple.svg)](.)

> 🎯 **Give Your Agents Memory** - Learn to create stateful agents that remember user information and maintain context across interactions

## 🧠 What Are Sessions in ADK?

**Sessions** in ADK provide persistent memory for your agents, enabling them to maintain context, store user data, and build relationships over time rather than forgetting everything between interactions.

### 🔄 Stateless vs Stateful Agents

```mermaid
graph TB
    subgraph "Stateless Agent"
        A1[User Query 1] --> B1[Fresh Agent]
        B1 --> C1[Response 1]
        C1 --> D1[Forget Everything]
        
        A2[User Query 2] --> B2[Fresh Agent]
        B2 --> C2[Response 2]
        C2 --> D2[Forget Everything]
    end
    
    subgraph "Stateful Agent"
        A3[User Query 1] --> B3[Agent + Session]
        B3 --> C3[Response 1]
        C3 --> D3[Store Context]
        
        A4[User Query 2] --> B4[Agent + Session]
        B4 --> E4[Access Previous Context]
        E4 --> C4[Contextual Response 2]
        C4 --> D4[Update Context]
    end
    
    style D1 fill:#ffcdd2
    style D2 fill:#ffcdd2
    style D3 fill:#c8e6c9
    style D4 fill:#c8e6c9
    style E4 fill:#fff3e0
```

### 🏗️ Core Session Capabilities

| Capability | Description | Benefit |
|------------|-------------|---------|
| 💾 **Maintain State** | Store user data and preferences persistently | Personalized experiences |
| 📜 **Conversation History** | Automatic message history tracking | Context-aware responses |
| 🎯 **Personalization** | Use stored information for tailored responses | Better user relationships |
| 🔄 **Context Continuity** | Remember previous interactions | Seamless multi-turn conversations |
| 📊 **User Profiling** | Build comprehensive user profiles over time | Adaptive behavior |

## 🏗️ Session Architecture

### 🔧 Session Lifecycle

```mermaid
sequenceDiagram
    participant U as User
    participant R as Runner
    participant S as Session Service
    participant A as Agent
    participant M as Memory Store
    
    U->>R: Start Conversation
    R->>S: Create/Load Session
    S->>M: Initialize State
    M->>S: State Ready
    S->>R: Session Created
    
    loop Each Interaction
        U->>R: Send Message
        R->>S: Get Current State
        S->>A: Provide Context
        A->>A: Process with Context
        A->>S: Update State
        S->>M: Persist Changes
        A->>U: Contextual Response
    end
```

### 📊 State Management Flow

```mermaid
graph TD
    A[Session Creation] --> B[Initial State Setup]
    B --> C[Agent Execution]
    C --> D[Template Variable Resolution]
    D --> E[Context-Aware Processing]
    E --> F[State Updates]
    F --> G[Persistence Layer]
    G --> H[Next Interaction Ready]
    
    H --> C
    
    style A fill:#e3f2fd
    style E fill:#4caf50
    style G fill:#ff9800
    style H fill:#9c27b0
```

### 🗄️ Session Components

```mermaid
graph TD
    A[Session System] --> B[Session Service]
    A --> C[State Store]
    A --> D[Template Engine]
    A --> E[Runner Integration]
    
    B --> B1[InMemorySessionService]
    B --> B2[DatabaseSessionService]
    B --> B3[Custom Service]
    
    C --> C1[User Preferences]
    C --> C2[Conversation History]
    C --> C3[Context Data]
    C --> C4[Metadata]
    
    D --> D1[Variable Substitution]
    D --> D2[Dynamic Instructions]
    
    E --> E1[Automatic State Management]
    E --> E2[Session Lifecycle]
    
    style A fill:#2196f3
    style B1 fill:#4caf50
    style C1 fill:#ff9800
    style D1 fill:#9c27b0
    style E1 fill:#f44336
```

## 🎯 Example Overview

### 👤 User Profile Management

```mermaid
mindmap
  root)User Profile(
    Personal Info
      Name
      Age
      Location
      Contact details
    Preferences
      Interests
      Hobbies
      Favorite foods
      Entertainment
    Behavior
      Communication style
      Response preferences
      Interaction patterns
      Feedback history
    Context
      Current session
      Previous conversations
      Goals and objectives
      Relationship status
```

### 🔄 State Updates and Access

```mermaid
graph LR
    A[User Input] --> B[Agent Processing]
    B --> C{State Update Needed?}
    
    C -->|Yes| D[Update State]
    C -->|No| E[Use Existing State]
    
    D --> F[Template Resolution]
    E --> F
    
    F --> G[Generate Response]
    G --> H[Store Interaction History]
    H --> I[Return Response]
    
    style D fill:#4caf50
    style E fill:#ff9800
    style H fill:#9c27b0
```

## 🏗️ Project Structure

### 📁 Directory Organization

```mermaid
graph TD
    A[5-sessions-and-state/] --> B[basic_stateful_session.py]
    A --> C[question_answering_agent/]
    A --> D[README.md]
    A --> E[.env.example]
    
    B --> F[Main Example Script]
    F --> G[Session Creation]
    F --> H[State Management]
    F --> I[Agent Execution]
    
    C --> J[__init__.py]
    C --> K[agent.py]
    
    J --> L[Package Discovery]
    K --> M[Agent Definition]
    K --> N[Template Variables]
    K --> O[State Access]
    
    style A fill:#e3f2fd
    style B fill:#4caf50
    style K fill:#ff9800
    style N fill:#9c27b0
```

```
5-sessions-and-state/
│
├── basic_stateful_session.py      # 🚀 Main example execution
│   ├── Session creation
│   ├── State initialization  
│   ├── Agent configuration
│   └── Interactive demonstration
│
├── question_answering_agent/      # 🤖 Stateful Agent Package
│   ├── __init__.py               # 📦 Package initialization
│   └── agent.py                  # 🧠 Agent with template variables
│
├── .env.example                  # 📋 Environment template
└── README.md                     # 📖 Documentation
```

## 🔧 Key Components Deep Dive

### 1️⃣ Session Service Types

```mermaid
graph TD
    A[Session Service Options] --> B[InMemorySessionService]
    A --> C[DatabaseSessionService]
    A --> D[Custom Implementation]
    
    B --> B1[Development & Testing]
    B --> B2[Temporary Storage]
    B --> B3[Fast Access]
    
    C --> C1[Production Use]
    C --> C2[Persistent Storage]
    C --> C3[Scalable Solution]
    
    D --> D1[Specialized Requirements]
    D --> D2[External Systems]
    D --> D3[Custom Logic]
    
    style B fill:#4caf50
    style C fill:#ff9800
    style D fill:#9c27b0
```

| Service Type | Use Case | Persistence | Scalability |
|--------------|----------|-------------|-------------|
| 💾 **InMemory** | Development, testing | Temporary | Single instance |
| 🗄️ **Database** | Production, enterprise | Permanent | Highly scalable |
| 🔧 **Custom** | Specialized needs | Configurable | Depends on implementation |

### 2️⃣ Initial State Configuration

```mermaid
graph LR
    A[Initial State] --> B[User Information]
    A --> C[Preferences]
    A --> D[Context Data]
    A --> E[Metadata]
    
    B --> B1[Name, ID, Profile]
    C --> C1[Interests, Settings]
    D --> D1[Current Goals, Status]
    E --> E1[Created, Modified, Version]
    
    style A fill:#2196f3
    style B1 fill:#4caf50
    style C1 fill:#ff9800
    style D1 fill:#9c27b0
    style E1 fill:#f44336
```

#### 📋 State Structure Example

```python
initial_state = {
    # User Identity
    "user_name": "Brandon Hancock",
    "user_id": "user_12345",
    
    # Preferences & Interests
    "user_preferences": {
        "sports": ["Pickleball", "Disc Golf", "Tennis"],
        "food": ["Mexican", "Italian"],
        "entertainment": ["Game of Thrones", "YouTube"],
        "communication_style": "casual_friendly"
    },
    
    # Context & Goals
    "current_context": {
        "session_goal": "learning_about_preferences",
        "interaction_count": 0,
        "last_topic": None
    },
    
    # History & Metadata
    "session_metadata": {
        "created_at": "2023-11-01T10:00:00Z",
        "last_updated": "2023-11-01T10:00:00Z",
        "version": "1.0"
    }
}
```

### 3️⃣ Template Variables in Action

```mermaid
sequenceDiagram
    participant A as Agent Instructions
    participant T as Template Engine
    participant S as Session State
    participant L as LLM
    
    A->>T: Raw Instruction with {variables}
    T->>S: Request Current State
    S->>T: Return State Data
    T->>T: Replace Variables with Values
    T->>L: Send Resolved Instructions
    L->>A: Process with Context
```

#### 🔧 Template Resolution Example

```python
# Original instruction with template variables
instruction = """
You are a helpful assistant for {user_name}.

User Preferences:
{user_preferences}

Current Context:
{current_context}
"""

# After template resolution
resolved_instruction = """
You are a helpful assistant for Brandon Hancock.

User Preferences:
Sports: Pickleball, Disc Golf, Tennis
Food: Mexican cuisine
Shows: Game of Thrones

Current Context:
Goal: Learning about user preferences
Interaction: 3rd conversation
"""
```

## 🚀 Getting Started

### 📋 Prerequisites Checklist

- [ ] ✅ Virtual environment activated
- [ ] 🔑 Google API key configured
- [ ] 🧠 Understanding of agent basics
- [ ] 📊 Familiarity with data structures

### 🔧 Environment Setup

```mermaid
graph LR
    A[Root Directory] --> B[Activate .venv]
    B --> C[Navigate to 5-sessions-and-state]
    C --> D[Configure API Key]
    D --> E[Ready to Run]
    
    style A fill:#e3f2fd
    style E fill:#c8e6c9
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

#### 🔑 API Key Configuration

Create `.env` file in the project directory:

```bash
# Copy template and configure
cp .env.example .env

# Add your API key
GOOGLE_API_KEY=your_google_api_key_here
```

## 🎮 Running the Example

### 🖥️ Script Execution

```mermaid
graph TD
    A[Run basic_stateful_session.py] --> B[Session Creation]
    B --> C[Initial State Setup]
    C --> D[Agent Initialization]
    D --> E[Template Resolution]
    E --> F[User Query Processing]
    F --> G[Contextual Response]
    G --> H[State Update]
    H --> I[Display Results]
    
    style A fill:#e3f2fd
    style G fill:#4caf50
    style H fill:#ff9800
    style I fill:#9c27b0
```

### 📝 Step-by-Step Execution

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1️⃣ | **Navigate to directory** | `cd 5-sessions-and-state` |
| 2️⃣ | **Run example script** | `python basic_stateful_session.py` |
| 3️⃣ | **Observe session creation** | Session initialized with user data |
| 4️⃣ | **Watch template resolution** | Variables replaced with actual values |
| 5️⃣ | **View contextual response** | Agent responds using stored preferences |

### 🔄 Execution Flow

```mermaid
sequenceDiagram
    participant S as Script
    participant SS as Session Service
    participant AG as Agent
    participant R as Runner
    
    S->>SS: Create InMemorySessionService
    S->>SS: Create session with initial state
    SS->>S: Return session ID
    
    S->>AG: Initialize agent with templates
    S->>R: Create runner with session service
    
    S->>R: Send user query
    R->>SS: Get session state
    R->>AG: Execute with context
    AG->>R: Return contextual response
    R->>S: Display result
```

## 💬 Example Interactions and Results

### 🎯 Sample Queries and Responses

```mermaid
graph LR
    A[User Queries] --> B[Sports Interests]
    A --> C[Food Preferences]
    A --> D[Entertainment]
    A --> E[Personal Details]
    
    B --> F[Contextual Sports Response]
    C --> G[Food Recommendation]
    D --> H[Show Discussion]
    E --> I[Personalized Interaction]
    
    style F fill:#4caf50
    style G fill:#4caf50
    style H fill:#4caf50
    style I fill:#4caf50
```

### 📊 Response Quality Comparison

| Query Type | Without Session | With Session | Improvement |
|------------|-----------------|--------------|-------------|
| 🏓 **Sports** | Generic sports info | Personalized to pickleball, disc golf, tennis | 🎯 Highly targeted |
| 🌮 **Food** | General food advice | Mexican cuisine focus | 🎯 Preference-aware |
| 📺 **Entertainment** | Random suggestions | Game of Thrones references | 🎯 Interest-aligned |
| 👤 **Personal** | Formal responses | Uses name "Brandon" | 🎯 Relationship building |

### 🔄 State Evolution

```mermaid
graph TD
    A[Initial State] --> B[First Interaction]
    B --> C[Updated Preferences]
    C --> D[Second Interaction]
    D --> E[Enriched Context]
    E --> F[Third Interaction]
    F --> G[Comprehensive Profile]
    
    A --> A1[Basic user info]
    C --> C1[Interaction patterns]
    E --> E1[Conversation history]
    G --> G1[Rich user model]
    
    style A1 fill:#ffcdd2
    style C1 fill:#fff3e0
    style E1 fill:#e8f5e8
    style G1 fill:#e3f2fd
```

## 🎉 Success Indicators

### ✅ Your Session Management is Working When:

```mermaid
pie title Session Success Metrics
    "State Persistence" : 25
    "Context Awareness" : 25
    "Template Resolution" : 25
    "Personalization" : 25
```

| Indicator | Description | What to Look For |
|-----------|-------------|------------------|
| 💾 **State Persistence** | Data survives between interactions | Preferences remembered |
| 🧠 **Context Awareness** | Agent uses stored information | Relevant, personalized responses |
| 🔧 **Template Resolution** | Variables properly substituted | Instructions include user data |
| 🎯 **Personalization** | Responses tailored to user | Name usage, preference alignment |

### 🔧 Testing Checklist

- [ ] 💾 Session created successfully
- [ ] 📋 Initial state populated correctly
- [ ] 🔧 Template variables resolved
- [ ] 🧠 Agent accesses session data
- [ ] 🎯 Responses show personalization
- [ ] 🔄 State updates between interactions
- [ ] 📊 Conversation history maintained

## 🔄 Advanced Session Patterns

### 🏗️ Complex State Management

```mermaid
graph TD
    A[Advanced State Patterns] --> B[Nested Objects]
    A --> C[Dynamic Updates]
    A --> D[State Validation]
    A --> E[Cross-Session Data]
    
    B --> B1[User Profile Hierarchy]
    B --> B2[Preference Categories]
    
    C --> C1[Real-time Updates]
    C --> C2[Incremental Changes]
    
    D --> D1[Schema Validation]
    D --> D2[Data Integrity]
    
    E --> E1[Shared Preferences]
    E --> E2[Global Context]
    
    style A fill:#2196f3
    style B1 fill:#4caf50
    style C1 fill:#ff9800
    style D1 fill:#9c27b0
    style E1 fill:#f44336
```

### 📊 State Schema Design

```mermaid
classDiagram
    class SessionState {
        +string user_id
        +UserProfile user_profile
        +Preferences preferences
        +Context current_context
        +History conversation_history
        +Metadata metadata
    }
    
    class UserProfile {
        +string name
        +string email
        +Demographics demographics
        +ContactInfo contact
    }
    
    class Preferences {
        +dict interests
        +dict settings
        +dict communication_style
        +dict content_preferences
    }
    
    class Context {
        +string current_goal
        +string session_type
        +dict temporary_data
        +list active_topics
    }
    
    SessionState --> UserProfile
    SessionState --> Preferences
    SessionState --> Context
```

### 🔐 Session Security and Privacy

```mermaid
mindmap
  root)Session Security(
    Data Protection
      Encryption at rest
      Secure transmission
      Access controls
      Data anonymization
    Privacy Compliance
      GDPR compliance
      Data retention policies
      User consent
      Right to deletion
    Session Management
      Secure session IDs
      Session expiration
      Logout handling
      Concurrent sessions
    Access Controls
      Authentication
      Authorization
      Role-based access
      Audit logging
```

## 🚪 Troubleshooting

### 🔧 Common Issues

```mermaid
flowchart TD
    A[Session Issue Detected] --> B{Template Error?}
    B -->|Yes| C[Check Variable Names]
    B -->|No| D{State Not Persisting?}
    D -->|Yes| E[Verify Session Service]
    D -->|No| F{Context Missing?}
    F -->|Yes| G[Check State Structure]
    F -->|No| H{Performance Issues?}
    H -->|Yes| I[Optimize State Size]
    H -->|No| J[Check Agent Configuration]
    
    style A fill:#f44336
    style C fill:#ff9800
    style E fill:#ff9800
    style G fill:#ff9800
    style I fill:#ff9800
    style J fill:#ff9800
```

| Issue | Cause | Solution |
|-------|-------|----------|
| 🔧 **Template Errors** | Variable name mismatch | Check variable naming consistency |
| 💾 **State Not Persisting** | Session service misconfiguration | Verify session service setup |
| 🧠 **Missing Context** | Incorrect state structure | Validate state schema |
| ⚡ **Performance Issues** | Large state objects | Optimize state data size |
| 🔍 **Variables Not Resolving** | Template syntax errors | Check template syntax |

### 🛠️ Debug Commands

```bash
# Test session creation
python -c "from basic_stateful_session import *; test_session_creation()"

# Inspect session state
python -c "from basic_stateful_session import *; print_session_state()"

# Validate template resolution
python -c "from basic_stateful_session import *; test_template_resolution()"
```

### 🛑 Exit Options

```bash
# Stop script execution
Ctrl+C
```

## 🎓 What You've Learned

### 🏆 Key Achievements

- [ ] 🧠 Implemented persistent memory for agents
- [ ] 💾 Created and managed session services
- [ ] 🔧 Used template variables for dynamic instructions
- [ ] 📊 Built comprehensive user state models
- [ ] 🎯 Achieved personalized agent responses
- [ ] 🔄 Managed state lifecycle and updates
- [ ] 🛠️ Mastered session troubleshooting
- [ ] 🔐 Understood security considerations

### 🚀 Next Steps

Ready for more advanced concepts?

| Next Example | Focus | Complexity | Key Concepts |
|--------------|-------|------------|--------------|
| 🏪 **Persistent Storage** | Database integration | ⭐⭐⭐ | Data durability, scaling |
| 🤖 **Multi-Agent** | Agent orchestration | ⭐⭐⭐⭐ | Agent coordination |
| 🔄 **Stateful Multi-Agent** | Complex state management | ⭐⭐⭐⭐⭐ | Distributed state |

### 🎯 Advanced Concepts to Explore

```mermaid
graph TD
    A[Current: Sessions & State] --> B[Persistent Storage]
    A --> C[Multi-Agent Systems]
    A --> D[Stateful Multi-Agent]
    
    B --> E[Database Integration]
    B --> F[Data Scaling]
    
    C --> G[Agent Coordination]
    C --> H[Message Passing]
    
    D --> I[Distributed State]
    D --> J[Complex Workflows]
    
    style A fill:#4caf50
    style B fill:#ff9800
    style C fill:#2196f3
    style D fill:#9c27b0
```

## 📚 Additional Resources

### 🔗 Official Documentation

| Resource | Focus | Link |
|----------|-------|------|
| 📖 **ADK Sessions** | Complete session guide | [ADK Sessions Documentation](https://google.github.io/adk-docs/sessions/session/) |
| 🔧 **State Management** | Advanced state techniques | [State Management Guide](https://google.github.io/adk-docs/sessions/state/) |
| 🛠️ **Session Services** | Service implementation patterns | [Session Service Patterns](https://google.github.io/adk-docs/sessions/session_service/) |
| 📊 **Template Variables** | Dynamic instruction generation | [Template Documentation](https://google.github.io/adk-docs/sessions/template_variables/) |

### 🎯 Best Practices

```mermaid
mindmap
  root)Session Best Practices(
    State Design
      Keep states focused
      Avoid deep nesting
      Use clear naming
      Plan for scalability
    Performance
      Minimize state size
      Efficient updates
      Lazy loading
      Cache frequently used data
    Security
      Encrypt sensitive data
      Validate inputs
      Implement access controls
      Audit state changes
    Maintenance
      Document state schema
      Version state structure
      Handle migrations
      Monitor usage patterns
```

### 📊 Session Performance Patterns

| Pattern | Use Case | Benefits | Considerations |
|---------|----------|----------|----------------|
| 🔄 **Minimal State** | Simple preferences | Fast access, low memory | Limited context |
| 📋 **Rich Profiles** | Complex personalization | Deep context, better UX | Higher resource usage |
| 🗂️ **Hierarchical State** | Organized data | Structured access | Complexity overhead |
| ⚡ **Cached State** | High-frequency access | Performance optimized | Cache invalidation |

---

<div align="center">

### 🎉 Congratulations! 

You've mastered sessions and state management in ADK! 

[![Next: Persistent Storage](https://img.shields.io/badge/Next-Persistent%20Storage-brown?style=for-the-badge&logo=arrow-right)](../6-persistent-storage/)
[![Previous: Structured Outputs](https://img.shields.io/badge/Previous-Structured%20Outputs-teal?style=for-the-badge&logo=arrow-left)](../4-structured-outputs/)
[![Back to Main](https://img.shields.io/badge/Back-Main%20Course-green?style=for-the-badge&logo=home)](../)

*Ready to make your data permanent? Let's explore persistent storage! 🏪*

</div>

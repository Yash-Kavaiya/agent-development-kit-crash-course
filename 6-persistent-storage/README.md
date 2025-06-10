# 🏪 Persistent Storage in ADK

[![ADK](https://img.shields.io/badge/ADK-Persistent%20Storage-brown.svg)](https://google.github.io/adk-docs/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Advanced-red.svg)](.)
[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Database](https://img.shields.io/badge/Database-SQLite%20%7C%20PostgreSQL-green.svg)](.)

> 🎯 **Make Your Agents Remember Forever** - Learn to implement persistent storage for long-term memory, conversation history, and production-ready data durability

## 🗄️ What is Persistent Storage in ADK?

**Persistent Storage** in ADK enables your agents to maintain long-term memory by storing session data in databases, ensuring information survives application restarts, deployments, and system failures.

### 💾 Memory Persistence Comparison

```mermaid
graph TB
    subgraph "InMemory Storage (Temporary)"
        A1[Agent Session] --> B1[RAM Storage]
        B1 --> C1[Application Restart]
        C1 --> D1[Data Lost Forever]
        
        style D1 fill:#ffcdd2
    end
    
    subgraph "Persistent Storage (Permanent)"
        A2[Agent Session] --> B2[Database Storage]
        B2 --> C2[Application Restart]
        C2 --> D2[Data Survives]
        D2 --> E2[Session Continues]
        
        style D2 fill:#c8e6c9
        style E2 fill:#c8e6c9
    end
    
    F[Production Benefits] --> G[Long-term Memory]
    F --> H[Multi-user Support]
    F --> I[Scalability]
    F --> J[Data Integrity]
```

### 🏗️ Core Benefits

| Benefit | Description | Impact |
|---------|-------------|--------|
| 🕒 **Long-term Memory** | Data persists across restarts | Continuous user relationships |
| 🔄 **Session Continuity** | Resume conversations anywhere | Seamless user experience |
| 👥 **Multi-user Support** | Separate, secure user data | Enterprise scalability |
| 📈 **Production Ready** | Handle real-world loads | Business-grade applications |
| 🛡️ **Data Integrity** | ACID compliance | Reliable data operations |

## 🏗️ Persistent Storage Architecture

### 🔧 Database Integration Flow

```mermaid
sequenceDiagram
    participant A as Agent
    participant D as DatabaseSessionService
    participant DB as Database
    participant S as SQL Engine
    
    A->>D: Initialize Session
    D->>DB: Check Existing Sessions
    DB->>S: Query Sessions Table
    S->>DB: Return Results
    DB->>D: Session Data
    
    alt Existing Session Found
        D->>A: Load Previous State
    else No Session
        D->>DB: Create New Session
        DB->>S: INSERT Session
        S->>DB: Confirm Creation
        D->>A: Fresh Session Ready
    end
    
    loop Each Interaction
        A->>D: Update State
        D->>DB: Persist Changes
        DB->>S: COMMIT Transaction
    end
```

### 🗄️ Database Service Architecture

```mermaid
graph TD
    A[ADK Application] --> B[DatabaseSessionService]
    B --> C[SQLAlchemy Engine]
    C --> D[Database Adapter]
    
    D --> E[SQLite]
    D --> F[PostgreSQL]
    D --> G[MySQL]
    D --> H[SQL Server]
    
    B --> I[Session Management]
    B --> J[State Persistence]
    B --> K[Transaction Handling]
    
    I --> L[Create/Load Sessions]
    J --> M[Automatic State Sync]
    K --> N[ACID Compliance]
    
    style B fill:#4caf50
    style C fill:#2196f3
    style I fill:#ff9800
    style J fill:#9c27b0
    style K fill:#f44336
```

### 📊 Storage Comparison Matrix

```mermaid
graph LR
    A[Storage Options] --> B[InMemory]
    A --> C[SQLite]
    A --> D[PostgreSQL]
    A --> E[Enterprise DB]
    
    B --> B1[Development Only]
    C --> C1[Small to Medium Scale]
    D --> D1[Production Scale]
    E --> E1[Enterprise Scale]
    
    style B1 fill:#ffcdd2
    style C1 fill:#fff3e0
    style D1 fill:#c8e6c9
    style E1 fill:#e3f2fd
```

## 🎯 Reminder Agent Example

### 🧠 Agent Capabilities

```mermaid
mindmap
  root)Reminder Agent(
    Personal Memory
      User names
      Preferences
      Interaction history
      Relationship context
    Task Management
      Add reminders
      Update tasks
      Delete completed items
      Priority management
    Data Persistence
      Cross-session memory
      Long-term storage
      Backup and recovery
      Data integrity
    User Experience
      Continuous conversations
      Personalized responses
      Context awareness
      Relationship building
```

### 🔄 State Management with Tools

```mermaid
graph TD
    A[User Request] --> B[Agent Processing]
    B --> C{Tool Required?}
    
    C -->|Yes| D[Execute Tool]
    C -->|No| E[Direct Response]
    
    D --> F[Tool Context Access]
    F --> G[Read Current State]
    G --> H[Modify State Data]
    H --> I[Auto-Persist to DB]
    
    E --> J[Generate Response]
    I --> J
    
    J --> K[Return to User]
    
    style D fill:#4caf50
    style I fill:#ff9800
    style K fill:#2196f3
```

### 🛠️ Tool-State Integration

```mermaid
sequenceDiagram
    participant U as User
    participant A as Agent
    participant T as Tool
    participant TC as ToolContext
    participant DB as Database
    
    U->>A: "Add reminder: buy groceries"
    A->>T: add_reminder(reminder, tool_context)
    T->>TC: Get current state
    TC->>DB: Fetch existing reminders
    DB->>TC: Return reminder list
    TC->>T: Current reminders data
    
    T->>T: Add new reminder to list
    T->>TC: Update state with new list
    TC->>DB: Persist updated state
    DB->>TC: Confirm persistence
    
    T->>A: Return success message
    A->>U: "Added reminder: buy groceries"
```

## 🏗️ Project Structure

### 📁 Directory Organization

```mermaid
graph TD
    A[6-persistent-storage/] --> B[memory_agent/]
    A --> C[main.py]
    A --> D[utils.py]
    A --> E[my_agent_data.db]
    A --> F[.env]
    A --> G[README.md]
    
    B --> H[__init__.py]
    B --> I[agent.py]
    
    C --> J[Application Entry Point]
    J --> K[Database Setup]
    J --> L[Session Management]
    J --> M[User Interface]
    
    D --> N[Terminal UI Functions]
    D --> O[Agent Interaction Helpers]
    
    E --> P[SQLite Database File]
    P --> Q[Sessions Table]
    P --> R[State Data]
    P --> S[Conversation History]
    
    I --> T[Agent Definition]
    T --> U[Reminder Tools]
    T --> V[State Access]
    T --> W[Persistence Logic]
    
    style A fill:#e3f2fd
    style E fill:#4caf50
    style I fill:#ff9800
    style T fill:#9c27b0
```

```
6-persistent-storage/
│
├── memory_agent/               # 🧠 Persistent Memory Agent
│   ├── __init__.py            # 📦 Package discovery
│   └── agent.py               # 🤖 Agent with persistent tools
│
├── main.py                    # 🚀 Application entry point
├── utils.py                   # 🛠️ Terminal UI utilities
├── my_agent_data.db          # 💾 SQLite database file
├── .env                      # 🔑 Environment variables
└── README.md                 # 📖 Documentation
```

## 🔧 Key Components Deep Dive

### 1️⃣ DatabaseSessionService Configuration

```mermaid
graph TD
    A[DatabaseSessionService] --> B[Database URL]
    A --> C[Connection Pooling]
    A --> D[Schema Management]
    A --> E[Transaction Handling]
    
    B --> B1[SQLite: sqlite:///./data.db]
    B --> B2[PostgreSQL: postgresql://user:pass@host/db]
    B --> B3[MySQL: mysql://user:pass@host/db]
    
    C --> C1[Connection Pool Size]
    C --> C2[Timeout Settings]
    C --> C3[Retry Logic]
    
    D --> D1[Auto Table Creation]
    D --> D2[Schema Migration]
    D --> D3[Index Management]
    
    E --> E1[ACID Compliance]
    E --> E2[Rollback Support]
    E --> E3[Deadlock Handling]
    
    style A fill:#2196f3
    style B1 fill:#4caf50
    style D1 fill:#ff9800
    style E1 fill:#9c27b0
```

#### 🔧 Database URL Examples

| Database | URL Format | Use Case |
|----------|------------|----------|
| 💾 **SQLite** | `sqlite:///./my_data.db` | Development, small deployments |
| 🐘 **PostgreSQL** | `postgresql://user:pass@host:5432/dbname` | Production, high concurrency |
| 🐬 **MySQL** | `mysql://user:pass@host:3306/dbname` | Web applications, shared hosting |
| 🏢 **SQL Server** | `mssql://user:pass@host/dbname` | Enterprise environments |

### 2️⃣ Session Lifecycle Management

```mermaid
stateDiagram-v2
    [*] --> CheckExisting
    CheckExisting --> LoadExisting: Session Found
    CheckExisting --> CreateNew: No Session
    
    LoadExisting --> Active
    CreateNew --> Active
    
    Active --> UpdateState: User Interaction
    UpdateState --> PersistData
    PersistData --> Active
    
    Active --> Cleanup: Session End
    Cleanup --> [*]
    
    note right of PersistData
        Automatic database
        persistence after
        every state change
    end note
```

### 3️⃣ State Persistence Mechanics

```mermaid
graph LR
    A[Tool Execution] --> B[Access ToolContext]
    B --> C[Read Current State]
    C --> D[Modify State Data]
    D --> E[Automatic Persistence]
    E --> F[Database Transaction]
    F --> G[COMMIT/ROLLBACK]
    
    G --> H{Success?}
    H -->|Yes| I[State Updated]
    H -->|No| J[Rollback Changes]
    
    style E fill:#4caf50
    style I fill:#c8e6c9
    style J fill:#ffcdd2
```

## 🚀 Getting Started

### 📋 Prerequisites Checklist

- [ ] ✅ Python 3.9+ installed
- [ ] 🔑 Google API key configured
- [ ] 💾 Database system available (SQLite included)
- [ ] 📦 Virtual environment activated

### 🔧 Environment Setup

```mermaid
graph LR
    A[Root Directory] --> B[Activate .venv]
    B --> C[Navigate to 6-persistent-storage]
    C --> D[Configure Database]
    D --> E[Set API Key]
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

#### 🔑 Environment Configuration

```bash
# Configure environment variables
GOOGLE_API_KEY=your_google_api_key_here
DATABASE_URL=sqlite:///./my_agent_data.db  # Optional, defaults to SQLite
```

## 🎮 Running the Example

### 🖥️ Interactive Session

```mermaid
graph TD
    A[Run: python main.py] --> B[Database Connection]
    B --> C[Check Existing Sessions]
    C --> D{Previous Session?}
    
    D -->|Yes| E[Load Existing Session]
    D -->|No| F[Create New Session]
    
    E --> G[Display Previous State]
    F --> H[Initialize Fresh State]
    
    G --> I[Start Interactive Loop]
    H --> I
    
    I --> J[Process User Input]
    J --> K[Execute Tools if Needed]
    K --> L[Persist State Changes]
    L --> M[Display Response]
    M --> I
    
    style E fill:#4caf50
    style L fill:#ff9800
    style M fill:#2196f3
```

### 📝 Step-by-Step Execution

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1️⃣ | **Navigate to directory** | `cd 6-persistent-storage` |
| 2️⃣ | **Run application** | `python main.py` |
| 3️⃣ | **Database initialization** | SQLite file created if needed |
| 4️⃣ | **Session check** | Load existing or create new session |
| 5️⃣ | **Interactive mode** | Start conversation with persistent agent |

### 🔄 Application Flow

```mermaid
sequenceDiagram
    participant U as User
    participant M as Main App
    participant D as DatabaseService
    participant A as Agent
    participant DB as SQLite DB
    
    U->>M: python main.py
    M->>D: Initialize DatabaseSessionService
    D->>DB: Connect to database
    
    M->>D: List existing sessions
    D->>DB: Query sessions table
    DB->>D: Return session list
    
    alt Session Exists
        D->>M: Load existing session
        M->>U: "Continuing previous session..."
    else No Session
        D->>M: Create new session
        M->>U: "Starting new session..."
    end
    
    loop Interactive Conversation
        U->>M: User input
        M->>A: Process with context
        A->>D: Update state (if needed)
        D->>DB: Persist changes
        A->>M: Generate response
        M->>U: Display response
    end
```

## 💬 Example Interactions and Testing

### 🎯 Testing Persistent Memory

```mermaid
graph LR
    A[Session 1] --> B[Learn User Name]
    A --> C[Add Reminders]
    A --> D[Exit Application]
    
    E[Session 2] --> F[Remember Name]
    E --> G[Recall Reminders]
    E --> H[Modify Data]
    
    D --> E
    
    style F fill:#4caf50
    style G fill:#4caf50
```

### 📊 Multi-Session Testing Scenarios

| Test Scenario | Session 1 Actions | Session 2 Actions | Expected Result |
|---------------|-------------------|-------------------|-----------------|
| 🧑 **Name Memory** | "My name is John" | "What's my name?" | Agent remembers "John" |
| 📝 **Reminder Storage** | "Add reminder: buy milk" | "What are my reminders?" | Shows previous reminder |
| ✏️ **Data Modification** | Add 3 reminders | Update 2nd reminder | Changes persist |
| 🗑️ **Data Deletion** | Add multiple items | Delete specific item | Deletion persists |

### 🎭 Interaction Examples

#### 🔄 First Session
```
User: "What's my name?"
Agent: "I don't have your name stored yet. What would you like me to call you?"

User: "My name is Sarah"
Agent: "Nice to meet you, Sarah! I'll remember that."

User: "Add a reminder to buy groceries"
Agent: "Added reminder: buy groceries"

User: "Add another reminder to finish the report"
Agent: "Added reminder: finish the report"

User: "What are my reminders?"
Agent: "Your reminders: 1. buy groceries, 2. finish the report"

User: "exit"
```

#### 🔄 Second Session (After Restart)
```
User: "What's my name?"
Agent: "Hello Sarah! Good to see you again."

User: "What reminders do I have?"
Agent: "Your reminders: 1. buy groceries, 2. finish the report"

User: "Update my second reminder to submit the report by Friday"
Agent: "Updated reminder: submit the report by Friday"

User: "Delete the first reminder"
Agent: "Deleted reminder: buy groceries"
```

## 🎉 Success Indicators

### ✅ Your Persistent Storage is Working When:

```mermaid
pie title Persistent Storage Success Metrics
    "Data Persistence" : 30
    "Session Continuity" : 25
    "Performance" : 20
    "Data Integrity" : 25
```

| Indicator | Description | What to Look For |
|-----------|-------------|------------------|
| 💾 **Data Persistence** | Information survives restarts | Database file grows, data remains |
| 🔄 **Session Continuity** | Seamless conversation resumption | Previous context available |
| ⚡ **Performance** | Fast database operations | Quick response times |
| 🛡️ **Data Integrity** | No corruption or loss | Consistent, accurate data |

### 🔧 Testing Checklist

- [ ] 💾 Database file created automatically
- [ ] 📊 Sessions listed correctly
- [ ] 🔄 Previous sessions load with full state
- [ ] 🛠️ Tools update state persistently
- [ ] 🧠 Agent remembers user information
- [ ] 📝 Reminders persist across sessions
- [ ] ⚡ Performance remains acceptable
- [ ] 🛡️ No data corruption or loss

## 🏭 Production Database Considerations

### 🗄️ Database Selection Matrix

```mermaid
graph TD
    A[Production Requirements] --> B[Scale]
    A --> C[Performance]
    A --> D[Features]
    A --> E[Cost]
    
    B --> F{Concurrent Users}
    F -->|<100| G[SQLite]
    F -->|100-10K| H[PostgreSQL]
    F -->|>10K| I[Enterprise DB]
    
    C --> J{Response Time}
    J -->|<100ms| K[In-Memory + Persistence]
    J -->|<500ms| L[Optimized Queries]
    J -->|>500ms| M[Scaling Required]
    
    D --> N[ACID Compliance]
    D --> O[Backup & Recovery]
    D --> P[High Availability]
    
    style G fill:#fff3e0
    style H fill:#c8e6c9
    style I fill:#e3f2fd
```

### 📊 Database Comparison

| Database | Concurrency | Max Size | Features | Complexity | Cost |
|----------|-------------|----------|----------|------------|------|
| 💾 **SQLite** | Low | ~280TB | File-based, embedded | Simple | Free |
| 🐘 **PostgreSQL** | High | Unlimited | Full SQL, extensions | Medium | Free |
| 🐬 **MySQL** | High | Unlimited | Wide support, replication | Medium | Free |
| 🏢 **Enterprise** | Very High | Unlimited | Advanced features | High | Licensed |

### 🔐 Production Security

```mermaid
mindmap
  root)Database Security(
    Authentication
      Strong passwords
      User accounts
      Role-based access
      Multi-factor auth
    Encryption
      Data at rest
      Data in transit
      Key management
      Certificate handling
    Network Security
      Firewall rules
      VPN access
      IP restrictions
      SSL/TLS only
    Compliance
      Data retention
      Privacy regulations
      Audit logging
      Backup policies
```

### ⚡ Performance Optimization

```mermaid
graph LR
    A[Performance Tuning] --> B[Indexing]
    A --> C[Connection Pooling]
    A --> D[Query Optimization]
    A --> E[Caching]
    
    B --> B1[Primary Keys]
    B --> B2[Session Indexes]
    B --> B3[User ID Indexes]
    
    C --> C1[Pool Size Tuning]
    C --> C2[Connection Lifecycle]
    C --> C3[Timeout Configuration]
    
    D --> D1[Query Analysis]
    D --> D2[Batch Operations]
    D --> D3[Prepared Statements]
    
    E --> E1[Redis Integration]
    E --> E2[Application-level Cache]
    E --> E3[Query Result Cache]
    
    style B1 fill:#4caf50
    style C1 fill:#ff9800
    style D1 fill:#2196f3
    style E1 fill:#9c27b0
```

## 🚪 Troubleshooting

### 🔧 Common Issues

```mermaid
flowchart TD
    A[Database Issue Detected] --> B{Connection Error?}
    B -->|Yes| C[Check Database URL]
    B -->|No| D{Permission Error?}
    D -->|Yes| E[Verify File Permissions]
    D -->|No| F{Schema Error?}
    F -->|Yes| G[Check Table Structure]
    F -->|No| H{Performance Issue?}
    H -->|Yes| I[Optimize Queries]
    H -->|No| J{Data Corruption?}
    J -->|Yes| K[Restore from Backup]
    J -->|No| L[Check Application Logs]
    
    style A fill:#f44336
    style C fill:#ff9800
    style E fill:#ff9800
    style G fill:#ff9800
    style I fill:#ff9800
    style K fill:#ff9800
    style L fill:#ff9800
```

| Issue | Symptoms | Cause | Solution |
|-------|----------|-------|---------|
| 🚫 **Connection Failed** | Database errors on startup | Wrong URL, permissions | Check connection string, file permissions |
| 💾 **SQLite Locked** | Database is locked errors | Concurrent access | Implement proper connection pooling |
| 📊 **Schema Mismatch** | Column/table errors | Version mismatch | Update schema or recreate database |
| ⚡ **Slow Performance** | Long response times | Large data, no indexes | Add indexes, optimize queries |
| 🗄️ **Disk Full** | Write errors | No disk space | Clean up space, archive old data |

### 🛠️ Debug Commands

```bash
# Check database file
ls -la my_agent_data.db

# Inspect SQLite database
sqlite3 my_agent_data.db ".schema"
sqlite3 my_agent_data.db "SELECT * FROM sessions;"

# Test database connection
python -c "from google.adk.sessions import DatabaseSessionService; print('OK')"

# Check table structure
python -c "
import sqlite3
conn = sqlite3.connect('my_agent_data.db')
cursor = conn.cursor()
cursor.execute('SELECT sql FROM sqlite_master WHERE type=\"table\";')
print(cursor.fetchall())
"
```

### 🛑 Data Recovery

```mermaid
graph TD
    A[Data Loss Detected] --> B{Backup Available?}
    B -->|Yes| C[Restore from Backup]
    B -->|No| D[Check Database Recovery]
    
    C --> E[Verify Data Integrity]
    D --> F[SQLite Recovery Tools]
    
    E --> G{Data Complete?}
    F --> G
    
    G -->|Yes| H[Resume Operations]
    G -->|No| I[Partial Recovery]
    
    I --> J[Assess Data Loss]
    J --> K[Inform Users]
    K --> L[Implement Better Backups]
    
    style C fill:#4caf50
    style H fill:#c8e6c9
    style I fill:#fff3e0
    style L fill:#e3f2fd
```

## 🎓 What You've Learned

### 🏆 Key Achievements

- [ ] 🗄️ Implemented persistent database storage for agents
- [ ] 💾 Configured DatabaseSessionService with SQLite
- [ ] 🔄 Managed session lifecycle across application restarts
- [ ] 🛠️ Created tools that automatically persist state changes
- [ ] 📊 Built a production-ready reminder management system
- [ ] 🏭 Understood production database considerations
- [ ] 🔐 Applied security best practices for data persistence
- [ ] ⚡ Optimized database performance and scaling

### 🚀 Next Steps

Ready for multi-agent orchestration?

| Next Example | Focus | Complexity | Key Concepts |
|--------------|-------|------------|--------------|
| 🤖 **Multi-Agent** | Agent coordination | ⭐⭐⭐⭐ | Agent orchestration, message passing |
| 🔄 **Stateful Multi-Agent** | Complex distributed state | ⭐⭐⭐⭐⭐ | Shared state, agent communication |
| 📊 **Callbacks** | Event monitoring | ⭐⭐⭐ | Real-time monitoring, event handling |

### 🎯 Advanced Concepts to Explore

```mermaid
graph TD
    A[Current: Persistent Storage] --> B[Multi-Agent Systems]
    A --> C[Stateful Multi-Agent]
    A --> D[Enterprise Scaling]
    
    B --> E[Agent Coordination]
    B --> F[Message Passing]
    
    C --> G[Distributed State Management]
    C --> H[Complex Workflows]
    
    D --> I[Database Clustering]
    D --> J[High Availability]
    D --> K[Performance Monitoring]
    
    style A fill:#4caf50
    style B fill:#2196f3
    style C fill:#ff9800
    style D fill:#9c27b0
```

## 📚 Additional Resources

### 🔗 Official Documentation

| Resource | Focus | Link |
|----------|-------|------|
| 📖 **ADK Sessions** | Session management guide | [ADK Sessions Documentation](https://google.github.io/adk-docs/sessions/session/) |
| 🗄️ **Session Services** | Database service implementations | [Session Service Guide](https://google.github.io/adk-docs/sessions/session/#sessionservice-implementations) |
| 📊 **State Management** | Advanced state techniques | [State Management Documentation](https://google.github.io/adk-docs/sessions/state/) |
| 🔧 **SQLAlchemy** | Database ORM and configuration | [SQLAlchemy Documentation](https://docs.sqlalchemy.org/) |

### 🎯 Best Practices

```mermaid
mindmap
  root)Persistent Storage Best Practices(
    Database Design
      Proper indexing
      Normalized schema
      Data types optimization
      Query performance
    Security
      Encrypted connections
      Strong authentication
      Regular backups
      Access controls
    Performance
      Connection pooling
      Query optimization
      Caching strategies
      Monitoring
    Maintenance
      Regular backups
      Schema migrations
      Performance tuning
      Capacity planning
```

### 📊 Scaling Strategies

| Strategy | Implementation | Benefits | Considerations |
|----------|----------------|----------|----------------|
| 🔄 **Vertical Scaling** | Increase server resources | Simple, immediate | Cost increases, limits |
| 📈 **Horizontal Scaling** | Multiple database servers | Better performance | Complexity, consistency |
| 🗂️ **Sharding** | Partition data across DBs | Massive scale | Application complexity |
| 💾 **Caching** | Redis/Memcached layer | Faster reads | Cache invalidation |

---

<div align="center">

### 🎉 Congratulations! 

You've mastered persistent storage and database integration! 

[![Next: Multi-Agent](https://img.shields.io/badge/Next-Multi--Agent-darkblue?style=for-the-badge&logo=arrow-right)](../7-multi-agent/)
[![Previous: Sessions & State](https://img.shields.io/badge/Previous-Sessions%20%26%20State-indigo?style=for-the-badge&logo=arrow-left)](../5-sessions-and-state/)
[![Back to Main](https://img.shields.io/badge/Back-Main%20Course-green?style=for-the-badge&logo=home)](../)

*Ready to orchestrate multiple agents? Let's explore multi-agent systems! 🤖*

</div>

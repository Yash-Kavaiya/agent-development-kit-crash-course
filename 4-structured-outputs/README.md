# 📊 Structured Outputs in ADK

[![ADK](https://img.shields.io/badge/ADK-Structured%20Outputs-teal.svg)](https://google.github.io/adk-docs/)
[![Difficulty](https://img.shields.io/badge/Difficulty-Intermediate-yellow.svg)](.)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Pydantic](https://img.shields.io/badge/Pydantic-Schema%20Validation-red.svg)](https://docs.pydantic.dev/)

> 🎯 **Master Consistent Data Formatting** - Learn to implement structured outputs using Pydantic models for guaranteed format consistency

## 📋 What are Structured Outputs?

**Structured Outputs** in ADK enable you to define exact data formats for agent responses using Pydantic models, ensuring consistent, validated, and predictable output formats every time.

### 🔄 Unstructured vs Structured Outputs

```mermaid
graph TB
    subgraph "Unstructured Output"
        A1[User Request] --> B1[LLM Processing]
        B1 --> C1[Free-form Text Response]
        C1 --> D1[Unpredictable Format]
        D1 --> E1[Manual Parsing Required]
        E1 --> F1[Error-Prone Integration]
    end
    
    subgraph "Structured Output"
        A2[User Request] --> B2[LLM Processing]
        B2 --> C2[Pydantic Schema Validation]
        C2 --> D2[Guaranteed JSON Structure]
        D2 --> E2[Automatic Validation]
        E2 --> F2[Seamless Integration]
    end
    
    style C2 fill:#4caf50
    style D2 fill:#4caf50
    style E2 fill:#4caf50
    style F2 fill:#4caf50
    style F1 fill:#f44336
```

### 🏗️ Core Benefits

| Benefit | Description | Impact |
|---------|-------------|--------|
| 🎯 **Controlled Format** | `output_schema` ensures consistent JSON structure | Predictable responses |
| ✅ **Data Validation** | Pydantic validates fields and types | Error prevention |
| 🔄 **Easy Integration** | Structured data works seamlessly with other systems | Reduced complexity |
| 📊 **Type Safety** | Strong typing prevents runtime errors | Better reliability |
| 🛠️ **Developer Experience** | IDE support with autocompletion | Faster development |

## 🏗️ Structured Output Architecture

### 🔧 How Structured Outputs Work

```mermaid
sequenceDiagram
    participant U as User
    participant A as ADK Agent
    participant L as LLM
    participant P as Pydantic Schema
    participant S as Session State
    
    U->>A: User Request
    A->>L: Process with Schema Instructions
    L->>P: Generate JSON Response
    P->>P: Validate Against Schema
    
    alt Validation Success
        P->>S: Store in Session State
        S->>U: Return Structured Data
    else Validation Failure
        P->>L: Request Retry
        L->>P: Generate New Response
    end
```

### 📊 Schema Definition Flow

```mermaid
graph TD
    A[Define Pydantic Model] --> B[Field Definitions]
    A --> C[Field Descriptions]
    A --> D[Type Annotations]
    
    B --> E[Agent Configuration]
    C --> E
    D --> E
    
    E --> F[output_schema Parameter]
    F --> G[LLM Instructions]
    G --> H[Structured Response]
    
    H --> I[Automatic Validation]
    I --> J[Session Storage]
    
    style A fill:#2196f3
    style E fill:#4caf50
    style I fill:#ff9800
    style J fill:#9c27b0
```

## 📧 Email Generator Example

### 🎯 Use Case Overview

```mermaid
mindmap
  root)Email Generator(
    Input
      Email purpose
      Target audience
      Tone requirements
      Key information
    Processing
      Content generation
      Structure formatting
      Schema validation
      Quality assurance
    Output
      Subject line
      Email body
      Proper formatting
      Consistent structure
```

### 📝 Schema Definition

```mermaid
classDiagram
    class EmailContent {
        +str subject
        +str body
        +validate_subject()
        +validate_body()
        +format_output()
    }
    
    EmailContent : subject "Concise, descriptive subject line"
    EmailContent : body "Well-formatted email content"
    
    class Field {
        +description: str
        +validation_rules: list
        +type_constraint: type
    }
    
    EmailContent --> Field : uses
```

#### 🔧 Pydantic Model Implementation

```python
class EmailContent(BaseModel):
    """Schema for email content with subject and body."""
    
    subject: str = Field(
        description="The subject line of the email. Should be concise and descriptive."
    )
    body: str = Field(
        description="The main content of the email. Should be well-formatted with proper greeting, paragraphs, and signature."
    )
```

### 🔄 Processing Workflow

```mermaid
graph LR
    A[User Prompt] --> B[Agent Analysis]
    B --> C[Content Generation]
    C --> D[Schema Formatting]
    D --> E[Validation Check]
    E --> F{Valid?}
    
    F -->|Yes| G[Return Structured Output]
    F -->|No| H[Regenerate Response]
    H --> D
    
    G --> I[Store in Session]
    I --> J[Available for Other Agents]
    
    style A fill:#e3f2fd
    style G fill:#c8e6c9
    style I fill:#fff3e0
    style J fill:#f3e5f5
```

### 📊 Email Content Structure

```mermaid
graph TD
    A[EmailContent] --> B[Subject Field]
    A --> C[Body Field]
    
    B --> B1[Requirements]
    B1 --> B2[Concise]
    B1 --> B3[Descriptive]
    B1 --> B4[Relevant]
    
    C --> C1[Structure]
    C1 --> C2[Greeting]
    C1 --> C3[Main Content]
    C1 --> C4[Call to Action]
    C1 --> C5[Signature]
    
    style A fill:#4caf50
    style B fill:#2196f3
    style C fill:#ff9800
```

## ⚠️ Important Limitations

### 🚫 Critical Constraints

```mermaid
graph TD
    A[Structured Output Limitations] --> B[No Tool Usage]
    A --> C[Direct JSON Response]
    A --> D[Clear Instructions Required]
    A --> E[Schema Complexity Limits]
    
    B --> B1["❌ Cannot use external tools"]
    C --> C1["📋 Must output valid JSON"]
    D --> D1["📝 Explicit formatting guidance needed"]
    E --> E1["🔧 Keep schemas simple and focused"]
    
    style B1 fill:#ffcdd2
    style C1 fill:#fff3e0
    style D1 fill:#e1f5fe
    style E1 fill:#f3e5f5
```

### 🔧 Constraint Details

| Limitation | Description | Workaround |
|------------|-------------|------------|
| 🚫 **No Tools** | Cannot use external tools or APIs | Use separate agents for tool operations |
| 📋 **JSON Only** | Must produce valid JSON matching schema | Provide clear formatting examples |
| 📝 **Explicit Instructions** | LLM needs detailed output guidance | Include schema examples in instructions |
| 🎯 **Single Purpose** | One schema per agent execution | Use multiple agents for complex workflows |

### 🛠️ Workaround Strategies

```mermaid
graph LR
    A[Complex Workflow] --> B[Agent 1: Tool Usage]
    B --> C[Agent 2: Data Processing]
    C --> D[Agent 3: Structured Output]
    
    A1[Data Collection] --> B
    A2[Analysis] --> C
    A3[Formatting] --> D
    
    style D fill:#4caf50
```

## 🏗️ Project Structure

### 📁 Directory Organization

```mermaid
graph TD
    A[4-structured-outputs/] --> B[email_agent/]
    A --> C[README.md]
    A --> D[.env.example]
    
    B --> E[__init__.py]
    B --> F[agent.py]
    B --> G[.env]
    
    E --> H[Package Discovery]
    F --> I[Agent Definition]
    F --> J[Pydantic Schema]
    F --> K[Output Configuration]
    G --> L[API Keys]
    
    style A fill:#e3f2fd
    style F fill:#4caf50
    style J fill:#ff9800
```

```
4-structured-outputs/
│
├── email_agent/                   # 📧 Email Generator Package
│   ├── __init__.py               # 📦 Package initialization
│   ├── agent.py                  # 🤖 Agent with output schema
│   └── .env                      # 🔑 Environment variables
│
├── .env.example                  # 📋 Environment template
└── README.md                     # 📖 Documentation
```

## 🚀 Getting Started

### 📋 Prerequisites Checklist

- [ ] ✅ Virtual environment activated
- [ ] 🔑 Google API key configured
- [ ] 📦 Pydantic understanding (basic)
- [ ] 📁 Proper project structure

### 🔧 Environment Setup

```mermaid
graph LR
    A[Root Directory] --> B[Activate .venv]
    B --> C[Navigate to 4-structured-outputs]
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

| Step | Action | Details |
|------|--------|---------|
| 1️⃣ | **Locate Template** | Find `.env.example` in email_agent folder |
| 2️⃣ | **Create Config** | Copy to `.env` in email_agent folder |
| 3️⃣ | **Add API Key** | `GOOGLE_API_KEY=your_key_here` |
| 4️⃣ | **Verify Setup** | Check agent loads correctly |

## 🎮 Running the Example

### 🌐 Interactive Web UI

```mermaid
graph TD
    A[Navigate to 4-structured-outputs] --> B[Run: adk web]
    B --> C[Server Starts]
    C --> D[Open Browser: localhost:8000]
    D --> E[Select 'email_generator']
    E --> F[Test Structured Outputs]
    
    F --> G[Input Email Request]
    F --> H[Receive JSON Response]
    F --> I[Validate Schema Compliance]
    
    style F fill:#e3f2fd
    style H fill:#4caf50
    style I fill:#ff9800
```

### 🛠️ Available Run Methods

| Method | Command | Interface | Best For |
|--------|---------|-----------|----------|
| 🌐 **Web UI** | `adk web` | Browser-based | Interactive schema testing |
| 💻 **Terminal** | `adk run email_generator` | Command line | Quick validation |
| 🔌 **API Server** | `adk api_server` | REST endpoints | Integration testing |

### 📝 Step-by-Step Process

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1️⃣ | Navigate to directory | `cd 4-structured-outputs` |
| 2️⃣ | Start web server | `adk web` |
| 3️⃣ | Open browser | Visit `http://localhost:8000` |
| 4️⃣ | Select agent | Choose "email_generator" from dropdown |
| 5️⃣ | Test functionality | Input email requests, receive JSON |

## 💬 Example Interactions

### 📧 Email Generation Tests

```mermaid
graph LR
    A[Business Email] --> B[Professional Response]
    C[Client Communication] --> D[Formal Structure]
    E[Team Update] --> F[Collaborative Tone]
    G[Meeting Request] --> H[Clear Call-to-Action]
    
    B --> I[Consistent JSON Format]
    D --> I
    F --> I
    H --> I
    
    style I fill:#4caf50
```

### 📊 Test Categories

| Category | Example Prompts | Expected Output |
|----------|-----------------|-----------------|
| 💼 **Professional** | "Write a professional email to my team about the upcoming project deadline..." | Formal tone, clear structure |
| 📞 **Client Communication** | "Draft an email to a client explaining that we need additional information..." | Professional, helpful tone |
| 📅 **Meeting Requests** | "Create an email to schedule a meeting with the marketing department..." | Clear agenda, action items |
| 📈 **Project Updates** | "Send an update about the quarterly results to stakeholders..." | Informative, data-focused |

### 🎯 Detailed Test Examples

#### 💼 Professional Email Test

**Input:**
```
Write a professional email to my team about the upcoming project deadline that has been extended by two weeks.
```

**Expected Output Structure:**
```json
{
  "subject": "Project Deadline Extension - Updated Timeline",
  "body": "Dear Team,\n\nI hope this email finds you well. I wanted to inform you about an important update regarding our current project timeline...\n\nBest regards,\n[Your Name]"
}
```

#### 📞 Client Communication Test

**Input:**
```
Draft an email to a client explaining that we need additional information before we can proceed with their order.
```

**Expected Output Structure:**
```json
{
  "subject": "Additional Information Required for Your Order",
  "body": "Dear [Client Name],\n\nThank you for your recent order. To ensure we deliver exactly what you need...\n\nBest regards,\n[Your Name]"
}
```

## 🎉 Success Indicators

### ✅ Your Structured Output Agent is Working When:

```mermaid
pie title Structured Output Success Metrics
    "Schema Compliance" : 30
    "Content Quality" : 25
    "Consistent Format" : 25
    "Validation Success" : 20
```

| Indicator | Description | What to Look For |
|-----------|-------------|------------------|
| 📋 **Schema Compliance** | Output matches Pydantic model exactly | Valid JSON with all required fields |
| 📝 **Content Quality** | Generated content is relevant and well-written | Professional, coherent text |
| 🔄 **Consistent Format** | Every response follows same structure | Identical JSON keys and structure |
| ✅ **Validation Success** | No schema validation errors | Clean execution without retries |

### 🔧 Testing Checklist

- [ ] 📋 All responses are valid JSON
- [ ] 📝 Subject lines are concise and descriptive
- [ ] 📧 Email bodies are well-formatted
- [ ] 🔄 Output structure is consistent across requests
- [ ] ✅ No Pydantic validation errors
- [ ] 💾 Results stored correctly in session state

## 🔄 Advanced Schema Concepts

### 🏗️ Complex Schema Design

```mermaid
graph TD
    A[Advanced Schema Patterns] --> B[Nested Objects]
    A --> C[List Fields]
    A --> D[Optional Fields]
    A --> E[Validation Rules]
    
    B --> B1[Contact Information]
    B --> B2[Address Objects]
    
    C --> C1[Email Recipients]
    C --> C2[Attachment List]
    
    D --> D1[Optional CC/BCC]
    D --> D2[Priority Level]
    
    E --> E1[Email Format Validation]
    E --> E2[Length Constraints]
    
    style A fill:#2196f3
    style B1 fill:#4caf50
    style C1 fill:#ff9800
    style D1 fill:#9c27b0
    style E1 fill:#f44336
```

#### 🔧 Advanced Pydantic Example

```python
class AdvancedEmailContent(BaseModel):
    """Advanced email schema with nested objects and validation."""
    
    subject: str = Field(
        description="Email subject line",
        min_length=5,
        max_length=100
    )
    
    body: str = Field(
        description="Email body content",
        min_length=20
    )
    
    priority: Optional[str] = Field(
        default="normal",
        description="Email priority level",
        regex="^(low|normal|high)$"
    )
    
    recipients: List[str] = Field(
        description="List of recipient email addresses",
        min_items=1
    )
    
    metadata: Optional[Dict[str, Any]] = Field(
        default_factory=dict,
        description="Additional email metadata"
    )
```

### 📊 Schema Validation Flow

```mermaid
sequenceDiagram
    participant L as LLM
    participant P as Pydantic
    participant V as Validators
    participant S as Session
    
    L->>P: Generate JSON Response
    P->>V: Field Validation
    
    alt Required Fields Missing
        V->>L: ValidationError - Missing Fields
    else Type Mismatch
        V->>L: ValidationError - Wrong Type
    else Constraint Violation
        V->>L: ValidationError - Constraint Failed
    else All Valid
        V->>S: Store Validated Data
        S->>P: Success Response
    end
```

### 🎯 Best Practices for Schema Design

```mermaid
mindmap
  root)Schema Best Practices(
    Simplicity
      Keep schemas focused
      Avoid deep nesting
      Clear field names
      Minimal required fields
    Validation
      Use appropriate types
      Add length constraints
      Validate formats
      Provide good defaults
    Documentation
      Clear descriptions
      Usage examples
      Field purposes
      Validation rules
    Performance
      Avoid complex validations
      Minimize field count
      Use efficient types
      Cache when possible
```

## 🚪 Troubleshooting

### 🔧 Common Issues

```mermaid
flowchart TD
    A[Schema Issue Detected] --> B{Validation Error?}
    B -->|Yes| C[Check Field Types]
    B -->|No| D{Missing Fields?}
    D -->|Yes| E[Add Required Fields]
    D -->|No| F{Format Error?}
    F -->|Yes| G[Fix JSON Structure]
    F -->|No| H{Content Issue?}
    H -->|Yes| I[Improve Instructions]
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
| 🚫 **Validation Error** | Field type mismatch | Check Pydantic model types |
| 📋 **Missing Fields** | Required field not provided | Update agent instructions |
| 🔧 **Format Error** | Invalid JSON structure | Fix LLM output formatting |
| 📝 **Content Quality** | Poor generated content | Improve prompt engineering |
| ⚙️ **Schema Error** | Pydantic model issues | Validate model definition |

### 🛠️ Debug Commands

```bash
# Test Pydantic model directly
python -c "from email_agent.agent import EmailContent; print(EmailContent.schema())"

# Validate sample data
python -c "from email_agent.agent import EmailContent; EmailContent(subject='Test', body='Test body')"

# Check agent configuration
adk config validate email_generator
```

### 🛑 Exit Options

```bash
# Stop any running ADK command
Ctrl+C
```

## 🎓 What You've Learned

### 🏆 Key Achievements

- [ ] 📊 Implemented structured outputs with Pydantic models
- [ ] 🔧 Configured output schemas for consistent formatting
- [ ] ✅ Applied data validation and type safety
- [ ] 📝 Created professional email generation system
- [ ] 🔄 Understood structured data flow in ADK
- [ ] 🛠️ Mastered schema design best practices
- [ ] 🔧 Learned troubleshooting techniques
- [ ] 💾 Implemented session state storage

### 🚀 Next Steps

Ready for more advanced concepts?

| Next Example | Focus | Complexity | Key Concepts |
|--------------|-------|------------|--------------|
| 💾 **Sessions & State** | Memory management | ⭐⭐⭐ | State persistence, context |
| 🏪 **Persistent Storage** | Data durability | ⭐⭐⭐ | Database integration |
| 🤖 **Multi-Agent** | Agent orchestration | ⭐⭐⭐⭐ | Agent coordination |

### 🎯 Advanced Concepts to Explore

```mermaid
graph TD
    A[Current: Structured Outputs] --> B[Sessions & State]
    A --> C[Persistent Storage]
    A --> D[Multi-Agent Systems]
    
    B --> E[Stateful Multi-Agent]
    C --> E
    D --> E
    
    E --> F[Callbacks & Monitoring]
    E --> G[Sequential Agents]
    E --> H[Parallel Agents]
    
    style A fill:#4caf50
    style E fill:#ff9800
    style F fill:#2196f3
    style G fill:#2196f3
    style H fill:#2196f3
```

## 📚 Additional Resources

### 🔗 Official Documentation

| Resource | Focus | Link |
|----------|-------|------|
| 📖 **ADK Structured Data** | Complete structured data guide | [ADK Documentation](https://google.github.io/adk-docs/agents/llm-agents/#structuring-data-input_schema-output_schema-output_key) |
| 🔧 **Pydantic Models** | Schema definition and validation | [Pydantic Documentation](https://docs.pydantic.dev/latest/) |
| 📋 **JSON Schema** | Understanding JSON Schema format | [JSON Schema Guide](https://json-schema.org/) |
| ✅ **Data Validation** | Advanced validation techniques | [Pydantic Validators](https://docs.pydantic.dev/latest/usage/validators/) |

### 🎯 Schema Design Patterns

```mermaid
mindmap
  root)Schema Design Patterns(
    Simple Schemas
      Single purpose
      Minimal fields
      Clear naming
      Basic types
    Complex Schemas
      Nested objects
      List validation
      Custom validators
      Dynamic fields
    Integration Patterns
      API compatibility
      Database mapping
      Service contracts
      Event schemas
    Validation Strategies
      Type checking
      Format validation
      Business rules
      Cross-field validation
```

### 📊 Performance Considerations

| Aspect | Simple Schema | Complex Schema | Recommendation |
|--------|---------------|----------------|----------------|
| ⚡ **Validation Speed** | Fast | Slower | Keep schemas focused |
| 🧠 **LLM Performance** | Better | More challenging | Provide clear examples |
| 🔧 **Maintenance** | Easy | Complex | Document thoroughly |
| 🎯 **Error Rate** | Low | Higher | Test extensively |

---

<div align="center">

### 🎉 Congratulations! 

You've mastered structured outputs with Pydantic schemas! 

[![Next: Sessions & State](https://img.shields.io/badge/Next-Sessions%20%26%20State-indigo?style=for-the-badge&logo=arrow-right)](../5-sessions-state/)
[![Previous: LiteLLM Agent](https://img.shields.io/badge/Previous-LiteLLM%20Agent-purple?style=for-the-badge&logo=arrow-left)](../3-litellm-agent/)
[![Back to Main](https://img.shields.io/badge/Back-Main%20Course-green?style=for-the-badge&logo=home)](../)

*Ready to add memory to your agents? Let's explore sessions and state! 💾*

</div>

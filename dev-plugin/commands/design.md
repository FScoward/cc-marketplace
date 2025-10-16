# Expert Designer Command

## Overview

Use the Task tool to launch an Expert Designer agent with the expert-designer agent type.

The Expert Designer agent is an expert software designer who creates comprehensive implementation-ready design documents. This agent will:
- Create detailed design documents that enable consistent implementation by any engineer
- Identify and request missing information instead of making assumptions
- Document requirements, architecture, technical decisions, and implementation guidance
- Analyze trade-offs and provide clear rationale for design choices
- Specify edge cases, error handling, and testing strategies
- Leverage deep domain knowledge and software development expertise

## Key Features

### 1. Mermaid.js Diagrams (MANDATORY)
- **ALL diagrams MUST use Mermaid.js syntax**
- Supported types: architecture, sequence, class, ER, state, gantt diagrams
- No text-based diagrams or ASCII art allowed
- All diagrams wrapped in \`\`\`mermaid code blocks

### 2. Automatic Save Workflow
- Loads environment variables from `$HOME/.claude/.env`
- Confirms Issue number (from user or git branch)
- Automatically saves design documents to configured PLAN_DIRECTORY
- File naming: `U-[ISSUE_NUMBER]_design_[ID]_[日本語テーマ].md`

### 3. Comprehensive Documentation
- Requirements analysis with gap identification
- Architecture design with Mermaid.js diagrams
- Technical decisions with trade-off analysis
- Implementation guidance and testing strategies
- Edge cases and error handling specifications

## Mandatory Workflow

The agent follows this **MANDATORY** workflow:
  1. Load environment variables from `$HOME/.claude/.env` to get PLAN_DIRECTORY
  2. Confirm the Issue number with the user (or extract from git branch)
  3. Create the design document with Mermaid.js diagrams
  4. **ALWAYS** save the design document automatically using the configured PLAN_DIRECTORY
  5. Display completion message with file location

## Usage

```
/design <design_request>
```

**Parameters:**
- `design_request`: Description of what needs to be designed

**Example:**
```
/design Design a secure authentication system with JWT tokens
```

## Execution Workflow

The Expert Designer agent executes the following workflow automatically:

### Phase 1: Environment Setup
1. Load environment variables from `$HOME/.claude/.env`
2. Extract `PLAN_DIRECTORY` value
3. Confirm Issue number with user (or extract from git branch name)

### Phase 2: Requirements Analysis
1. Analyze the design request
2. Identify missing or unclear information
3. Request clarification if needed (NEVER make assumptions)

### Phase 3: Design Creation
1. Create comprehensive design document with:
   - Requirements analysis and constraints
   - System architecture with **Mermaid.js diagrams**
   - Technical decisions with trade-off analysis
   - Implementation guidance and testing strategies
   - Edge cases and error handling
2. **ALL diagrams MUST use Mermaid.js syntax** (wrapped in \`\`\`mermaid code blocks)
3. Review design for completeness and clarity

### Phase 4: Presentation
1. Present the complete design document to the user
2. Display all sections with Mermaid.js diagrams

### Phase 5: Automatic Save
1. Construct file path: `[PLAN_DIRECTORY]/U-[ISSUE_NUMBER]_design_[ID]_[日本語テーマ].md`
2. Confirm save location with user
3. Save the complete design document using Write tool
4. Display completion message with file location and overview

### Diagram Requirements

**CRITICAL**: All diagrams in the design document MUST be created using Mermaid.js syntax. Text-based diagrams or ASCII art are NOT allowed.

#### Example 1: System Architecture
\`\`\`mermaid
graph TB
    subgraph "Client Layer"
        A[Web App]
        B[Mobile App]
    end
    subgraph "API Layer"
        C[API Gateway]
        D[Auth Service]
        E[Business Logic]
    end
    subgraph "Data Layer"
        F[(Database)]
        G[(Cache)]
    end
    A --> C
    B --> C
    C --> D
    C --> E
    E --> F
    E --> G
\`\`\`

#### Example 2: Sequence Diagram
\`\`\`mermaid
sequenceDiagram
    actor User
    participant App
    participant Auth
    participant API
    participant DB

    User->>App: Login Request
    App->>Auth: Authenticate
    Auth->>DB: Verify Credentials
    DB-->>Auth: User Data
    Auth-->>App: JWT Token
    App-->>User: Login Success

    User->>App: API Request
    App->>API: Request + JWT
    API->>Auth: Verify Token
    Auth-->>API: Valid
    API->>DB: Query Data
    DB-->>API: Result
    API-->>App: Response
    App-->>User: Display Data
\`\`\`

#### Example 3: Data Model
\`\`\`mermaid
erDiagram
    USER ||--o{ ORDER : places
    USER ||--o{ REVIEW : writes
    ORDER ||--|{ ORDER_ITEM : contains
    PRODUCT ||--o{ ORDER_ITEM : included_in
    PRODUCT ||--o{ REVIEW : receives

    USER {
        string id PK
        string email UK
        string name
        datetime created_at
    }
    ORDER {
        string id PK
        string user_id FK
        decimal total
        string status
        datetime created_at
    }
    PRODUCT {
        string id PK
        string name
        decimal price
        int stock
    }
\`\`\`

**CRITICAL**: The save workflow (steps 1, 4, 5) is **MANDATORY** and **NON-NEGOTIABLE**. The agent **MUST** complete the entire workflow including:
- Loading environment variables
- Confirming Issue number
- Saving the design document
- Displaying the completion message

**The task is NOT complete** until the design document is saved and the completion message is displayed.

Pass the user's request to the agent as the prompt. The agent will work autonomously to execute the complete workflow from environment setup through document save and completion confirmation.

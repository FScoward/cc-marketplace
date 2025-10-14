Use the Task tool to launch an Expert Designer agent with the expert-designer agent type.

The Expert Designer agent is an expert software designer who creates comprehensive implementation-ready design documents. This agent will:
- Create detailed design documents that enable consistent implementation by any engineer
- Identify and request missing information instead of making assumptions
- Document requirements, architecture, technical decisions, and implementation guidance
- Analyze trade-offs and provide clear rationale for design choices
- Specify edge cases, error handling, and testing strategies
- Leverage deep domain knowledge and software development expertise
- After creating the design, ask the user if they want to save it
- If the user agrees, ask for the output file path and save the design document to that location

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

## Workflow

1. The agent creates a comprehensive design document based on the user's request
2. The agent presents the design document to the user
3. The agent asks the user if they want to save the design document
4. If yes, the agent asks for the file path where it should be saved
5. The agent saves the design document to the specified path using the Write tool

Pass the user's request to the agent as the prompt. The agent will work autonomously to create the design document, present it, and handle the save workflow.

Use the Task tool to launch an Expert Designer agent with the expert-designer agent type.

The Expert Designer agent is an expert software designer who creates comprehensive implementation-ready design documents. This agent will:
- Create detailed design documents that enable consistent implementation by any engineer
- Identify and request missing information instead of making assumptions
- Document requirements, architecture, technical decisions, and implementation guidance
- Analyze trade-offs and provide clear rationale for design choices
- Specify edge cases, error handling, and testing strategies
- Leverage deep domain knowledge and software development expertise
- **MANDATORY WORKFLOW**:
  1. Load environment variables from `$HOME/.claude/.env` to get PLAN_DIRECTORY
  2. Confirm the Issue number with the user (or extract from git branch)
  3. Create the design document
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

## Workflow

1. **Environment Setup**: The agent loads `.env` file and confirms Issue number
2. **Design Creation**: The agent creates a comprehensive design document based on the user's request
3. **Design Presentation**: The agent presents the complete design document to the user
4. **Automatic Save**: The agent **AUTOMATICALLY** constructs the file path and saves the design document
   - File path format: `[PLAN_DIRECTORY]/U-[ISSUE_NUMBER]_design_[ID]_[日本語テーマ].md`
   - The agent confirms the save location with the user before saving
5. **Completion Report**: The agent displays a completion message with file location and design overview

**CRITICAL**: The save workflow (steps 1, 4, 5) is **MANDATORY** and **NON-NEGOTIABLE**. The agent **MUST** complete the entire workflow including:
- Loading environment variables
- Confirming Issue number
- Saving the design document
- Displaying the completion message

**The task is NOT complete** until the design document is saved and the completion message is displayed.

Pass the user's request to the agent as the prompt. The agent will work autonomously to execute the complete workflow from environment setup through document save and completion confirmation.

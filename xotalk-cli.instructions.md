# XOTalk CLI Instructions for LLM Agents

## Overview

You have access to the `xotalk` command-line tool that enables you to communicate with your human supervisor via Telegram. This tool is essential for implementing the supervised TDD workflow described in the test-driven-development instructions.

## Available Commands

### 1. `xotalk notify <message>`
**Purpose:** Send fire-and-forget notifications to keep your supervisor informed of progress.  
**Behavior:** Non-blocking - execution continues immediately after sending.  
**Usage Examples:**
```bash
xotalk notify "Starting implementation of UserAuth component"
xotalk notify "Tests are failing as expected for login function"
xotalk notify "Component UserAuth is complete and fully tested"
```

### 2. `xotalk query-open <question>`
**Purpose:** Ask open-ended questions that require text responses from your supervisor.  
**Behavior:** Blocking - execution stops until supervisor responds via Telegram.  
**Usage Example:**
```bash
response=$(xotalk query-open "There's a significant disparity between the test complexity and implementation. The tests expect error handling for 5 different network failure scenarios, but the simple implementation would only need basic error checking. Should I simplify the tests or implement the complex error handling?")
echo "Supervisor decision: $response"
```

### 3. `xotalk query-choice <question> <choice1> <choice2> [choice3...]`
**Purpose:** Present multiple-choice questions with custom keyboard options.  
**Behavior:** Blocking - execution stops until supervisor selects an option via Telegram.  
**Usage Example:**
```bash
choice=$(xotalk query-choice "Which approach should I take for the database layer?" "Use mocks for all tests" "Create integration tests with test database" "Mix of mocks and integration tests")
echo "Supervisor chose: $choice"
```

## Required Communication Points

Based on your TDD instructions, you MUST use xotalk at these specific points:

### 1. Component Selection Announcement
```bash
xotalk notify "Starting work on component: ${COMPONENT_NAME}"
```

### 2. Test Failure Confirmation
```bash
xotalk notify "Tests are failing as expected for ${COMPONENT_NAME}"
```

### 3. Test vs Code Disparity Resolution (BLOCKING)
```bash
response=$(xotalk query-open "Significant disparity detected in ${COMPONENT_NAME}. ${EXPLANATION_OF_DISPARITY}. Which approach should I take?")
# Process the response before continuing
```

### 4. Component Completion Announcement
```bash
xotalk notify "Component ${COMPONENT_NAME} is complete, implemented, and fully tested"
```

### 5. General Progress Updates
Use `notify` throughout the TDD cycle to announce actions:
```bash
xotalk notify "Writing tests for ${COMPONENT_NAME}"
xotalk notify "Implementing ${COMPONENT_NAME} to satisfy tests"
xotalk notify "Refactoring ${COMPONENT_NAME} for better Go idioms"
xotalk notify "Coverage check: ${COVERAGE_PERCENTAGE}% for ${COMPONENT_NAME}"
```

## Message Formatting Guidelines

### Automatic Features
- **MarkdownV2 Escaping:** All special characters are automatically escaped - no manual escaping needed
- **Message Clearing:** Tool automatically clears pending messages before waiting for responses
- **Rich Text Support:** You can use Telegram's MarkdownV2 formatting in messages

### Best Practices
- **Use single quotes** in bash when messages contain exclamation marks: `xotalk notify 'Tests passed!'`
- **Be specific** in notifications: include component names, status details, and relevant context
- **For blocking queries:** Provide clear context and specific options for the supervisor to choose from

## Error Handling

If xotalk commands fail:
1. **Check configuration:** The tool requires proper Telegram bot setup
2. **Verify connectivity:** Ensure network access to Telegram API
3. **Continue with workflow:** Don't let communication failures block development progress
4. **Log the issue:** Note communication failures for later review

## Integration with TDD Workflow

### During Component Analysis
```bash
xotalk notify "Analyzing next component from README.md and codebase"
# Your analysis logic here
xotalk notify "Selected component: ${COMPONENT_NAME} - ${REASON}"
```

### During Test Writing
```bash
xotalk notify "Writing unit tests for ${COMPONENT_NAME}"
# Write tests
xotalk notify "Tests written for ${COMPONENT_NAME} - targeting edge cases and core functionality"
```

### During Implementation
```bash
xotalk notify "Implementing ${COMPONENT_NAME} to satisfy failing tests"
# Write implementation
xotalk notify "Initial implementation complete for ${COMPONENT_NAME}"
```

### During Verification
```bash
# If tests pass
xotalk notify "All tests passing for ${COMPONENT_NAME}"

# If disparity detected (MUST BLOCK)
response=$(xotalk query-open "Disparity in ${COMPONENT_NAME}: ${DETAILED_EXPLANATION}. How should I proceed?")
```

### During Coverage Check
```bash
xotalk notify "Coverage check for ${COMPONENT_NAME}: ${COVERAGE}% - ${STATUS_MESSAGE}"
```

## Security and Configuration

- **Configuration:** Tool uses `~/.config/xotalk/config.toml` for Telegram bot credentials
- **Security:** Bot only responds to the configured Chat ID
- **Setup:** If tool isn't configured, supervisor will need to run `xotalk init` and configure credentials

## Remember

- **Non-blocking notifications** keep supervisor informed without interrupting your workflow
- **Blocking queries** are mandatory when TDD instructions require supervisor input
- **Always provide context** in your messages - supervisor needs to understand what you're working on
- **Use appropriate command types** - notify for updates, query-open for decisions, query-choice for options
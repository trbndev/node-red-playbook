# Naming Conventions

## Descriptive Node Names

Name nodes to clearly indicate their purpose, following a verb-noun format when applicable.

✅ **Good Examples:**
- "Format Customer Data"
- "Validate API Response" 
- "Extract Order Details"
- "Update User Profile"

❌ **Bad Examples:**
- "Function 1"
- "Process"
- "API"
- "Fix Data"

## Context Variable Naming

### Context Scope Guidelines

1. **Global context:** Store application-wide constants and shared state
2. **Flow context:** Store flow-specific utilities and data
3. **Node context:** Store data specific to a single node

### Naming Patterns

Use consistent prefixes to indicate the purpose and type of context variables:

| Prefix    | Purpose                   | Example               |
|-----------|---------------------------|----------------------|
| `const_`  | Constants                 | `const_API_ENDPOINT` |
| `config_` | Configuration settings    | `config_retryLimit`  |
| `state_`  | Stateful information      | `state_processQueue` |
| `utils_`  | Utility functions         | `utils_formatters`   |
| `cache_`  | Cached data               | `cache_userProfiles` |

### Context Registry

Maintain a "Context Registry" flow that documents all context variables:

1. Create a comment node listing all global context variables
2. For each flow, add a comment node listing flow context variables
3. Document the purpose, type, and structure of each variable

Example comment:

```text
Global Context Registry:

const_API_ENDPOINTS (Object): External API endpoints
state_SYSTEM_STATUS (String): Current system operational status
utils_FORMATTERS (Object): Shared data formatting functions
```

## Link Node Naming

Name link nodes using event-based conventions to clearly show the flow of execution.

### Link Out Nodes

Pattern: `[Trigger|Event]:[Action]`

Examples:
- "Trigger:NewOrder"
- "Event:DataValidationFailed"
- "Trigger:MaintenanceRequired"
- "Event:PaymentReceived"

### Link In Nodes

Pattern: `[On|Handle]:[Action]`

Examples:
- "On:NewOrder"
- "Handle:DataValidationFailed"
- "On:MaintenanceRequired"
- "Handle:PaymentReceived"

Always ensure Link In and Link Out nodes use matching names (except for the prefix) to maintain clarity in flow connections.

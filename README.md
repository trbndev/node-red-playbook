# Node-RED Style Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Utility Context Pattern](#utility-context-pattern)
3. [Naming Conventions](#naming-conventions)
   - [Descriptive Node Names](#descriptive-node-names)
   - [Context Variable Naming](#context-variable-naming)
   - [Link Node Naming](#link-node-naming)
4. [Flow Organization](#flow-organization)
   - [Atomic Function Groups](#atomic-function-groups)
   - [Flow Structure: Main, Callbacks, Utilities](#flow-structure)
   - [Using Subflows](#using-subflows)
5. [Version Control](#version-control)
6. [Best Practices](#best-practices)

## Introduction <a name="introduction"></a>

This style guide establishes consistent patterns and practices for developing Node-RED flows. Following these guidelines will help create flows that are easier to understand, maintain, and collaborate on. Consistency in approach benefits both individual developers and teams working on shared projects.

## Utility Context Pattern <a name="utility-context-pattern"></a>

The Utility Context Pattern is a powerful approach to store and reuse functions throughout your flows.

### Core Principles

1. **Store reusable functions in context** during initialization
2. **Reference these functions** when needed instead of duplicating code
3. **Clean up** context when stopping flows to prevent memory leaks

### Implementation

#### Flow Utilities

Use a dedicated function node (typically named "Initialize Flow Utilities") that runs on deployment:

    // On Start
    const flowUtils = {
        // Format date in consistent way
        formatDate: function(date) {
            return new Date(date).toISOString().split('T')[0];
        },
        
        // Validate required fields
        validateFields: function(obj, requiredFields) {
            const missing = requiredFields.filter(field => !obj[field]);
            return missing.length === 0 ? null : `Missing required fields: ${missing.join(', ')}`;
        }
    };

    // Store utils in flow context
    flow.set("utils", flowUtils);

    // On Stop
    flow.set("utils", null);

#### Using Flow Utilities

In other function nodes:

    // Access utilities
    const utils = flow.get("utils");
    if (!utils) return node.error("Flow utilities not initialized");

    // Use utilities
    const error = utils.validateFields(msg.payload, ["id", "name"]);
    if (error) {
        node.error(error, msg);
        return null;
    }

    // Process valid message
    msg.payload.formattedDate = utils.formatDate(msg.payload.date);
    return msg;

#### Node-Specific Utilities

For functions only needed within a single node:

    // On Start
    context.set("utils", {
        parseSpecialFormat: function(data) {
            // Node-specific parsing logic
            return parsed;
        }
    });

    // On Message
    const nodeUtils = context.get("utils");
    msg.payload = nodeUtils.parseSpecialFormat(msg.payload);
    return msg;

    // On Stop
    context.set("utils", null);

## Naming Conventions <a name="naming-conventions"></a>

### Descriptive Node Names <a name="descriptive-node-names"></a>

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

### Context Variable Naming <a name="context-variable-naming"></a>

#### Context Scope Guidelines

1. **Global context:** Store application-wide constants and shared state
2. **Flow context:** Store flow-specific utilities and data
3. **Node context:** Store data specific to a single node

#### Naming Patterns

Use consistent prefixes to indicate the purpose and type of context variables:

| Prefix    | Purpose                   | Example               |
|-----------|---------------------------|----------------------|
| `const_`  | Constants                 | `const_API_ENDPOINT` |
| `config_` | Configuration settings    | `config_retryLimit`  |
| `state_`  | Stateful information      | `state_processQueue` |
| `utils_`  | Utility functions         | `utils_formatters`   |
| `cache_`  | Cached data               | `cache_userProfiles` |

#### Context Registry

Maintain a "Context Registry" flow that documents all context variables:

1. Create a comment node listing all global context variables
2. For each flow, add a comment node listing flow context variables
3. Document the purpose, type, and structure of each variable

Example comment:

    Global Context Registry:
    - const_API_ENDPOINTS (Object): External API endpoints
    - state_SYSTEM_STATUS (String): Current system operational status
    - utils_FORMATTERS (Object): Shared data formatting functions

### Link Node Naming <a name="link-node-naming"></a>

Name link nodes using event-based conventions to clearly show the flow of execution.

#### Link Out Nodes

Pattern: `[Trigger|Event]:[Action]`

Examples:
- "Trigger:NewOrder"
- "Event:DataValidationFailed"
- "Trigger:MaintenanceRequired"
- "Event:PaymentReceived"

#### Link In Nodes

Pattern: `[On|Handle]:[Action]`

Examples:
- "On:NewOrder"
- "Handle:DataValidationFailed"
- "On:MaintenanceRequired"
- "Handle:PaymentReceived"

Always ensure Link In and Link Out nodes use matching names (except for the prefix) to maintain clarity in flow connections.

## Flow Organization <a name="flow-organization"></a>

### Atomic Function Groups <a name="atomic-function-groups"></a>

Group nodes based on atomic functions - collections of nodes that perform a single logical operation.

1. **Use Node-RED groups** to visually organize related nodes
2. **Name groups** to describe their collective function
3. **Keep groups focused** on a single responsibility
4. **Limit group size** to maintain clarity (ideally 3-7 nodes)

Examples of atomic function groups:
- "API Data Retrieval"
- "User Validation"
- "Notification Processing"
- "Error Handling"

### Flow Structure: Main, Callbacks, Utilities <a name="flow-structure"></a>

Organize nodes into three distinct sections within each flow:

1. **Main Flow** - Primary execution path
   - Core business logic
   - Sequential processing steps
   - Decision points

2. **Callbacks** - Terminal processing paths
   - Success handlers
   - Error handlers
   - Conditional branch endpoints
   - Named with pattern: "On [Event] [Action]"

3. **Utilities** - Supporting functions
   - Initialization nodes
   - Utility function nodes
   - Helper functions
   - Named with pattern: "Util: [Purpose]"

Use horizontal or vertical separation to clearly distinguish these sections, with consistent placement across all flows.

### Using Subflows <a name="using-subflows"></a>

Create subflows when specific patterns repeat throughout your flows.

#### When to Use Subflows

- The same sequence of nodes is used in multiple places
- A discrete functional unit would benefit from encapsulation
- Common error handling patterns are repeated

#### Subflow Guidelines

1. **Give subflows clear, descriptive names** that indicate their function
2. **Document subflows** with a comment node explaining inputs, outputs, and purpose
3. **Make subflows parametrizable** using environment variables
4. **Keep subflows focused** on a single responsibility
5. **Version subflows** in comments to track changes

Example subflows:
- "API Request with Retry Logic"
- "Data Validation Pipeline"
- "Standardized Error Handler"
- "Audit Log Generator"

## Version Control <a name="version-control"></a>

### Using GitHub Projects for Git Syncing

1. **Initialize Node-RED project** using the Projects feature
2. **Configure GitHub integration**:
   - Use SSH keys for authentication
   - Set remote origin to your GitHub repository
   - Configure user name and email

3. **Develop using feature branches**:
   - Create branches for new features or fixes
   - Use meaningful branch names (feature/api-integration, fix/validation-error)
   - Commit frequently with descriptive messages

4. **Follow standard Git workflow**:
   - Pull latest changes before starting work
   - Create Pull Requests for review before merging
   - Use GitHub Actions for automated testing if applicable

5. **Manage flow files**:
   - Keep flows organized in logical files
   - Avoid large monolithic flow files
   - Use meaningful file names that describe the flow's purpose

6. **Exclude sensitive data**:
   - Use environment variables or credentials encryption
   - Add sensitive files to .gitignore
   - Never commit credentials or tokens

## Best Practices <a name="best-practices"></a>

### General Guidelines

1. **Comment complex nodes** - Explain "why" not just "what"
2. **Use debug nodes strategically** - Include them but disable when not needed
3. **Handle errors explicitly** - Never allow flows to fail silently
4. **Design for restart resilience** - Flows should recover after Node-RED restarts
5. **Limit message size** - Be aware of memory usage with large payloads
6. **Validate inputs** - Check message format before processing
7. **Use status nodes** - Provide visual indicators of flow status
8. **Create test flows** - Build separate flows to test complex functionality
9. **Document API endpoints** - If exposing HTTP nodes, document their usage
10. **Monitor performance** - Be mindful of resource-intensive operations

### Contextual Data Management

1. **Prefer msg properties** for data that flows through nodes
2. **Use flow/global context sparingly** for shared state and utilities
3. **Clean up context data** that is no longer needed
4. **Document all context usage** in the Context Registry

### Deployment Considerations

1. **Test before deploying** to production
2. **Use credentials encryption** for sensitive information
3. **Consider resource utilization** on target hardware
4. **Version flows meaningfully** with semantic version numbers
5. **Maintain a changelog** of significant changes

By following this style guide, your Node-RED flows will be more readable, maintainable, and collaborative.

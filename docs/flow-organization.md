# Flow Organization

## Atomic Function Groups

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

## Flow Structure: Main, Callbacks, Utilities

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

## Using Subflows

Create subflows when specific patterns repeat throughout your flows.

### When to Use Subflows

- The same sequence of nodes is used in multiple places
- A discrete functional unit would benefit from encapsulation
- Common error handling patterns are repeated

### Subflow Guidelines

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

# Utility Context Pattern

The Utility Context Pattern is a powerful approach to store and reuse functions throughout your flows.

## Core Principles

1. **Store reusable functions in context** during initialization
2. **Reference these functions** when needed instead of duplicating code
3. **Clean up** context when stopping flows to prevent memory leaks

## Implementation

### Flow Utilities

Use a dedicated function node (typically named "Initialize Flow Utilities") that runs on deployment:

```javascript
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
```

### Using Flow Utilities
In other function nodes:

```javascript
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
```

### Node-Specific Utilities
For functions only needed within a single node:

```javascript
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
```


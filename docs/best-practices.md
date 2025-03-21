# Best Practices

## General Guidelines

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

## Contextual Data Management

1. **Prefer msg properties** for data that flows through nodes
2. **Use flow/global context sparingly** for shared state and utilities
3. **Clean up context data** that is no longer needed
4. **Document all context usage** in the Context Registry

## Deployment Considerations

1. **Test before deploying** to production
2. **Use credentials encryption** for sensitive information
3. **Consider resource utilization** on target hardware
4. **Version flows meaningfully** with semantic version numbers
5. **Maintain a changelog** of significant changes

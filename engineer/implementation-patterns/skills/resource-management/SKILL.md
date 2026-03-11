---
name: resource-management
description: RAII (Resource Acquisition Is Initialization), cleanup patterns, resource leaks, and lifetime management.
---

# Resource Management

Managing scarce resources (file handles, connections, memory) safely.

## Context

You are managing resources safely. Follow RAII and cleanup patterns.

## Domain Context

- **RAII**: Acquire in constructor, release in destructor; guarantees cleanup
- **Cleanup**: Ensure resources are freed even on exception
- **Lifetimes**: How long does a resource live? Who owns it?
- **Scoping**: Use scope to define resource lifetime

## Instructions

1. **Use RAII**: Constructor acquires; destructor releases
2. **Or Try-Finally**: Explicit try/finally blocks for cleanup
3. **Or Defer**: Defer statements (Go, Rust) guarantee cleanup
4. **Test Cleanup**: Verify resources are freed on error paths
5. **Avoid Leaks**: Every allocation has a matching deallocation
6. **Document Ownership**: Who owns this resource? Who's responsible for cleanup?

## Anti-Patterns

- Manual cleanup scattered throughout code; use RAII or defer
- Forgetting cleanup on error paths; use exception-safe code
- Unclear ownership; leads to double-free or use-after-free
- Resource pooling without cleanup; pools grow unbounded
- Holding resources longer than needed; tie lifetime to scope

## Further Reading

- Herb Sutter, _RAII_ (C++ resource management)
- Go documentation on defer statements
- Rust documentation on Drop trait and ownership

---
name: grpc-service-design
description: Protocol buffers, service definitions, streaming RPC, and performance-oriented API design.
---

# gRPC Service Design

High-performance RPC using protocol buffers and HTTP/2.

## Context

You are designing gRPC services. Define message types and service methods.

## Domain Context

- **Protocol Buffers**: Binary serialization; smaller/faster than JSON
- **HTTP/2**: Multiplexing; bidirectional streaming
- **Unary RPC**: Request/response like REST
- **Server Streaming**: Server sends multiple responses
- **Client Streaming**: Client sends multiple requests
- **Bidirectional**: Both send streams

## Instructions

1. **Define Messages**: Protobuf message types; all fields numbered
2. **Define Services**: Methods taking request, returning response
3. **Choose RPC Types**: Unary, server-stream, client-stream, bidirectional
4. **Plan Deadlines**: Timeout values; defaults are often wrong
5. **Error Handling**: gRPC status codes (OK, NOT_FOUND, INTERNAL)
6. **Streaming**: Use when latency matters or data is large

## Anti-Patterns

- Treating gRPC as magic; it's binary RPC, still has latency
- Bidirectional streaming when unary suffices; unnecessary complexity
- No backpressure handling; fast sender overwhelms slow receiver
- Ignoring message versioning; Protobuf handles this well, use it
- Not setting deadlines; requests hang indefinitely

## Further Reading

- gRPC documentation
- Protobuf documentation
- gRPC best practices guide

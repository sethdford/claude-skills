---
name: service-mesh-patterns
description: Implement service mesh patterns for observability, resilience, and traffic management. Use when managing complex microservices communication at scale.
---

# Service Mesh Patterns

Apply service mesh patterns (Istio, Linkerd) to decouple service communication from business logic, enabling uniform resilience and observability.

## Context

You are designing service mesh infrastructure for microservices. The user is dealing with complex service-to-service communication, resilience challenges, or observability gaps. Read their current infrastructure.

## Domain Context

Based on Istio/Linkerd reference implementations and distributed systems research:

- **Sidecar Proxy**: Per-service proxy handling network concerns (retries, circuit breaking, auth)
- **Control Plane**: Centralized configuration of routing, security, observability
- **Mutual TLS**: Encrypted, authenticated service-to-service communication by default
- **Traffic Management**: Canary deployments, retries, timeouts, load balancing
- **Observability**: Distributed tracing, metrics collection, access logs

## Instructions

1. **Assess Mesh Necessity**: Service mesh adds complexity. Evaluate: are you managing >10 services? Do you need fine-grained traffic control? Do you have mTLS requirements? If yes to 2+, mesh may help.

2. **Design Sidecar Injection**: Configure automatic sidecar injection for namespaces. Specify resource requests (sidecars consume ~10-50MB memory per instance).

3. **Configure Routing & Load Balancing**: Define traffic policies (round-robin, least request, random). For canary deployments, specify traffic split (90% stable, 10% canary).

4. **Implement Resilience Policies**: For each service-to-service communication, specify:
   - Retry policy (max 3 attempts, backoff)
   - Timeout (2s)
   - Circuit breaker (fail if error rate > 50%)

5. **Enable Observability**: Configure telemetry collection. Send metrics to Prometheus, traces to Jaeger. Define dashboards for request latency, error rate, saturation.

## Anti-Patterns

- **Mesh Without Observability**: Adds sidecar proxies but no metrics/tracing. Result: can't debug why requests fail. **Guard**: Require metrics and tracing before deploying mesh.
- **Mesh for Small Scale**: Added 10 sidecars and control plane for 5 services. Result: complexity exceeds benefit. **Guard**: Mesh ROI positive at >10 services.
- **Ignoring Sidecar Overhead**: Assumes no performance impact. Result: latency increase and memory bloat. **Guard**: Measure p95 latency before/after mesh; set acceptable overhead budget.
- **mTLS Everywhere Immediately**: Breaks debugging and testing. Result: developers can't test locally without mesh. **Guard**: Enable mTLS gradually; provide options to bypass for dev.

## Further Reading

- _Istio in Action_ by Christian Posta and Burr Sutter — practical service mesh implementation
- _Designing Microservices Platforms_ — service mesh operational patterns
- _Linkerd Documentation_ — lightweight mesh alternative to Istio

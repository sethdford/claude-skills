---
name: deployment-topology
description: Plan container orchestration, load balancing, high availability, and scaling. Design deployment topologies for production systems. Use when architecting deployment infrastructure or modernizing deployment practices.
---

# Deployment Topology

Design deployment architectures with high availability, automatic scaling, health management, and service discovery.

## Context

You are planning how services are deployed and scaled. Design topology for HA, choose orchestration platform, plan service communication, and manage state. Read current deployment practices, SLA requirements, and team operational maturity.

## Domain Context

Based on container orchestration and deployment patterns:

- **Container Orchestration**: Kubernetes (manual control, cloud-agnostic), ECS (AWS-native), Cloud Run (serverless)
- **Service Discovery**: Automatic registration/deregistration; clients find healthy instances
- **Load Balancing**: Distribute traffic across instances; internal (mesh) and external (ingress)
- **Health Checks**: Liveness (restart if dead), readiness (traffic if ready), startup probes
- **Rolling Updates**: Gradual replacement of old instances with new; zero-downtime deployments

## Instructions

1. **Choose Orchestration Platform**: Kubernetes for multi-cloud, complex services. ECS for AWS-only, simpler setup. Cloud Run/App Engine for stateless workloads.

2. **Design Service Topology**: How many replicas per service? Plan for peak load + buffer. Multi-AZ for resilience. Blue-green deployments for safe rollouts.

3. **Implement Service Discovery**: Kubernetes: DNS service records. ECS: load balancer targets. Clients discover healthy endpoints automatically.

4. **Plan Load Balancing**: External load balancer for ingress. Service mesh (Istio) for internal traffic management, circuit breaking, retries.

5. **Configure Health Checks**: Readiness probe: app ready to serve? Liveness probe: process alive? Startup probe: give time to initialize. Tune thresholds to avoid flaky restarts.

## Anti-Patterns

- **Too Many Replicas**: Set replicas to 10 for small service. Result: cost, complexity, no benefit. **Guard**: Calculate required capacity; auto-scale based on CPU/memory, not arbitrary numbers.
- **Health Checks Too Strict**: Fail readiness on any non-200 response. Result: cascading failures, thrashing restarts. **Guard**: Design probes to be lenient on transient errors; only fail on persistent issues.
- **No Graceful Shutdown**: Kill processes immediately. Result: in-flight requests dropped. **Guard**: Drain connections; wait for graceful shutdown before kill.
- **Ignoring Service Mesh Complexity**: Add service mesh (Istio) for features you don't need. Result: operational overhead, debugging difficulty. **Guard**: Start simple; add mesh when you need advanced features (traffic splitting, security policies).

## Further Reading

- _Kubernetes in Action_ by Marko Luksa — Kubernetes deployment patterns
- _Site Reliability Engineering_ by Google — production deployment practices
- _The Phoenix Project_ by Gene Kim — deployment culture and practices

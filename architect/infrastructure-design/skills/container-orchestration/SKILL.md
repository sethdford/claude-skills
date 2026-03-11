---
name: container-orchestration
description: Design Kubernetes clusters for scaling, service discovery, storage, and networking. Plan upgrades and multi-cluster strategies. Use when architecting container infrastructure.
---

# Container Orchestration

Design and operate Kubernetes clusters for scalable, resilient container deployments.

## Context

You are designing Kubernetes infrastructure. Plan cluster architecture, scaling policies, storage, networking, and operations. Read workload characteristics, scale requirements, and team Kubernetes maturity.

## Domain Context

Based on Kubernetes best practices (CNCF, Google, AWS EKS):

- **Clusters**: Logical Kubernetes environment; runs multiple services. Multi-cluster for HA across regions or failure domains.
- **Nodes**: Worker machines (EC2 instances). Auto-scaling groups scale nodes based on demand.
- **Pods**: Smallest deployable unit; usually one container per pod. Co-locate dependent containers sparingly.
- **StatefulSets**: For databases, caches with persistent state. PersistentVolumes for storage. StatelessSets for typical applications.
- **Service Mesh**: Advanced traffic management (Istio); not needed for simple deployments

## Instructions

1. **Design Cluster Topology**: Single cluster (simpler) or multi-cluster (HA, isolation)? Multi-AZ for resilience. Master nodes (API server, etcd) managed by cloud provider (EKS, GKE).

2. **Plan Node Sizing**: How many nodes for peak load? Large nodes (fewer, simpler) vs small nodes (more flexible). Use auto-scaling to handle traffic spikes.

3. **Configure Storage**: Stateless apps: no storage needed. Stateful: PersistentVolumes for databases, caches. Use managed databases (RDS) for data, K8s for cache (Redis).

4. **Set Up Networking**: Calico or Weave for container networking. Service mesh (Istio) for traffic management. Ingress controller for external traffic. Network policies for security.

5. **Plan Operations**: Helm for templating deployments. Flux or ArgoCD for GitOps-driven deployments. Monitoring (Prometheus), logging (ELK), tracing (Jaeger). Regular upgrades.

## Anti-Patterns

- **Over-Complexity from Start**: Add service mesh, istio, monitoring before you need them. Result: hard to operate, debug. **Guard**: Start simple; add features when you hit concrete problems.
- **Ignoring Resource Limits**: Pods unbounded CPU/memory. Result: noisy neighbors, thrashing. **Guard**: Set requests (guaranteed) and limits (max). Monitor utilization.
- **No Pod Disruption Budgets**: Kill pods ungracefully during node drains. Result: request loss. **Guard**: PodDisruptionBudgets ensure minimum replicas during maintenance.
- **Persistent State in Pods**: Use local storage for databases. Result: lost data on pod restart. **Guard**: Use PersistentVolumes or managed databases for state.

## Further Reading

- _Kubernetes in Action_ by Marko Luksa — comprehensive Kubernetes patterns
- _The Phoenix Project_ by Gene Kim — operational discipline
- _Cloud Native DevOps with Kubernetes_ by John Arundel and Justin Domingus — production K8s

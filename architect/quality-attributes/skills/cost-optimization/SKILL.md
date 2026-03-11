---
name: cost-optimization
description: Optimize infrastructure and operational costs without sacrificing performance or reliability. Use when managing cloud budgets or improving unit economics.
---

# Cost Optimization

Systematically reduce infrastructure and operational costs while maintaining SLAs and performance.

## Context

You are optimizing costs. The user faces high cloud bills or needs to improve unit economics. Read their current infrastructure and cost breakdown.

## Domain Context

Based on AWS, Google Cloud, and Azure cost optimization practices:

- **Reserved Instances**: Commit to usage upfront; 30-70% discount vs on-demand
- **Spot Instances**: Unused capacity at 70-90% discount; risk of interruption
- **Right-Sizing**: Match instance type to actual usage (many over-provisioned)
- **Resource Scheduling**: Run infrastructure only when needed (dev, test, non-critical workloads)
- **Data Transfer Costs**: Moving data between regions or to internet expensive; design to minimize

## Instructions

1. **Measure Current Costs**: Break down: compute (instances, pods), storage (databases, backups, archives), networking (data transfer, CDN), managed services. Identify top 3 cost drivers.

2. **Baseline Cost per Unit**: Calculate cost per request, per transaction, per user. Enables comparing optimizations objectively.

3. **Identify Optimization Opportunities**:
   - Compute: Right-size instances, use reserved/spot, schedule non-critical
   - Storage: Archive old data, compress backups, dedup
   - Transfer: Use CDN, minimize cross-region, batch transfers
   - Waste: Unused resources (old databases, unused backups, forgotten VMs)

4. **Model Impact**: For each optimization, estimate savings and implementation effort. Prioritize by ROI (savings / effort).

5. **Implement & Monitor**: Deploy changes. Measure cost reduction. Re-baseline and repeat.

## Anti-Patterns

- **Chasing Lowest Cost**: Use cheapest options (spot instances, no redundancy). Result: outages and data loss. **Guard**: Optimize cost subject to SLA constraints.
- **Over-Provisioning for Safety**: Buy 10x capacity to "be safe." Result: wasted money. **Guard**: Monitor actual usage; right-size to p95 load.
- **Ignoring Total Cost of Ownership**: Count compute but not operations. Result: hidden costs. **Guard**: Include all costs (instances, storage, monitoring, support, ops time).
- **One-Time Optimization**: Cut costs once, never revisit. Result: costs creep back up. **Guard**: Quarterly cost review; treat as ongoing process.

## Further Reading

- _AWS Well-Architected Framework (Cost Optimization Pillar)_ — systematic cost reduction
- _Cloud Economics_ by Joe Weinman — understanding cloud cost models and optimization
- _Google Cloud Cost Optimization Best Practices_ — practical examples and case studies

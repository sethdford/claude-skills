---
name: cloud-architecture
description: Design cloud infrastructure for AWS, GCP, or Azure. Plan compute, storage, networking, and compliance. Use when architecting cloud systems or migrating to cloud.
---

# Cloud Architecture

Design scalable, cost-effective, secure cloud infrastructure on AWS, GCP, or Azure.

## Context

You are designing cloud infrastructure. Select services, plan scaling, networking, security, and cost. Read requirements, existing infrastructure, regulatory constraints, and team cloud maturity.

## Domain Context

Based on cloud architecture best practices (AWS Well-Architected Framework, Google Cloud Architecture Framework):

- **Compute**: Servers (EC2/Compute Engine), containers (ECS/GKE), functions (Lambda/Cloud Functions), management burden increases
- **Storage**: Object storage (S3), databases (RDS/Cloud SQL), data warehouses (Redshift/BigQuery)
- **Networking**: VPC isolation, subnets, security groups, load balancing, DNS
- **Observability**: Metrics, logs, traces; CloudWatch, Stackdriver, DataDog
- **Compliance**: Shared responsibility; you manage application, cloud owns infrastructure

## Instructions

1. **Select Core Services**: What workloads? Web app → App Engine/Elastic Beanstalk. Data processing → Spark on Kubernetes. Database → RDS PostgreSQL. Data warehouse → BigQuery.

2. **Design Resilient Architecture**: Multi-AZ (availability zone) for redundancy. Health checks and auto-recovery. Load balancing across instances. Plan RPO/RTO requirements.

3. **Plan Networking**: VPC with public and private subnets. Bastion for private access. Security groups restrict traffic. NAT Gateway for outbound access. CloudFlare or WAF for DDoS.

4. **Implement Security**: IAM roles (principle of least privilege). Encrypt data at rest (KMS) and in transit (TLS). Secrets management (Secrets Manager/Vault). Regular patching.

5. **Cost Optimize**: Reserved instances for predictable workloads (30-70% discount). Spot instances for batch/non-critical (70% discount). Right-size instances; monitor utilization. Use managed services to reduce operational overhead.

## Anti-Patterns

- **Lift-and-Shift Without Optimization**: Move VMs to cloud as-is. Result: expensive, not cloud-native. **Guard**: Rearchitect for cloud; use managed services where appropriate.
- **Single-AZ for Critical Services**: Cut costs by using single availability zone. Result: outage when AZ fails. **Guard**: Multi-AZ for production; single-AZ acceptable for non-critical dev.
- **Ignoring Cloud-Native Patterns**: Treat cloud like traditional datacenter. Result: underutilize auto-scaling, caching, global distribution. **Guard**: Design for elasticity; use services like CDN, auto-scaling groups.
- **No Cost Monitoring**: Assume cloud is cheaper than on-prem. Result: bill shock. **Guard**: Set up cost alerts; monitor per-service usage; optimize continuously.

## Further Reading

- _AWS Well-Architected Framework_ — foundational cloud design principles
- _Building Microservices on AWS_ — cloud-native architecture patterns
- _Cloud Security Best Practices_ — security architecture for cloud

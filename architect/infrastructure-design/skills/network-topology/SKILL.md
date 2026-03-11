---
name: network-topology
description: Design VPCs, subnets, security groups, load balancing, and DNS architecture. Plan for segmentation, DDoS protection, and failover. Use when architecting network infrastructure.
---

# Network Topology

Design secure, scalable network architecture with proper segmentation, load balancing, and failover.

## Context

You are designing network infrastructure. Plan VPCs, subnets, security groups, load balancers, DNS, DDoS protection. Read application requirements, compliance needs, and expected traffic patterns.

## Domain Context

Based on network architecture best practices (AWS VPC, GCP VPC):

- **VPC**: Virtual private cloud; isolated network environment. Multiple subnets for segmentation.
- **Subnets**: Public (NAT to internet) and private (no direct internet). Separate database tier from web tier.
- **Security Groups**: Stateful firewall rules. Default-deny, whitelist only needed ports.
- **Load Balancing**: ALB for HTTP/HTTPS, NLB for TCP/UDP. Distribute traffic across instances.
- **DNS**: Route 53 for DNS with health checks and failover routing

## Instructions

1. **Design VPC**: CIDR block (10.0.0.0/16 typical). Public subnets in AZ-1 and AZ-2 for web tier. Private subnets for database tier. NAT Gateway for outbound access from private.

2. **Segment with Security Groups**: Web tier: allow 80/443. App tier: allow traffic from web only. Database tier: allow traffic from app tier only. Principle of least privilege.

3. **Plan Load Balancing**: Application Load Balancer (ALB) for web traffic; routes by hostname/path. Network Load Balancer (NLB) for high performance, millions of RPS.

4. **Set Up DNS**: Route 53 routes users to nearest region or healthy endpoint. Health checks detect failures; failover to standby. Support multiple A records for multi-region.

5. **Implement DDoS Protection**: CloudFlare or Shield Standard for volumetric attacks. WAF for application-layer attacks (SQL injection, XSS). Rate limiting for API abuse.

## Anti-Patterns

- **Single Subnet for Everything**: All servers in one subnet. Result: hard to enforce policies, lateral movement risk. **Guard**: Segment by tier; use security groups for access control.
- **Overly Permissive Security Groups**: Allow 0.0.0.0/0 (anywhere) on all ports. Result: security risk. **Guard**: Default-deny; whitelist specific ports/IPs.
- **No Health Checks**: Load balancer routes to dead instance. Result: user errors. **Guard**: Health checks detect failures; remove from load balancer.
- **Ignoring DDoS**: Assume no one will attack. Result: downtime during attack. **Guard**: DDoS protection layers (WAF, rate limiting, CDN); plan capacity for spikes.

## Further Reading

- _AWS Well-Architected Framework_ (Reliability Pillar) — network resilience
- _Site Reliability Engineering_ by Google — network design for reliability
- _Cloudflare Learning Center_ — DDoS protection and security

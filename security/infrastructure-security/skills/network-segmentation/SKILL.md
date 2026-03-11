---
name: network-segmentation
description: Design and implement network segmentation to limit lateral movement and contain breaches.
---

# Network Segmentation

Design and implement network segmentation to isolate systems and limit breach impact.

## Context

You are a senior network security architect designing network segmentation for $ARGUMENTS. Segmentation isolates critical systems, limits lateral movement during breaches, and enforces zero-trust principles. Without segmentation, a compromised web server can directly access databases and internal systems.

## Domain Context

- **Segmentation Strategies**: DMZ (demilitarized zone), tier-based (web, app, database), micro-segmentation, zero-trust
- **Tools**: VPCs/VNets (cloud), VLANs (on-prem), security groups, network ACLs, firewalls, network policies (Kubernetes)
- **Protocols**: Only allow necessary protocols (block unnecessary); default-deny, whitelist approach
- **Monitoring**: Network flow logs capture inter-segment traffic; analyze for suspicious patterns

## Instructions

1. **Design Segmentation Model**:
   - **DMZ (Demilitarized Zone)**: Internet-facing servers (web, API, reverse proxy); isolated from internal systems
   - **Web Tier**: Application servers; can reach database tier, not internet
   - **App Tier**: Business logic; can reach database tier; limited external access
   - **Database Tier**: Databases; only reachable from app tier; no direct internet access
   - **Admin Tier**: Bastion host, jump box, management servers; restrictive access
   - **Data/Backup Tier**: Isolated, encrypted; limited access
   - **User Tier**: Workstations, laptops; isolated from servers

2. **Implement Segmentation Controls**:
   - **Cloud (AWS, Azure, GCP)**:
     - VPC/VNet for logical isolation
     - Subnets for tier separation
     - Security Groups/NSGs for whitelist rules (source IP, port, protocol)
     - Network ACLs for additional network-layer filtering
   - **On-Premise**:
     - VLANs for tier separation
     - Firewalls between tiers (allow only necessary traffic)
     - Access Control Lists (ACLs) on switches/routers

3. **Define Inter-Segment Communication Rules**:
   - **DMZ to Web**: Any (external traffic)
   - **Web to App**: Only necessary ports (e.g., 443 for HTTPS API calls)
   - **App to Database**: Only database port (e.g., 3306 for MySQL)
   - **Database to Internet**: Block (databases should never initiate outbound connections)
   - **Admin to All Tiers**: Limited set of admin operations (patching, backup, monitoring)
   - **Workstations to Servers**: Only necessary services (no full network access)

4. **Monitor & Enforce Segmentation**:
   - Enable network flow logs; analyze for policy violations
   - Alert on traffic that violates segmentation rules
   - Regularly test segmentation (verify rules work as expected)
   - Document rules for future maintenance
   - Review rules quarterly for stale/unnecessary rules

5. **Implement Zero-Trust Principles**:
   - Don't assume internal traffic is trustworthy
   - Require authentication and authorization for all inter-segment access
   - Use micro-segmentation for highly sensitive systems (east-west traffic encryption)
   - Assume breach: design so compromised systems can't easily reach others

## Anti-Patterns

- Overly permissive rules ("allow all traffic between tiers"); **specify exact ports and protocols needed**
- No monitoring of inter-segment traffic; **you won't detect lateral movement**
- Complex rules that operators don't understand; **document rules and test regularly**
- Segmentation only at network layer; **combine with application-layer controls (API authz, database access controls)**
- Forgetting about third-party access (vendors, contractors); **they should go through same segmentation**

## Further Reading

- NIST SP 800-53 (Network Segmentation Controls): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf
- CIS Controls (Access Control): https://www.cisecurity.org/cis-controls/
- Cloud Security Alliance Network Security: https://cloudsecurityalliance.org/
- AWS VPC Documentation: https://docs.aws.amazon.com/vpc/

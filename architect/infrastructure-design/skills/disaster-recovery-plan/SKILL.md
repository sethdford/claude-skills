---
name: disaster-recovery-plan
description: Define recovery objectives (RTO/RPO), backup strategies, failover procedures, and testing protocols. Use when planning disaster recovery or establishing continuity practices.
---

# Disaster Recovery Plan

Design recovery strategies with defined objectives, tested procedures, and regular validation.

## Context

You are planning disaster recovery. Define RTO/RPO requirements, design backup and failover strategies, plan testing. Read business impact analysis, current backups, and regulatory requirements.

## Domain Context

Based on IT disaster recovery best practices (NIST, ISO 27031):

- **RTO (Recovery Time Objective)**: How long can system be down? 1 hour? 1 day? Determines failover strategy.
- **RPO (Recovery Point Objective)**: How much data loss acceptable? 1 hour? 1 day? Determines backup frequency.
- **Backup Strategies**: Full (complete copy), incremental (only changes since last backup), continuous replication
- **Failover**: Automatic (heartbeat-driven) vs manual (operations-triggered). Planned vs unplanned.
- **Testing**: Regular drills validate procedures; practice before disaster strikes

## Instructions

1. **Define Business Requirements**: For each critical system, what's RTO (max downtime) and RPO (max data loss)? Business impact: lost revenue, SLA violations, customer trust?

2. **Design Backup Strategy**: Full daily backup + hourly incremental. Or continuous replication for stricter RPO. Test recovery from backups monthly; document recovery steps.

3. **Plan Failover**: For RTO < 1 hour, set up active-passive (standby system). For RTO < 5 minutes, active-active (both systems live). Implement health checks and automatic failover.

4. **Document Procedures**: Who decides to failover? What are manual steps? How do you know failover succeeded? Test documentation with dry runs; update after each test.

5. **Schedule Regular Testing**: Monthly failover drills for critical systems. Test both planned (maintenance window) and unplanned (kill production server) scenarios. Document findings and improvements.

## Anti-Patterns

- **RTO/RPO Undefined**: Assume everything needs sub-minute RTO. Result: over-engineering cost. **Guard**: Quantify business impact; set RTO/RPO accordingly per system.
- **Backups Never Tested**: Assume they work. Result: discover failures during actual disaster. **Guard**: Regular restore drills; track recovery metrics.
- **Manual Failover for Low RTO**: Plan manual process for 5-minute RTO. Result: missed SLA. **Guard**: Automate failover if RTO tight; test automation regularly.
- **Ignoring Data Consistency in Failover**: Assume data identical between systems. Result: data loss or corruption. **Guard**: Validate data integrity post-failover; have reconciliation procedure.

## Further Reading

- _Site Reliability Engineering_ by Google — production disaster recovery practices
- _Disaster Recovery Planning_ by Salvatore D. Ficara — comprehensive DR framework
- _Resilience Engineering_ by Erik Hollnagel — thinking about recovery and resilience

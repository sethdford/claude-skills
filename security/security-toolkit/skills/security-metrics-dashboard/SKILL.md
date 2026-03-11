---
name: security-metrics-dashboard
description: Create security metrics dashboards to track program effectiveness, trends, and KPIs for leadership reporting.
---

# Security Metrics Dashboard

Create security metrics dashboards to track program effectiveness and communicate to leadership.

## Context

You are a senior security metrics officer creating dashboards for $ARGUMENTS. Metrics demonstrate security program value, identify trends, and highlight areas needing improvement. Well-designed dashboards communicate complex data to non-technical executives.

## Domain Context

- **Metrics Types**: Leading indicators (activities to prevent breaches), lagging indicators (breaches that happened)
- **Data Sources**: SIEM, vulnerability scanners, penetration tests, incident logs, audit findings
- **Audience**: Security team (operational dashboards), executives (strategic dashboards), board (risk dashboards)
- **Tools**: Splunk, Tableau, Grafana, custom scripts

## Instructions

1. **Select Key Metrics**:
   - **Vulnerability Metrics**:
     - Total open vulnerabilities (by severity)
     - Remediation rate (fixed per month)
     - Age of vulnerabilities (how long open?)
     - Mean time to fix (MTTF) by severity
   - **Detection & Response Metrics**:
     - Mean time to detect (MTTD) attacks
     - Mean time to respond (MTTR)
     - Alert volume (overall, by priority)
     - False positive rate (signal-to-noise)
   - **Compliance Metrics**:
     - Compliance score (controls implemented/total required)
     - Audit findings (open, remediated)
     - Training completion rate
   - **Risk Metrics**:
     - Overall risk score (quantified)
     - Risk trend (improving, worsening)
     - Top risks (prioritized for remediation)

2. **Design Dashboards for Audience**:
   - **Security Team (Operational)**:
     - Real-time: Current alerts, open incidents, SIEM dashboard
     - Daily: Attack trends, new vulnerabilities, alert volume
     - Weekly: Remediation progress, deployment status
     - Tools: SIEM, Grafana
   - **Leadership (Strategic)**:
     - Monthly: Key metrics (vulnerabilities, incidents, MTTD/MTTR)
     - Quarterly: Risk posture, compliance status, budget spend vs. plan
     - Annual: Program effectiveness, ROI, recommendations
     - Tools: Executive dashboard (Tableau, PowerBI, custom reports)
   - **Board (Risk)**:
     - Quarterly: Overall risk posture, major incidents, regulatory status
     - Annual: Risk metrics, competitive benchmarking, strategic improvements
     - Tools: One-page executive brief

3. **Visualize Data Effectively**:
   - **Trends Over Time**: Line graphs (vulnerabilities decreasing/increasing?)
   - **Distribution**: Bar charts (vulnerabilities by severity)
   - **Status**: Traffic lights (red/yellow/green for risk level)
   - **Benchmarking**: Compare to industry standards (are we above/below average?)
   - **Sparklines**: Mini trend charts (quick visual of trend direction)

4. **Establish Baselines & Targets**:
   - **Baselines**: Current state (where we are)
     - Example: 150 open vulnerabilities, 45-day MTTF
   - **Targets**: Goal state (where we want to be)
     - Example: 50 open vulnerabilities by end of year, 30-day MTTF
   - **SLAs**: Standards for operational metrics
     - Example: Critical alerts triaged within 15 minutes, >80% resolved within 4 hours

5. **Report & Communicate**:
   - **Executive Summary**: 1-2 page summary of key findings
   - **Detailed Report**: Full metrics, trends, analysis
   - **Traffic Light Status**: Red (at risk), Yellow (needs attention), Green (on track)
   - **Recommendations**: Actions to improve metrics
   - **Frequency**: Monthly to security leadership, quarterly to executives, annual to board

6. **Improve Dashboard Iteratively**:
   - **Feedback**: Ask viewers what metrics matter most
   - **Refinement**: Add/remove metrics based on feedback
   - **Automation**: Automate data collection to reduce manual reporting effort
   - **Tools**: Evaluate new tools to improve visualization/automation
   - **Benchmarking**: Compare to industry standards (Gartner, SANS reports)

## Anti-Patterns

- Vanity metrics (look good but don't correlate to security); **metrics must indicate security posture**
- Too many metrics (overwhelming); **focus on 5-10 key metrics**
- Lagging indicators only (we can't change past); **include leading indicators (activities to prevent breaches)**
- No targets (how do we know if we're improving?); **establish baselines and targets**
- Beautiful dashboards that hide bad news (misleading); **honest reporting, even if uncomfortable**

## Further Reading

- NIST SP 800-55 (Security Metrics & Measurement): https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-55.pdf
- Gartner Security Metrics Reports: Industry benchmarking data
- SANS Security Metrics: https://www.sans.org/white-papers/
- Splunk Dashboards: https://docs.splunk.com/Documentation/

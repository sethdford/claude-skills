# Release Checklist

Pre-release validation across all roles: PM sign-off, QA test pass, security scan, performance baseline, rollback plan, monitoring setup.

## Domain Context

Releases are high-risk events. A single missing step can cause customer impact, security breaches, or performance degradation. The release checklist ensures that before code goes to production, all teams have signed off and contingency plans are in place.

A release includes:

- One or more features that have passed testing and security
- Updated documentation and release notes
- Deployment and rollback procedures
- Monitoring and alerting configured
- Team trained on the release
- Incident response plan ready

**ISO/IEC 12207 Reference:**

- 5.3.8 Verification (all testing complete)
- 5.3.9 Transition (release readiness, deployment procedures)

## Instructions

### Step 1: Establish Release Scope

- **Input**: Set of features/fixes to be released, target date
- **Ask**: What's included in this release? (feature list)
- **Ask**: What's the deployment strategy? (blue-green, canary, gradual rollout)
- **Ask**: What's the rollback plan if something goes wrong?

### Step 2: PM Sign-Off

Check:

- **Release Notes**: Are they written and approved?
- **Customer Communications**: Have customer-facing announcements been prepared?
- **Success Metrics**: Are the metrics for this release defined?
- **Stakeholder Approval**: Have business stakeholders approved the release?
- **Go/No-Go Timeline**: Is there a clear deadline for the go/no-go decision?

Output: PM release readiness checklist

### Step 3: QA Sign-Off

Check:

- **Test Execution**: Have all features been tested per their test plans?
- **Regression Testing**: Have related features been tested for regression?
- **Severity Assessment**: Are all known bugs categorized by severity?
- **Blockers**: Are there any critical bugs that would block release?
- **Release Testing**: Has the release (with all features together) been tested?
- **Browser/Device Coverage**: Have all target browsers/devices been tested?

Output: QA sign-off with test pass rate, known issues, severity breakdown

### Step 4: Security Sign-Off

Check:

- **Vulnerability Scan**: Have all dependencies been scanned? No high/critical CVEs?
- **SAST Results**: Have all code changes passed static analysis?
- **DAST Results**: For web features, has dynamic testing been completed?
- **Secrets Scan**: Are there any committed secrets or credentials?
- **Penetration Testing**: Has security team done a limited pen test (if high-risk release)?
- **Security Changes Review**: Have any new auth, encryption, or access control changes been reviewed?

Output: Security sign-off with scan results and any exceptions

### Step 5: Performance Baseline

Check:

- **Load Testing**: Has the release been tested under expected load?
- **Performance Regression**: Will this release impact performance metrics? (p99 latency, throughput)
- **Resource Usage**: Have memory, CPU, disk consumption been measured?
- **Scaling**: Will this scale to peak traffic?
- **Monitoring**: Are performance metrics configured in monitoring system?

Output: Performance baseline captured, regression analysis

### Step 6: Operations Readiness

Check:

- **Monitoring Configured**: Are all metrics and alerts set up?
- **Logging**: Are important events being logged at appropriate levels?
- **Runbook**: Is there a runbook for running the release in production?
- **Incident Response**: Are incident response procedures documented?
- **Scaling Plan**: Is there a plan to scale if metrics spike?
- **Communication**: Are on-call engineers aware of the release?

Output: Operations readiness checklist

### Step 7: Deployment Plan

Check:

- **Deployment Steps**: Are deployment steps documented and tested?
- **Rollback Plan**: Is there a tested procedure to roll back if needed?
- **Deployment Timeline**: Is there a clear window and sequence?
- **Team Assignments**: Are people assigned to: deploy, monitor, communicate, respond to incidents?
- **Pre-Flight Checks**: Have pre-deployment verification steps been defined?
- **Post-Flight Checks**: Have post-deployment verification steps been defined?

Output: Deployment and rollback procedures

### Step 8: Team Readiness

Check:

- **Training**: Have team members been trained on new features?
- **Support Prep**: Has customer support been prepared for support calls?
- **Documentation**: Is user documentation updated and available?
- **Internal Communication**: Have all teams been informed of the release plan?

Output: Team readiness verification

### Step 9: Consolidate Release Checklist
```

Release Checklist: [Release Name/Version]
Target Date: [Date]
Deployment Strategy: [blue-green / canary / gradual]

Scope:
Features: [list]
Bug Fixes: [list]
Tech Debt: [list]

[ ] PM Sign-Off
[ ] Release notes written and approved
[ ] Customer communications prepared
[ ] Success metrics defined
[ ] Stakeholder approval obtained
[ ] Go/no-go decision date set

[ ] QA Sign-Off
[ ] All features tested per test plan
[ ] Regression testing complete
[ ] All bugs categorized by severity
[ ] No critical/blocking bugs
[ ] Release testing complete (all features together)
[ ] Browser/device coverage complete

[ ] Security Sign-Off
[ ] Vulnerability scans passed
[ ] SAST scans passed
[ ] DAST scans passed (if applicable)
[ ] No secrets/credentials committed
[ ] Security-related changes reviewed
[ ] Exception report (if any deviations)

[ ] Performance Baseline
[ ] Load testing passed
[ ] No performance regression
[ ] Resource usage acceptable
[ ] Scaling plan verified
[ ] Performance monitoring configured

[ ] Operations Readiness
[ ] Monitoring metrics configured
[ ] Logging configured
[ ] Runbook prepared
[ ] Incident response procedures documented
[ ] Scaling procedures documented
[ ] On-call team aware of release

[ ] Deployment Plan
[ ] Deployment steps documented
[ ] Deployment steps tested (in staging)
[ ] Rollback procedure documented
[ ] Rollback procedure tested
[ ] Deployment timeline scheduled
[ ] Team assignments confirmed
[ ] Pre-flight checks defined
[ ] Post-flight checks defined

[ ] Team Readiness
[ ] Engineering team trained
[ ] Support team prepared
[ ] User documentation updated
[ ] All teams notified of schedule

Release Ready? [ ] Yes (all checks passed) [ ] No (see blocking issues below)

Blocking Issues:
[List any checks that failed, required fixes, and estimated time to fix]

Sign-Offs:
PM: ********\_******** Date: **\_\_\_**
QA: ********\_******** Date: **\_\_\_**
Security: ****\_\_\_**** Date: **\_\_\_**
Tech Lead: ****\_\_**** Date: **\_\_\_**

```

### Step 10: Make the Release Decision

**Go Decision:**
- All checklists passed
- No blocking issues
- All sign-offs obtained
- Document: "Release approved and scheduled for [date] [time]"
- Notify: All teams, customers, support

**No-Go Decision:**
- Blocking issues exist
- Document: "Release postponed. Blocking issues: [list]. Re-evaluate on [date]."
- Notify: All teams, customers

## Anti-Patterns

1. **Treating the checklist as a rubber stamp**
   - Mistake: "All boxes are checked, so we ship"
   - Correct: Checklists inform judgment; require explicit human sign-off
   - Fix: Require sign-off from PM, QA, security, tech lead; not just automated checks

2. **Skipping security or performance review for "small" releases**
   - Mistake: "This is just a one-line bug fix, no need for security scan"
   - Correct: Every release should pass the same bar
   - Fix: Automate security and performance checks; fail if not done

3. **Not testing the rollback procedure**
   - Mistake: "We have a rollback plan, so we're ready"
   - Correct: Rollback must be practiced before production
   - Fix: Do a rollback test in staging; time it; document actual steps

4. **Releasing during risky windows**
   - Mistake: "Friday evening deployment"
   - Correct: Releases happen during business hours with full team coverage
   - Fix: Define release windows (e.g., "only Mon-Thu, 10am-12pm")

5. **Not communicating with support and customers**
   - Mistake: "We deployed, now tell customers"
   - Correct: Customers should know about major changes before release
   - Fix: Notify customers 24-48 hours before, during, and after release

## Further Reading

- **Continuous Deployment** — Humble, J. & Farley, D., "Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation" (Addison-Wesley)
- **Release Management** — Clegg, D. & Barker, R., "Case Method Fast-Track: A RAD Approach" (Addison-Wesley)
- **Deployment Strategies** — https://martinfowler.com/bliki/DeploymentPipeline.html
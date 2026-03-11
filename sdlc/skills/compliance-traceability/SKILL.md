# Compliance Traceability

Maps requirements → design decisions → implementation → tests → deployment to ensure full traceability for regulated environments.

## Domain Context

In regulated industries (finance, healthcare, aviation, automotive), you must be able to prove:

- This requirement is implemented (not forgotten)
- This code change is justified (required by a requirement or architectural decision)
- This test validates a requirement (test coverage is intentional, not accidental)
- This deployment includes all required changes (no partial rollouts)

Traceability is the audit trail that proves the system was built intentionally, not accidentally.

**Relevant Standards:**

- **ISO/IEC 12207** — Software lifecycle processes (5.2.1 Requirements, 5.3 Technical processes)
- **ISO/IEC 15288** — Systems and software engineering lifecycle
- **FDA 21 CFR Part 11** — Electronic records for regulated industries
- **SOC 2** — Compliance for cloud services
- **HIPAA** — Healthcare data protection
- **PCI-DSS** — Payment card security

## Instructions

### Step 1: Establish Traceability Scope

- **Input**: Regulation/framework (e.g., SOC 2, HIPAA, PCI-DSS), feature or system to audit
- **Ask**: What requirements must be traced?
- **Ask**: What's the risk level? (critical infrastructure, customer data, financial systems)

Output: Traceability scope

### Step 2: Requirements Definition

Document each requirement:
```

Requirement ID: REQ-001
Title: [Descriptive title]
Description: [What must be true?]
Regulatory Reference: [Which regulation requires this?]
Risk if not met: [What happens if we don't do this?]
Status: [New / Designed / Implemented / Verified / Deployed / Closed]

```

Output: Requirements registry

### Step 3: Design Decisions

For each requirement, document design decisions:
```

Requirement: REQ-001
Design Decision: DD-001
Title: [How we decided to implement this]
Alternatives Considered: [Other approaches we considered]
Trade-offs: [Why we chose this over alternatives]
Architecture Diagram: [Link to diagram showing how this works]
Risk Mitigation: [How we address risks]
Status: [Approved / Rejected / Revised]

```

Output: Design decision registry

### Step 4: Implementation

For each design decision, document code:
```

Design Decision: DD-001
Implementation: IMPL-001
Code Component: [File, function, class]
Code Location: [GitHub link with line numbers]
Implementation Notes: [How does this code implement the design decision?]
Code Review: [PR link, reviewer approval]
Status: [In Progress / Complete / In Testing / In Deployment]

```

Output: Implementation registry

### Step 5: Test Coverage

For each implementation, document tests:
```

Implementation: IMPL-001
Test: TEST-001
Test Type: [Unit / Integration / System / Acceptance / Compliance]
Test Scope: [What does this test validate?]
Test Location: [File, test class, test name]
Expected Result: [What should happen?]
Actual Result: [Does it pass?]
Test Status: [Passing / Failing / Skipped]
Evidence: [Test run logs, coverage report]

```

Output: Test evidence registry

### Step 6: Deployment Verification

For each test, verify deployment:
```

Test: TEST-001
Deployment: DEPLOY-001
Environment: [Dev / Staging / Production]
Deployment Checklist:
[ ] Code merged to main branch
[ ] Tests passing in CI/CD
[ ] Security scans passed
[ ] Performance baselines met
[ ] Monitoring configured
[ ] Rollback plan ready
Deployment Date: [Date]
Deployment Evidence: [Build logs, deployment ticket, monitoring alerts]
Status: [Deployed / Reverted / On Hold]

```

Output: Deployment evidence

### Step 7: Create the Traceability Matrix

Build a matrix showing requirements → design → implementation → tests → deployment:

```

Requirement | Design Decision | Implementation | Tests | Deployment | Status
REQ-001 | DD-001 | IMPL-001 | TEST-001 | DEPLOY-001 | Complete
REQ-002 | DD-002 | IMPL-002 | TEST-002 | DEPLOY-002 | Complete
...

Coverage Statistics:
Requirements Traced: [N / N]
Design Decisions Documented: [N / N]
Code Covered by Tests: [N%]
All Tests Passing: [Yes / No]
All Deployed to Production: [Yes / No]
Traceability Gap: [%]

```

Output: Traceability matrix

### Step 8: Identify Gaps

For each unmapped item:
- **Orphaned Requirement** — Requirement with no design/implementation
- **Orphaned Code** — Code not required by any requirement
- **Missing Tests** — Implementation with no tests
- **Undeployed Changes** — Tested code not yet deployed

Output: Gap analysis with remediation plan

### Step 9: Compliance Sign-Off

```

Traceability Audit: [Feature / System]
Date: [Date]
Auditor: [PM / Tech Lead]
Framework: [SOC 2 / HIPAA / PCI-DSS / etc.]

Coverage:
[ ] All requirements traced to design decisions
[ ] All design decisions traced to implementation
[ ] All implementation traced to tests
[ ] All tests traced to deployment
[ ] No orphaned requirements
[ ] No orphaned code
[ ] Code coverage >= [threshold]%
[ ] All tests passing
[ ] All code deployed to production

Compliance Status:
[ ] Compliant — All items traced and verified
[ ] Conditionally Compliant — [List gaps, remediation plan]
[ ] Non-Compliant — [List critical gaps, must fix before release]

Auditor Sign-Off:
Audit Owner: ******\_****** Date: **\_\_\_**
Remediation Owner: **\_\_\_** Date: **\_\_\_**

```

## Anti-Patterns

1. **Traceability added after the fact**
   - Mistake: "We shipped the feature, now let's add traceability"
   - Correct: Traceability is part of the design process, not an afterthought
   - Fix: Traceability starts in requirements phase; maintained during design/implementation

2. **Traceability for documentation, not for confidence**
   - Mistake: "We have a traceability matrix for compliance, but no one actually uses it"
   - Correct: Traceability should help you answer: "Will this requirement be tested before deployment?"
   - Fix: Traceability matrix should be a living document; reviewed before each deployment

3. **Orphaned code (code with no requirement)**
   - Mistake: "We added a feature, but it wasn't in the original requirements"
   - Correct: If code exists, there should be a requirement that justifies it
   - Fix: When unplanned code appears, retroactively create the requirement

4. **Over-tracing (creating artifacts that aren't real)**
   - Mistake: "Traceability matrix requires 10 documents per requirement, so we created dummy documents"
   - Correct: Traceability should reflect actual work; don't create fake artifacts
   - Fix: Trace only what's real; adjust documentation burden to match team capacity

5. **Not catching traceability gaps during development**
   - Mistake: "We discover gap analysis at audit time"
   - Correct: Traceability gaps should be caught before deployment
   - Fix: Pre-deployment checklist includes: "Run traceability audit, verify no gaps"

## Further Reading

- **ISO/IEC 12207** — Software lifecycle processes (Section 5, Lifecycle processes)
- **FDA Software Validation** — https://www.fda.gov/regulatory-information/search-fda-guidance-documents/part-11-electronic-records-electronic-signatures
- **Requirements Traceability** — IEEE 830, IEEE 1028
- **Compliance Frameworks** — https://www.aicpa.org/interestareas/informationtechnology/researcha-and-guidance/aicpa-soc-2-criteria
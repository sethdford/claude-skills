---
description: Estimate a feature or epic and surface hidden risks.
argument-hint: [feature description or epic name]
---

Chain these steps:

1. Use the `work-breakdown-structure` skill to decompose the feature into epics and work streams
2. Use the `estimation-techniques` skill to size each epic (S/M/L) and identify estimation confidence gaps
3. Use the `risk-register` skill to identify risks that could expand estimates (vendor risk, architecture unknowns, team capacity risk)
4. Synthesize into a final estimate with confidence band (e.g., "M with 60% confidence, could be L if [risk] materializes")

After completion, suggest:

- What spike or proof-of-concept would reduce estimation uncertainty
- Which dependencies must be resolved before this feature starts
- Whether technical debt should be addressed first to unblock faster development

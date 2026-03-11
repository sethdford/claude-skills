# Threat Modeling Plugin

Comprehensive threat modeling toolkit for identifying, analyzing, and prioritizing security threats using industry frameworks like STRIDE, attack trees, and data flow analysis.

## Skills

### 1. stride-analysis

Apply STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege) to systematically identify threats across all categories.

### 2. attack-tree-modeling

Build hierarchical attack trees showing how attackers decompose goals into sub-goals and exploits, enabling effort/cost assessment.

### 3. data-flow-diagram-security

Create security-focused Data Flow Diagrams (DFDs) that illuminate data flows across trust boundaries, storage, and processing points.

### 4. threat-identification

Systematically identify threats from threat libraries, MITRE ATT&CK, CWE/CVE, and historical attack patterns relevant to your industry.

### 5. abuse-case-design

Design abuse cases (negative use cases) showing how attackers misuse system features and exploit business logic.

### 6. trust-boundary-analysis

Identify trust boundaries in system architecture where privilege levels, security contexts, or threat models change.

### 7. asset-inventory

Create comprehensive inventory of critical assets (data, systems, infrastructure, people) and their business value and dependencies.

### 8. threat-library

Build and maintain a reusable, customized threat library tailored to your organization, platform, and threat landscape.

### 9. risk-scoring

Quantify risk using likelihood and impact, apply severity ratings, and prioritize mitigations.

## Commands

### model-threats

Conduct comprehensive threat modeling using STRIDE, attack trees, and risk scoring. Produces threat model document, attack trees, asset inventory, risk register, and mitigation roadmap.

### analyze-attack-surface

Analyze the attack surface to identify exposed components, entry points, and potential attack vectors. Maps external vs. internal components and prioritizes attack vectors.

### assess-risk

Quantify organizational risk from identified threats using likelihood, impact, and risk scoring. Produces risk register, scoring matrix, executive summary, and mitigation roadmap.

### map-trust-boundaries

Identify and document trust boundaries showing where privilege levels and security contexts change. Produces architecture diagram with marked boundaries, control matrix, and hardening recommendations.

## Quick Start

1. **First threat modeling session**: Use `model-threats` command with your system architecture
2. **After threat modeling**: Use `assess-risk` to prioritize mitigations
3. **For architecture reviews**: Use `map-trust-boundaries` to ensure controls at critical boundaries
4. **For attack surface analysis**: Use `analyze-attack-surface` to identify external entry points

## Plugin Info

- **Version**: 1.0.0
- **Author**: Seth Ford
- **License**: MIT
- **Keywords**: threat-modeling, STRIDE, attack-trees, risk-assessment, security

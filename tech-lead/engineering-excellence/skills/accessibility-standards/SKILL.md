---
name: accessibility-standards
description: Establish accessibility standards that make products usable for people with disabilities without being an afterthought. Use when building user-facing systems or scaling the product.
---

# Accessibility Standards

Build accessibility into design and development, not as a QA check at the end.

## Context

You are a senior tech lead establishing accessibility standards for $ARGUMENTS. Accessibility is often treated as afterthought or compliance checkbox. Real accessibility improves products for everyone.

## Domain Context

- **Accessibility benefits everyone** — curb cut (wheelchair ramps) benefits parents with strollers, elderly, travelers. Good accessibility helps 15%+ of users who have some disability.
- **WCAG standards exist** — Web Content Accessibility Guidelines (A, AA, AAA levels). AA is reasonable target for public-facing products. Standards give clear targets.
- **Design for accessibility prevents rework** — building accessible from start is easier than retrofitting. Retrofit = expensive, breaks features.
- **Automated testing finds 30% of issues** — linters catch missing alt text, color contrast, heading hierarchy. Manual testing catches semantic issues. Both needed.

## Instructions

1. **Know WCAG standards**: WCAG AA is standard for public websites. Covers: perceivable (readable, visible), operable (keyboard navigable, not flashing), understandable (clear language, predictable), robust (compatible with assistive tech).

2. **Checklist per level**: Level A: alt text on images, keyboard navigation, semantic HTML. Level AA: color contrast (4.5:1 for text), error messages clear, focus visible. AA is reasonable target.

3. **Integrate into workflow**: Accessibility audit as part of design review. Accessibility testing in QA. Automated checks in CI (contrast, missing alt text, heading hierarchy).

4. **Involve people with disabilities**: Test with real users using screen readers, keyboard navigation, magnification. Automated testing finds only obvious issues. User testing finds experience issues.

5. **Measure and track**: Run WCAG audit quarterly. Track # of violations. Fix critical ones (color contrast, missing alt text) immediately. Fix others in roadmap.

## Anti-Patterns

- **Accessibility as compliance**: "We need WCAG AA to pass audit." Compliance mindset = minimum effort. Better: "Our product should work for everyone" = design mindset.
- **Retrofit approach**: Building feature, then trying to make accessible. Hard. Expensive. Broken promises. Build accessible from start.
- **Automated testing only**: Running axe/lighthouse, fixing issues. Solves 30%. Miss 70% (semantic, UX issues for disabled users). Include user testing.
- **No enforcement**: "We care about accessibility" but no design review, no testing requirement. Doesn't happen. Make it part of DoD.
- **Generic alt text**: Image of woman smiling: alt="woman." Wrong. Context matters. Alt="Sarah accepting her award at the conference." Better.

## Further Reading

- "Web Content Accessibility Guidelines (WCAG)" (W3C) — standards
- _Inclusive Design for a Digital World_ (Regnie Witherspoon) — philosophy
- "Testing with Real Users" (WebAIM) — user testing for accessibility
- "Axe Accessibility Checker" — automated testing tool reference

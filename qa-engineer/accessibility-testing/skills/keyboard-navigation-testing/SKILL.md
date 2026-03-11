---
name: keyboard-navigation-testing
description: Verify full keyboard operability of interactive UI elements per WCAG 2.1 SC 2.1.1. Use when testing web or desktop applications for accessibility compliance.
---

# Keyboard Navigation Testing

Systematically verify that all interactive functionality is operable via keyboard alone, with visible focus indicators, logical tab order, and no keyboard traps — a foundational requirement for accessibility.

## Context

You are a senior QA engineer testing keyboard accessibility for $ARGUMENTS. Keyboard operability is a Level A WCAG requirement and a legal obligation in most jurisdictions.

## Domain Context

- **WCAG 2.2 Success Criterion 2.1.1 (Keyboard)**: All functionality must be operable through a keyboard interface without requiring specific timings for individual keystrokes (Level A)
- **WCAG 2.2 SC 2.1.2 (No Keyboard Trap)**: If keyboard focus can be moved to a component, focus can be moved away using only the keyboard (Level A)
- **WCAG 2.2 SC 2.4.3 (Focus Order)**: Focusable components receive focus in an order that preserves meaning and operability (Level A)
- **WCAG 2.2 SC 2.4.7 (Focus Visible)**: Any keyboard operable UI has a mode of operation where the keyboard focus indicator is visible (Level AA)
- **WAI-ARIA Authoring Practices 1.2**: Defines expected keyboard interaction patterns for common widgets (tabs, menus, dialogs, trees, grids, comboboxes)
- **Section 508 / EN 301 549**: Legal standards requiring keyboard accessibility for government and public sector applications

## Instructions

1. **Inventory interactive elements**: Catalog all interactive elements on the page/screen — links, buttons, form inputs, custom widgets, modals, tooltips, drag-and-drop areas, media controls. Each must be keyboard-operable
2. **Test tab order**: Press Tab through the entire page. Verify:
   - Focus moves in a logical, predictable order (generally left-to-right, top-to-bottom for LTR languages)
   - No elements are skipped that should be focusable
   - No hidden or off-screen elements receive unexpected focus
   - Shift+Tab reverses the order correctly
   - `tabindex` values > 0 are not used (they break natural order)
3. **Test focus visibility**: At each stop, verify the focus indicator is clearly visible — high contrast, sufficient size, not obscured by other elements. Test in both light and dark modes if applicable
4. **Test keyboard interactions**: For each interactive element, verify the expected keyboard behavior:
   - Buttons: Enter and Space activate
   - Links: Enter activates
   - Checkboxes: Space toggles
   - Radio buttons: Arrow keys move selection within group
   - Select/dropdown: Arrow keys navigate, Enter selects
   - Custom widgets: Follow WAI-ARIA keyboard patterns for the widget role
5. **Test keyboard traps**: Verify you can always Tab or Escape out of any component. Pay special attention to: modals (focus should be trapped _inside_ but Escape dismisses), date pickers, rich text editors, embedded iframes, video players, and autocomplete dropdowns
6. **Test skip navigation**: Verify skip links exist and work (e.g., "Skip to main content") for pages with repetitive navigation. The skip link should be the first focusable element and should be visible on focus

## Anti-Patterns

- **Mouse-path mimicry** — LLMs test keyboard navigation by replicating the visual mouse path instead of testing actual keyboard interaction contracts (e.g., verifying hover states instead of focus states). **Guard:** Test plans must reference specific keyboard events (Tab, Enter, Space, Escape, Arrow keys), not mouse events.
- **Ignoring custom widget keyboard patterns** — LLMs apply generic Tab/Enter testing to custom ARIA widgets that require specific keyboard patterns (e.g., a tablist needs Arrow keys, not Tab, to move between tabs). **Guard:** For every custom widget, look up the WAI-ARIA Authoring Practices keyboard pattern for that widget role.
- **Focus indicator subjectivity** — LLMs describe focus indicators as "visible" without measurable criteria. **Guard:** Focus indicators must meet WCAG 2.2 SC 2.4.13 minimum area (at least 2px perimeter) and 3:1 contrast ratio against adjacent colors. Use a contrast checker tool, not visual judgment.

## Further Reading

- W3C WAI-ARIA Authoring Practices 1.2 — Keyboard interaction patterns for all standard widget roles
- WCAG 2.2, Success Criteria 2.1.1, 2.1.2, 2.4.3, 2.4.7, 2.4.13 — Keyboard and focus requirements
- Deque University, "Keyboard Testing Guide" — Practical keyboard testing methodology
- WebAIM, "Keyboard Accessibility" — Quick reference for expected keyboard behaviors by element type

---

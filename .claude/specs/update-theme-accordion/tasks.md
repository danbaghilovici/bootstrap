# Implementation Plan: Update Theme Accordion

## Task Overview

This implementation updates Bootstrap's Accordion component styling to match Carbon Design System by adding 6 variable overrides in `_variables.scss`. The flush variant works automatically through Bootstrap's existing CSS classes.

## Steering Document Compliance

- **tech.md**: Uses Bootstrap's variable override pattern exclusively
- **structure.md**: Changes isolated to `scss/_variables.scss` in a new Carbon Accordion Overrides section

## Atomic Task Requirements

Each task meets the criteria for optimal agent execution:
- **File Scope**: 1-2 files per task
- **Time Boxing**: 5-15 minutes each
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Exact file paths specified
- **Agent-Friendly**: Clear input/output with implementation code provided

## Tasks

- [ ] 1. Add Accordion variable overrides in `_variables.scss`
  - File: `scss/_variables.scss`
  - Add after Carbon List Group Overrides section (after line 374)
  - Add section header comment with Carbon reference
  - Override `$accordion-padding-y` to `$spacer * .75` (12px)
  - Override `$accordion-padding-x` to `$spacer` (16px)
  - Override `$accordion-border-color` to `$gray-300`
  - Override `$accordion-button-active-bg` to `$body-bg`
  - Override `$accordion-button-active-color` to `$body-color`
  - Override `$accordion-icon-active-color` to `$body-color`
  - Include `stylelint-disable/enable scss/dollar-variable-default` comments
  - _Leverage: `scss/_variables.scss` lines 341-374 (list group override pattern)_
  - _Requirements: 1.3, 2.2, 2.3, 3.1, 3.2, 4.4_

- [ ] 2. Build and verify CSS compilation
  - Run `npm run css` to compile CSS
  - Run `npm run css-lint` to verify no SCSS linting errors
  - Verify compiled CSS contains updated accordion values
  - Check `--bs-accordion-btn-padding-y` is 0.75rem (12px)
  - Check `--bs-accordion-btn-padding-x` is 1rem (16px)
  - _Requirements: All (verification)_

- [ ] 3. Create `demo/carbon-accordion.html` visual test page
  - File: `demo/carbon-accordion.html`
  - Include default accordion with 3 items
  - Include accordion with first item expanded by default
  - Include accordion-flush variant
  - Include accordion with always-open behavior
  - Add visual comparison notes for Carbon styling
  - _Leverage: `demo/carbon-buttons.html` structure and styling_
  - _Requirements: 1.1, 1.2, 1.3, 2.1-2.4, 3.1-3.3, 4.1-4.4, 5.1-5.2, 6.1-6.3, 7.1-7.3_

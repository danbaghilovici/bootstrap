# Implementation Plan: Update Theme List

## Task Overview

This implementation updates Bootstrap's List Group component styling to match Carbon Design System by adding 5 variable overrides in `_variables.scss`. Basic HTML lists require no changes as Bootstrap's defaults already align with Carbon's approach.

## Steering Document Compliance

- **tech.md**: Uses Bootstrap's variable override pattern exclusively
- **structure.md**: Changes isolated to `scss/_variables.scss` in a new Carbon List Group Overrides section

## Atomic Task Requirements

Each task meets the criteria for optimal agent execution:
- **File Scope**: 1-2 files per task
- **Time Boxing**: 5-15 minutes each
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Exact file paths specified
- **Agent-Friendly**: Clear input/output with implementation code provided

## Tasks

- [ ] 1. Add List Group variable overrides in `_variables.scss`
  - File: `scss/_variables.scss`
  - Add after Carbon Border Radius Overrides section (after line 336)
  - Add section header comment with Carbon reference
  - Override `$list-group-item-padding-y` to `$spacer * .75` (12px)
  - Override `$list-group-action-color` to `$body-color`
  - Override `$list-group-hover-bg` to `$gray-100`
  - Override `$list-group-action-active-bg` to `$gray-200`
  - Override `$list-group-disabled-color` to `$gray-500`
  - Include `stylelint-disable/enable scss/dollar-variable-default` comments
  - _Leverage: `scss/_variables.scss` lines 308-336 (border radius override pattern)_
  - _Requirements: 2.2, 4.3, 4.5, 6.1, 6.3, 7.2, 7.3_

- [ ] 2. Build and verify CSS compilation
  - Run `npm run css` to compile CSS
  - Run `npm run css-lint` to verify no SCSS linting errors
  - Verify compiled CSS contains updated List Group values
  - Check `--bs-list-group-item-padding-y` is 0.75rem (12px)
  - _Requirements: 7.4_

- [ ] 3. Create `demo/carbon-lists.html` visual test page
  - File: `demo/carbon-lists.html`
  - Include basic HTML lists: `ol`, `ul`, nested lists, `dl` with `dt`/`dd`
  - Include List Group: default, flush, horizontal variants
  - Include List Group states: active, disabled, hover (via instructions)
  - Include actionable List Group items (links and buttons)
  - Include List Group with badges
  - Include List Group with custom content
  - _Leverage: `demo/carbon-buttons.html` structure and styling_
  - _Requirements: 1.1, 1.2, 2.1, 2.2, 3.1, 3.2, 4.1-4.5, 5.1-5.3, 6.1-6.4_

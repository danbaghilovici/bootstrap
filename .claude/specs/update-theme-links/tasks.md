# Implementation Plan: Update Theme Links

## Task Overview

This implementation updates Bootstrap's link styling to match Carbon Design System by modifying link variables in `_variables.scss`. The changes are minimal - updating existing link color overrides to use Bootstrap theme variables and adding two new decoration variables.

## Steering Document Compliance

- **tech.md**: Uses Bootstrap's variable override pattern exclusively
- **structure.md**: Changes isolated to `scss/_variables.scss` in the Carbon Color Overrides section

## Atomic Task Requirements

Each task meets the criteria for optimal agent execution:
- **File Scope**: 1-2 files per task
- **Time Boxing**: 5-15 minutes each
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Exact file paths specified
- **Agent-Friendly**: Clear input/output with implementation code provided

## Tasks

- [ ] 1. Update link variable overrides in `_variables.scss`
  - File: `scss/_variables.scss`
  - Update existing link color section (lines 222-226)
  - Change `$link-color` from `#0f62fe` to `$primary`
  - Change `$link-hover-color` from `#0043ce` to `$info`
  - Add `$link-decoration: underline;`
  - Add `$link-hover-decoration: underline;`
  - Add Carbon reference comment for link style documentation
  - _Leverage: `scss/_variables.scss` lines 201-211 (theme colors pattern)_
  - _Requirements: 1.1, 1.2, 2.1, 2.2, 6.2, 6.3_

- [ ] 2. Build and verify CSS compilation
  - Run `npm run css` to compile CSS
  - Run `npm run css-lint` to verify no SCSS linting errors
  - Verify compiled CSS contains correct `--bs-link-color` and `--bs-link-hover-color` values
  - Verify `--bs-link-hover-decoration: underline` is present in compiled CSS
  - _Requirements: 6.4_

- [ ] 3. Create `demo/carbon-links.html` visual test page
  - File: `demo/carbon-links.html`
  - Include examples of default links, hover states (via instructions)
  - Include links within paragraphs (inline context)
  - Include standalone links
  - Include icon links using Bootstrap's `.icon-link` class
  - Include links in various components (cards, lists, nav)
  - Include disabled link example
  - _Leverage: `demo/carbon-buttons.html` structure and styling_
  - _Requirements: 1.1, 1.2, 2.1, 2.2, 3.1, 5.1, 5.2_

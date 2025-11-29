# Implementation Plan: Update Theme Buttons

## Task Overview

Implement Carbon Design System button styling by adding Bootstrap variable overrides to `scss/_variables.scss`. This is a single-file change following the established pattern used for colors, typography, and spacing customizations.

## Steering Document Compliance

- **tech.md**: Variable-only customization using Bootstrap's `!default` pattern
- **structure.md**: All changes in `scss/_variables.scss`, with Carbon token comments

## Atomic Task Requirements

All tasks follow these criteria:
- **File Scope**: Single file (`scss/_variables.scss`)
- **Time Boxing**: Each task completable in 5-15 minutes
- **Single Purpose**: One aspect of button styling per task
- **Specific Location**: After line 231 (end of Carbon Color Overrides section)

## Tasks

- [ ] 1. Add button shape variables to scss/_variables.scss
  - File: `scss/_variables.scss` (after line 231)
  - Add section header comment for Carbon Button Overrides
  - Add `$btn-border-radius: 0`
  - Add `$btn-border-radius-sm: 0`
  - Add `$btn-border-radius-lg: 0`
  - Include Carbon reference comments
  - _Requirements: 1.1, 1.2, 1.3_

- [ ] 2. Add button sizing variables for default buttons
  - File: `scss/_variables.scss` (continue button section)
  - Add `$btn-padding-y: 0.625rem` (10px for 40px height)
  - Add `$btn-padding-x: 1rem` (16px)
  - Add `$btn-font-size: 0.875rem` (14px)
  - Add `$btn-line-height: 1.29` (18px line)
  - Include height calculation comments
  - _Requirements: 2.1, 2.4, 2.5_

- [ ] 3. Add button sizing variables for small and large buttons
  - File: `scss/_variables.scss` (continue button section)
  - Add small button: `$btn-padding-y-sm: 0.3125rem`, `$btn-padding-x-sm: 1rem`, `$btn-font-size-sm: 0.875rem`
  - Add large button: `$btn-padding-y-lg: 0.875rem`, `$btn-padding-x-lg: 1rem`, `$btn-font-size-lg: 0.875rem`
  - Include height calculation comments
  - _Requirements: 2.2, 2.3_

- [ ] 4. Add button typography variable
  - File: `scss/_variables.scss` (continue button section)
  - Add `$btn-font-weight: $font-weight-normal` (references existing variable)
  - _Requirements: 3.1, 3.2_

- [ ] 5. Add button focus state variables
  - File: `scss/_variables.scss` (continue button section)
  - Add `$btn-focus-width: 2px`
  - Add `$btn-focus-box-shadow: inset 0 0 0 2px #0f62fe`
  - Include Carbon Blue 60 focus reference comment
  - _Requirements: 4.1, 4.2, 4.3_

- [ ] 6. Add button box shadow and transition variables
  - File: `scss/_variables.scss` (continue button section)
  - Add `$btn-box-shadow: none`
  - Add `$btn-active-box-shadow: none`
  - Add `$btn-transition` with 150ms timing
  - Add section closing comment
  - _Requirements: 5.4, 6.3, 8.1, 8.2, 8.3_

- [ ] 7. Add button disabled opacity variable
  - File: `scss/_variables.scss` (continue button section)
  - Add `$btn-disabled-opacity: 1`
  - Include comment explaining Carbon disabled limitation
  - _Requirements: 7.3_

- [ ] 8. Build and verify CSS compilation
  - Run `npm run css` to compile SCSS
  - Verify no compilation errors
  - Run `npm run css-lint` to check for linting issues
  - _Requirements: 9.1, 9.2_

- [ ] 9. Create button demo page
  - File: `demo/carbon-buttons.html`
  - Create HTML showcasing all button variants (primary, secondary, danger, etc.)
  - Include all sizes (sm, default, lg)
  - Include all states (normal, hover demo, focus demo, disabled)
  - Include outline button variants
  - Include button groups example
  - _Requirements: All (visual verification)_

# Implementation Plan: Update Theme Alert

## Task Overview

Implement Carbon Design System styling for Bootstrap alerts through variable overrides and a dedicated custom styles file. The implementation follows the established pattern of the carbon/ directory for component-specific customizations.

## Steering Document Compliance

- **structure.md**: Custom styles in `scss/carbon/_alert.scss`, variables in `scss/_variables.scss`
- **tech.md**: Variable-only customization where possible, custom file for left-border styling

## Atomic Task Requirements

Each task is designed to:
- Touch 1-3 related files maximum
- Be completable in 15-30 minutes
- Have one testable outcome
- Specify exact files to create/modify

## Tasks

- [ ] 1. Add Carbon alert variable overrides in _variables.scss
  - File: `scss/_variables.scss` (modify, around line 1960)
  - Add before Bootstrap's default alert variables section
  - Set `$alert-padding-y: $spacer * .75` (12px)
  - Set `$alert-padding-x: $spacer` (16px)
  - Set `$alert-border-radius: 0` (square corners)
  - Set `$alert-border-width: 1px`
  - Set `$alert-link-font-weight: $font-weight-semibold`
  - Purpose: Override Bootstrap defaults with Carbon spacing and styling
  - _Leverage: Existing Carbon color variables ($danger, $success, etc.)_
  - _Requirements: 1.3, 3.1, 3.2, 3.5_

- [ ] 2. Create carbon/_alert.scss with base alert styles
  - File: `scss/carbon/_alert.scss` (create new)
  - Add file header comments referencing Carbon notification component
  - Add base `.alert` rule with `border-left-width: 3px`
  - Set default border-color to `#e0e0e0` (Carbon ui-03)
  - Set text color to `$body-color` (#161616)
  - Purpose: Establish Carbon left-border accent pattern
  - _Leverage: `scss/carbon/_accordion.scss` as pattern reference_
  - _Requirements: 1.1, 1.4, 1.5_

- [ ] 3. Add alert color variant styles to carbon/_alert.scss
  - File: `scss/carbon/_alert.scss` (continue from task 2)
  - Add `@each` loop over `$theme-colors` map
  - For each `.alert-#{$state}` set:
    - `border-left-color: $value`
    - `--#{$prefix}alert-color: #{$body-color}`
    - `--#{$prefix}alert-bg: #{tint-color($value, 90%)}`
    - `--#{$prefix}alert-border-color: #e0e0e0`
  - Purpose: Generate Carbon-styled variants for all theme colors
  - _Leverage: Bootstrap's `$theme-colors` map, `tint-color()` function_
  - _Requirements: 2.1, 2.2, 2.3, 2.4, 2.5, 2.6_

- [ ] 4. Add focus states for alert interactive elements
  - File: `scss/carbon/_alert.scss` (continue from task 3)
  - Add `.alert-link:focus` with `outline: 2px solid #0f62fe` and `outline-offset: 2px`
  - Add `.alert-dismissible .btn-close:focus` with matching outline and `box-shadow: none`
  - Purpose: Ensure accessible keyboard navigation with Carbon focus ring
  - _Leverage: Focus pattern from `scss/carbon/_accordion.scss`_
  - _Requirements: 5.1, 5.2, 4.2_

- [ ] 5. Add high-contrast alert variant (optional)
  - File: `scss/carbon/_alert.scss` (continue from task 4)
  - Add `.alert-high-contrast` modifier class
  - Set `border-left-width: 0`
  - Add variant-specific overrides for danger, success, warning, info, primary
  - Set full background color and white text for each
  - Purpose: Provide prominent alert option for critical messages
  - _Requirements: 6.1, 6.2, 6.3_

- [ ] 6. Update carbon/_index.scss to import alert styles
  - File: `scss/carbon/_index.scss` (modify)
  - Add `@import "alert";` after existing imports
  - Purpose: Include alert styles in build output
  - _Leverage: Existing import pattern in _index.scss_
  - _Requirements: All (enables all alert styles)_

- [ ] 7. Build and verify CSS output
  - Run: `npm run css` to compile
  - Verify `dist/css/bootstrap.css` contains alert customizations
  - Check for any Sass compilation errors
  - Purpose: Confirm successful build integration
  - _Requirements: All_

- [ ] 8. Create demo HTML file for visual testing
  - File: `demo/carbon-alert.html` (create new)
  - Add examples of all alert variants (danger, success, warning, info, primary, secondary)
  - Include dismissible alert example
  - Include alert with heading and link
  - Include high-contrast variant examples
  - Add focus state testing section
  - Purpose: Enable visual verification of all requirements
  - _Leverage: `demo/carbon-accordion.html` as pattern_
  - _Requirements: All_

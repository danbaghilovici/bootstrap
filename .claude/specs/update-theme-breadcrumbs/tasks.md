# Implementation Plan: Update Theme Breadcrumbs

## Task Overview

Implement Carbon Design System styling for Bootstrap breadcrumbs through variable overrides and a dedicated custom styles file. The implementation follows the established pattern of the carbon/ directory for component-specific customizations.

## Steering Document Compliance

- **structure.md**: Custom styles in `scss/carbon/_breadcrumb.scss`, variables in `scss/_variables.scss`
- **tech.md**: Variable-only customization where possible, custom file for link/focus styling

## Atomic Task Requirements

Each task is designed to:
- Touch 1-3 related files maximum
- Be completable in 15-30 minutes
- Have one testable outcome
- Specify exact files to create/modify

## Tasks

- [ ] 1. Add Carbon breadcrumb variable overrides in _variables.scss
  - File: `scss/_variables.scss` (modify, around line 2074)
  - Add before Bootstrap's default breadcrumb variables section
  - Set `$breadcrumb-font-size: 0.875rem` (14px)
  - Set `$breadcrumb-item-padding-x: 0.5rem` (8px)
  - Set `$breadcrumb-divider-color: $body-color` (#161616)
  - Set `$breadcrumb-active-color: $body-color` (#161616)
  - Set `$breadcrumb-divider: quote("/")` (forward slash)
  - Purpose: Override Bootstrap defaults with Carbon typography and colors
  - _Leverage: Existing Carbon color variables ($body-color, $primary)_
  - _Requirements: 1.1, 3.1, 4.1, 4.2, 6.3_

- [ ] 2. Create carbon/_breadcrumb.scss with link styles
  - File: `scss/carbon/_breadcrumb.scss` (create new)
  - Add file header comments referencing Carbon breadcrumb component
  - Add `.breadcrumb-item a` rule with:
    - `color: $primary` (Blue 60)
    - `text-decoration: none`
    - `white-space: nowrap`
  - Add hover state with `color: $info` (Blue 70) and `text-decoration: underline`
  - Purpose: Style breadcrumb links to match Carbon design
  - _Leverage: `scss/carbon/_alert.scss` as pattern reference_
  - _Requirements: 2.1, 2.2, 2.3_

- [ ] 3. Add focus states to carbon/_breadcrumb.scss
  - File: `scss/carbon/_breadcrumb.scss` (continue from task 2)
  - Add `.breadcrumb-item a:focus` with:
    - `outline: 1px solid $primary` (Blue 60)
    - `outline-offset: 0`
  - Purpose: Ensure accessible keyboard navigation with Carbon focus ring
  - _Leverage: Focus pattern from `scss/carbon/_accordion.scss`_
  - _Requirements: 5.1, 5.2, 5.3_

- [ ] 4. Add active item styling to carbon/_breadcrumb.scss
  - File: `scss/carbon/_breadcrumb.scss` (continue from task 3)
  - Add `.breadcrumb-item.active` rule with `cursor: auto`
  - Purpose: Ensure current page item has correct cursor behavior
  - _Requirements: 3.2, 3.3_

- [ ] 5. Update carbon/_index.scss to import breadcrumb styles
  - File: `scss/carbon/_index.scss` (modify)
  - Add `@import "breadcrumb";` after existing imports
  - Purpose: Include breadcrumb styles in build output
  - _Leverage: Existing import pattern in _index.scss_
  - _Requirements: All (enables all breadcrumb styles)_

- [ ] 6. Build and verify CSS output
  - Run: `npm run css` to compile
  - Verify `dist/css/bootstrap.css` contains breadcrumb customizations
  - Check for any Sass compilation errors
  - Purpose: Confirm successful build integration
  - _Requirements: All_

- [ ] 7. Create demo HTML file for visual testing
  - File: `demo/carbon-breadcrumb.html` (create new)
  - Add basic breadcrumb navigation example
  - Include multi-level breadcrumb with active item
  - Add focus state testing section
  - Add color reference table
  - Purpose: Enable visual verification of all requirements
  - _Leverage: `demo/carbon-alert.html` as pattern_
  - _Requirements: All_

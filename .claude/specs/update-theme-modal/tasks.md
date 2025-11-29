# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's modal component via variable overrides and minimal custom styles. The modal requires variable overrides for container, header, footer, backdrop, and sizes, plus a small custom style file for title typography and close button focus state.

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_modal.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Atomic Task Requirements

Each task meets these criteria for optimal agent execution:
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify

## Tasks

- [ ] 1. Add modal variable overrides to `scss/_variables-carbon.scss`
  - File: `scss/_variables-carbon.scss`
  - Add Carbon Modal section after tooltip section
  - Define container variables: `$modal-inner-padding` (1rem), `$modal-content-color` ($body-color), `$modal-content-bg` ($body-bg), `$modal-content-border-color` ($gray-200), `$modal-content-border-width` (1px), `$modal-content-border-radius` (0), `$modal-content-box-shadow-xs` and `$modal-content-box-shadow-sm-up`
  - Define header variables: `$modal-header-border-color` ($gray-200), `$modal-header-border-width` (1px), `$modal-header-padding-y` (1rem), `$modal-header-padding-x` (1rem)
  - Define footer variables: `$modal-footer-bg` ($body-bg), `$modal-footer-border-color` ($gray-200), `$modal-footer-border-width` (1px)
  - Define backdrop variables: `$modal-backdrop-bg` ($gray-900), `$modal-backdrop-opacity` (.5)
  - Define size variables: `$modal-sm` (448px), `$modal-md` (576px), `$modal-lg` (672px), `$modal-xl` (896px)
  - Include stylelint disable/enable comments
  - _Requirements: 1.1-1.5, 2.1-2.2, 3.1-3.2, 4.1-4.2, 5.1-5.3, 6.1-6.4_
  - _Leverage: scss/_variables-carbon.scss (tooltip section pattern)_

- [ ] 2. Create modal custom styles in `scss/carbon/_modal.scss`
  - File: `scss/carbon/_modal.scss` (new file)
  - Create new file with Carbon reference comment
  - Add `.modal-title` styles: `font-size: 1.25rem`, `font-weight: 400`
  - Add `.modal-header .btn-close:focus-visible` styles: 2px solid `$primary` outline with 1px offset
  - _Requirements: 3.3, 3.4, 7.2_
  - _Leverage: scss/carbon/_tooltip.scss (custom styles pattern)_

- [ ] 3. Update `scss/carbon/_index.scss` to import modal
  - File: `scss/carbon/_index.scss`
  - Add `@import "modal";` after tooltip import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 4. Create demo page `demo/carbon-modal.html`
  - File: `demo/carbon-modal.html` (new file)
  - Follow structure from `demo/carbon-tooltip.html`
  - Include: default modal, small modal, large modal, xl modal
  - Include: modal with scrollable content, centered modal
  - Add buttons to trigger each modal variant
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - Include Bootstrap modal JavaScript initialization
  - _Leverage: demo/carbon-tooltip.html (demo page structure)_

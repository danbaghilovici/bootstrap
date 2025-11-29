# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's toast component via variable overrides and custom styles. The toast requires variable overrides for container styling (colors, borders, shadow) and custom styles for the left accent border and variant classes (`.toast-success`, `.toast-warning`, `.toast-danger`, `.toast-info`).

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_toast.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Atomic Task Requirements

Each task meets these criteria for optimal agent execution:
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify

## Tasks

- [ ] 1. Add toast variable overrides to `scss/_variables-carbon.scss`
  - File: `scss/_variables-carbon.scss`
  - Add Carbon Toast section after form section
  - Define container variables: `$toast-max-width` (350px), `$toast-padding-x` (0.75rem), `$toast-padding-y` (0.75rem), `$toast-font-size` (0.875rem), `$toast-color` ($body-color), `$toast-background-color` ($body-bg), `$toast-border-width` (1px), `$toast-border-color` ($gray-200), `$toast-border-radius` (0), `$toast-box-shadow` (0 2px 6px rgba(0, 0, 0, .3))
  - Define header variables: `$toast-header-color` ($body-color), `$toast-header-background-color` ($body-bg), `$toast-header-border-color` ($gray-200)
  - Include stylelint disable/enable comments
  - _Requirements: 1.1-1.5, 3.1-3.3, 4.1-4.3, 6.1_
  - _Leverage: scss/_variables-carbon.scss (form section pattern)_

- [ ] 2. Create toast custom styles in `scss/carbon/_toast.scss`
  - File: `scss/carbon/_toast.scss` (new file)
  - Create new file with Carbon reference comment
  - Add base `.toast` styles: `border-left-width: 3px`, `border-left-color: $primary`
  - Add `.toast-success` styles: `border-left-color: $success`
  - Add `.toast-warning` styles: `border-left-color: $warning`
  - Add `.toast-danger` styles: `border-left-color: $danger`
  - Add `.toast-info` styles: `border-left-color: $info`
  - Add `.toast-header .text-body-secondary` styles: `color: $gray-700 !important`
  - Add `.toast-header .btn-close:focus` styles: 2px solid `$primary` outline with -2px offset, no box-shadow
  - _Requirements: 2.1-2.6, 3.4, 5.2-5.3_
  - _Leverage: scss/carbon/_alert.scss (left border pattern)_

- [ ] 3. Update `scss/carbon/_index.scss` to import toast
  - File: `scss/carbon/_index.scss`
  - Add `@import "toast";` after form import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 4. Create demo page `demo/carbon-toast.html`
  - File: `demo/carbon-toast.html` (new file)
  - Follow structure from `demo/carbon-modal.html`
  - Include: default toast with header and body
  - Include: success toast (`.toast-success`)
  - Include: warning toast (`.toast-warning`)
  - Include: danger toast (`.toast-danger`)
  - Include: info toast (`.toast-info`)
  - Include: toast with timestamp
  - Include: stacked toasts example
  - Add buttons to trigger each toast variant
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - Include Bootstrap toast JavaScript initialization
  - _Leverage: demo/carbon-modal.html (demo page structure)_

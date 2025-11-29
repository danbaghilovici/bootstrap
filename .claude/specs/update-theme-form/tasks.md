# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's form components via variable overrides and custom styles. The form requires variable overrides for labels, helper text, input sizing, colors, disabled states, focus states, input groups, and validation. Custom styles are needed for focus outline (Carbon uses outline instead of box-shadow) and hover states.

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_form.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Atomic Task Requirements

Each task meets these criteria for optimal agent execution:
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify

## Tasks

- [ ] 1. Add form variable overrides to `scss/_variables-carbon.scss`
  - File: `scss/_variables-carbon.scss`
  - Add Carbon Form section after modal section
  - Define label variables: `$form-label-margin-bottom` (0.5rem), `$form-label-font-size` (0.75rem), `$form-label-font-weight` (400), `$form-label-color` ($gray-700)
  - Define helper text variables: `$form-text-margin-top` (0.25rem), `$form-text-font-size` (0.75rem), `$form-text-color` ($gray-700)
  - Define input sizing variables for default (40px), small (32px), and large (48px): `$input-btn-padding-y`, `$input-btn-padding-x`, `$input-btn-font-size`, `$input-btn-line-height` and size variants
  - Define input color variables: `$input-bg` ($body-bg), `$input-color` ($body-color), `$input-border-color` ($gray-500), `$input-placeholder-color` ($gray-600)
  - Define disabled state variables: `$input-disabled-color` ($gray-300), `$input-disabled-bg` ($gray-100), `$input-disabled-border-color` ($gray-300)
  - Define focus variables: `$input-focus-border-color` ($primary), `$input-focus-box-shadow` (none), `$input-btn-focus-box-shadow` (none)
  - Define input group variables: `$input-group-addon-bg` ($gray-200), `$input-group-addon-border-color` ($gray-500)
  - Define form select focus: `$form-select-focus-box-shadow` (none)
  - Define validation variables: `$form-feedback-valid-color`, `$form-feedback-invalid-color`, `$form-valid-color`, `$form-valid-border-color`, `$form-invalid-color`, `$form-invalid-border-color`
  - Include stylelint disable/enable comments
  - _Requirements: 1.1-1.4, 2.1-2.5, 3.1-3.2, 4.1-4.3, 5.1-5.4, 6.1-6.3, 7.1-7.5, 8.1-8.4, 9.1-9.3_
  - _Leverage: scss/_variables-carbon.scss (modal section pattern)_

- [ ] 2. Create form custom styles in `scss/carbon/_form.scss`
  - File: `scss/carbon/_form.scss` (new file)
  - Create new file with Carbon reference comment
  - Add `.form-control:focus` and `.form-select:focus` styles: `outline: 2px solid $primary`, `outline-offset: -2px`
  - Add `.form-control:hover:not(:disabled):not(:focus)` and `.form-select:hover:not(:disabled):not(:focus)` styles: `border-color: $gray-900`
  - Add `.form-control.is-invalid:focus` and `.form-select.is-invalid:focus` styles: `outline: 2px solid $danger`, `outline-offset: -2px`
  - Add `.form-control.is-valid:focus` and `.form-select.is-valid:focus` styles: `outline: 2px solid $success`, `outline-offset: -2px`
  - Add `.input-group:focus-within .input-group-text` styles: `border-color: $primary`
  - _Requirements: 3.3, 4.1-4.2, 7.2, 7.4_
  - _Leverage: scss/carbon/_modal.scss (custom styles pattern)_

- [ ] 3. Update `scss/carbon/_index.scss` to import form
  - File: `scss/carbon/_index.scss`
  - Add `@import "form";` after modal import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 4. Create demo page `demo/carbon-form.html`
  - File: `demo/carbon-form.html` (new file)
  - Follow structure from `demo/carbon-modal.html`
  - Include: text input (default, small, large sizes)
  - Include: text input states (normal, focus, hover, disabled)
  - Include: select dropdown (all sizes)
  - Include: textarea
  - Include: labels and helper text examples
  - Include: input groups with prepend/append
  - Include: validation states (valid, invalid with feedback messages)
  - Include: password input example
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - _Leverage: demo/carbon-modal.html (demo page structure)_

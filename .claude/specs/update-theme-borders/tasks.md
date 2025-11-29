# Implementation Plan: Update Theme Borders

## Task Overview

This implementation transforms Bootstrap's default rounded corners to Carbon Design System's rectangular (0 border-radius) aesthetic through variable overrides and utility map manipulation. The work is divided into three atomic tasks: variable overrides, utility customization file, and import order update.

## Steering Document Compliance

- **tech.md**: Uses Bootstrap's approved `!default` variable override pattern and utility API
- **structure.md**: Changes isolated to `scss/_variables.scss`, new `scss/_utilities-custom.scss`, and `scss/bootstrap.scss`

## Atomic Task Requirements

Each task meets the criteria for optimal agent execution:
- **File Scope**: 1 file per task
- **Time Boxing**: 10-15 minutes each
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Exact file paths specified
- **Agent-Friendly**: Clear input/output with implementation code provided

## Tasks

- [ ] 1. Add Carbon border-radius variable overrides in `_variables.scss`
  - File: `scss/_variables.scss`
  - Add after the Carbon Button Overrides section (after line 306)
  - Include section header comment with Carbon reference
  - Set all `$border-radius-*` variables to `0`
  - Set `$form-check-input-border-radius` to `0` for square checkboxes
  - Include `stylelint-disable/enable scss/dollar-variable-default` comments
  - Verify radio button border-radius is NOT overridden (stays 50%)
  - _Leverage: `scss/_variables.scss` lines 233-306 (button override pattern)_
  - _Requirements: 1.1-1.6, 2.1-2.5, 8.2, 8.4_

- [ ] 2. Create `_utilities-custom.scss` to remove rounded circle/pill utilities
  - File: `scss/_utilities-custom.scss` (new file)
  - Create helper function `remove-rounded-variants()` using `map-remove()`
  - Use `map-merge()` to update `$utilities` map for all 5 rounded utility groups
  - Remove "circle" and "pill" values from: rounded, rounded-top, rounded-end, rounded-bottom, rounded-start
  - Include section header and end comments
  - _Leverage: Bootstrap's utility API pattern from `scss/_utilities.scss`_
  - _Requirements: 7.1-7.4, 8.3_

- [ ] 3. Update `bootstrap.scss` to import `_utilities-custom.scss`
  - File: `scss/bootstrap.scss`
  - Add import for `utilities-custom` AFTER `utilities` import
  - Add comment indicating Carbon utility customizations
  - _Leverage: `scss/bootstrap.scss` existing import structure_
  - _Requirements: 8.1, 8.3_

- [ ] 4. Build and verify CSS compilation
  - Run `npm run css` to compile CSS
  - Run `npm run css-lint` to verify no SCSS linting errors
  - Verify compiled CSS does NOT contain `.rounded-circle` or `.rounded-pill` classes
  - Verify compilation succeeds without errors
  - _Requirements: 7.1, 7.2, 8.5_

- [ ] 5. Create `demo/carbon-borders.html` visual test page
  - File: `demo/carbon-borders.html`
  - Include examples of all affected components from design document
  - Include form elements: inputs, selects, textareas, checkboxes, radio buttons, switches
  - Include content components: cards, alerts, badges, list groups, accordions
  - Include overlay components: modal trigger, tooltip, popover, toast
  - Include navigation: tabs, pills, pagination, dropdowns
  - Include miscellaneous: progress bars, thumbnails
  - Verify radio buttons display as circles and form switches as pills
  - _Leverage: `demo/carbon-buttons.html` structure and styling_
  - _Requirements: 2.5, 2.6, 3.1-3.5, 4.1-4.5, 5.1-5.4, 6.1-6.3_

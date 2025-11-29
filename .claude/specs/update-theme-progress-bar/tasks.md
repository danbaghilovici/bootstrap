# Implementation Plan

## Task Overview

Implementation of Carbon Design System styling for Bootstrap's progress bar component through variable overrides and custom styles for status variants. This requires variable additions to `_variables-carbon.scss`, a new custom styles file, and a demo page for visual verification.

## Steering Document Compliance

- **tech.md**: Variable-only customization as primary approach, custom styles only for status variants
- **structure.md**: Changes in `scss/_variables-carbon.scss` (primary) and `scss/carbon/` (secondary)

## Atomic Task Requirements

Each task meets these criteria:
- **File Scope**: 1-2 files maximum
- **Time Boxing**: 10-20 minutes each
- **Single Purpose**: One testable outcome
- **Specific Files**: Exact paths provided
- **Agent-Friendly**: Clear input/output

## Tasks

- [ ] 1. Add progress bar variable overrides to _variables-carbon.scss
  - **File**: `scss/_variables-carbon.scss`
  - Add new section after the popover overrides section (after line 642)
  - Add section header comment block for Carbon Progress Bar Overrides
  - Add track variables: `$progress-height`, `$progress-bg`, `$progress-border-radius`, `$progress-box-shadow`
  - Add bar variables: `$progress-bar-color`, `$progress-bar-bg`, `$progress-bar-transition`
  - Add font variable: `$progress-font-size`
  - Include Carbon reference comments for each value
  - **Purpose**: Define all Carbon progress bar styling via Bootstrap variable overrides
  - _Leverage: Existing variable patterns in scss/_variables-carbon.scss (popover section lines 598-642)_
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 2.1, 2.3, 2.4, 5.1, 5.2, 5.3_

- [ ] 2. Create progress bar custom styles file
  - **File**: `scss/carbon/_progress.scss`
  - Create new file with Carbon Progress Bar Customizations header
  - Add small variant class `.progress-sm` with `--bs-progress-height: .25rem`
  - Add success state classes: `.progress-success .progress-bar` and `.progress-bar-success`
  - Add error state classes: `.progress-error .progress-bar` and `.progress-bar-error`
  - Use CSS custom property overrides (`--#{$prefix}progress-bar-bg`)
  - **Purpose**: Add size variant and status states not achievable via variable overrides
  - _Leverage: Existing custom styles pattern from scss/carbon/_popover.scss (if exists) or scss/carbon/_pagination.scss_
  - _Requirements: 3.2, 4.1, 4.2, 4.3_

- [ ] 3. Add progress import to carbon index
  - **File**: `scss/carbon/_index.scss`
  - Add `@import "progress";` after the existing imports
  - Maintain alphabetical or logical ordering with other imports
  - **Purpose**: Include progress custom styles in the build
  - _Leverage: Existing import pattern in scss/carbon/_index.scss_
  - _Requirements: 5.1_

- [ ] 4. Create progress bar demo HTML file
  - **File**: `demo/carbon-progress-bar.html`
  - Create HTML file with Bootstrap CSS link (`../dist/css/bootstrap.css`)
  - Add demo sections for:
    - Default progress bar (0%, 25%, 50%, 75%, 100%)
    - Small variant progress bar (`.progress-sm`)
    - Success status progress bar
    - Error status progress bar
    - Progress bar with label text inside
    - Stacked progress bars
  - Include Carbon design specs reference table
  - Add HTML structure reference section
  - **Purpose**: Provide visual testing page for Carbon progress bar styling
  - _Leverage: Existing demo file pattern from demo/carbon-popover.html_
  - _Requirements: 1.1, 1.2, 1.3, 2.1, 3.1, 3.2, 4.1, 4.2_

- [ ] 5. Build and verify progress bar styling
  - **Files**: `dist/css/bootstrap.css` (output verification)
  - Run `npm run css-lint` to verify no SCSS errors
  - Run `npm run build-theme` to compile CSS
  - Verify compiled CSS contains expected `--bs-progress-*` custom properties
  - Check values match Carbon specifications:
    - `--bs-progress-height: 0.5rem`
    - `--bs-progress-bg: #f4f4f4`
    - `--bs-progress-border-radius: 0`
    - `--bs-progress-box-shadow: none`
    - `--bs-progress-bar-bg: #0f62fe`
  - Verify custom status classes are present in compiled CSS
  - **Purpose**: Validate that variable overrides and custom styles compile correctly
  - _Leverage: Build scripts from package.json_
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 2.1, 3.2, 4.1, 4.2, 5.1, 5.2_

## Task Dependencies

```
Task 1 (Variables) ─┬─→ Task 3 (Index) ─→ Task 5 (Build & Verify)
Task 2 (Custom)    ─┘
Task 4 (Demo)      ─────────────────────→ Task 5 (Build & Verify)
```

- Tasks 1, 2, and 4 can run in parallel
- Task 3 depends on Task 2 (file must exist before importing)
- Task 5 depends on Tasks 1, 2, and 3 completion

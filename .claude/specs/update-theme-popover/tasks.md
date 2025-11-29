# Implementation Plan

## Task Overview

Implementation of Carbon Design System styling for Bootstrap's popover component through variable overrides. This is a straightforward customization requiring variable additions to `_variables-carbon.scss` and a demo file for visual verification.

## Steering Document Compliance

- **tech.md**: Variable-only customization, no Bootstrap source modifications
- **structure.md**: Changes in `scss/_variables-carbon.scss` (primary customization point)

## Atomic Task Requirements

Each task meets these criteria:
- **File Scope**: 1-2 files maximum
- **Time Boxing**: 10-20 minutes each
- **Single Purpose**: One testable outcome
- **Specific Files**: Exact paths provided
- **Agent-Friendly**: Clear input/output

## Tasks

- [ ] 1. Add popover variable overrides to _variables-carbon.scss
  - **File**: `scss/_variables-carbon.scss`
  - Add new section after line 596 (after pagination-nav variables)
  - Add section header comment block for Carbon Popover Overrides
  - Add container variables: `$popover-font-size`, `$popover-bg`, `$popover-border-width`, `$popover-border-color`, `$popover-border-radius`, `$popover-box-shadow`
  - Add header variables: `$popover-header-font-size`, `$popover-header-bg`, `$popover-header-color`, `$popover-header-padding-y`, `$popover-header-padding-x`
  - Add body variables: `$popover-body-color`, `$popover-body-padding-y`, `$popover-body-padding-x`
  - Add size variable: `$popover-max-width`
  - Add arrow variables: `$popover-arrow-width`, `$popover-arrow-height`
  - Include Carbon reference comments for each value
  - **Purpose**: Define all Carbon popover styling via Bootstrap variable overrides
  - _Leverage: Existing variable patterns in scss/_variables-carbon.scss (pagination section lines 480-596)_
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 2.1, 2.2, 2.3, 2.4, 2.5, 3.1, 3.2, 4.1, 4.2, 4.3, 5.1, 5.2, 5.3_

- [ ] 2. Create popover demo HTML file
  - **File**: `demo/carbon-popover.html`
  - Create HTML file with Bootstrap CSS link (`../dist/css/bootstrap.css`)
  - Add demo sections for:
    - Basic popover (body only) with all 4 placements (top, bottom, left, right)
    - Popover with header and body
    - Popover with long content (to test max-width constraint)
  - Include Bootstrap JS for popover functionality
  - Add inline styles for demo layout (padding, background)
  - Add HTML structure reference section
  - **Purpose**: Provide visual testing page for Carbon popover styling
  - _Leverage: Existing demo file pattern from demo/carbon-pagination-nav.html_
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 2.5, 3.4_

- [ ] 3. Build and verify popover styling
  - **Files**: `dist/css/bootstrap.css` (output verification)
  - Run `npm run css-lint` to verify no SCSS errors
  - Run `npm run build-theme` to compile CSS
  - Verify compiled CSS contains expected `--bs-popover-*` custom properties
  - Check values match Carbon specifications:
    - `--bs-popover-bg: #fff`
    - `--bs-popover-border-radius: 2px`
    - `--bs-popover-box-shadow: 0 2px 2px rgba(0, 0, 0, 0.2)`
    - `--bs-popover-max-width: 368px`
    - `--bs-popover-arrow-width: 0.75rem`
    - `--bs-popover-arrow-height: 0.375rem`
  - **Purpose**: Validate that variable overrides compile correctly
  - _Leverage: Build scripts from package.json_
  - _Requirements: 1.1, 1.2, 1.3, 2.5, 3.1, 5.1, 5.2_

## Task Dependencies

```
Task 1 (Variables) → Task 3 (Build & Verify)
                  ↘
Task 2 (Demo)     → Task 3 (Build & Verify)
```

Tasks 1 and 2 can be done in parallel. Task 3 depends on Task 1 completion.

# Implementation Plan: Update Theme Colors

## Task Overview

This implementation adds Carbon Design System color values to the Bootstrap theme by overriding Sass variables in `scss/_variables.scss`. All changes follow Bootstrap's variable-only customization approach - no Bootstrap source files are modified directly.

## Steering Document Compliance

- **structure.md**: All changes go in `scss/_variables.scss` as the primary customization point
- **tech.md**: Variable-only approach, Carbon reference comments on each override
- **Naming**: Bootstrap's existing variable names used

## Atomic Task Requirements

**Each task must meet these criteria for optimal agent execution:**
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify
- **Agent-Friendly**: Clear input/output with minimal context switching

## Tasks

### Phase 1: Color Variables

- [x] 1. Add Carbon colors section header comment
  - **File**: `scss/_variables.scss`
  - **Location**: After the Carbon Grid Overrides section (after line ~165, after `// End Carbon Grid Overrides`)
  - **Implementation**:
    - Add multi-line comment block explaining:
      - These are Carbon Design System color overrides
      - Variables must appear BEFORE Bootstrap's defaults
      - Reference to Carbon documentation URL
    - Add stylelint-disable comment for scss/dollar-variable-default
  - **Verification**: Comment is clear and follows existing Carbon section style
  - _Requirements: 7.3_

- [x] 2. Add gray scale variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After the colors section header from Task 1
  - **Implementation**:
    - Add `$white: #ffffff;`
    - Add `$gray-100: #f4f4f4;` with comment `// Carbon: Gray 10`
    - Add `$gray-200: #e0e0e0;` with comment `// Carbon: Gray 20`
    - Add `$gray-300: #c6c6c6;` with comment `// Carbon: Gray 30`
    - Add `$gray-400: #a8a8a8;` with comment `// Carbon: Gray 40`
    - Add `$gray-500: #8d8d8d;` with comment `// Carbon: Gray 50`
    - Add `$gray-600: #6f6f6f;` with comment `// Carbon: Gray 60`
    - Add `$gray-700: #525252;` with comment `// Carbon: Gray 70`
    - Add `$gray-800: #393939;` with comment `// Carbon: Gray 80`
    - Add `$gray-900: #161616;` with comment `// Carbon: Gray 100`
    - Add `$black: #000000;`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 170-180
  - _Leverage: scss/_variables.scss lines 170-180 for reference_
  - _Requirements: 3.1-3.9_

- [x] 3. Add base color variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After gray scale variables from Task 2
  - **Implementation**:
    - Add `$blue: #0f62fe;` with comment `// Carbon: Blue 60 (interactive-01)`
    - Add `$red: #da1e28;` with comment `// Carbon: Red 60 (danger)`
    - Add `$green: #24a148;` with comment `// Carbon: Green 50 (success)`
    - Add `$yellow: #f1c21b;` with comment `// Carbon: Yellow 30 (warning)`
    - Add `$cyan: #1192e8;` with comment `// Carbon: Cyan 50`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 200-209
  - _Leverage: scss/_variables.scss lines 200-209 for reference_
  - _Requirements: 6.1-6.5_

- [x] 4. Add theme color variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After base color variables from Task 3
  - **Implementation**:
    - Add `$primary: #0f62fe;` with comment `// Carbon: Blue 60 (interactive-01)`
    - Add `$secondary: #393939;` with comment `// Carbon: Gray 80 (interactive-02)`
    - Add `$success: #24a148;` with comment `// Carbon: Green 50 (support-02)`
    - Add `$info: #0043ce;` with comment `// Carbon: Blue 70 (support-04)`
    - Add `$warning: #f1c21b;` with comment `// Carbon: Yellow 30 (support-03)`
    - Add `$danger: #da1e28;` with comment `// Carbon: Red 60 (support-01)`
    - Add `$light: #f4f4f4;` with comment `// Carbon: Gray 10`
    - Add `$dark: #161616;` with comment `// Carbon: Gray 100`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 462-469
  - _Leverage: scss/_variables.scss lines 462-469 for reference_
  - _Requirements: 1.1-1.4, 2.1-2.4_

- [x] 5. Add body color variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After theme color variables from Task 4
  - **Implementation**:
    - Add `$body-color: #161616;` with comment `// Carbon: text-01 (Gray 100)`
    - Add `$body-bg: #ffffff;` with comment `// Carbon: ui-background`
    - Add `$body-secondary-color: #525252;` with comment `// Carbon: text-02 (Gray 70)`
    - Add `$body-tertiary-color: #8d8d8d;` with comment `// Carbon: text-03 (Gray 50)`
    - Add `$body-emphasis-color: #000000;` with comment `// Carbon: text emphasis`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 599-600
  - _Leverage: scss/_variables.scss lines 599-600 for reference_
  - _Requirements: 4.1-4.3_

- [x] 6. Add link color variable overrides and close section
  - **File**: `scss/_variables.scss`
  - **Location**: After body color variables from Task 5
  - **Implementation**:
    - Add `$link-color: #0f62fe;` with comment `// Carbon: link-01 (Blue 60)`
    - Add `$link-hover-color: #0043ce;` with comment `// Carbon: Blue 70`
    - Add stylelint-enable comment
    - Add closing comment: `// End Carbon Color Overrides`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 614+
  - _Leverage: scss/_variables.scss lines 614+ for reference_
  - _Requirements: 4.4, 1.4_

### Phase 2: Build and Verification

- [x] 7. Build CSS and verify compilation succeeds
  - **Command**: `npm run css`
  - **Verification**:
    - Build completes without errors
    - No Sass errors about undefined variables
    - Check `dist/css/bootstrap.css` contains new color values
  - **Rollback**: If build fails, review variable syntax
  - _Requirements: 7.1, 7.2_

- [x] 8. Run CSS linter to verify code quality
  - **Command**: `npm run css-lint`
  - **Verification**:
    - No linting errors related to new variables
    - Stylelint passes with Bootstrap config
  - **Fix**: Address any linting issues in variable formatting
  - _Requirements: 7.3_

- [x] 9. Build theme and copy to output directory
  - **Command**: `npm run build-theme`
  - **Verification**:
    - Build completes successfully
    - `dist/css/bootstrap.min.css` is updated
    - File is copied to `../../themes/bs-carbon/static/css/styles.min.css`
  - _Requirements: 7.1_

### Phase 3: Validation

- [x] 10. Verify theme colors in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - CSS contains `--bs-primary: #0f62fe`
    - CSS contains `--bs-secondary: #393939`
    - CSS contains `--bs-success: #24a148`
    - CSS contains `--bs-info: #0043ce`
    - CSS contains `--bs-warning: #f1c21b`
    - CSS contains `--bs-danger: #da1e28`
  - **Rollback**: If colors are wrong, review theme color variables
  - _Requirements: 1.1-1.3, 2.1-2.4_

- [x] 11. Verify body and link colors in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - CSS contains `--bs-body-color: #161616`
    - CSS contains `--bs-body-bg: #ffffff`
    - CSS contains `--bs-link-color: #0f62fe`
    - CSS contains `--bs-link-hover-color: #0043ce`
    - `.text-muted` or secondary text uses #525252
  - **Rollback**: If colors are wrong, review body/link variables
  - _Requirements: 4.1-4.4_

- [x] 12. Verify gray scale in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - CSS contains `--bs-gray-100: #f4f4f4`
    - CSS contains `--bs-gray-500: #8d8d8d`
    - CSS contains `--bs-gray-900: #161616`
    - `.bg-light` uses #f4f4f4
    - `.bg-dark` uses #161616
  - **Rollback**: If grays are wrong, review gray scale variables
  - _Requirements: 3.1, 3.5, 3.9_

## Task Dependencies

```
Task 1 (header) ─► Task 2 (grays) ─► Task 3 (base colors) ─► Task 4 (theme colors)
                                                                      │
                                                                      ▼
                                                          Task 5 (body colors)
                                                                      │
                                                                      ▼
                                                          Task 6 (link colors)
                                                                      │
                                                                      ▼
                                          Task 7 (build) ─► Task 8 (lint) ─► Task 9 (theme)
                                                                                    │
                                                              ┌───────────────┬─────┴─────┐
                                                              ▼               ▼           ▼
                                                          Task 10        Task 11     Task 12
                                                        (theme colors) (body/links)  (grays)
```

## Verification Checklist

After all tasks complete, verify:

- [x] All color variables are in `scss/_variables.scss` after grid overrides
- [x] Each variable has a Carbon reference comment
- [x] `npm run css` builds without errors
- [x] `npm run css-lint` passes
- [x] `npm run build-theme` copies file successfully
- [x] CSS contains `--bs-primary: #0f62fe`
- [x] CSS contains `--bs-danger: #da1e28`
- [x] CSS contains `--bs-body-color: #161616`
- [x] CSS contains `--bs-link-color: #0f62fe`
- [x] `.btn-primary` uses Blue 60 (#0f62fe)
- [x] `.text-muted` uses Gray 70 (#525252)
- [x] `.bg-light` uses Gray 10 (#f4f4f4)
- [x] Links display in Blue 60 (#0f62fe)
- [x] All text colors meet WCAG AA contrast requirements

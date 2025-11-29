# Implementation Plan: Update Theme Grid

## Task Overview

This implementation adds Carbon Design System 2x grid values to the Bootstrap theme by overriding Sass variables in `scss/_variables.scss`. All changes follow Bootstrap's variable-only customization approach - no Bootstrap source files are modified directly.

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

### Phase 1: Grid Variables

- [ ] 1. Add Carbon grid section header comment
  - **File**: `scss/_variables.scss`
  - **Location**: After the Carbon Spacing Overrides section (after line ~115, after `// End Carbon Spacing Overrides`)
  - **Implementation**:
    - Add multi-line comment block explaining:
      - These are Carbon Design System 2x grid overrides
      - Variables must appear BEFORE Bootstrap's defaults
      - Reference to Carbon documentation URL
    - Add stylelint-disable comment for scss/dollar-variable-default
  - **Verification**: Comment is clear and follows existing Carbon section style
  - _Requirements: 5.3_

- [ ] 2. Add grid breakpoints map override
  - **File**: `scss/_variables.scss`
  - **Location**: After the grid section header from Task 1
  - **Implementation**:
    - Add `$grid-breakpoints` Sass map with Carbon values:
      - `xs: 0`
      - `sm: 320px` with comment `// Carbon: sm`
      - `md: 672px` with comment `// Carbon: md`
      - `lg: 1056px` with comment `// Carbon: lg`
      - `xl: 1312px` with comment `// Carbon: xlg`
      - `xxl: 1584px` with comment `// Carbon: max`
  - **Verification**: Map appears before Bootstrap's default at line 595
  - _Leverage: scss/_variables.scss lines 595-602 for reference_
  - _Requirements: 1.1-1.6_

- [ ] 3. Add container max-widths map override
  - **File**: `scss/_variables.scss`
  - **Location**: After grid breakpoints from Task 2
  - **Implementation**:
    - Add `$container-max-widths` Sass map:
      - `sm: 288px` with comment `// Carbon: sm - gutter`
      - `md: 640px` with comment `// Carbon: md - gutter`
      - `lg: 1024px` with comment `// Carbon: lg - gutter`
      - `xl: 1280px` with comment `// Carbon: xlg - gutter`
      - `xxl: 1584px` with comment `// Carbon: max-width`
  - **Verification**: Map appears before Bootstrap's default at line 614
  - _Leverage: scss/_variables.scss lines 614-620 for reference_
  - _Requirements: 2.1-2.5_

- [ ] 4. Add grid configuration variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After container max-widths from Task 3
  - **Implementation**:
    - Add `$grid-columns: 16;` with comment `// Carbon: 16-column grid`
    - Add `$grid-gutter-width: 2rem;` with comment `// Carbon: wide mode (32px)`
    - Add `$grid-row-columns: 8;` with comment `// Half of grid columns`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 630-632
  - _Leverage: scss/_variables.scss lines 630-632 for reference_
  - _Requirements: 3.1, 4.1_

- [ ] 5. Add container padding variable override
  - **File**: `scss/_variables.scss`
  - **Location**: After grid configuration from Task 4
  - **Implementation**:
    - Add `$container-padding-x: $grid-gutter-width;` with comment `// Carbon: matches gutter`
    - Add stylelint-enable comment
    - Add closing comment: `// End Carbon Grid Overrides`
  - **Verification**: Variable appears before Bootstrap's default at line 636
  - _Leverage: scss/_variables.scss line 636 for reference_
  - _Requirements: 4.2_

### Phase 2: Build and Verification

- [ ] 6. Build CSS and verify compilation succeeds
  - **Command**: `npm run css`
  - **Verification**:
    - Build completes without errors
    - No Sass errors about non-ascending breakpoints
    - Check `dist/css/bootstrap.css` contains `.col-16` class (confirms 16 columns)
  - **Rollback**: If build fails, review variable syntax and map structure
  - _Requirements: 3.2, 6.1-6.4_

- [ ] 7. Run CSS linter to verify code quality
  - **Command**: `npm run css-lint`
  - **Verification**:
    - No linting errors related to new variables
    - Stylelint passes with Bootstrap config
  - **Fix**: Address any linting issues in variable formatting
  - _Requirements: 5.1, 5.2_

- [ ] 8. Build theme and copy to output directory
  - **Command**: `npm run build-theme`
  - **Verification**:
    - Build completes successfully
    - `dist/css/bootstrap.min.css` is updated
    - File is copied to `../../themes/bs-carbon/static/css/styles.min.css`
  - _Requirements: 5.1_

### Phase 3: Validation

- [ ] 9. Verify grid breakpoints in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - Media query `@media (min-width: 320px)` exists (sm breakpoint)
    - Media query `@media (min-width: 672px)` exists (md breakpoint)
    - Media query `@media (min-width: 1056px)` exists (lg breakpoint)
    - Media query `@media (min-width: 1312px)` exists (xl breakpoint)
    - Media query `@media (min-width: 1584px)` exists (xxl breakpoint)
  - **Rollback**: If breakpoints are wrong, review $grid-breakpoints map
  - _Requirements: 1.1-1.6_

- [ ] 10. Verify column and container classes in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - `.col-16` class exists with `flex: 0 0 auto; width: 100%`
    - `.col-8` class exists with `width: 50%` (half of 16)
    - `.col-4` class exists with `width: 25%` (quarter of 16)
    - `.offset-15` class exists
    - `.container` has `max-width: 1584px` at xxl breakpoint
    - `.row-cols-8` class exists
  - **Rollback**: If columns are wrong, review $grid-columns value
  - _Requirements: 2.5, 3.1-3.4_

- [ ] 11. Verify gutter width in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - `.row` has `--bs-gutter-x: 2rem` (32px)
    - `.container` has `padding-right: 2rem` and `padding-left: 2rem`
    - Gutter utility `.gx-0` through `.gx-5` exist
  - **Rollback**: If gutter is wrong, review $grid-gutter-width value
  - _Requirements: 4.1, 4.2_

## Task Dependencies

```
Task 1 (header) ─► Task 2 (breakpoints) ─► Task 3 (containers) ─► Task 4 (grid config)
                                                                          │
                                                                          ▼
                                                              Task 5 (container padding)
                                                                          │
                                                                          ▼
                                                  Task 6 (build) ─► Task 7 (lint) ─► Task 8 (theme)
                                                                                          │
                                                                          ┌───────────────┼───────────────┐
                                                                          ▼               ▼               ▼
                                                                    Task 9          Task 10         Task 11
                                                                  (breakpoints)    (columns)       (gutters)
```

## Verification Checklist

After all tasks complete, verify:

- [ ] All grid variables are in `scss/_variables.scss` after spacing overrides
- [ ] Each variable has a Carbon reference comment
- [ ] `npm run css` builds without errors
- [ ] `npm run css-lint` passes
- [ ] `npm run build-theme` copies file successfully
- [ ] Media queries use Carbon breakpoints (320, 672, 1056, 1312, 1584px)
- [ ] CSS contains `.col-1` through `.col-16` classes
- [ ] CSS contains `.offset-0` through `.offset-15` classes
- [ ] CSS contains `.row-cols-1` through `.row-cols-8` classes
- [ ] Container max-width is 1584px at xxl
- [ ] Grid gutter is 2rem (32px)
- [ ] Container padding matches gutter (2rem)

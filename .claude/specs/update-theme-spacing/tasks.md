# Implementation Plan: Update Theme Spacing

## Task Overview

This implementation adds Carbon Design System spacing to the Bootstrap theme by overriding Sass variables in `scss/_variables.scss`. All changes follow Bootstrap's variable-only customization approach - no Bootstrap source files are modified directly.

## Steering Document Compliance

- **structure.md**: All changes go in `scss/_variables.scss` as the primary customization point
- **tech.md**: Variable-only approach, Carbon reference comments on each override
- **Naming**: Bootstrap's `$component-state-property-size` convention followed

## Atomic Task Requirements

**Each task must meet these criteria for optimal agent execution:**
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify
- **Agent-Friendly**: Clear input/output with minimal context switching

## Tasks

### Phase 1: Spacing Variables

- [ ] 1. Add Carbon spacing section header comment
  - **File**: `scss/_variables.scss`
  - **Location**: After the Carbon Typography Overrides section (after line ~70, after `// End Carbon Typography Overrides`)
  - **Implementation**:
    - Add multi-line comment block explaining:
      - These are Carbon Design System spacing overrides
      - Variables must appear BEFORE Bootstrap's defaults
      - Reference to Carbon documentation URL
    - Add stylelint-disable comment for scss/dollar-variable-default
  - **Verification**: Comment is clear and follows Bootstrap's comment style
  - _Requirements: 5.3_

- [ ] 2. Add base spacer variable override
  - **File**: `scss/_variables.scss`
  - **Location**: After the spacing section header from Task 1
  - **Implementation**:
    - Add `$spacer: 1rem;` with comment `// Carbon: 16px (spacing-05)`
  - **Verification**: Variable appears before Bootstrap's default at line 482
  - _Leverage: scss/_variables.scss line 482 for reference_
  - _Requirements: 1.1, 1.2_

- [ ] 3. Add extended spacers map override
  - **File**: `scss/_variables.scss`
  - **Location**: After base spacer from Task 2
  - **Implementation**:
    - Add `$spacers` Sass map with Carbon-aligned values:
      - `0: 0` (no spacing)
      - `1: $spacer * .25` with comment `// Carbon: spacing-02 (4px)`
      - `2: $spacer * .5` with comment `// Carbon: spacing-03 (8px)`
      - `3: $spacer` with comment `// Carbon: spacing-05 (16px)`
      - `4: $spacer * 1.5` with comment `// Carbon: spacing-06 (24px)`
      - `5: $spacer * 3` with comment `// Carbon: spacing-09 (48px)`
      - `6: $spacer * .125` with comment `// Carbon: spacing-01 (2px)`
      - `7: $spacer * .75` with comment `// Carbon: spacing-04 (12px)`
      - `8: $spacer * 2` with comment `// Carbon: spacing-07 (32px)`
      - `9: $spacer * 2.5` with comment `// Carbon: spacing-08 (40px)`
    - Add stylelint-enable comment after the map
    - Add closing comment: `// End Carbon Spacing Overrides`
  - **Verification**: Map appears before Bootstrap's default at lines 483-490
  - _Leverage: scss/_variables.scss lines 483-490 for reference_
  - _Requirements: 2.1-2.7, 3.1-3.4_

### Phase 2: Build and Verification

- [ ] 4. Build CSS and verify compilation succeeds
  - **Command**: `npm run css`
  - **Verification**:
    - Build completes without errors
    - Check `dist/css/bootstrap.css` contains `.m-6`, `.m-7`, `.m-8`, `.m-9` classes
    - Check `.p-6`, `.p-7`, `.p-8`, `.p-9` padding utilities exist
    - Check `.gap-6`, `.gap-7`, `.gap-8`, `.gap-9` gap utilities exist
  - **Rollback**: If build fails, review variable syntax and placement
  - _Requirements: 4.1, 4.2, 4.3_

- [ ] 5. Run CSS linter to verify code quality
  - **Command**: `npm run css-lint`
  - **Verification**:
    - No linting errors related to new variables
    - Stylelint passes with Bootstrap config
  - **Fix**: Address any linting issues in variable formatting
  - _Requirements: 5.1, 5.2_

- [ ] 6. Build theme and copy to output directory
  - **Command**: `npm run build-theme`
  - **Verification**:
    - Build completes successfully
    - `dist/css/bootstrap.min.css` is updated
    - File is copied to `../../themes/bs-carbon/static/css/styles.min.css`
  - _Requirements: 5.1_

### Phase 3: Validation

- [ ] 7. Verify spacing values in compiled CSS
  - **File**: `dist/css/bootstrap.css`
  - **Verification**:
    - `.m-6` has `margin: 0.125rem` (2px)
    - `.m-7` has `margin: 0.75rem` (12px)
    - `.m-8` has `margin: 2rem` (32px)
    - `.m-9` has `margin: 2.5rem` (40px)
    - Existing `.m-3` still has `margin: 1rem` (16px)
    - Negative margins exist: `.m-n6` through `.m-n9`
  - **Rollback**: If values are incorrect, review spacer map calculations
  - _Requirements: 2.3-2.7, 3.1-3.4, 4.4_

## Task Dependencies

```
Task 1 (header) ─► Task 2 (base spacer) ─► Task 3 (spacers map)
                                                    │
                                                    ▼
                              Task 4 (build) ─► Task 5 (lint)
                                                    │
                                                    ▼
                              Task 6 (theme) ─► Task 7 (validate)
```

## Verification Checklist

After all tasks complete, verify:

- [ ] All spacing variables are in `scss/_variables.scss` after typography overrides
- [ ] Each variable has a Carbon reference comment
- [ ] `npm run css` builds without errors
- [ ] `npm run css-lint` passes
- [ ] `npm run build-theme` copies file successfully
- [ ] CSS contains utility classes `.m-6` through `.m-9`
- [ ] CSS contains utility classes `.p-6` through `.p-9`
- [ ] CSS contains utility classes `.gap-6` through `.gap-9`
- [ ] CSS contains negative margin classes `.m-n6` through `.m-n9`
- [ ] Browser DevTools shows correct values:
  - `.m-6`: margin: 0.125rem (2px)
  - `.m-7`: margin: 0.75rem (12px)
  - `.m-8`: margin: 2rem (32px)
  - `.m-9`: margin: 2.5rem (40px)

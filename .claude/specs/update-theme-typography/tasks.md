# Implementation Plan: Update Theme Typography

## Task Overview

This implementation adds Carbon Design System typography to the Bootstrap theme by overriding Sass variables in `scss/_variables.scss`. All changes follow Bootstrap's variable-only customization approach - no Bootstrap source files are modified directly.

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

### Phase 1: Font Family Variables

- [ ] 1. Add IBM Plex Sans font family variable override
  - **File**: `scss/_variables.scss`
  - **Location**: Add at the TOP of the file, before line 1 (before existing color variables)
  - **Implementation**:
    - Add `$font-family-sans-serif` variable with IBM Plex Sans as primary font
    - Include full fallback stack: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", "Noto Sans", "Liberation Sans", Arial, sans-serif, emoji fonts
    - Add comment: `// Carbon: IBM Plex Sans`
  - **Verification**: Variable appears before Bootstrap's default definition
  - _Leverage: scss/_variables.scss lines 606-607 for reference to existing font variables_
  - _Requirements: 1.1, 1.3_

- [ ] 2. Add IBM Plex Mono font family variable override
  - **File**: `scss/_variables.scss`
  - **Location**: Immediately after the sans-serif variable from Task 1
  - **Implementation**:
    - Add `$font-family-monospace` variable with IBM Plex Mono as primary font
    - Include fallback stack: SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace
    - Add comment: `// Carbon: IBM Plex Mono`
  - **Verification**: Variable appears before Bootstrap's default definition
  - _Leverage: scss/_variables.scss line 607 for reference_
  - _Requirements: 1.2, 1.3_

### Phase 2: Base Typography Variables

- [ ] 3. Add base typography variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After font family variables from Tasks 1-2
  - **Implementation**:
    - Add `$font-size-base: 1rem;` with comment `// Carbon: 16px`
    - Add `$font-weight-base: 400;` with comment `// Carbon: regular`
    - Add `$line-height-base: 1.5;` with comment `// Carbon: body-long-02`
    - Add `$font-size-sm: .875rem;` with comment `// Carbon: 14px (body-short-01)`
    - Add `$font-size-lg: 1.25rem;` with comment `// Carbon: 20px`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 614-617
  - _Leverage: scss/_variables.scss lines 614-631 for reference_
  - _Requirements: 2.1, 2.2, 2.3, 2.4_

### Phase 3: Heading Typography Variables

- [ ] 4. Add heading font size variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After base typography variables from Task 3
  - **Implementation**:
    - Add `$h1-font-size: 2rem;` with comment `// Carbon: productive-heading-05`
    - Add `$h2-font-size: 1.75rem;` with comment `// Carbon: productive-heading-04`
    - Add `$h3-font-size: 1.25rem;` with comment `// Carbon: productive-heading-03`
    - Add `$h4-font-size: 1rem;` with comment `// Carbon: productive-heading-02`
    - Add `$h5-font-size: .875rem;` with comment `// Carbon: productive-heading-01`
    - Add `$h6-font-size: .875rem;` with comment `// Carbon: productive-heading-01`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 633-638
  - _Leverage: scss/_variables.scss lines 633-638 for reference_
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5, 3.6_

- [ ] 5. Add heading style variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After heading font sizes from Task 4
  - **Implementation**:
    - Add `$headings-font-weight: 400;` with comment `// Carbon: h1-h3 use 400 (design decision)`
    - Add `$headings-line-height: 1.3;` with comment `// Carbon: balanced value (design decision)`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 652-658
  - _Leverage: scss/_variables.scss lines 652-658 for reference_
  - _Requirements: 3.7_

### Phase 4: Display Typography Variables

- [ ] 6. Add display font sizes map override
  - **File**: `scss/_variables.scss`
  - **Location**: After heading variables from Task 5
  - **Implementation**:
    - Add `$display-font-sizes` Sass map with values:
      - `1: 3.75rem` (60px - Carbon expressive)
      - `2: 3.25rem` (52px)
      - `3: 2.75rem` (44px)
      - `4: 2.25rem` (36px)
      - `5: 2rem` (32px)
      - `6: 1.75rem` (28px)
    - Add comment: `// Carbon: expressive display sizes`
  - **Verification**: Map appears before Bootstrap's default at lines 662-669
  - _Leverage: scss/_variables.scss lines 662-669 for reference_
  - _Requirements: 4.1_

- [ ] 7. Add display style variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After display font sizes from Task 6
  - **Implementation**:
    - Add `$display-font-weight: 300;` with comment `// Carbon: light weight for display`
    - Add `$display-line-height: 1.2;` with comment `// Carbon: tighter for large text`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 673-674
  - _Leverage: scss/_variables.scss lines 671-674 for reference_
  - _Requirements: 4.2, 4.3_

### Phase 5: Utility Typography Variables

- [ ] 8. Add utility typography variable overrides
  - **File**: `scss/_variables.scss`
  - **Location**: After display variables from Task 7
  - **Implementation**:
    - Add `$lead-font-size: 1.25rem;` with comment `// Carbon: emphasis text`
    - Add `$lead-font-weight: 300;` with comment `// Carbon: light emphasis`
    - Add `$small-font-size: .875em;` with comment `// Carbon: 14px equivalent`
    - Add `$blockquote-font-size: 1.25rem;` with comment `// Carbon: quote styling`
    - Add `$code-font-size: .875em;` with comment `// Carbon: code-02`
  - **Verification**: Variables appear before Bootstrap's defaults at lines 678-689
  - _Leverage: scss/_variables.scss lines 678-692 for reference_
  - _Requirements: 5.1, 5.2, 5.3, 5.4_

### Phase 6: RFS (Responsive Font Sizing) Tuning

- [ ] 9. Add RFS variable overrides for Carbon-like responsive behavior
  - **File**: `scss/_variables.scss`
  - **Location**: After utility typography variables from Task 8
  - **Implementation**:
    - Add `$rfs-base-value: 1rem;` with comment `// Carbon: minimum body size`
    - Add `$rfs-breakpoint: 1056px;` with comment `// Carbon: 66rem breakpoint`
    - Add `$rfs-factor: 8;` with comment `// Carbon: more aggressive than default (10)`
  - **Verification**: Variables appear before Bootstrap processes them (before line 381 where `$enable-rfs` is set)
  - _Leverage: scss/vendor/_rfs.scss lines 12-31 for reference_
  - _Requirements: Design Decision 3_

### Phase 7: Build and Verification

- [ ] 10. Build CSS and verify compilation succeeds
  - **Command**: `npm run css`
  - **Verification**:
    - Build completes without errors
    - Check `dist/css/bootstrap.css` contains IBM Plex font references
    - Check CSS custom properties `--bs-font-sans-serif` and `--bs-font-monospace` in output
  - **Rollback**: If build fails, review variable syntax and placement
  - _Requirements: 6.1, 6.2_

- [ ] 11. Run CSS linter to verify code quality
  - **Command**: `npm run css-lint`
  - **Verification**:
    - No linting errors related to new variables
    - Stylelint passes with Bootstrap config
  - **Fix**: Address any linting issues in variable formatting
  - _Requirements: 6.3_

- [ ] 12. Build theme and copy to output directory
  - **Command**: `npm run build-theme`
  - **Verification**:
    - Build completes successfully
    - `dist/css/bootstrap.min.css` is updated
    - File is copied to `../../themes/bs-carbon/static/css/styles.min.css`
  - _Requirements: 6.1_

### Phase 8: Documentation

- [ ] 13. Add section header comment for Carbon typography overrides
  - **File**: `scss/_variables.scss`
  - **Location**: At the very top of the file, before Task 1's font family variable
  - **Implementation**:
    - Add multi-line comment block explaining:
      - These are Carbon Design System typography overrides
      - Variables must appear BEFORE Bootstrap's defaults
      - Reference to Carbon documentation URL
  - **Verification**: Comment is clear and follows Bootstrap's comment style
  - _Requirements: 6.3, 6.4_

## Task Dependencies

```
Task 1 (sans-serif) ─┐
                     ├─► Task 3 (base) ─► Task 4 (heading sizes) ─► Task 5 (heading styles)
Task 2 (monospace) ──┘                                                      │
                                                                            ▼
                                          Task 6 (display sizes) ─► Task 7 (display styles)
                                                                            │
                                                                            ▼
                                                           Task 8 (utility) ─► Task 9 (RFS)
                                                                                    │
                                                                                    ▼
                                                              Task 10 (build) ─► Task 11 (lint)
                                                                                    │
                                                                                    ▼
                                                              Task 12 (theme) ─► Task 13 (docs)
```

## Verification Checklist

After all tasks complete, verify:

- [ ] All typography variables are at the TOP of `scss/_variables.scss`
- [ ] Each variable has a Carbon reference comment
- [ ] `npm run css` builds without errors
- [ ] `npm run css-lint` passes
- [ ] `npm run build-theme` copies file successfully
- [ ] Browser DevTools shows `--bs-font-sans-serif` contains "IBM Plex Sans"
- [ ] Browser DevTools shows `--bs-font-monospace` contains "IBM Plex Mono"
- [ ] Headings render at correct sizes (h1: 32px, h2: 28px, h3: 20px, etc.)

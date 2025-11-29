# Requirements: Update Theme Pagination

## Overview

Update Bootstrap's pagination component to match the Carbon Design System styling while maintaining full Bootstrap functionality and accessibility.

## Background

Bootstrap's default pagination uses rounded corners, link-style colors, and Bootstrap's standard spacing. Carbon Design System pagination uses rectangular elements, layer-based backgrounds, and consistent 40px height for default size.

## Functional Requirements

### FR-1: Typography
- **FR-1.1**: Pagination items must use body-compact-01 token (14px / 0.875rem font size)
- **FR-1.2**: Font weight must be 400 (regular)
- **FR-1.3**: Line height must follow Carbon body-compact specifications

### FR-2: Sizing
- **FR-2.1**: Default pagination height must be 40px (matching Carbon's default)
- **FR-2.2**: Small pagination (pagination-sm) must be 32px height
- **FR-2.3**: Large pagination (pagination-lg) must be 48px height
- **FR-2.4**: Horizontal padding must use spacing-05 (16px / 1rem)

### FR-3: Colors
- **FR-3.1**: Default background must use body-bg (white)
- **FR-3.2**: Border color must use border-subtle (Gray 20 / #e0e0e0)
- **FR-3.3**: Text color must use text-primary (Gray 100 / #161616)
- **FR-3.4**: Active state background must use primary (Blue 60 / #0f62fe)
- **FR-3.5**: Active state text must be white

### FR-4: Interactive States
- **FR-4.1**: Hover state must show layer-hover background (Gray 10 / #f4f4f4)
- **FR-4.2**: Focus state must use 2px Blue 60 outline (matching Carbon focus pattern)
- **FR-4.3**: Disabled state text must use text-disabled (Gray 50 / #8d8d8d)
- **FR-4.4**: Disabled state must show not-allowed cursor

### FR-5: Shape
- **FR-5.1**: Pagination items must have 0 border-radius (rectangular)
- **FR-5.2**: All size variants must maintain 0 border-radius

## Non-Functional Requirements

### NFR-1: Maintainability
- **NFR-1.1**: All customizations must be done via variable overrides in `_variables-carbon.scss`
- **NFR-1.2**: Custom styles not achievable via variables must go in `scss/carbon/_pagination.scss`
- **NFR-1.3**: Bootstrap's `_pagination.scss` must remain unmodified

### NFR-2: Compatibility
- **NFR-2.1**: All existing Bootstrap pagination classes must continue to work
- **NFR-2.2**: Pagination sizing variants (sm, lg) must remain functional
- **NFR-2.3**: RTL support must be maintained

### NFR-3: Accessibility
- **NFR-3.1**: Focus states must be clearly visible (WCAG 2.1 AA compliance)
- **NFR-3.2**: Color contrast ratios must meet WCAG requirements
- **NFR-3.3**: Disabled states must be visually distinct

## Out of Scope

- Carbon's select-based pagination variant (Bootstrap doesn't have this pattern)
- Items-per-page selector functionality
- Page number input field

## Acceptance Criteria

1. Pagination matches Carbon visual specifications for colors, spacing, and typography
2. All three size variants (default, sm, lg) are properly styled
3. All interactive states (hover, focus, active, disabled) work correctly
4. Build completes without errors (`npm run css`)
5. Lint passes without new errors (`npm run css-lint`)
6. Demo page shows all pagination variants and states

## References

- Carbon Pagination: https://carbondesignsystem.com/components/pagination/style/
- Bootstrap Pagination: https://getbootstrap.com/docs/5.3/components/pagination/
- Carbon Tokens: https://carbondesignsystem.com/elements/color/tokens/

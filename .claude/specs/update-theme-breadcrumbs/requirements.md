# Requirements: Update Theme Breadcrumbs

## Overview

Update the Bootstrap breadcrumb component to match Carbon Design System's breadcrumb styling. This includes typography, link colors, separator styling, and focus states while maintaining Bootstrap's structure and functionality.

## Reference

- Carbon Breadcrumb Style: https://carbondesignsystem.com/components/breadcrumb/style/
- Carbon Breadcrumb Source: https://github.com/carbon-design-system/carbon/blob/main/packages/styles/scss/components/breadcrumb/_breadcrumb.scss

## Functional Requirements

### 1. Typography

- 1.1 Breadcrumb text uses `body-compact-01` typography token (14px, 400 weight, 18px line-height)
- 1.2 Font family inherits from body (IBM Plex Sans in Carbon theme)

### 2. Link Styling

- 2.1 Default link color uses `$link-primary` (#0f62fe / Blue 60)
- 2.2 Hover state uses `$link-primary-hover` (#0043ce / Blue 70) with underline
- 2.3 Links use `white-space: nowrap` to prevent wrapping

### 3. Active/Current Page

- 3.1 Current page text uses `$text-primary` (#161616)
- 3.2 Current page has no hover effect
- 3.3 Current page cursor is `auto` (not pointer)

### 4. Separator

- 4.1 Separator character is forward slash "/"
- 4.2 Separator color uses `$text-primary` (#161616)
- 4.3 Separator has appropriate spacing from adjacent items

### 5. Focus States

- 5.1 Link focus outline: `1px solid $focus` (#0f62fe)
- 5.2 Focus outline-offset: `0`
- 5.3 No box-shadow on focus

### 6. Layout

- 6.1 Display as inline/flex with wrap capability
- 6.2 Items aligned center vertically
- 6.3 Appropriate spacing between items (Carbon: `$spacing-03` / 8px)

## Non-Functional Requirements

### 7. Implementation Approach

- 7.1 Use Bootstrap variable overrides in `_variables.scss` where possible
- 7.2 Custom styles in `scss/carbon/_breadcrumb.scss` for properties not achievable via variables
- 7.3 Follow existing pattern from `_accordion.scss` and `_alert.scss`
- 7.4 No modifications to Bootstrap source files

### 8. Accessibility

- 8.1 Focus states meet WCAG 2.1 visibility requirements (3:1 contrast)
- 8.2 Color contrast for text meets WCAG AA (4.5:1)
- 8.3 Maintain semantic HTML structure (nav, ol/ul, li)

## Out of Scope

- Overflow menu functionality (not supported in Bootstrap)
- Small variant sizing
- RTL support beyond Bootstrap's default

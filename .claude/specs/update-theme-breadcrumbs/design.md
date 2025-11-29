# Design Document: Update Theme Breadcrumbs

## Overview

This design defines how to update Bootstrap's breadcrumb component to match Carbon Design System's styling. The implementation uses Bootstrap's variable override system for most customizations, with a dedicated `scss/carbon/_breadcrumb.scss` file for styles that cannot be achieved through variables alone.

## Steering Document Alignment

### Technical Standards (tech.md)
- **Variable-only customization**: Breadcrumb styling will primarily use Bootstrap's `$breadcrumb-*` variables
- **No Bootstrap source modifications**: All changes via overrides and the carbon/ directory
- **Carbon color tokens**: Use existing `$primary`, `$body-color` variables

### Project Structure (structure.md)
- Custom styles placed in `scss/carbon/_breadcrumb.scss`
- Variables overridden in `scss/_variables.scss` in the breadcrumb section
- Index updated in `scss/carbon/_index.scss`

## Code Reuse Analysis

### Existing Components to Leverage
- **Color variables**: `$primary` (#0f62fe), `$body-color` (#161616)
- **Link colors**: `$link-color`, `$link-hover-color`
- **Spacing variables**: `$spacer` (16px base)
- **Focus color**: `#0f62fe` (Blue 60) used consistently across components

### Integration Points
- **Bootstrap _breadcrumb.scss**: Uses CSS custom properties set via `$breadcrumb-*` variables
- **Carbon custom directory**: Follow pattern established by `_accordion.scss` and `_alert.scss`

## Architecture

```mermaid
graph TD
    A[_variables.scss] -->|Breadcrumb variable overrides| B[Bootstrap _breadcrumb.scss]
    B -->|Generates .breadcrumb classes| C[Compiled CSS]
    D[carbon/_breadcrumb.scss] -->|Custom link/focus styles| C
    E[carbon/_index.scss] -->|@import breadcrumb| D
```

## Design Specifications

### Visual Structure

```
Home / Products / Category / Current Page
 ↑        ↑          ↑           ↑
Link   Separator   Link     Active (no link)
Blue 60  Gray 100  Blue 60    Gray 100
```

### Color Mapping

| Element | Color | Carbon Token |
|---------|-------|--------------|
| Link (default) | #0f62fe | Blue 60 / $link-primary |
| Link (hover) | #0043ce | Blue 70 / $link-primary-hover |
| Separator | #161616 | Gray 100 / $text-primary |
| Active item | #161616 | Gray 100 / $text-primary |
| Focus outline | #0f62fe | Blue 60 / $focus |

### Spacing Specifications

| Property | Value | Carbon Token |
|----------|-------|--------------|
| Item padding | 0.5rem (8px) | spacing-03 |
| Font size | 0.875rem (14px) | body-compact-01 |
| Line height | 1.125rem (18px) | body-compact-01 |

## Components and Interfaces

### Component 1: Breadcrumb Variable Overrides

**Purpose:** Override Bootstrap's default breadcrumb variables to match Carbon styling
**Location:** `scss/_variables.scss` (breadcrumb section, around line 2077)
**Approach:** Set variables before Bootstrap's `!default` assignment

```scss
// Carbon Breadcrumb Overrides
$breadcrumb-font-size: 0.875rem;                    // 14px (body-compact-01)
$breadcrumb-item-padding-x: 0.5rem;                 // 8px (spacing-03)
$breadcrumb-divider-color: $body-color;             // #161616
$breadcrumb-active-color: $body-color;              // #161616
$breadcrumb-divider: quote("/");                    // Forward slash (Carbon default)
```

### Component 2: Breadcrumb Custom Styles

**Purpose:** Apply Carbon-specific styling that cannot be achieved via variables
**Location:** `scss/carbon/_breadcrumb.scss`
**Dependencies:** Bootstrap breadcrumb classes, Carbon color variables

Key customizations:
1. Link color to Blue 60
2. Link hover color to Blue 70 with underline
3. Focus state with 1px outline
4. White-space nowrap for links

## Implementation Details

### File 1: Variable Overrides (`scss/_variables.scss`)

Add Carbon breadcrumb overrides before Bootstrap's defaults (around line 2074):

```scss
// ============================================================================
// Carbon Breadcrumb Overrides
// ============================================================================
// Reference: https://carbondesignsystem.com/components/breadcrumb/style

$breadcrumb-font-size: 0.875rem;                    // Carbon: body-compact-01 (14px)
$breadcrumb-item-padding-x: 0.5rem;                 // Carbon: spacing-03 (8px)
$breadcrumb-divider-color: $body-color;             // Carbon: $text-primary (#161616)
$breadcrumb-active-color: $body-color;              // Carbon: $text-primary (#161616)
$breadcrumb-divider: quote("/");                    // Carbon: forward slash
```

### File 2: Custom Styles (`scss/carbon/_breadcrumb.scss`)

```scss
// Carbon Breadcrumb Customizations
// Link colors and focus states for navigation breadcrumbs
// Reference: https://carbondesignsystem.com/components/breadcrumb/style

// Link styling
.breadcrumb-item {
  a {
    color: $primary;               // Blue 60
    text-decoration: none;
    white-space: nowrap;

    &:hover {
      color: $info;                // Blue 70
      text-decoration: underline;
    }

    &:focus {
      outline: 1px solid $primary; // Blue 60
      outline-offset: 0;
    }
  }

  // Active/current page styling
  &.active {
    cursor: auto;
  }
}
```

### File 3: Index Update (`scss/carbon/_index.scss`)

```scss
@import "type";
@import "accordion";
@import "alert";
@import "breadcrumb";
```

## Error Handling

### Error Scenarios

1. **Color contrast issues**
   - **Handling:** Use `$body-color` (#161616) for separator and active text
   - **User Impact:** Ensures WCAG AA compliance for readability

2. **Variable order issues**
   - **Handling:** Place Carbon overrides BEFORE Bootstrap's `!default` assignments
   - **User Impact:** None if implemented correctly

## Testing Strategy

### Visual Testing
- Verify link colors match Blue 60 (#0f62fe)
- Confirm hover state changes to Blue 70 with underline
- Check separator uses forward slash in correct color
- Validate active item appears in gray text without link styling

### Accessibility Testing
- Test color contrast ratios meet WCAG AA (4.5:1)
- Verify focus indicators are visible (3:1 contrast)
- Test keyboard navigation through breadcrumb links

### Browser Testing
- Test in Chrome, Firefox, Safari
- Verify CSS custom properties work correctly

## File Summary

| File | Action | Purpose |
|------|--------|---------|
| `scss/_variables.scss` | Modify | Add breadcrumb variable overrides |
| `scss/carbon/_breadcrumb.scss` | Create | Custom link colors and focus styles |
| `scss/carbon/_index.scss` | Modify | Add `@import "breadcrumb"` |

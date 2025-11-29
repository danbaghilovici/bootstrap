# Design Document: Update Theme Alert

## Overview

This design defines how to update Bootstrap's alert component to match Carbon Design System's inline notification styling. The implementation uses Bootstrap's variable override system for most customizations, with a dedicated `scss/carbon/_alert.scss` file for styles that cannot be achieved through variables alone.

## Steering Document Alignment

### Technical Standards (tech.md)
- **Variable-only customization**: Alert styling will primarily use Bootstrap's `$alert-*` variables
- **No Bootstrap source modifications**: All changes via overrides and the carbon/ directory
- **Carbon color tokens**: Use existing `$danger`, `$success`, `$warning`, `$info` variables

### Project Structure (structure.md)
- Custom styles placed in `scss/carbon/_alert.scss`
- Variables overridden in `scss/_variables.scss` in the alert section
- Index updated in `scss/carbon/_index.scss`

## Code Reuse Analysis

### Existing Components to Leverage
- **Color variables**: `$danger` (#da1e28), `$success` (#24a148), `$warning` (#f1c21b), `$info` (#0043ce), `$primary` (#0f62fe)
- **Spacing variables**: `$spacer` (16px base)
- **Bootstrap subtle color system**: `*-bg-subtle`, `*-text-emphasis`, `*-border-subtle` variables
- **Focus color**: `#0f62fe` (Blue 60) used consistently across components

### Integration Points
- **Bootstrap _alert.scss**: Uses CSS custom properties set via `$alert-*` variables
- **Theme color system**: Alerts use `$theme-colors` map for variant generation
- **Carbon custom directory**: Follow pattern established by `_accordion.scss` and `_type.scss`

## Architecture

```mermaid
graph TD
    A[_variables.scss] -->|Alert variable overrides| B[Bootstrap _alert.scss]
    B -->|Generates .alert classes| C[Compiled CSS]
    D[carbon/_alert.scss] -->|Custom left-border styles| C
    E[carbon/_index.scss] -->|@import alert| D
```

## Design Specifications

### Visual Structure

```
┌─────────────────────────────────────────────────────────┐
│ ███ │  Alert content goes here with appropriate         │
│ ███ │  padding and typography.                     [×]  │
└─────────────────────────────────────────────────────────┘
  ↑                                                    ↑
  3px left accent border                         Close button
  (status color)                                 (dismissible)
```

### Color Mapping

| Bootstrap Class | Left Border Color | Background | Text Color |
|----------------|-------------------|------------|------------|
| `.alert-danger` | #da1e28 (Red 60) | tint-color(#da1e28, 90%) | #161616 |
| `.alert-success` | #24a148 (Green 50) | tint-color(#24a148, 90%) | #161616 |
| `.alert-warning` | #f1c21b (Yellow 30) | tint-color(#f1c21b, 90%) | #161616 |
| `.alert-info` | #0043ce (Blue 70) | tint-color(#0043ce, 90%) | #161616 |
| `.alert-primary` | #0f62fe (Blue 60) | tint-color(#0f62fe, 90%) | #161616 |
| `.alert-secondary` | #525252 (Gray 70) | tint-color(#525252, 90%) | #161616 |

### Spacing Specifications

| Property | Value | Carbon Token |
|----------|-------|--------------|
| Padding Y | 0.75rem (12px) | spacing-04 |
| Padding X | 1rem (16px) | spacing-05 |
| Left border width | 3px | - |
| Other borders | 1px solid #e0e0e0 | ui-03 |
| Border radius | 0 | - |
| Margin bottom | 1rem (16px) | spacing-05 |

## Components and Interfaces

### Component 1: Alert Variable Overrides

**Purpose:** Override Bootstrap's default alert variables to match Carbon styling
**Location:** `scss/_variables.scss` (alert section, around line 1960)
**Approach:** Set variables before Bootstrap's `!default` assignment

```scss
// Carbon Alert Overrides
$alert-padding-y: $spacer * .75;           // 12px (spacing-04)
$alert-padding-x: $spacer;                  // 16px (spacing-05)
$alert-border-radius: 0;                    // Carbon: square corners
$alert-border-width: 1px;                   // Subtle border (overridden per-side in custom)
$alert-link-font-weight: $font-weight-semibold;
```

### Component 2: Alert Custom Styles

**Purpose:** Apply Carbon-specific styling that cannot be achieved via variables
**Location:** `scss/carbon/_alert.scss`
**Dependencies:** Bootstrap alert classes, Carbon color variables

Key customizations:
1. Left accent border (3px in status color)
2. Override subtle border colors to use gray
3. Dark text color for all variants
4. Focus states for interactive elements

### Component 3: High-Contrast Variant

**Purpose:** Optional modifier for critical/prominent alerts
**Location:** `scss/carbon/_alert.scss`
**Class:** `.alert-high-contrast`

## Implementation Details

### File 1: Variable Overrides (`scss/_variables.scss`)

Add Carbon alert overrides before Bootstrap's defaults (around line 1960):

```scss
// ============================================================================
// Carbon Alert Overrides
// ============================================================================
// Reference: https://carbondesignsystem.com/components/notification/style

$alert-padding-y: $spacer * .75;           // Carbon: spacing-04 (12px)
$alert-padding-x: $spacer;                  // Carbon: spacing-05 (16px)
$alert-border-radius: 0;                    // Carbon: square corners
$alert-border-width: 1px;                   // Base border width
$alert-link-font-weight: $font-weight-semibold; // Carbon: 600
```

### File 2: Custom Styles (`scss/carbon/_alert.scss`)

```scss
// Carbon Alert Customizations
// Left accent border and refined styling for inline notifications

.alert {
  // Override border to be subtle gray on top/right/bottom
  border-color: #e0e0e0; // Carbon: ui-03
  // Left border will be set per-variant below
  border-left-width: 3px;

  // Ensure dark text for readability
  color: $body-color; // #161616
}

// Generate left border colors for each variant
@each $state, $value in $theme-colors {
  .alert-#{$state} {
    border-left-color: $value;
    // Override text to be dark (not the tinted emphasis color)
    --#{$prefix}alert-color: #{$body-color};
    // Lighter background
    --#{$prefix}alert-bg: #{tint-color($value, 90%)};
    // Keep gray borders except left
    --#{$prefix}alert-border-color: #e0e0e0;
  }
}

// Focus states
.alert-link:focus {
  outline: 2px solid #0f62fe;
  outline-offset: 2px;
}

.alert-dismissible .btn-close:focus {
  outline: 2px solid #0f62fe;
  outline-offset: -2px;
  box-shadow: none;
}

// High-contrast variant (optional)
.alert-high-contrast {
  border-left-width: 0;
  color: #fff;

  &.alert-danger {
    --#{$prefix}alert-bg: #{$danger};
    --#{$prefix}alert-color: #fff;
    --#{$prefix}alert-border-color: #{$danger};
  }
  // ... similar for other variants
}
```

### File 3: Index Update (`scss/carbon/_index.scss`)

```scss
@import "type";
@import "accordion";
@import "alert";
```

## Error Handling

### Error Scenarios

1. **Color contrast issues**
   - **Handling:** Use `$body-color` (#161616) for text in low-contrast mode
   - **User Impact:** Ensures WCAG AA compliance for readability

2. **Variable order issues**
   - **Handling:** Place Carbon overrides BEFORE Bootstrap's `!default` assignments
   - **User Impact:** None if implemented correctly

## Testing Strategy

### Visual Testing
- Verify all 6 alert variants display correct left border colors
- Confirm square corners (no border-radius)
- Check padding matches Carbon spacing tokens
- Validate focus states on links and close buttons

### Accessibility Testing
- Test color contrast ratios meet WCAG AA (4.5:1)
- Verify focus indicators are visible (3:1 contrast)
- Test with screen reader to confirm alert role

### Browser Testing
- Test in Chrome, Firefox, Safari
- Verify CSS custom properties work correctly
- Check high-contrast mode in Windows

## File Summary

| File | Action | Purpose |
|------|--------|---------|
| `scss/_variables.scss` | Modify | Add alert variable overrides |
| `scss/carbon/_alert.scss` | Create | Custom left-border and text color styles |
| `scss/carbon/_index.scss` | Modify | Add `@import "alert"` |

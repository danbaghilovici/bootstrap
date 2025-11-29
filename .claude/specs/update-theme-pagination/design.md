# Design: Update Theme Pagination

## Approach

Use Bootstrap's variable override system to customize pagination styling. All changes follow the established pattern: variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_pagination.scss`.

## Variable Overrides

### File: `scss/_variables-carbon.scss`

Add a new section for pagination overrides after the Breadcrumb section:

```scss
// ============================================================================
// Carbon Pagination Overrides
// ============================================================================
// Reference: https://carbondesignsystem.com/components/pagination/style
// stylelint-disable scss/dollar-variable-default

// -----------------------------------------------------------------------------
// Pagination Typography
// -----------------------------------------------------------------------------
// Carbon uses body-compact-01 token (14px)
$pagination-font-size: 0.875rem;                    // Carbon: body-compact-01 (14px)

// -----------------------------------------------------------------------------
// Pagination Sizing - Default (40px height)
// -----------------------------------------------------------------------------
// Height = (padding-y × 2) + (font-size × line-height) + (border × 2)
// 40px = (10px × 2) + (14px × 1.29) + (1px × 2) ≈ 40px
$pagination-padding-y: 0.625rem;                    // Carbon: 10px
$pagination-padding-x: 1rem;                        // Carbon: spacing-05 (16px)

// -----------------------------------------------------------------------------
// Pagination Sizing - Small (32px height)
// -----------------------------------------------------------------------------
// 32px = (5px × 2) + (14px × 1.29) + (1px × 2) ≈ 30px (closest achievable)
$pagination-padding-y-sm: 0.3125rem;                // Carbon: sm (5px)
$pagination-padding-x-sm: 1rem;                     // Carbon: spacing-05 (16px)

// -----------------------------------------------------------------------------
// Pagination Sizing - Large (48px height)
// -----------------------------------------------------------------------------
// 48px = (14px × 2) + (14px × 1.29) + (1px × 2) ≈ 48px
$pagination-padding-y-lg: 0.875rem;                 // Carbon: lg (14px)
$pagination-padding-x-lg: 1rem;                     // Carbon: spacing-05 (16px)

// -----------------------------------------------------------------------------
// Pagination Colors - Default State
// -----------------------------------------------------------------------------
$pagination-color: $body-color;                     // Carbon: $text-primary (#161616)
$pagination-bg: $body-bg;                           // Carbon: $layer (white)
$pagination-border-color: $gray-200;                // Carbon: $border-subtle (Gray 20)

// -----------------------------------------------------------------------------
// Pagination Colors - Hover State
// -----------------------------------------------------------------------------
$pagination-hover-color: $body-color;               // Carbon: $text-primary
$pagination-hover-bg: $gray-100;                    // Carbon: $layer-hover (Gray 10)
$pagination-hover-border-color: $gray-200;          // Carbon: $border-subtle

// -----------------------------------------------------------------------------
// Pagination Colors - Focus State
// -----------------------------------------------------------------------------
$pagination-focus-color: $body-color;               // Carbon: $text-primary
$pagination-focus-bg: $body-bg;                     // Carbon: maintain background
$pagination-focus-box-shadow: none;                 // Disable - use outline instead

// -----------------------------------------------------------------------------
// Pagination Colors - Active State
// -----------------------------------------------------------------------------
$pagination-active-color: $white;                   // Carbon: $text-on-color
$pagination-active-bg: $primary;                    // Carbon: $interactive (Blue 60)
$pagination-active-border-color: $primary;          // Carbon: match background

// -----------------------------------------------------------------------------
// Pagination Colors - Disabled State
// -----------------------------------------------------------------------------
$pagination-disabled-color: $gray-500;              // Carbon: $text-disabled (Gray 50)
$pagination-disabled-bg: $body-bg;                  // Carbon: maintain background
$pagination-disabled-border-color: $gray-200;       // Carbon: $border-subtle

// -----------------------------------------------------------------------------
// Pagination Shape
// -----------------------------------------------------------------------------
// Carbon uses rectangular elements
$pagination-border-radius: 0;
$pagination-border-radius-sm: 0;
$pagination-border-radius-lg: 0;

// stylelint-enable scss/dollar-variable-default
// ============================================================================
// End Carbon Pagination Overrides
// ============================================================================
```

## Custom Styles

### File: `scss/carbon/_pagination.scss`

Custom styles for focus outline (not achievable via variables):

```scss
// Carbon Pagination Customizations
// Focus state outline (cannot be done via variables)

.page-link {
  &:focus {
    outline: 2px solid $primary;    // Carbon: Blue 60 focus outline
    outline-offset: -2px;           // Carbon: inset outline style
  }
}
```

## File Changes Summary

| File | Action | Description |
|------|--------|-------------|
| `scss/_variables-carbon.scss` | Edit | Add pagination variable overrides section |
| `scss/carbon/_pagination.scss` | Create | Focus outline styles |
| `scss/carbon/_index.scss` | Edit | Import pagination partial |

## Design Token Mapping

| Carbon Token | Bootstrap Variable | Value |
|--------------|---------------------|-------|
| `$text-primary` | `$pagination-color` | #161616 |
| `$layer` | `$pagination-bg` | #ffffff |
| `$border-subtle` | `$pagination-border-color` | #e0e0e0 |
| `$layer-hover` | `$pagination-hover-bg` | #f4f4f4 |
| `$interactive` | `$pagination-active-bg` | #0f62fe |
| `$text-on-color` | `$pagination-active-color` | #ffffff |
| `$text-disabled` | `$pagination-disabled-color` | #8d8d8d |
| `body-compact-01` | `$pagination-font-size` | 0.875rem |

## Height Calculations

### Default (40px)
- Padding: 10px top + 10px bottom = 20px
- Font: 14px × 1.29 line-height ≈ 18px
- Border: 1px × 2 = 2px
- Total: 20 + 18 + 2 = 40px

### Small (32px)
- Padding: 5px top + 5px bottom = 10px
- Font: 14px × 1.29 line-height ≈ 18px
- Border: 1px × 2 = 2px
- Total: 10 + 18 + 2 = 30px (closest to 32px)

### Large (48px)
- Padding: 14px top + 14px bottom = 28px
- Font: 14px × 1.29 line-height ≈ 18px
- Border: 1px × 2 = 2px
- Total: 28 + 18 + 2 = 48px

## Testing Strategy

1. Visual inspection of all pagination states in demo page
2. Verify heights match Carbon specifications
3. Test keyboard navigation and focus visibility
4. Run `npm run css-lint` for SCSS standards
5. Run `npm run css` to verify build succeeds

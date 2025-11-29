# Design Document: Update Theme Spacing

## Overview

This design document describes how to update the Bootstrap theme's spacing system to align with IBM's Carbon Design System spacing scale. The implementation follows Bootstrap's recommended customization approach by overriding Sass variables in `scss/_variables.scss` before Bootstrap processes them. No Bootstrap source files will be modified directly.

## Steering Document Alignment

### Technical Standards (tech.md)

This design strictly follows the **Variable-Only Customization** approach documented in tech.md:

1. **Variable overrides**: All spacing changes are made by setting Sass variables before Bootstrap imports
2. **No source file modifications**: Bootstrap's spacing-related files remain untouched
3. **Carbon reference comments**: Each variable override includes a comment referencing the Carbon token

The design uses the Carbon Spacing Tokens documented in tech.md:
- **Base unit**: 2px
- **Scale**: 2, 4, 8, 12, 16, 24, 32, 40, 48px

### Project Structure (structure.md)

Following structure.md conventions:

1. **Primary customization point**: `scss/_variables.scss` - all spacing variable overrides go here
2. **Variable naming**: Uses Bootstrap's `$component-state-property-size` convention
3. **No component file edits**: Per "What NOT to Do" section, we won't modify Bootstrap source files

## Prerequisites

None. Spacing is a pure variable override that doesn't require any external dependencies.

## Code Reuse Analysis

### Existing Components to Leverage

- **`scss/_variables.scss`**: The existing variables file where all spacing overrides will be added (lines 482-490 contain current spacing variables)
- **Bootstrap's `!default` pattern**: All Bootstrap variables use `!default`, so our overrides take precedence
- **Utility API**: Bootstrap's utility API automatically generates margin, padding, and gap utilities from `$spacers` map

### Integration Points

- **Utility classes**: All `m-*`, `p-*`, `gap-*` utilities are generated from `$spacers` map
- **Component spacing**: Many components reference `$spacer` for internal spacing calculations
- **Negative margins**: Bootstrap generates negative margin utilities from `$negative-spacers` (derived from `$spacers`)

## Architecture

The spacing customization flows through Bootstrap's existing architecture:

```
$spacer (base value)
    │
    ▼
$spacers (map of values)
    │
    ├──► _utilities.scss (generates m-*, p-*, gap-* classes)
    │
    └──► Components (use $spacer for calculations)
```

## Design Decisions

### Decision 1: Mapping Strategy

**Problem**: Carbon has 9 spacing tokens (spacing-01 through spacing-09), while Bootstrap has 6 values (0-5). How do we map these?

**Options Considered**:
1. Replace Bootstrap's 0-5 with Carbon's closest values
2. Extend Bootstrap's map to include all Carbon values (0-9)
3. Create a hybrid that maintains Bootstrap conventions while adding Carbon values

**Decision**: Use Option 3 - Hybrid approach

**Mapping**:
| Bootstrap Key | Carbon Token | Value |
|---------------|--------------|-------|
| 0 | - | 0 |
| 1 | spacing-02 | 0.25rem (4px) |
| 2 | spacing-03 | 0.5rem (8px) |
| 3 | spacing-05 | 1rem (16px) |
| 4 | spacing-06 | 1.5rem (24px) |
| 5 | spacing-09 | 3rem (48px) |
| 6 | spacing-01 | 0.125rem (2px) |
| 7 | spacing-04 | 0.75rem (12px) |
| 8 | spacing-07 | 2rem (32px) |
| 9 | spacing-08 | 2.5rem (40px) |

**Rationale**:
- Keys 0-5 maintain Bootstrap compatibility (existing code using `.m-3`, `.p-4` continues to work)
- Keys 1-5 are mapped to Carbon values that are closest to Bootstrap's original values
- Keys 6-9 add the remaining Carbon values that fill gaps in the scale
- This allows gradual adoption - existing Bootstrap patterns work, with new Carbon values available

### Decision 2: Base Spacer Value

**Problem**: Should `$spacer` remain 1rem or change?

**Decision**: Keep `$spacer: 1rem` (unchanged)

**Rationale**:
- 1rem (16px) equals Carbon's spacing-05, which is the core body spacing value
- Many Bootstrap components use `$spacer` for calculations
- Changing this could have unintended effects on component spacing
- The spacers map provides all the granularity needed

### Decision 3: Negative Spacers

**Problem**: Bootstrap generates `$negative-spacers` from `$spacers` for negative margin utilities. Should we customize this?

**Decision**: Let Bootstrap generate negative spacers automatically

**Rationale**:
- Bootstrap's default behavior creates negative spacers for all non-zero values
- Our extended `$spacers` map will automatically generate corresponding negative margin utilities
- No custom override needed

### Decision 4: Additional Carbon Spacing Tokens

**Problem**: Carbon has spacing-10 through spacing-13 for larger layout spacing (64px, 80px, 96px, 160px). Should we include these?

**Decision**: Exclude spacing-10 through spacing-13 from initial implementation

**Rationale**:
- These are layout-level tokens, typically used for page sections and containers
- Bootstrap's spacing utilities are designed for component-level spacing
- Including these would create utility classes (`.m-10`, `.p-13`) that may not align with Bootstrap conventions
- Can be added in a future iteration if needed for layout purposes

## Components and Interfaces

### Component 1: Base Spacer Variable

- **Purpose**: Define the base spacing unit
- **Variable**: `$spacer: 1rem;`
- **Dependencies**: None
- **Impact**: Used by components for relative spacing calculations

### Component 2: Extended Spacers Map

- **Purpose**: Define all spacing values for utility generation
- **Variable**: `$spacers` Sass map
- **Dependencies**: `$spacer`
- **Impact**: Generates all margin, padding, and gap utility classes

## Data Models

### Complete Variable Override

```scss
// ============================================================================
// Carbon Design System Spacing Overrides
// ============================================================================
// These variables override Bootstrap's defaults to match IBM's Carbon Design System.
// They MUST appear BEFORE Bootstrap's default definitions to take effect.
// Reference: https://carbondesignsystem.com/elements/spacing/overview/
// ============================================================================

// -----------------------------------------------------------------------------
// Base Spacer (Carbon: spacing-05)
// -----------------------------------------------------------------------------
$spacer: 1rem; // Carbon: 16px (spacing-05)

// -----------------------------------------------------------------------------
// Spacers Map (Carbon Spacing Scale)
// -----------------------------------------------------------------------------
// Keys 0-5: Bootstrap-compatible values mapped to nearest Carbon tokens
// Keys 6-9: Additional Carbon spacing values
// -----------------------------------------------------------------------------
$spacers: (
  0: 0,                    // No spacing
  1: $spacer * .25,        // Carbon: spacing-02 (4px)
  2: $spacer * .5,         // Carbon: spacing-03 (8px)
  3: $spacer,              // Carbon: spacing-05 (16px)
  4: $spacer * 1.5,        // Carbon: spacing-06 (24px)
  5: $spacer * 3,          // Carbon: spacing-09 (48px)
  6: $spacer * .125,       // Carbon: spacing-01 (2px)
  7: $spacer * .75,        // Carbon: spacing-04 (12px)
  8: $spacer * 2,          // Carbon: spacing-07 (32px)
  9: $spacer * 2.5,        // Carbon: spacing-08 (40px)
);
```

### Generated Utility Classes

The following utility classes will be generated:

**Margin utilities**: `.m-0` through `.m-9`, with directional variants (`mt-`, `mb-`, `ms-`, `me-`, `mx-`, `my-`)

**Padding utilities**: `.p-0` through `.p-9`, with directional variants (`pt-`, `pb-`, `ps-`, `pe-`, `px-`, `py-`)

**Gap utilities**: `.gap-0` through `.gap-9`, with directional variants (`row-gap-`, `column-gap-`)

**Negative margins**: `.m-n1` through `.m-n9`, with directional variants

### Carbon Token Reference Table

| Utility Class | Carbon Token | rem Value | px Value |
|---------------|--------------|-----------|----------|
| `*-0` | - | 0 | 0 |
| `*-1` | spacing-02 | 0.25rem | 4px |
| `*-2` | spacing-03 | 0.5rem | 8px |
| `*-3` | spacing-05 | 1rem | 16px |
| `*-4` | spacing-06 | 1.5rem | 24px |
| `*-5` | spacing-09 | 3rem | 48px |
| `*-6` | spacing-01 | 0.125rem | 2px |
| `*-7` | spacing-04 | 0.75rem | 12px |
| `*-8` | spacing-07 | 2rem | 32px |
| `*-9` | spacing-08 | 2.5rem | 40px |

## Error Handling

### Error Scenarios

1. **Spacer map syntax error**
   - **Handling**: Build will fail with Sass compilation error
   - **Prevention**: Follow exact Sass map syntax with proper commas and parentheses

2. **Variable override not taking effect**
   - **Handling**: Ensure override appears BEFORE Bootstrap's `_variables.scss` is processed
   - **User Impact**: Would see Bootstrap default spacing; caught during development/testing

3. **Missing spacer key**
   - **Handling**: Utility classes for that key won't be generated
   - **Prevention**: Include all keys 0-9 in the map

## Testing Strategy

### Unit Testing

- **SCSS Compilation**: Verify build completes without errors using `npm run css`
- **Variable Override Verification**: Check that compiled CSS contains expected spacing values
- **Utility Class Generation**: Verify all `.m-*`, `.p-*`, `.gap-*` classes exist in output
- **Sass lint**: Run `npm run css-lint` to verify no style issues

### Integration Testing

- **Component Spacing**: Verify buttons, forms, cards use updated spacing
- **Utility Classes**: Test `.m-6`, `.p-7`, `.gap-8`, `.m-9` work correctly
- **Responsive Behavior**: Test spacing at different breakpoints
- **Negative Margins**: Verify `.m-n6` through `.m-n9` work correctly

### End-to-End Testing

- **Visual Inspection**: Review spacing in browser DevTools
- **Layout Verification**: Check that common layouts render correctly
- **Cross-browser**: Test in Chrome, Firefox, Safari, Edge

### Verification Checklist

After implementation, verify:
- [ ] `npm run css` builds without errors
- [ ] `npm run css-lint` passes
- [ ] CSS output contains `.m-6`, `.m-7`, `.m-8`, `.m-9` classes
- [ ] CSS output contains `.p-6`, `.p-7`, `.p-8`, `.p-9` classes
- [ ] CSS output contains `.gap-6`, `.gap-7`, `.gap-8`, `.gap-9` classes
- [ ] Existing `.m-3`, `.p-4` classes still work as expected
- [ ] DevTools shows correct pixel values for each spacing utility

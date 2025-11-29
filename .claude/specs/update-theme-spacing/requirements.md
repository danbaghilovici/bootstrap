# Requirements Document: Update Theme Spacing

## Introduction

This specification defines the requirements for updating the Bootstrap theme's spacing system to align with IBM's Carbon Design System spacing scale. The goal is to replace Bootstrap's default spacing values with Carbon's spacing tokens while maintaining Bootstrap's utility-first customization approach through variable overrides only.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Spacing is fundamental to Carbon's visual rhythm and layout
2. **"Phase 1 - Foundation"** - Spacing is item #3 in the component priority order
3. **"Systematic"** - Carbon's mathematical spacing scale provides consistent, predictable layout behavior

## Background: Carbon vs Bootstrap Spacing

### Carbon Spacing Scale
Carbon uses a 2px base unit with a mathematical progression:

| Token | Value (px) | Value (rem) |
|-------|------------|-------------|
| spacing-01 | 2px | 0.125rem |
| spacing-02 | 4px | 0.25rem |
| spacing-03 | 8px | 0.5rem |
| spacing-04 | 12px | 0.75rem |
| spacing-05 | 16px | 1rem |
| spacing-06 | 24px | 1.5rem |
| spacing-07 | 32px | 2rem |
| spacing-08 | 40px | 2.5rem |
| spacing-09 | 48px | 3rem |

### Bootstrap Default Spacing
Bootstrap uses a multiplier-based scale from `$spacer: 1rem`:

| Class | Multiplier | Value |
|-------|------------|-------|
| 0 | 0 | 0 |
| 1 | 0.25 | 4px |
| 2 | 0.5 | 8px |
| 3 | 1 | 16px |
| 4 | 1.5 | 24px |
| 5 | 3 | 48px |

### Key Differences
- Carbon has more granular small values (2px, 4px, 8px, 12px)
- Bootstrap jumps from 24px (4) to 48px (5), missing 32px and 40px
- Carbon's scale is more comprehensive for precise layout control

## Requirements

### Requirement 1: Base Spacer Value

**User Story:** As a developer, I want the base spacer value to align with Carbon's spacing-05, so that spacing utilities are consistent with Carbon Design System.

#### Acceptance Criteria

1. WHEN spacing is calculated THEN the system SHALL use 1rem (16px) as the base spacer value
2. WHEN the `$spacer` variable is used THEN it SHALL equal Carbon's spacing-05 token

### Requirement 2: Extended Spacing Scale

**User Story:** As a developer, I want access to more spacing values that match Carbon's scale, so that I can create precise layouts matching Carbon Design System.

#### Acceptance Criteria

1. WHEN spacing utility classes are generated THEN the system SHALL include values for Carbon spacing-01 through spacing-09
2. WHEN using spacing value 0 THEN the system SHALL output 0 (no spacing)
3. WHEN using spacing value 1 THEN the system SHALL output 0.25rem (4px / Carbon spacing-02)
4. WHEN using spacing value 2 THEN the system SHALL output 0.5rem (8px / Carbon spacing-03)
5. WHEN using spacing value 3 THEN the system SHALL output 1rem (16px / Carbon spacing-05)
6. WHEN using spacing value 4 THEN the system SHALL output 1.5rem (24px / Carbon spacing-06)
7. WHEN using spacing value 5 THEN the system SHALL output 3rem (48px / Carbon spacing-09)

### Requirement 3: Additional Spacing Values

**User Story:** As a developer, I want access to additional spacing values beyond Bootstrap's default 0-5 scale, so that I can use the full range of Carbon spacing tokens.

#### Acceptance Criteria

1. WHEN using spacing value 6 THEN the system SHALL output 0.125rem (2px / Carbon spacing-01)
2. WHEN using spacing value 7 THEN the system SHALL output 0.75rem (12px / Carbon spacing-04)
3. WHEN using spacing value 8 THEN the system SHALL output 2rem (32px / Carbon spacing-07)
4. WHEN using spacing value 9 THEN the system SHALL output 2.5rem (40px / Carbon spacing-08)

### Requirement 4: Utility Class Generation

**User Story:** As a developer, I want all spacing utility classes (m-*, p-*, gap-*) to reflect the Carbon spacing scale, so that I can use consistent spacing throughout my markup.

#### Acceptance Criteria

1. WHEN margin utilities are generated THEN they SHALL use the Carbon-aligned spacer values
2. WHEN padding utilities are generated THEN they SHALL use the Carbon-aligned spacer values
3. WHEN gap utilities are generated THEN they SHALL use the Carbon-aligned spacer values
4. WHEN negative margin utilities are generated THEN they SHALL use the Carbon-aligned spacer values

### Requirement 5: Variable-Only Implementation

**User Story:** As a developer, I want spacing changes to be implemented through Bootstrap variable overrides only, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN spacing is customized THEN the system SHALL NOT modify Bootstrap source files directly
2. WHEN spacing variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon spacing tokens
4. IF a Bootstrap variable exists for a spacing property THEN it SHALL be used instead of custom CSS

### Requirement 6: Component Spacing Inheritance

**User Story:** As a developer, I want Bootstrap components to automatically use the Carbon-aligned spacing, so that forms, cards, and other components have consistent spacing.

#### Acceptance Criteria

1. WHEN Bootstrap components use `$spacer` THEN they SHALL receive the Carbon-aligned value
2. WHEN component-specific spacing variables exist THEN they MAY be overridden to match Carbon specifications
3. WHEN spacing changes are applied THEN existing Bootstrap components SHALL continue to function correctly

## Non-Functional Requirements

### Maintainability
- All spacing overrides must be clearly documented with Carbon token references
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's `$component-state-property-size` naming convention

### Compatibility
- Spacing must work correctly with all Bootstrap components
- Utility classes must generate for all responsive breakpoints
- Changes must not break existing layouts that use Bootstrap spacing utilities

### Performance
- Spacing changes should not significantly increase CSS output size
- The extended spacer map should only add necessary values

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Container widths** - Container max-widths are a separate customization
2. **Grid gutters** - May be addressed in a separate specification
3. **Component-specific spacing** - Individual component spacing (e.g., button padding, card margins) will be handled when each component is customized
4. **Layout tokens** - Carbon's layout tokens (for page-level spacing) are not part of this initial spacing update

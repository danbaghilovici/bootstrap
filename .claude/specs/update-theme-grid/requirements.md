# Requirements Document: Update Theme Grid

## Introduction

This specification defines the requirements for updating the Bootstrap theme's grid system to align with IBM's Carbon Design System 2x grid. The goal is to replace Bootstrap's default breakpoints and container widths with Carbon's breakpoint values while maintaining Bootstrap's 12-column grid system and utility-first customization approach through variable overrides only.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - The grid system is foundational to Carbon's layout structure
2. **"Phase 1 - Foundation"** - Grid/layout is part of the foundational styling elements
3. **"Maintain Bootstrap's utility and component structure"** - We adapt Carbon breakpoints to Bootstrap's grid system

## Background: Carbon vs Bootstrap Grid

### Carbon 2x Grid Breakpoints
Carbon uses a 2x grid system with these breakpoints:

| Name | Min-Width | Columns |
|------|-----------|---------|
| sm | 320px | 4 |
| md | 672px | 8 |
| lg | 1056px | 16 |
| xlg | 1312px | 16 |
| max | 1584px | 16 |

### Carbon Grid Modes
Carbon provides three grid gutter modes:

| Mode | Gutter Width | Use Case |
|------|--------------|----------|
| Wide (default) | 32px (2rem) | Standard layouts, most components |
| Narrow | 16px (1rem) | Tighter layouts |
| Condensed | 1px | Compact UI, data-dense layouts |

### Carbon Container Margins
Carbon uses responsive container padding:

| Breakpoint | Container Padding |
|------------|-------------------|
| < 672px | 16px (1rem) |
| 672px - 1583px | 32px (2rem) |
| 1584px+ | 40px (2.5rem) |

**Max-width**: 1584px (99rem)

### Bootstrap Default Breakpoints
Bootstrap uses these breakpoints:

| Name | Min-Width |
|------|-----------|
| xs | 0 |
| sm | 576px |
| md | 768px |
| lg | 992px |
| xl | 1200px |
| xxl | 1400px |

### Key Differences
- Carbon has 5 named breakpoints (sm, md, lg, xlg, max) vs Bootstrap's 6 (xs, sm, md, lg, xl, xxl)
- Carbon breakpoints are at different pixel values
- Carbon uses 16 columns (at lg+) vs Bootstrap's default 12
- Carbon's default gutter is 32px vs Bootstrap's 24px (1.5rem)
- Carbon's max container width is 1584px vs Bootstrap's 1320px (at xxl)
- Carbon has three grid modes (wide/narrow/condensed) vs Bootstrap's single mode

### Design Decision: Breakpoint Strategy

**Problem**: Carbon and Bootstrap have different breakpoint naming and values. How do we map them?

**Decision**: Adopt Carbon's 5 breakpoints with Bootstrap's naming convention for familiarity.

**Mapping**:
| Bootstrap Name | Carbon Equivalent | Value |
|----------------|-------------------|-------|
| xs | (base) | 0 |
| sm | sm | 320px |
| md | md | 672px |
| lg | lg | 1056px |
| xl | xlg | 1312px |
| xxl | max | 1584px |

**Rationale**:
- Maintains Bootstrap's 6-tier breakpoint system (xs through xxl)
- Maps Carbon values to familiar Bootstrap names
- Allows existing Bootstrap utility classes (.col-md-*, .d-lg-*, etc.) to work at Carbon breakpoints
- Container max-widths can be adjusted to complement Carbon breakpoints

## Requirements

### Requirement 1: Grid Breakpoints

**User Story:** As a developer, I want grid breakpoints to match Carbon's responsive design points, so that layouts respond at the same viewport widths as Carbon applications.

#### Acceptance Criteria

1. WHEN the viewport is below 320px THEN the system SHALL apply xs (extra-small) styles
2. WHEN the viewport is 320px or wider THEN the system SHALL apply sm (small) styles
3. WHEN the viewport is 672px or wider THEN the system SHALL apply md (medium) styles
4. WHEN the viewport is 1056px or wider THEN the system SHALL apply lg (large) styles
5. WHEN the viewport is 1312px or wider THEN the system SHALL apply xl (extra-large) styles
6. WHEN the viewport is 1584px or wider THEN the system SHALL apply xxl (extra-extra-large) styles

### Requirement 2: Container Max-Widths

**User Story:** As a developer, I want container max-widths that complement Carbon breakpoints, so that content areas have appropriate widths at each responsive tier.

#### Acceptance Criteria

1. WHEN using a container at sm breakpoint THEN the system SHALL limit max-width appropriately (approximately 304px)
2. WHEN using a container at md breakpoint THEN the system SHALL limit max-width appropriately (approximately 640px)
3. WHEN using a container at lg breakpoint THEN the system SHALL limit max-width appropriately (approximately 1024px)
4. WHEN using a container at xl breakpoint THEN the system SHALL limit max-width appropriately (approximately 1280px)
5. WHEN using a container at xxl breakpoint THEN the system SHALL limit max-width to 1584px (Carbon max)

### Requirement 3: Grid Columns

**User Story:** As a developer, I want a 16-column grid system matching Carbon's recommendation, so that I have more granular control over layouts.

#### Acceptance Criteria

1. WHEN using grid columns THEN the system SHALL provide 16 columns at all breakpoints
2. WHEN using column utilities (.col-*, .col-md-*, etc.) THEN they SHALL support values 1-16
3. WHEN using offset utilities (.offset-*, .offset-md-*, etc.) THEN they SHALL support values 0-15
4. WHEN using row-columns utilities (.row-cols-*) THEN they SHALL function correctly with the 16-column system

### Requirement 4: Grid Gutter Width

**User Story:** As a developer, I want gutter widths that align with Carbon's spacing system, so that grid spacing is consistent with other Carbon-inspired spacing.

#### Acceptance Criteria

1. WHEN grid gutters are applied THEN the system SHALL use 2rem (32px) as the default gutter width
2. WHEN container padding is applied THEN it SHALL match the grid gutter width (2rem)

### Requirement 5: Variable-Only Implementation

**User Story:** As a developer, I want grid changes to be implemented through Bootstrap variable overrides only, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN grid values are customized THEN the system SHALL NOT modify Bootstrap source files directly
2. WHEN grid variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
4. IF a Bootstrap variable exists for a grid property THEN it SHALL be used instead of custom CSS

### Requirement 6: Responsive Utility Compatibility

**User Story:** As a developer, I want all Bootstrap responsive utilities to work with the new breakpoints, so that I can use familiar utility classes for responsive design.

#### Acceptance Criteria

1. WHEN using display utilities (.d-none, .d-md-block, etc.) THEN they SHALL respond at Carbon breakpoints
2. WHEN using flex utilities (.flex-column, .flex-lg-row, etc.) THEN they SHALL respond at Carbon breakpoints
3. WHEN using spacing utilities (.mt-md-3, .px-lg-4, etc.) THEN they SHALL respond at Carbon breakpoints
4. WHEN using text utilities (.text-center, .text-md-start, etc.) THEN they SHALL respond at Carbon breakpoints

## Non-Functional Requirements

### Maintainability
- All grid overrides must be clearly documented with Carbon reference comments
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility
- Grid must work correctly with all Bootstrap components
- Responsive utilities must function at all new breakpoints
- Changes must not break existing layouts that use Bootstrap grid classes

### Performance
- Grid changes should not significantly increase CSS output size
- Media queries should be efficiently generated

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Variable column count per breakpoint** - Carbon uses 4/8/16 columns at different breakpoints, but implementing variable columns would require significant customization beyond variable overrides. We use a consistent 16-column system throughout.
2. **Carbon's narrow/condensed grid modes** - Carbon provides three gutter modes (wide: 32px, narrow: 16px, condensed: 1px). We implement wide mode (32px) as the default. Narrow and condensed modes would require custom utility classes beyond variable overrides.
3. **Responsive container padding** - Carbon varies container padding by breakpoint (16px/32px/40px). Bootstrap uses a single `$container-padding-x` value. Implementing responsive padding would require custom CSS.
4. **Carbon's CSS Grid implementation** - Bootstrap uses flexbox grid; we maintain this approach
5. **Subgrid features** - Not part of Bootstrap's current grid system

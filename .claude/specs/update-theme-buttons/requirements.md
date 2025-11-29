# Requirements Document: Update Theme Buttons

## Introduction

This specification defines the requirements for updating the Bootstrap theme's button components to align with IBM's Carbon Design System button styling. The goal is to customize Bootstrap's button variables to match Carbon's button appearance, including sizing, typography, colors, and interactive states, while maintaining Bootstrap's utility-first customization approach through variable overrides only.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Buttons are a core UI component that significantly impacts the site's visual identity
2. **"Phase 2 - Basic Components"** - Buttons are item #5 in the component priority order, the first basic component after foundation elements
3. **"Accessible"** - Carbon buttons are designed with WCAG compliance for focus states and contrast ratios
4. **"Variable-Only Customization"** - All changes will be made through Bootstrap variable overrides, not modifying source files

## Background: Carbon vs Bootstrap Buttons

### Carbon Button Characteristics

Carbon buttons have distinct characteristics:

1. **No border radius** - Carbon buttons are rectangular (0 border radius)
2. **Specific heights**: 32px (sm), 40px (md/default), 48px (lg/field), 64px (xl/expressive)
3. **14px font size** with 400 weight and tight letter-spacing (0.16px)
4. **16px horizontal padding** minimum, icons have additional spacing rules
5. **Five variants**: Primary, Secondary, Tertiary, Ghost, Danger
6. **Solid focus outline** (2px Blue 60) instead of Bootstrap's box-shadow

### Bootstrap Button Defaults

Bootstrap uses:
- Rounded corners (`$border-radius`)
- Different padding ratios
- Box-shadow for focus states
- Shade/tint functions for hover/active states

## Requirements

### Requirement 1: Button Shape (Border Radius)

**User Story:** As a site visitor, I want buttons to have a rectangular shape matching Carbon's design language, so that the UI is visually consistent with Carbon Design System.

#### Acceptance Criteria

1. WHEN a button is rendered THEN it SHALL have 0 border radius (rectangular)
2. WHEN a small button is rendered THEN it SHALL have 0 border radius
3. WHEN a large button is rendered THEN it SHALL have 0 border radius

### Requirement 2: Button Sizing

**User Story:** As a site visitor, I want buttons sized according to Carbon's specifications, so that interactive elements have proper touch targets and visual hierarchy.

#### Acceptance Criteria

1. WHEN a default button is rendered THEN it SHALL have a height of approximately 40px (2.5rem)
2. WHEN a small button (.btn-sm) is rendered THEN it SHALL have a height of approximately 32px (2rem)
3. WHEN a large button (.btn-lg) is rendered THEN it SHALL have a height of approximately 48px (3rem)
4. WHEN a button is rendered THEN horizontal padding SHALL be at least 16px (1rem)
5. WHEN a button is rendered THEN vertical padding SHALL create the specified heights

### Requirement 3: Button Typography

**User Story:** As a site visitor, I want button text styled according to Carbon's typography, so that buttons are readable and consistent with the design system.

#### Acceptance Criteria

1. WHEN a button is rendered THEN the font size SHALL be 14px (0.875rem)
2. WHEN a button is rendered THEN the font weight SHALL be 400 (regular)
3. WHEN a small button is rendered THEN the font size SHALL be 14px (0.875rem)
4. WHEN a large button is rendered THEN the font size SHALL be 14px (0.875rem)
5. WHEN a button is rendered THEN the line height SHALL provide proper vertical centering

### Requirement 4: Button Focus States

**User Story:** As a site visitor using keyboard navigation, I want visible focus indicators that match Carbon's accessibility standards, so that I can navigate the site accessibly.

#### Acceptance Criteria

1. WHEN a button receives focus THEN it SHALL display a 2px solid outline in Blue 60 (#0f62fe)
2. WHEN a button receives focus THEN the outline SHALL have a -2px offset (inset appearance)
3. WHEN a button receives focus THEN the focus indicator SHALL NOT use box-shadow blur
4. WHEN a button receives focus THEN the contrast ratio SHALL meet WCAG AA requirements

### Requirement 5: Button Hover States

**User Story:** As a site visitor, I want buttons to provide clear visual feedback on hover, so that I know the element is interactive.

#### Acceptance Criteria

1. WHEN a primary button is hovered THEN the background SHALL darken to #0353e9 (Blue 70)
2. WHEN a secondary button is hovered THEN the background SHALL lighten to #4c4c4c
3. WHEN a danger button is hovered THEN the background SHALL darken appropriately
4. WHEN any button is hovered THEN the transition SHALL be smooth (150ms ease-in-out)

### Requirement 6: Button Active States

**User Story:** As a site visitor, I want buttons to show a pressed state when clicked, so that I receive feedback that my action is registered.

#### Acceptance Criteria

1. WHEN a primary button is active/pressed THEN the background SHALL darken to #002d9c (Blue 80)
2. WHEN a secondary button is active/pressed THEN the background SHALL change to #6f6f6f
3. WHEN any button is active THEN the active state SHALL NOT use inset box-shadow

### Requirement 7: Button Disabled States

**User Story:** As a site visitor, I want disabled buttons to be clearly distinguishable from active buttons, so that I understand which actions are available.

#### Acceptance Criteria

1. WHEN a button is disabled THEN the background color SHALL be #c6c6c6 (Gray 30)
2. WHEN a button is disabled THEN the text color SHALL be #8d8d8d (Gray 50)
3. WHEN a button is disabled THEN the opacity approach SHALL NOT be used (use explicit colors)

### Requirement 8: Button Box Shadow

**User Story:** As a developer, I want buttons without Bootstrap's default decorative shadows, so that the appearance matches Carbon's flat design aesthetic.

#### Acceptance Criteria

1. WHEN a button is rendered THEN it SHALL NOT have decorative box-shadow
2. WHEN a button is in active state THEN it SHALL NOT have inset box-shadow
3. WHEN a button receives focus THEN it SHALL use outline instead of box-shadow for focus ring

### Requirement 9: Variable-Only Implementation

**User Story:** As a developer, I want button changes implemented through Bootstrap variable overrides only, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN buttons are customized THEN the system SHALL NOT modify Bootstrap source files directly
2. WHEN button variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
4. IF a Bootstrap variable exists for a button property THEN it SHALL be used instead of custom CSS

## Non-Functional Requirements

### Accessibility

- Focus indicators must maintain WCAG 2.2 AA contrast requirements (3:1 minimum)
- Buttons must be operable via keyboard
- Focus must be visible and clear

### Maintainability

- All button overrides must be clearly documented with Carbon token references
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility

- Buttons must work correctly with all Bootstrap button variants (.btn-primary, .btn-secondary, etc.)
- Outline button variants (.btn-outline-*) must remain functional
- Button sizes (.btn-sm, .btn-lg) must work correctly
- Button groups must render properly

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Icon buttons** - Carbon has specific icon button patterns that may require additional work
2. **Button groups** - Will be addressed separately if needed
3. **Loading/spinner states** - Carbon has specific loading button patterns
4. **Expressive/XL buttons** - Carbon's 64px expressive size is not a standard Bootstrap variant
5. **Tertiary/Ghost variants** - These require different implementation approaches beyond variable overrides

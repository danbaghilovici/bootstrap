# Requirements Document: Update Theme Colors

## Introduction

This specification defines the requirements for updating the Bootstrap theme's color system to align with IBM's Carbon Design System. The goal is to replace Bootstrap's default color values with Carbon's color palette and semantic color tokens while maintaining Bootstrap's utility-first customization approach through variable overrides only.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Colors are fundamental to Carbon's visual identity
2. **"Carbon color palette adapted to Bootstrap's color system"** - Explicitly listed in the project scope
3. **"Phase 1 - Foundation"** - Colors are item #1 in the component priority order
4. **"Accessible"** - Carbon colors are designed for WCAG compliance

## Background: Carbon vs Bootstrap Colors

### Carbon Color System Overview

Carbon uses a structured color token system with:

1. **Color Palettes**: Named color families (Blue, Gray, Red, Green, etc.) with 10 shades each (10-100)
2. **Semantic Tokens**: Role-based tokens like `$interactive-01`, `$text-01`, `$support-01`
3. **Theme Support**: Colors adapt across themes (White, Gray 10, Gray 90, Gray 100)

### Carbon Gray Palette (Neutral)

| Token | Hex | Usage |
|-------|-----|-------|
| Gray 10 | #f4f4f4 | Subtle backgrounds |
| Gray 20 | #e0e0e0 | Borders, dividers |
| Gray 30 | #c6c6c6 | Disabled states |
| Gray 40 | #a8a8a8 | Placeholder text |
| Gray 50 | #8d8d8d | Secondary icons |
| Gray 60 | #6f6f6f | Tertiary text |
| Gray 70 | #525252 | Secondary text |
| Gray 80 | #393939 | Primary dark elements |
| Gray 90 | #262626 | Dark backgrounds |
| Gray 100 | #161616 | Primary text, darkest |

### Carbon Blue Palette (Primary/Interactive)

| Token | Hex | Usage |
|-------|-----|-------|
| Blue 10 | #edf5ff | Subtle blue backgrounds |
| Blue 20 | #d0e2ff | Light blue accents |
| Blue 30 | #a6c8ff | Hover backgrounds |
| Blue 40 | #78a9ff | Secondary buttons |
| Blue 50 | #4589ff | Links (dark theme) |
| Blue 60 | #0f62fe | Primary interactive |
| Blue 70 | #0043ce | Hover primary |
| Blue 80 | #002d9c | Active primary |
| Blue 90 | #001d6c | Dark accents |
| Blue 100 | #001141 | Darkest blue |

### Carbon Support/Status Colors

| Role | Token | Hex |
|------|-------|-----|
| Error/Danger | Red 60 | #da1e28 |
| Success | Green 50 | #24a148 |
| Warning | Yellow 30 | #f1c21b |
| Info | Blue 70 | #0043ce |

### Carbon UI Tokens (White/Light Theme)

| Token | Value | Bootstrap Equivalent |
|-------|-------|---------------------|
| $ui-background | #ffffff | $body-bg |
| $ui-01 | #f4f4f4 | $gray-100 |
| $ui-02 | #ffffff | $white |
| $ui-03 | #e0e0e0 | $gray-300 |
| $text-01 | #161616 | $body-color |
| $text-02 | #525252 | $text-muted |
| $interactive-01 | #0f62fe | $primary |
| $interactive-02 | #393939 | $secondary |
| $link-01 | #0f62fe | $link-color |
| $focus | #0f62fe | $focus-ring-color |

### Bootstrap Default Colors

Bootstrap uses these default values:

| Variable | Default |
|----------|---------|
| $blue | #0d6efd |
| $primary | $blue |
| $secondary | $gray-600 |
| $success | #198754 |
| $danger | #dc3545 |
| $warning | #ffc107 |
| $info | #0dcaf0 |
| $body-color | $gray-900 |
| $body-bg | $white |

### Key Differences

- Carbon Blue 60 (#0f62fe) vs Bootstrap Blue (#0d6efd) - slightly different blues
- Carbon's Gray scale is different from Bootstrap's (Carbon uses #f4f4f4 for Gray 10, Bootstrap uses #f8f9fa for Gray 100)
- Carbon danger (#da1e28) is more saturated than Bootstrap (#dc3545)
- Carbon success (#24a148) differs from Bootstrap (#198754)
- Carbon warning (#f1c21b) is more gold vs Bootstrap's yellow (#ffc107)

## Requirements

### Requirement 1: Primary Theme Colors

**User Story:** As a site visitor, I want the site to use Carbon's primary color palette, so that the visual appearance matches Carbon Design System.

#### Acceptance Criteria

1. WHEN the primary color is used THEN the system SHALL use Blue 60 (#0f62fe)
2. WHEN the secondary color is used THEN the system SHALL use Gray 80 (#393939)
3. WHEN interactive elements are displayed THEN they SHALL use Blue 60 (#0f62fe) as the base
4. WHEN buttons and links are hovered THEN they SHALL use Blue 70 (#0043ce)
5. WHEN buttons and links are active THEN they SHALL use Blue 80 (#002d9c)

### Requirement 2: Status/Support Colors

**User Story:** As a site visitor, I want status indicators to use Carbon's support colors, so that success, error, and warning states are visually consistent with Carbon.

#### Acceptance Criteria

1. WHEN danger/error states are shown THEN the system SHALL use Red 60 (#da1e28)
2. WHEN success states are shown THEN the system SHALL use Green 50 (#24a148)
3. WHEN warning states are shown THEN the system SHALL use Yellow 30 (#f1c21b)
4. WHEN info states are shown THEN the system SHALL use Blue 70 (#0043ce)

### Requirement 3: Gray Scale

**User Story:** As a developer, I want a gray scale that matches Carbon, so that text, borders, and backgrounds have consistent neutral tones.

#### Acceptance Criteria

1. WHEN $gray-100 is used THEN the system SHALL output #f4f4f4 (Carbon Gray 10)
2. WHEN $gray-200 is used THEN the system SHALL output #e0e0e0 (Carbon Gray 20)
3. WHEN $gray-300 is used THEN the system SHALL output #c6c6c6 (Carbon Gray 30)
4. WHEN $gray-400 is used THEN the system SHALL output #a8a8a8 (Carbon Gray 40)
5. WHEN $gray-500 is used THEN the system SHALL output #8d8d8d (Carbon Gray 50)
6. WHEN $gray-600 is used THEN the system SHALL output #6f6f6f (Carbon Gray 60)
7. WHEN $gray-700 is used THEN the system SHALL output #525252 (Carbon Gray 70)
8. WHEN $gray-800 is used THEN the system SHALL output #393939 (Carbon Gray 80)
9. WHEN $gray-900 is used THEN the system SHALL output #161616 (Carbon Gray 100)

### Requirement 4: Body and Text Colors

**User Story:** As a site visitor, I want readable text with proper contrast, so that content is accessible and matches Carbon's text hierarchy.

#### Acceptance Criteria

1. WHEN body text is displayed THEN it SHALL use #161616 (Carbon text-01/Gray 100)
2. WHEN secondary/muted text is displayed THEN it SHALL use #525252 (Carbon text-02/Gray 70)
3. WHEN the body background is displayed THEN it SHALL use #ffffff (White)
4. WHEN links are displayed THEN they SHALL use #0f62fe (Carbon link-01/Blue 60)

### Requirement 5: Focus and Interactive States

**User Story:** As a site visitor using keyboard navigation, I want visible focus indicators, so that I can navigate the site accessibly.

#### Acceptance Criteria

1. WHEN an element receives focus THEN the focus ring SHALL use Blue 60 (#0f62fe)
2. WHEN interactive elements are hovered THEN they SHALL darken appropriately using Carbon's hover values
3. WHEN interactive elements are disabled THEN they SHALL use Gray 30 (#c6c6c6)

### Requirement 6: Color Palette Variables

**User Story:** As a developer, I want access to Carbon's full color palette, so that I can use consistent colors throughout the theme.

#### Acceptance Criteria

1. WHEN the $blue variable is used THEN it SHALL equal Blue 60 (#0f62fe)
2. WHEN the $red variable is used THEN it SHALL equal Red 60 (#da1e28)
3. WHEN the $green variable is used THEN it SHALL equal Green 50 (#24a148)
4. WHEN the $yellow variable is used THEN it SHALL equal Yellow 30 (#f1c21b)
5. WHEN the $cyan variable is used THEN it SHALL equal Cyan 50 (#1192e8)

### Requirement 7: Variable-Only Implementation

**User Story:** As a developer, I want color changes to be implemented through Bootstrap variable overrides only, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN colors are customized THEN the system SHALL NOT modify Bootstrap source files directly
2. WHEN color variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
4. IF a Bootstrap variable exists for a color property THEN it SHALL be used instead of custom CSS

## Non-Functional Requirements

### Accessibility

- All text colors must maintain WCAG 2.2 AA contrast requirements (4.5:1 for body text, 3:1 for large text)
- Focus indicators must be clearly visible (3:1 contrast minimum)
- Color must not be the only means of conveying information

### Maintainability

- All color overrides must be clearly documented with Carbon token references
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility

- Colors must work correctly with all Bootstrap components
- Utility classes (.text-*, .bg-*, .border-*) must reflect new colors
- Changes must not break existing Bootstrap functionality

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Dark theme colors** - Focus is on light mode only per product.md
2. **Extended color palettes** - Only core Bootstrap color variables, not all Carbon shades
3. **Component-specific colors** - Will be handled when each component is customized
4. **CSS custom properties** - Focus on Sass variable overrides

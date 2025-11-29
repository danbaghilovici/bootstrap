# Requirements Document

## Introduction

Update Bootstrap's popover component styling to match IBM Carbon Design System specifications. The popover is a contextual overlay that displays additional information or content when triggered. This update will align the component's visual appearance with Carbon's design language while maintaining Bootstrap's JavaScript functionality.

## Alignment with Product Vision

This feature directly supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." The popover is a Phase 5 component (Overlays & Advanced) in the customization priority order. Implementing Carbon-style popovers ensures visual consistency across all overlay components (modals, dropdowns, tooltips, popovers, toasts).

## Requirements

### Requirement 1: Container Styling

**User Story:** As a developer, I want the popover container to use Carbon's visual style, so that it matches the overall Carbon-inspired theme.

#### Acceptance Criteria

1. WHEN a popover is displayed THEN the system SHALL render it with a white background (`#ffffff` / `$layer`)
2. WHEN a popover is displayed THEN the system SHALL apply Carbon's drop shadow (`0 2px 2px rgba(0, 0, 0, 0.2)`)
3. WHEN a popover is displayed THEN the system SHALL use a 2px border radius (Carbon standard)
4. WHEN a popover is displayed THEN the system SHALL apply a subtle border (`$border-subtle` / `#e0e0e0`)
5. WHEN a popover is displayed THEN the system SHALL use Carbon text color (`#161616` / `$text-primary`)

### Requirement 2: Typography and Spacing

**User Story:** As a developer, I want the popover to use Carbon's typography and spacing, so that content is readable and consistent.

#### Acceptance Criteria

1. WHEN a popover is displayed THEN the system SHALL use 14px (0.875rem) font size for body text
2. WHEN a popover header is present THEN the system SHALL use 16px (1rem) font size
3. WHEN a popover is displayed THEN the system SHALL use 16px (1rem) padding for body content
4. WHEN a popover header is present THEN the system SHALL use 8px (0.5rem) vertical padding and 16px horizontal padding
5. IF a popover exceeds max-width THEN the system SHALL constrain it to 368px (Carbon max-inline-size)

### Requirement 3: Arrow/Caret Styling

**User Story:** As a developer, I want the popover arrow to match Carbon's caret design, so that it visually connects to the trigger element.

#### Acceptance Criteria

1. WHEN a popover with arrow is displayed THEN the system SHALL render the arrow with 12px width and 6px height
2. WHEN a popover is displayed THEN the arrow SHALL match the popover background color
3. WHEN a popover is displayed THEN the arrow border SHALL match the popover border color
4. WHEN the popover is positioned in any direction (top/bottom/left/right) THEN the arrow SHALL point toward the trigger element

### Requirement 4: Header Styling

**User Story:** As a developer, I want the popover header to have a distinct but subtle appearance, so that it's clear but not distracting.

#### Acceptance Criteria

1. WHEN a popover header is present THEN the system SHALL use the same background color as the body (no separate header background)
2. WHEN a popover header is present THEN the system SHALL apply a subtle bottom border separating header from body
3. WHEN a popover header is present THEN the system SHALL use Carbon's text-primary color for header text

### Requirement 5: CSS Custom Properties

**User Story:** As a developer, I want popover styles to use CSS custom properties, so that they can be customized at runtime and adapt to theme changes.

#### Acceptance Criteria

1. WHEN popover styles are compiled THEN the system SHALL define CSS custom properties on the `.popover` class
2. WHEN CSS custom properties are defined THEN the system SHALL follow Bootstrap's naming convention (`--bs-popover-*`)
3. WHEN CSS custom properties reference colors THEN they SHALL reference theme-level variables (e.g., `$body-color`, `$body-bg`)

## Non-Functional Requirements

### Performance
- Popover styles should add minimal CSS overhead (< 1KB uncompressed)
- No additional JavaScript required (uses Bootstrap's existing popover.js)

### Accessibility
- Text contrast must meet WCAG 2.1 AA standards (already achieved with Carbon colors)
- Focus states must remain visible (handled by Bootstrap's JS)

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles only in `scss/carbon/_popover.scss` when variables are insufficient
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 popover JavaScript
- Must support all popover placements (top, bottom, left, right, auto)
- Must work with both header + body and body-only popovers

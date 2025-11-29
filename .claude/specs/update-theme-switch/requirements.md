# Requirements Document

## Introduction

Update Bootstrap's switch component (`.form-switch`) to match IBM Carbon Design System's toggle styling. The switch/toggle is a binary control that allows users to turn options on or off. This update will align the component's visual appearance with Carbon's design language while maintaining Bootstrap's JavaScript functionality and HTML structure.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Switches/toggles are part of the Forms component group and are commonly used in settings and preferences interfaces. Implementing Carbon-style toggles ensures visual consistency across all form controls.

## Requirements

### Requirement 1: Track Styling

**User Story:** As a developer, I want the switch track to use Carbon's dimensions and colors, so that it matches the Carbon toggle appearance.

#### Acceptance Criteria

1. WHEN a switch is displayed THEN the track SHALL have dimensions of 48px wide × 24px tall (default size)
2. WHEN a switch is displayed THEN the track SHALL have a border-radius of 12px (pill shape)
3. WHEN a switch is in the OFF state THEN the track background SHALL use Carbon's `$toggle-off` color (`#8d8d8d` Gray 50)
4. WHEN a switch is in the ON state THEN the track background SHALL use Carbon's `$support-success` color (`#24a148` Green 50)
5. WHEN a switch is displayed THEN the track SHALL have no border in interactive states

### Requirement 2: Handle/Knob Styling

**User Story:** As a developer, I want the switch handle to use Carbon's dimensions and positioning, so that the toggle feels properly weighted.

#### Acceptance Criteria

1. WHEN a switch is displayed THEN the handle SHALL be a circle with 18px diameter
2. WHEN a switch is displayed THEN the handle SHALL be white (`#ffffff`)
3. WHEN a switch is in the OFF state THEN the handle SHALL be positioned 3px from the left edge
4. WHEN a switch is in the ON state THEN the handle SHALL translate 24px to the right
5. WHEN the handle moves THEN it SHALL transition smoothly with Carbon's motion timing

### Requirement 3: Focus State

**User Story:** As a developer, I want the switch focus state to follow Carbon's accessibility pattern, so that keyboard users can see which element is focused.

#### Acceptance Criteria

1. WHEN a switch receives focus THEN the system SHALL display a 2px solid outline using Carbon's focus color (`#0f62fe` Blue 60)
2. WHEN a switch receives focus THEN the outline SHALL have a 1px offset from the track
3. WHEN a switch loses focus THEN the outline SHALL be removed

### Requirement 4: Disabled State

**User Story:** As a developer, I want disabled switches to be visually distinct, so that users understand they cannot interact with them.

#### Acceptance Criteria

1. WHEN a switch is disabled THEN the track background SHALL use Carbon's disabled color (`#c6c6c6` Gray 30)
2. WHEN a switch is disabled THEN the handle color SHALL be dimmed (`#8d8d8d` Gray 50)
3. WHEN a switch is disabled THEN the cursor SHALL be `not-allowed`
4. WHEN a switch is disabled THEN the label text SHALL use Carbon's `$text-disabled` color (`#c6c6c6`)

### Requirement 5: Size Variant

**User Story:** As a developer, I want a small switch variant, so that I can use it in compact layouts.

#### Acceptance Criteria

1. WHEN a small switch variant is used THEN the track SHALL be 32px wide × 16px tall
2. WHEN a small switch variant is used THEN the handle SHALL be 10px diameter
3. WHEN a small switch is in the ON state THEN the handle SHALL translate 16px to the right
4. WHEN a small switch variant is used THEN all other styling (colors, focus) SHALL remain consistent

### Requirement 6: CSS Custom Properties

**User Story:** As a developer, I want switch styles to use CSS custom properties, so that they can be customized at runtime.

#### Acceptance Criteria

1. WHEN switch styles are compiled THEN the system SHALL define CSS custom properties following Bootstrap's naming convention
2. WHEN CSS custom properties reference colors THEN they SHALL use theme-level variables for consistency

## Non-Functional Requirements

### Performance
- Switch styles should add minimal CSS overhead (< 1KB uncompressed)
- Transitions should use CSS transforms for GPU acceleration

### Accessibility
- Focus states must be clearly visible with sufficient contrast
- Color contrast between track states must meet WCAG 2.1 AA standards
- Switch must work with keyboard navigation (handled by Bootstrap's HTML)

### Maintainability
- Primary customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_switch.scss` for complex styling not achievable via variables
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 switch markup (`.form-switch` with `.form-check-input`)
- Must maintain Bootstrap's checkbox-based implementation
- Must support RTL layouts (handle position reversed)

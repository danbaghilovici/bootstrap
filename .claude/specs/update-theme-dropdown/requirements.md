# Requirements Document

## Introduction

Update Bootstrap's dropdown component to match IBM Carbon Design System's dropdown styling. Dropdowns are interactive menus that allow users to select options from a list. This update will align the dropdown trigger, menu container, and menu items with Carbon's design language, featuring consistent field styling, proper hover/focus states, and a clean menu appearance with drop shadow.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Dropdowns are essential UI components used in navigation, forms, and contextual menus. Implementing Carbon-style dropdowns ensures visual consistency with already-implemented form controls and maintains the professional, systematic design language.

## Requirements

### Requirement 1: Dropdown Menu Container Styling

**User Story:** As a developer, I want the dropdown menu container to use Carbon's styling, so that it matches the Carbon dropdown appearance.

#### Acceptance Criteria

1. WHEN a dropdown menu is displayed THEN the background color SHALL be white (`#ffffff`)
2. WHEN a dropdown menu is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)
3. WHEN a dropdown menu is displayed THEN the border-radius SHALL be 0 (Carbon uses square corners)
4. WHEN a dropdown menu is displayed THEN the box-shadow SHALL be `0 2px 6px rgba(0, 0, 0, 0.3)` (Carbon drop shadow)
5. WHEN a dropdown menu is displayed THEN the border SHALL be 1px solid `#e0e0e0` (Carbon border-subtle)

### Requirement 2: Dropdown Menu Item Styling

**User Story:** As a developer, I want dropdown menu items to use Carbon's typography and spacing, so that they are readable and well-proportioned.

#### Acceptance Criteria

1. WHEN a dropdown item is displayed THEN the padding SHALL be 0.5rem (8px) vertical and 1rem (16px) horizontal
2. WHEN a dropdown item is displayed THEN the font size SHALL be 0.875rem (14px)
3. WHEN a dropdown item is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)

### Requirement 3: Dropdown Menu Item Hover State

**User Story:** As a developer, I want dropdown items to have visible hover states, so that users can identify the item they're about to select.

#### Acceptance Criteria

1. WHEN a dropdown item is hovered THEN the background color SHALL be `#e0e0e0` (Carbon hover-ui)
2. WHEN a dropdown item is hovered THEN the text color SHALL remain `#161616`

### Requirement 4: Dropdown Menu Item Active/Selected State

**User Story:** As a developer, I want the active/selected dropdown item to be visually distinct, so that users know which option is currently selected.

#### Acceptance Criteria

1. WHEN a dropdown item is active/selected THEN the background color SHALL be `#0f62fe` (Carbon Blue 60)
2. WHEN a dropdown item is active/selected THEN the text color SHALL be white (`#ffffff`)

### Requirement 5: Dropdown Menu Item Disabled State

**User Story:** As a developer, I want disabled dropdown items to be visually indicated, so that users understand they cannot be selected.

#### Acceptance Criteria

1. WHEN a dropdown item is disabled THEN the text color SHALL be `#c6c6c6` (Carbon text-disabled)
2. WHEN a dropdown item is disabled THEN the background SHALL remain unchanged
3. WHEN a dropdown item is disabled THEN the cursor SHALL indicate non-interactive state

### Requirement 6: Dropdown Menu Item Focus State

**User Story:** As a developer, I want focused dropdown items to have clear focus indicators, so that keyboard users can navigate the menu.

#### Acceptance Criteria

1. WHEN a dropdown item receives focus THEN it SHALL display a 2px solid `#0f62fe` outline
2. WHEN a dropdown item receives focus THEN the outline offset SHALL be -2px (inset)

### Requirement 7: Dropdown Divider Styling

**User Story:** As a developer, I want dropdown dividers to match Carbon's subtle styling, so that sections are clearly separated.

#### Acceptance Criteria

1. WHEN a dropdown divider is displayed THEN the color SHALL be `#e0e0e0` (Carbon border-subtle)
2. WHEN a dropdown divider is displayed THEN the margin SHALL be 0.5rem (8px) vertical

### Requirement 8: Dropdown Header Styling

**User Story:** As a developer, I want dropdown headers to match Carbon's typography, so that sections are clearly labeled.

#### Acceptance Criteria

1. WHEN a dropdown header is displayed THEN the font size SHALL be 0.75rem (12px)
2. WHEN a dropdown header is displayed THEN the text color SHALL be `#525252` (Carbon text-secondary)
3. WHEN a dropdown header is displayed THEN the font weight SHALL be 600 (semibold)

## Non-Functional Requirements

### Performance
- Dropdown styles should add minimal CSS overhead (< 1KB uncompressed)
- No additional JavaScript required beyond Bootstrap's dropdown plugin

### Accessibility
- Focus states must be clearly visible (2px outline meets visibility requirements)
- Color contrast ratios must meet WCAG AA standards
- Keyboard navigation must work correctly
- Disabled items must be distinguishable

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_dropdown.scss` only if needed for focus states
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 dropdown markup and JavaScript
- Must support all dropdown variations (menu, split button, dropup, dropend, dropstart)
- Must work with dark dropdown variant (`.dropdown-menu-dark`)

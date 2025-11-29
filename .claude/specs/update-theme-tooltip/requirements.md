# Requirements Document

## Introduction

Update Bootstrap's tooltip component (`.tooltip`) to match IBM Carbon Design System's tooltip styling. Tooltips provide contextual information upon hover or focus. This update will align the component's visual appearance with Carbon's design language, featuring a dark background with white text, while maintaining Bootstrap's JavaScript functionality and HTML structure.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Tooltips are commonly used throughout web applications to provide contextual help and additional information. Implementing Carbon-style tooltips ensures visual consistency across all interactive components and maintains the professional, systematic design language.

## Requirements

### Requirement 1: Tooltip Container Styling

**User Story:** As a developer, I want the tooltip container to use Carbon's colors and dimensions, so that it matches the Carbon tooltip appearance.

#### Acceptance Criteria

1. WHEN a tooltip is displayed THEN the background color SHALL be `#393939` (Carbon Gray 80)
2. WHEN a tooltip is displayed THEN the text color SHALL be `#ffffff` (white)
3. WHEN a tooltip is displayed THEN the maximum width SHALL be 288px
4. WHEN a tooltip is displayed THEN the border-radius SHALL be 2px (Carbon standard)
5. WHEN a tooltip is displayed THEN the opacity SHALL be 1 (fully opaque, not translucent)

### Requirement 2: Typography Styling

**User Story:** As a developer, I want the tooltip text to use Carbon's typography specifications, so that it is readable and consistent with the design system.

#### Acceptance Criteria

1. WHEN a tooltip is displayed THEN the font size SHALL be 0.875rem (14px)
2. WHEN a tooltip is displayed THEN the font weight SHALL be 400 (regular)
3. WHEN a tooltip is displayed THEN the line height SHALL be approximately 1.29

### Requirement 3: Spacing/Padding

**User Story:** As a developer, I want the tooltip to have appropriate padding, so that the text has proper breathing room.

#### Acceptance Criteria

1. WHEN a tooltip is displayed THEN the vertical padding SHALL be 0.5rem (8px)
2. WHEN a tooltip is displayed THEN the horizontal padding SHALL be 1rem (16px)

### Requirement 4: Arrow/Caret Styling

**User Story:** As a developer, I want the tooltip arrow to match Carbon's caret specifications, so that it visually connects the tooltip to its trigger element.

#### Acceptance Criteria

1. WHEN a tooltip is displayed THEN the arrow width SHALL be 8px (0.5rem)
2. WHEN a tooltip is displayed THEN the arrow height SHALL be 4px (0.25rem)
3. WHEN a tooltip is displayed THEN the arrow color SHALL match the tooltip background (`#393939`)

### Requirement 5: Shadow/Elevation

**User Story:** As a developer, I want the tooltip to have appropriate elevation, so that it visually stands out from the page content.

#### Acceptance Criteria

1. WHEN a tooltip is displayed THEN the box-shadow SHALL be `0 2px 6px rgba(0, 0, 0, 0.3)` (Carbon drop shadow)

## Non-Functional Requirements

### Performance
- Tooltip styles should add minimal CSS overhead (< 0.5KB uncompressed)
- No additional JavaScript required beyond Bootstrap's tooltip plugin

### Accessibility
- Text contrast ratio must meet WCAG 2.1 AA standards (white on #393939 = 7.74:1, passes AAA)
- Tooltip must remain accessible via keyboard focus
- Tooltip content must be announced by screen readers

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_tooltip.scss` only if needed for complex styling
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 tooltip markup and JavaScript
- Must support all tooltip placements (top, bottom, left, right)
- Must work with both hover and focus triggers

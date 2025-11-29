# Requirements Document

## Introduction

Update Bootstrap's toast component to match IBM Carbon Design System's notification styling. Toasts are ephemeral messages that appear briefly to communicate status or feedback. This update will align the toast component with Carbon's notification design language, featuring a left accent border for status indication, consistent typography, and proper close button styling, while maintaining Bootstrap's JavaScript functionality.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Toasts are essential for user feedback in interactive applications. Implementing Carbon-style toasts ensures visual consistency with the already-implemented alerts (which use Carbon's inline notification pattern) and maintains the professional, systematic design language.

## Requirements

### Requirement 1: Toast Container Styling

**User Story:** As a developer, I want the toast container to use Carbon's notification colors and styling, so that it matches the Carbon notification appearance.

#### Acceptance Criteria

1. WHEN a toast is displayed THEN the background color SHALL be white (`#ffffff`)
2. WHEN a toast is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)
3. WHEN a toast is displayed THEN the border-radius SHALL be 0 (Carbon uses square corners)
4. WHEN a toast is displayed THEN the box-shadow SHALL be `0 2px 6px rgba(0, 0, 0, 0.3)` (Carbon drop shadow)
5. WHEN a toast is displayed THEN the border SHALL be 1px solid `#e0e0e0` (Carbon border-subtle)

### Requirement 2: Toast Left Accent Border

**User Story:** As a developer, I want toasts to have a left accent border like Carbon notifications, so that status is immediately visible.

#### Acceptance Criteria

1. WHEN a toast is displayed THEN it SHALL have a 3px left border for status indication
2. WHEN a default toast is displayed THEN the left border color SHALL be `#0f62fe` (Carbon Blue 60)
3. WHEN a success toast (`.toast-success`) is displayed THEN the left border color SHALL be `#24a148` (Carbon Green 50)
4. WHEN a warning toast (`.toast-warning`) is displayed THEN the left border color SHALL be `#f1c21b` (Carbon Yellow 30)
5. WHEN an error/danger toast (`.toast-danger`) is displayed THEN the left border color SHALL be `#da1e28` (Carbon Red 60)
6. WHEN an info toast (`.toast-info`) is displayed THEN the left border color SHALL be `#0043ce` (Carbon Blue 70)

### Requirement 3: Toast Header Styling

**User Story:** As a developer, I want the toast header to use Carbon's typography and styling, so that it provides clear message hierarchy.

#### Acceptance Criteria

1. WHEN a toast header is displayed THEN the background SHALL be white (`#ffffff`)
2. WHEN a toast header is displayed THEN the border-bottom SHALL be 1px solid `#e0e0e0`
3. WHEN a toast header is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)
4. WHEN a toast header contains a timestamp (.text-body-secondary) THEN the color SHALL be `#525252` (Carbon Gray 70)

### Requirement 4: Toast Body Styling

**User Story:** As a developer, I want the toast body to use Carbon's typography, so that message content is readable.

#### Acceptance Criteria

1. WHEN a toast body is displayed THEN the font size SHALL be 0.875rem (14px)
2. WHEN a toast body is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)
3. WHEN a toast body is displayed THEN the padding SHALL be 0.75rem (12px)

### Requirement 5: Toast Close Button Styling

**User Story:** As a developer, I want the close button to match Carbon's styling, so that it is clearly visible but not distracting.

#### Acceptance Criteria

1. WHEN a toast close button is displayed THEN it SHALL be positioned in the header
2. WHEN a toast close button receives focus THEN it SHALL display a 2px solid `#0f62fe` focus outline
3. WHEN a toast close button receives focus THEN the outline offset SHALL be -2px

### Requirement 6: Toast Sizing

**User Story:** As a developer, I want toasts to have appropriate sizing, so that they display content well without being too large.

#### Acceptance Criteria

1. WHEN a toast is displayed THEN the max-width SHALL be 350px
2. WHEN a toast is displayed THEN the minimum width SHALL allow readable content

## Non-Functional Requirements

### Performance
- Toast styles should add minimal CSS overhead (< 1KB uncompressed)
- No additional JavaScript required beyond Bootstrap's toast plugin

### Accessibility
- Close button must be keyboard accessible
- Toast must be dismissible via close button
- Focus must be visible on interactive elements
- Sufficient color contrast for all text (WCAG AA)

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_toast.scss` for left border and variant styles
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 toast markup and JavaScript
- Must support stacked toasts in toast container
- Must work with autohide and manual dismiss options

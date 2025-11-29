# Requirements Document

## Introduction

Update Bootstrap's modal component (`.modal`) to match IBM Carbon Design System's modal styling. Modals are dialog overlays that require user interaction before returning to the main content. This update will align the component's visual appearance with Carbon's design language, featuring a clean white container with subtle borders and a dark backdrop, while maintaining Bootstrap's JavaScript functionality and HTML structure.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Modals are essential UI components used for confirmations, forms, and focused content. Implementing Carbon-style modals ensures visual consistency across all overlay components (tooltips, popovers, modals) and maintains the professional, systematic design language.

## Requirements

### Requirement 1: Modal Container Styling

**User Story:** As a developer, I want the modal container to use Carbon's colors and styling, so that it matches the Carbon modal appearance.

#### Acceptance Criteria

1. WHEN a modal is displayed THEN the content background SHALL be white (`#ffffff`)
2. WHEN a modal is displayed THEN the content text color SHALL be `#161616` (Carbon text-primary)
3. WHEN a modal is displayed THEN the border SHALL be 1px solid `#e0e0e0` (Carbon border-subtle)
4. WHEN a modal is displayed THEN the border-radius SHALL be 0 (Carbon uses square corners for modals)
5. WHEN a modal is displayed THEN the box-shadow SHALL be `0 2px 6px rgba(0, 0, 0, 0.3)` (Carbon drop shadow)

### Requirement 2: Modal Backdrop/Overlay Styling

**User Story:** As a developer, I want the modal backdrop to use Carbon's overlay specifications, so that the modal stands out properly from the page content.

#### Acceptance Criteria

1. WHEN a modal is displayed THEN the backdrop background SHALL be `#161616` (Carbon Gray 100)
2. WHEN a modal is displayed THEN the backdrop opacity SHALL be 0.5 (50%)

### Requirement 3: Modal Header Styling

**User Story:** As a developer, I want the modal header to use Carbon's typography and spacing, so that it provides clear hierarchy.

#### Acceptance Criteria

1. WHEN a modal header is displayed THEN the padding SHALL be 1rem (16px) on all sides
2. WHEN a modal header is displayed THEN the border-bottom SHALL be 1px solid `#e0e0e0`
3. WHEN a modal header is displayed THEN the title font size SHALL be 1.25rem (20px, heading-03)
4. WHEN a modal header is displayed THEN the title font weight SHALL be 400

### Requirement 4: Modal Body Styling

**User Story:** As a developer, I want the modal body to use Carbon's spacing, so that content has proper breathing room.

#### Acceptance Criteria

1. WHEN a modal body is displayed THEN the padding SHALL be 1rem (16px) on all sides
2. WHEN a modal body is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)

### Requirement 5: Modal Footer Styling

**User Story:** As a developer, I want the modal footer to use Carbon's styling for action buttons area, so that it clearly separates from the body content.

#### Acceptance Criteria

1. WHEN a modal footer is displayed THEN the padding SHALL be 1rem (16px)
2. WHEN a modal footer is displayed THEN the border-top SHALL be 1px solid `#e0e0e0`
3. WHEN a modal footer is displayed THEN the background SHALL be white (`#ffffff`)

### Requirement 6: Modal Sizes

**User Story:** As a developer, I want standard modal size options, so that I can choose appropriate sizes for different content.

#### Acceptance Criteria

1. WHEN a small modal (`.modal-sm`) is used THEN the max-width SHALL be 448px
2. WHEN a default modal is used THEN the max-width SHALL be 576px
3. WHEN a large modal (`.modal-lg`) is used THEN the max-width SHALL be 672px
4. WHEN an extra-large modal (`.modal-xl`) is used THEN the max-width SHALL be 896px

### Requirement 7: Close Button Styling

**User Story:** As a developer, I want the close button to match Carbon's styling, so that it is clearly visible but not distracting.

#### Acceptance Criteria

1. WHEN a modal close button is displayed THEN it SHALL be positioned in the top-right corner
2. WHEN a modal close button receives focus THEN it SHALL display a 2px solid blue (`#0f62fe`) focus outline

## Non-Functional Requirements

### Performance
- Modal styles should add minimal CSS overhead (< 1KB uncompressed)
- No additional JavaScript required beyond Bootstrap's modal plugin

### Accessibility
- Focus must be trapped within the modal when open
- Close button must be keyboard accessible
- Modal must be dismissible via Escape key
- Sufficient color contrast for all text (handled by Bootstrap)

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_modal.scss` only if needed for complex styling
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 modal markup and JavaScript
- Must support all modal sizes (sm, default, lg, xl)
- Must support scrollable and centered modal variants
- Must work with static backdrop option

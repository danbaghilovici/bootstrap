# Requirements Document

## Introduction

Update Bootstrap's form components to match IBM Carbon Design System's form styling. Forms are fundamental UI elements for user input and interaction. This update will align text inputs, select dropdowns, labels, helper text, and validation states with Carbon's design language, featuring clean fields with subtle bottom borders, consistent field heights, and clear focus/error states.

## Alignment with Product Vision

This feature supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Forms are essential for contact pages, search functionality, and interactive elements. Implementing Carbon-style forms ensures visual consistency across all input components and maintains the professional, systematic design language.

## Requirements

### Requirement 1: Form Field Sizing

**User Story:** As a developer, I want form fields to match Carbon's height specifications, so that inputs have consistent sizing across all form elements.

#### Acceptance Criteria

1. WHEN a default form input is displayed THEN the height SHALL be approximately 40px (medium size)
2. WHEN a small form input (`.form-control-sm`) is displayed THEN the height SHALL be approximately 32px
3. WHEN a large form input (`.form-control-lg`) is displayed THEN the height SHALL be approximately 48px
4. WHEN a form select is displayed THEN it SHALL match the corresponding input height for each size variant

### Requirement 2: Form Field Colors and Background

**User Story:** As a developer, I want form fields to use Carbon's color palette, so that they match the overall design system.

#### Acceptance Criteria

1. WHEN a form field is displayed THEN the background color SHALL be white (`#ffffff`)
2. WHEN a form field is displayed THEN the text color SHALL be `#161616` (Carbon text-primary)
3. WHEN a form field has a placeholder THEN the placeholder color SHALL be `#6f6f6f` (Carbon Gray 60)
4. WHEN a form field is disabled THEN the background color SHALL be `#f4f4f4` (Carbon Gray 10)
5. WHEN a form field is disabled THEN the text color SHALL be `#c6c6c6` (Carbon disabled text)

### Requirement 3: Form Field Borders

**User Story:** As a developer, I want form fields to use Carbon's border styling, so that they have the characteristic Carbon appearance.

#### Acceptance Criteria

1. WHEN a form field is displayed THEN the border-radius SHALL be 0 (square corners)
2. WHEN a form field is displayed THEN it SHALL have a border of 1px solid `#8d8d8d` (Carbon Gray 50)
3. WHEN a form field is hovered THEN the border color SHALL change to `#161616` (Carbon Gray 100)

### Requirement 4: Form Field Focus States

**User Story:** As a developer, I want form fields to have clear focus indicators, so that keyboard users can easily identify the active field.

#### Acceptance Criteria

1. WHEN a form field receives focus THEN it SHALL display a 2px solid `#0f62fe` (Carbon Blue 60) outline
2. WHEN a form field receives focus THEN the outline offset SHALL be -2px (inset)
3. WHEN a form field receives focus THEN any box-shadow focus ring SHALL be disabled

### Requirement 5: Form Label Styling

**User Story:** As a developer, I want form labels to match Carbon's typography, so that they provide clear field identification.

#### Acceptance Criteria

1. WHEN a form label is displayed THEN the font size SHALL be 0.75rem (12px)
2. WHEN a form label is displayed THEN the font weight SHALL be 400
3. WHEN a form label is displayed THEN the color SHALL be `#525252` (Carbon Gray 70)
4. WHEN a form label is displayed THEN the margin-bottom SHALL be 0.5rem (8px)

### Requirement 6: Helper Text Styling

**User Story:** As a developer, I want helper text to match Carbon's specifications, so that contextual information is clearly displayed.

#### Acceptance Criteria

1. WHEN helper text (`.form-text`) is displayed THEN the font size SHALL be 0.75rem (12px)
2. WHEN helper text is displayed THEN the color SHALL be `#525252` (Carbon Gray 70)
3. WHEN helper text is displayed THEN the margin-top SHALL be 0.25rem (4px)

### Requirement 7: Validation States

**User Story:** As a developer, I want validation states to use Carbon's feedback colors, so that errors and success states are clearly communicated.

#### Acceptance Criteria

1. WHEN a form field has an error (`.is-invalid`) THEN the border color SHALL be `#da1e28` (Carbon Red 60)
2. WHEN a form field has an error THEN the focus outline SHALL be 2px solid `#da1e28`
3. WHEN error feedback text is displayed THEN the color SHALL be `#da1e28`
4. WHEN a form field is valid (`.is-valid`) THEN the border color SHALL be `#24a148` (Carbon Green 50)
5. WHEN success feedback text is displayed THEN the color SHALL be `#24a148`

### Requirement 8: Form Select Styling

**User Story:** As a developer, I want select dropdowns to match Carbon's styling, so that they are visually consistent with text inputs.

#### Acceptance Criteria

1. WHEN a form select is displayed THEN it SHALL have the same background, border, and text colors as text inputs
2. WHEN a form select is displayed THEN the border-radius SHALL be 0
3. WHEN a form select receives focus THEN it SHALL display the same 2px blue outline as text inputs
4. WHEN a form select is disabled THEN it SHALL match the disabled styling of text inputs

### Requirement 9: Input Group Styling

**User Story:** As a developer, I want input groups to match Carbon's styling, so that prepended/appended elements blend seamlessly with inputs.

#### Acceptance Criteria

1. WHEN an input group addon is displayed THEN the background SHALL be `#e0e0e0` (Carbon Gray 20)
2. WHEN an input group addon is displayed THEN the border color SHALL match the input border
3. WHEN an input group addon is displayed THEN the border-radius SHALL be 0

## Non-Functional Requirements

### Performance
- Form styles should add minimal CSS overhead
- No additional JavaScript required beyond Bootstrap's form validation

### Accessibility
- Focus states must be clearly visible (2px outline meets visibility requirements)
- Color contrast ratios must meet WCAG AA standards
- Disabled states must be distinguishable from enabled states
- Error messages must be programmatically associated with inputs

### Maintainability
- All customizations via variable overrides in `_variables-carbon.scss`
- Custom styles in `scss/carbon/_form.scss` only if needed for complex styling
- Clear comments referencing Carbon design tokens

### Compatibility
- Must work with Bootstrap 5.3.8 form markup and JavaScript
- Must support all form control sizes (sm, default, lg)
- Must support input groups, floating labels, and validation states
- Must work with form-check components (checkboxes, radios)

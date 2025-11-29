# Requirements Document: Update Theme Borders

## Introduction

This specification defines the requirements for updating the Bootstrap theme's border-radius styling across all components to align with IBM's Carbon Design System. Carbon uses rectangular (0 border-radius) elements for most UI components, creating a clean, industrial aesthetic. This change will transform Bootstrap's default rounded corners to square corners throughout the theme.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Border radius is a fundamental visual characteristic that significantly impacts the overall design language
2. **"Phase 1 - Foundation"** - Borders & Shadows is item #4 in the component priority order
3. **"Minimal"** - Square corners align with Carbon's clean, professional aesthetic
4. **"Systematic"** - Using consistent border-radius values (0) creates visual coherence

## Background: Carbon vs Bootstrap Borders

### Carbon Design Characteristics

Carbon Design System uses rectangular elements with 0 border-radius for most components:
- Buttons, form inputs, cards, modals, alerts: 0px border-radius
- Most containers and interactive elements: 0px border-radius

Exceptions in Carbon (remain rounded):
- Radio buttons: circular
- Toggle switches: pill-shaped ends
- Specific pill/tag elements

### Bootstrap Defaults

Bootstrap uses graduated border-radius values:
- `$border-radius`: 0.375rem (6px)
- `$border-radius-sm`: 0.25rem (4px)
- `$border-radius-lg`: 0.5rem (8px)
- `$border-radius-xl`: 1rem (16px)
- `$border-radius-xxl`: 2rem (32px)
- `$border-radius-pill`: 50rem (fully rounded)

## Assumptions and Constraints

### Assumptions
- Bootstrap version 5.3.x is in use
- Sass compilation pipeline is configured
- Variable overrides occur before Bootstrap imports
- Target browsers support modern CSS

### Constraints
- Cannot modify Bootstrap source files directly
- Must maintain backward compatibility with utility classes
- Must preserve accessibility of interactive elements

## Requirements

### Requirement 1: Base Border Radius Variables

**User Story:** As a site visitor, I want all UI elements to have consistent square corners matching Carbon's design language, so that the site has a cohesive, professional appearance.

#### Acceptance Criteria

1. WHEN any component using the base `$border-radius` is rendered THEN the system SHALL display the element with 0px border-radius
2. WHEN any small component using `$border-radius-sm` is rendered THEN the system SHALL display the element with 0px border-radius
3. WHEN any large component using `$border-radius-lg` is rendered THEN the system SHALL display the element with 0px border-radius
4. WHEN any extra-large component using `$border-radius-xl` is rendered THEN the system SHALL display the element with 0px border-radius
5. WHEN any xxl component using `$border-radius-xxl` is rendered THEN the system SHALL display the element with 0px border-radius
6. IF an element uses `$border-radius-pill` THEN the system SHALL display the element with fully rounded ends (50rem)

### Requirement 2: Form Elements

**User Story:** As a site visitor, I want form inputs, selects, and other form elements to have square corners, so that forms match the Carbon design language.

#### Acceptance Criteria

1. WHEN a text input field is rendered THEN the system SHALL display it with 0px border-radius on all corners
2. WHEN a select dropdown is rendered THEN the system SHALL display it with 0px border-radius
3. WHEN a textarea is rendered THEN the system SHALL display it with 0px border-radius
4. WHEN a checkbox (form-check-input) is rendered THEN the system SHALL display it with 0px border-radius (square)
5. WHEN a radio button is rendered THEN the system SHALL display it with 50% border-radius (circular shape preserved)
6. WHEN a form switch is rendered THEN the system SHALL maintain its pill shape for usability

### Requirement 3: Navigation Components

**User Story:** As a site visitor, I want navigation elements to have square corners matching Carbon's navigation patterns, so that the site navigation is visually consistent.

#### Acceptance Criteria

1. WHEN nav tabs are rendered THEN the system SHALL display them with 0px border-radius
2. WHEN nav pills are rendered THEN the system SHALL display them with 0px border-radius
3. WHEN the navbar toggler button is rendered THEN the system SHALL display it with 0px border-radius
4. WHEN a dropdown menu is rendered THEN the system SHALL display it with 0px border-radius
5. WHEN pagination links are rendered THEN the system SHALL display them with 0px border-radius

### Requirement 4: Content Components

**User Story:** As a site visitor, I want content containers like cards and list groups to have square corners, so that content areas match the Carbon aesthetic.

#### Acceptance Criteria

1. WHEN a card component is rendered THEN the system SHALL display it with 0px border-radius
2. WHEN a list group is rendered THEN the system SHALL display it with 0px border-radius
3. WHEN an accordion component is rendered THEN the system SHALL display it with 0px border-radius
4. WHEN an alert component is rendered THEN the system SHALL display it with 0px border-radius
5. WHEN a badge is rendered THEN the system SHALL display it with 0px border-radius

### Requirement 5: Overlay Components

**User Story:** As a site visitor, I want overlay components like modals and tooltips to have square corners, so that all UI layers are visually consistent.

#### Acceptance Criteria

1. WHEN a modal dialog is rendered THEN the system SHALL display it with 0px border-radius
2. WHEN a tooltip is rendered THEN the system SHALL display it with 0px border-radius
3. WHEN a popover is rendered THEN the system SHALL display it with 0px border-radius
4. WHEN a toast notification is rendered THEN the system SHALL display it with 0px border-radius

### Requirement 6: Miscellaneous Components

**User Story:** As a site visitor, I want other UI elements to have consistent square corners where appropriate.

#### Acceptance Criteria

1. WHEN a progress bar is rendered THEN the system SHALL display it with 0px border-radius
2. WHEN an image thumbnail is rendered THEN the system SHALL display it with 0px border-radius
3. IF a breadcrumb has background styling THEN the system SHALL display it with 0px border-radius

### Requirement 7: Remove Rounded Utility Classes

**User Story:** As a developer, I want the rounded utility classes (`.rounded-pill`, `.rounded-circle`) removed from the generated CSS, so that the theme maintains a consistent square design language without unused rounded utilities.

#### Acceptance Criteria

1. WHEN CSS is compiled THEN the system SHALL NOT generate `.rounded-pill` utility class
2. WHEN CSS is compiled THEN the system SHALL NOT generate `.rounded-circle` utility class
3. WHEN the `.rounded-0` utility is used THEN it SHALL continue to function correctly
4. WHEN numbered `.rounded-1` through `.rounded-5` utilities are used THEN they SHALL all apply 0px border-radius
5. IF a developer needs rounded elements THEN they SHALL use custom inline styles or custom CSS classes

### Requirement 8: Bootstrap-Approved Customization Methods

**User Story:** As a developer, I want border changes implemented through Bootstrap's approved customization methods (variable overrides and utility map manipulation), so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN borders are customized THEN the system SHALL NOT require modifications to Bootstrap source files
2. WHEN border variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN utility classes are removed THEN the system SHALL use Bootstrap's utility API map manipulation
4. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
5. IF a developer inspects compiled CSS THEN border-radius values SHALL match the specified 0px values

## Non-Functional Requirements

### Maintainability

- All border overrides must be clearly documented with Carbon references
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility

- Border changes must not break any Bootstrap component functionality
- Components must remain visually accessible with proper contrast
- Form elements must remain usable with adequate click/tap targets
- WHEN viewed in Chrome, Firefox, Safari, and Edge THEN borders SHALL render identically

### Accessibility

- Form elements must remain keyboard navigable
- Focus indicators must remain visible on all interactive elements
- Screen reader compatibility must be maintained

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Custom CSS rules** - Only Bootstrap variable overrides and utility map manipulation
2. **Border colors** - Already handled by color specification
3. **Border widths** - Not changing, using Bootstrap defaults
4. **Box shadows** - Separate concern, already removed for buttons
5. **JavaScript behavior** - No JS changes needed

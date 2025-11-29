# Requirements Document: Update Theme Links

## Introduction

This specification defines the requirements for updating the Bootstrap theme's link styling to align with IBM's Carbon Design System. Carbon links feature a distinctive appearance with specific color states, underline behavior, and focus styling that creates a clean, accessible, and professional look. This change will transform Bootstrap's default link styling to match Carbon's link conventions.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Links are fundamental UI elements that significantly impact the overall design language
2. **"Phase 1 - Foundation"** - Link styling is part of the base typography and color system foundation
3. **"Accessible"** - Carbon links are designed with WCAG compliance in mind, ensuring proper contrast and focus states
4. **"Professional"** - Carbon's link styling creates a clean, technical appearance suitable for a developer portfolio

## Background: Carbon vs Bootstrap Links

### Carbon Design Characteristics

Carbon Design System links have distinct characteristics:
- **Default color**: `#0f62fe` (Blue 60 / link-01)
- **Hover color**: `#0043ce` (Blue 70 / hover-primary-text)
- **Active/Visited color**: `#161616` (Gray 100 / text-01)
- **Disabled color**: `#8d8d8d` (Gray 50 / disabled-03)
- **Underline behavior**: Standalone links show underline only on hover/focus/active; inline links always have underline
- **Focus**: 2px solid outline using focus color

### Bootstrap Defaults

Bootstrap uses:
- `$link-color`: `$primary` (typically blue)
- `$link-decoration`: `underline` (always visible)
- `$link-hover-color`: Shifted by 20% darker
- `$link-hover-decoration`: `null` (no change)

## Assumptions and Constraints

### Assumptions
- Bootstrap version 5.3.x is in use
- Sass compilation pipeline is configured
- Variable overrides occur before Bootstrap imports
- Target browsers support CSS custom properties

### Constraints
- Cannot modify Bootstrap source files directly
- Must maintain backward compatibility with existing link utility classes
- Must preserve accessibility of link elements (focus states, contrast)
- Link colors already partially defined in `_variables.scss` (lines 225-226)

## Requirements

### Requirement 1: Base Link Colors

**User Story:** As a site visitor, I want links to use Carbon's blue color palette, so that the site has a consistent, professional appearance matching Carbon's design language.

#### Acceptance Criteria

1. WHEN a link is rendered in default state THEN the system SHALL display it with color `#0f62fe` (Carbon Blue 60)
2. WHEN a link is hovered THEN the system SHALL display it with color `#0043ce` (Carbon Blue 70)
3. WHEN a link has been visited THEN the system SHALL display it with color `#161616` (Carbon Gray 100)
4. IF a link is disabled THEN the system SHALL display it with color `#8d8d8d` (Carbon Gray 50)
5. WHEN a link is in active state (being clicked) THEN the system SHALL display it with color `#161616` (Carbon Gray 100)

### Requirement 2: Link Underline Behavior

**User Story:** As a site visitor, I want links to have appropriate underline styling that indicates interactivity, so that I can easily identify clickable elements.

#### Acceptance Criteria

1. WHEN a link is rendered in default state THEN the system SHALL display an underline
2. WHEN a link is hovered THEN the system SHALL maintain the underline
3. IF the underline offset variable is set THEN the system SHALL apply appropriate spacing between text and underline
4. WHEN CSS is compiled THEN the `$link-decoration` variable SHALL be set to `underline`

### Requirement 3: Link Focus State

**User Story:** As a keyboard user, I want links to have clearly visible focus indicators, so that I can navigate the site effectively.

#### Acceptance Criteria

1. WHEN a link receives keyboard focus THEN the system SHALL display a visible focus indicator
2. WHEN a link is focused THEN the focus indicator SHALL use Carbon's focus color (`#0f62fe`)
3. IF a link has custom focus styling THEN it SHALL maintain WCAG 2.1 AA compliance for focus visibility

### Requirement 4: Visited Link State

**User Story:** As a site visitor, I want visited links to be visually distinct from unvisited links, so that I can track which content I have already viewed.

#### Acceptance Criteria

1. WHEN a link has been visited THEN the system SHALL display it with a distinct color (`#161616`)
2. WHEN a visited link is hovered THEN the system SHALL apply hover styling while maintaining visited indication
3. IF visited link styling is applied THEN it SHALL maintain adequate contrast with the background

### Requirement 5: Icon Links

**User Story:** As a site visitor, I want links with icons to be properly styled and aligned, so that the visual hierarchy is clear.

#### Acceptance Criteria

1. WHEN an icon link is rendered THEN the icon SHALL be properly aligned with the link text
2. WHEN an icon link uses Bootstrap's `.icon-link` class THEN the icon gap SHALL be appropriate
3. IF an icon link is hovered THEN the icon transform animation SHALL apply smoothly

### Requirement 6: Bootstrap-Approved Customization Methods

**User Story:** As a developer, I want link changes implemented through Bootstrap's approved customization methods (variable overrides), so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN links are customized THEN the system SHALL NOT require modifications to Bootstrap source files
2. WHEN link variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
4. IF a developer inspects compiled CSS THEN link color values SHALL match the specified Carbon colors

## Non-Functional Requirements

### Maintainability

- All link overrides must be clearly documented with Carbon references
- Changes must be isolated to the Carbon Color Overrides section in `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility

- Link changes must not break any Bootstrap component that uses links
- Links must remain visually accessible with proper contrast ratios
- WHEN viewed in Chrome, Firefox, Safari, and Edge THEN links SHALL render identically

### Accessibility

- Links must maintain keyboard navigability
- Focus indicators must be visible on all link elements
- Color contrast must meet WCAG 2.1 AA standards (4.5:1 for normal text)
- Visited vs unvisited distinction must not rely solely on color

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Button links** - `.btn-link` styling is handled separately in button specification
2. **Navigation links** - Nav-specific link styling (handled by nav components)
3. **Custom link components** - Creating new link component classes
4. **Dark mode** - Link colors for dark theme (not in current scope)
5. **JavaScript behavior** - No JS changes needed

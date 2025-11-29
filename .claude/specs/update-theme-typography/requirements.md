# Requirements Document: Update Theme Typography

## Introduction

This specification defines the requirements for updating the Bootstrap theme's typography to match IBM's Carbon Design System. The goal is to replace Bootstrap's default typography (system fonts, sizing, weights) with Carbon's typography specifications (IBM Plex fonts, Carbon type scale) while maintaining Bootstrap's customization approach through variable overrides only.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Typography is a foundational element of Carbon's visual language
2. **"IBM Plex typography"** - Explicitly listed in the project scope
3. **"Clean, readable typography for blog content"** - Carbon's typography is designed for readability
4. **"Phase 1 - Foundation"** - Typography is item #2 in the component priority order

## Requirements

### Requirement 1: IBM Plex Font Families

**User Story:** As a site visitor, I want to see content rendered in IBM Plex fonts, so that the site has a consistent Carbon Design System appearance.

#### Acceptance Criteria

1. WHEN the page loads THEN the system SHALL render body text using IBM Plex Sans font family
2. WHEN code or monospace content is displayed THEN the system SHALL render it using IBM Plex Mono font family
3. IF IBM Plex fonts fail to load THEN the system SHALL fall back to appropriate system fonts (sans-serif, monospace)
4. WHEN fonts are loaded THEN the system SHALL use variable font versions (IBM Plex Sans VF, IBM Plex Mono) for optimal performance where supported

### Requirement 2: Base Typography Scale

**User Story:** As a site visitor, I want body text to be sized according to Carbon specifications, so that content is readable and visually consistent with Carbon Design System.

#### Acceptance Criteria

1. WHEN body text is rendered THEN the system SHALL use 1rem (16px) as the base font size
2. WHEN body text is rendered THEN the system SHALL use font-weight 400 (regular)
3. WHEN body text is rendered THEN the system SHALL use line-height 1.5
4. WHEN small text (.small, small) is rendered THEN the system SHALL use 0.875rem (14px)

### Requirement 3: Heading Typography

**User Story:** As a site visitor, I want headings to follow Carbon's type scale, so that the visual hierarchy is clear and consistent with Carbon Design System.

#### Acceptance Criteria

1. WHEN h1 is rendered THEN the system SHALL use font-size 2rem, font-weight 300-400, line-height 1.25
2. WHEN h2 is rendered THEN the system SHALL use font-size 1.75rem, font-weight 400, line-height 1.28572
3. WHEN h3 is rendered THEN the system SHALL use font-size 1.25rem, font-weight 400, line-height 1.4
4. WHEN h4 is rendered THEN the system SHALL use font-size 1rem, font-weight 600, line-height 1.375
5. WHEN h5 is rendered THEN the system SHALL use font-size 0.875rem, font-weight 600, line-height 1.28572
6. WHEN h6 is rendered THEN the system SHALL use font-size 0.875rem, font-weight 600, line-height 1.28572
7. WHEN any heading is rendered THEN the system SHALL use IBM Plex Sans font family

### Requirement 4: Display Typography

**User Story:** As a site visitor, I want display headings to use Carbon-inspired styling, so that hero sections and large text have appropriate visual impact.

#### Acceptance Criteria

1. WHEN display-1 is rendered THEN the system SHALL use a large font size (3.75rem or larger) with font-weight 300
2. WHEN display headings are rendered THEN the system SHALL use line-height appropriate for large text (1.2 or lower)
3. WHEN display headings are rendered THEN the system SHALL use IBM Plex Sans font family

### Requirement 5: Utility Text Styles

**User Story:** As a site visitor, I want utility text elements (labels, captions, helper text) to follow Carbon specifications, so that supporting content is appropriately sized.

#### Acceptance Criteria

1. WHEN lead text is rendered THEN the system SHALL use font-size 1.25rem with font-weight 300
2. WHEN blockquotes are rendered THEN the system SHALL use font-size 1.25rem
3. WHEN code is rendered inline THEN the system SHALL use IBM Plex Mono at 0.875em
4. WHEN code blocks are rendered THEN the system SHALL use IBM Plex Mono at appropriate size

### Requirement 6: Variable-Only Implementation

**User Story:** As a developer, I want typography changes to be implemented through Bootstrap variable overrides only, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN typography is customized THEN the system SHALL NOT modify Bootstrap source files directly
2. WHEN typography variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications (e.g., `// Carbon: productive-heading-02`)
4. IF a Bootstrap variable exists for a typography property THEN it SHALL be used instead of custom CSS

## Non-Functional Requirements

### Performance
- Font files should be loaded efficiently (prefer variable fonts, use font-display: swap)
- Total additional font weight should not exceed 200KB for initial load
- Consider using `font-display: swap` to prevent invisible text during font loading

### Accessibility
- All text must maintain WCAG 2.2 AA contrast requirements (4.5:1 for body text, 3:1 for large text)
- Font sizes must be specified in relative units (rem/em) to support user font scaling
- Line heights must provide adequate spacing for readability

### Maintainability
- All variable overrides must be clearly documented with Carbon token references
- Changes must be isolated to `scss/_variables.scss` or a dedicated custom variables file
- Implementation must follow Bootstrap's `$component-state-property-size` naming convention

### Compatibility
- Typography must render correctly in all modern browsers (Chrome, Firefox, Safari, Edge)
- Typography must be responsive and readable at all viewport sizes
- Changes must not break existing Bootstrap components that rely on typography variables

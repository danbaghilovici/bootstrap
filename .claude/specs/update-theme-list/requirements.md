# Requirements Document: Update Theme List

## Introduction

This specification defines the requirements for updating the Bootstrap theme's list styling to align with IBM's Carbon Design System. This covers both basic HTML lists (`ol`, `ul`, `dl`) and Bootstrap's List Group component. Carbon lists use consistent typography, proper spacing, and clean visual presentation that integrates with the overall design language.

## Alignment with Product Vision

This feature directly supports the product goals outlined in product.md:

1. **"Bring Carbon Design System's visual language to a Bootstrap-based personal site"** - Lists are essential content elements for blog posts and documentation
2. **"Phase 1 - Foundation"** - List styling is part of the base typography system
3. **"Accessible"** - Proper list spacing and typography improve readability
4. **"Clean, readable typography for blog content"** - Lists are heavily used in technical blog content

## Background: Carbon vs Bootstrap Lists

### Carbon Design Characteristics

Carbon Design System lists have these characteristics:
- **Typography**: Uses `body-long-02` token (1rem/16px, line-height 1.5, weight 400)
- **Spacing**: Consistent vertical rhythm with the spacing scale
- **Nested lists**: Proper indentation hierarchy
- **List markers**: Standard browser markers with proper positioning

### Bootstrap Defaults

Bootstrap's basic lists use:
- `padding-left: 2rem` for `ol` and `ul`
- `margin-bottom: 1rem` for lists
- Nested lists have `margin-bottom: 0`

### List Group Component

Bootstrap's List Group has extensive variables for:
- Colors, backgrounds, borders
- Padding (x and y)
- Active/hover/disabled states
- Action item styling

## Assumptions and Constraints

### Assumptions
- Bootstrap version 5.3.x is in use
- Basic lists use browser default markers
- List Group component is used for interactive lists

### Constraints
- Cannot modify Bootstrap source files directly
- Basic list styling is in `_reboot.scss` which has no variables for `ol`/`ul` padding
- Must maintain backward compatibility with existing list usage

## Requirements

### Requirement 1: Basic List Typography

**User Story:** As a site visitor reading blog content, I want lists to use consistent Carbon typography, so that content is easy to read.

#### Acceptance Criteria

1. WHEN a list is rendered THEN the system SHALL display list items using the base body typography (1rem, line-height 1.5)
2. WHEN list items contain text THEN the text color SHALL be `$body-color` (#161616)
3. IF a list appears in body content THEN it SHALL maintain vertical rhythm with surrounding paragraphs

### Requirement 2: List Spacing

**User Story:** As a site visitor, I want lists to have proper spacing that matches Carbon's design language, so that content is visually organized.

#### Acceptance Criteria

1. WHEN a list is rendered THEN the system SHALL apply appropriate bottom margin for separation from following content
2. WHEN list items are rendered THEN they SHALL have consistent vertical spacing
3. IF a list is nested THEN the nested list SHALL have proper indentation

### Requirement 3: Definition Lists

**User Story:** As a content creator, I want definition lists to be properly styled, so that term/definition pairs are clearly presented.

#### Acceptance Criteria

1. WHEN a definition term (`dt`) is rendered THEN it SHALL use bold font weight
2. WHEN a definition description (`dd`) is rendered THEN it SHALL have appropriate margin
3. IF multiple definitions follow a term THEN each definition SHALL be properly spaced

### Requirement 4: List Group Colors

**User Story:** As a site visitor, I want List Group components to use Carbon's color palette, so that they match the overall theme.

#### Acceptance Criteria

1. WHEN a List Group is rendered THEN the background SHALL use the body background color
2. WHEN a List Group item is rendered THEN the text color SHALL use `$body-color`
3. WHEN a List Group item is hovered THEN the background SHALL change to a subtle highlight
4. WHEN a List Group item is active THEN it SHALL use the primary color for background
5. IF a List Group item is disabled THEN it SHALL use muted colors

### Requirement 5: List Group Borders

**User Story:** As a site visitor, I want List Group borders to match Carbon's clean aesthetic, so that lists integrate with the theme.

#### Acceptance Criteria

1. WHEN a List Group is rendered THEN borders SHALL use `$border-color` (Carbon Gray 20)
2. WHEN borders are rendered THEN they SHALL have consistent width
3. IF the theme uses 0 border-radius THEN List Group items SHALL have square corners

### Requirement 6: List Group Interactive States

**User Story:** As a site visitor interacting with action lists, I want clear visual feedback, so that I know which items are interactive.

#### Acceptance Criteria

1. WHEN a List Group action item is hovered THEN the system SHALL display hover styling
2. WHEN a List Group action item is focused THEN the system SHALL display focus indicator
3. WHEN a List Group action item is clicked THEN the system SHALL display active styling
4. IF a List Group action item is a link THEN it SHALL inherit appropriate link styling

### Requirement 7: Bootstrap-Approved Customization Methods

**User Story:** As a developer, I want list changes implemented through Bootstrap's approved customization methods, so that I can easily merge future Bootstrap updates.

#### Acceptance Criteria

1. WHEN lists are customized THEN the system SHALL NOT require modifications to Bootstrap source files
2. WHEN List Group variables are set THEN they SHALL be defined before Bootstrap imports them
3. WHEN custom values are used THEN they SHALL include comments referencing Carbon specifications
4. IF a developer inspects compiled CSS THEN list values SHALL match the specified Carbon values

## Non-Functional Requirements

### Maintainability

- All list overrides must be clearly documented with Carbon references
- Changes must be isolated to `scss/_variables.scss`
- Implementation must follow Bootstrap's variable naming conventions

### Compatibility

- List changes must not break any existing list usage
- Lists must remain visually accessible with proper contrast
- WHEN viewed in Chrome, Firefox, Safari, and Edge THEN lists SHALL render identically

### Accessibility

- Lists must maintain proper semantic structure
- List items must be readable with adequate line spacing
- Interactive list items must have visible focus states

## Out of Scope

The following are explicitly out of scope for this specification:

1. **Custom list markers** - Using standard browser markers
2. **Inline lists** - Horizontal list layouts
3. **List animations** - No transition effects for list items
4. **Dark mode** - List colors for dark theme (not in current scope)
5. **JavaScript behavior** - No JS changes needed

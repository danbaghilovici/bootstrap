# update-theme-alert - Task 1

Execute task 1 for the update-theme-alert specification.

## Task Description
Add Carbon alert variable overrides in _variables.scss

## Code Reuse
**Leverage existing code**: Existing Carbon color variables ($danger, $success, etc.)

## Requirements Reference
**Requirements**: 1.3, 3.1, 3.2, 3.5

## Usage
```
/Task:1-update-theme-alert
```

## Instructions

Execute with @spec-task-executor agent the following task: "Add Carbon alert variable overrides in _variables.scss"

```
Use the @spec-task-executor agent to implement task 1: "Add Carbon alert variable overrides in _variables.scss" for the update-theme-alert specification and include all the below context.

# Steering Context
## Steering Documents Context (Pre-loaded)

### Product Context
# Product Overview

## Purpose
A custom Bootstrap 5 theme inspired by IBM's Carbon Design System, designed for a personal website that serves as both a portfolio and blog.

## Target Users
- Primary: The site owner (Dan) for showcasing work and publishing blog content
- Secondary: Visitors viewing the portfolio and reading blog posts

## Goals
1. Bring Carbon Design System's visual language to a Bootstrap-based personal site
2. Maintain Bootstrap's utility and component structure while adopting Carbon's aesthetics
3. Create a clean, professional, accessible design suitable for technical content

## Design Philosophy
- **Systematic**: Use consistent design tokens (colors, spacing, typography)
- **Accessible**: Follow WCAG guidelines, ensure readable contrast ratios
- **Minimal**: Clean, content-focused design without unnecessary decoration
- **Professional**: Suitable for a developer/technical portfolio

## Scope
- Light mode only (for now)
- All Bootstrap components, prioritized from basic to complex
- IBM Plex typography
- Carbon color palette adapted to Bootstrap's color system

## Success Metrics
- Visual consistency with Carbon Design System principles
- Maintained Bootstrap functionality and responsive behavior
- Clean, readable typography for blog content
- Professional appearance for portfolio presentation

---

### Technology Context
# Technology Stack

## Core Framework
- **Bootstrap 5.3.8**: Base CSS framework
- **Sass (dart-sass 1.78.0)**: CSS preprocessor for source files

## Build Tools
- **npm scripts**: Task runner for build processes
- **PostCSS + Autoprefixer**: CSS vendor prefixing
- **CleanCSS**: CSS minification
- **Rollup**: JavaScript bundling
- **Terser**: JavaScript minification

## Development Tools
- **Nodemon**: File watching for development
- **Stylelint**: CSS/SCSS linting (twbs-bootstrap config)
- **ESLint**: JavaScript linting

## Testing
- **Karma + Jasmine**: JavaScript unit testing
- **sass-true**: SCSS unit testing

## Documentation
- **Astro**: Static site generator for docs

## Key Scripts
- `npm run build-theme`: Build CSS and copy to parent theme directory
- `npm run watch-theme`: Watch SCSS and rebuild on changes
- `npm run css`: Full CSS build (compile, prefix, RTL, minify)
- `npm run dist`: Build both CSS and JS

## Output
- Compiled CSS goes to `dist/css/`
- Final minified CSS copied to `../../themes/bs-carbon/static/css/styles.min.css`

## Design System Reference
- **Carbon Design System**: https://carbondesignsystem.com/
- **Bootstrap Customization Guide**: https://getbootstrap.com/docs/5.3/customize/overview/
- Primary inspiration for colors, typography, and component styling

## Customization Philosophy

### CRITICAL: Variable-Only Customization
**DO NOT modify Bootstrap source files directly.** All customizations MUST be done through:

1. **Variable overrides**: Set variables BEFORE importing Bootstrap
2. **Sass maps**: Extend or modify Bootstrap's maps
3. **CSS custom properties**: Override at runtime where applicable
4. **Utility API**: Extend utilities through the utilities map

This approach ensures:
- Clean merges when Bootstrap releases updates
- Maintainable, traceable customizations
- Full access to Bootstrap's built-in utilities and variables

### Bootstrap Resources to Use
- **All Sass variables**: https://getbootstrap.com/docs/5.3/customize/sass/
- **CSS variables**: https://getbootstrap.com/docs/5.3/customize/css-variables/
- **Color system**: https://getbootstrap.com/docs/5.3/customize/color/
- **Component variables**: Check each component's documentation for available variables
- **Utility classes**: Use Bootstrap's utility classes extensively in markup

## Carbon Design Tokens (Reference)

### Colors (Light Mode)
- **Text primary**: `#161616`
- **Text secondary**: `#525252`
- **UI background**: `#ffffff`
- **UI-01 (container bg)**: `#f4f4f4`
- **UI-02 (subtle bg)**: `#e0e0e0`
- **Border subtle**: `#e0e0e0`
- **Interactive/Primary**: `#0f62fe` (Blue 60)
- **Success**: `#24a148` (Green 50)
- **Error**: `#da1e28` (Red 60)
- **Warning**: `#f1c21b` (Yellow 30)

### Typography
- **Sans-serif**: IBM Plex Sans
- **Monospace**: IBM Plex Mono
- **Base size**: 16px (1rem)
- **Line height**: 1.5 for body text

### Spacing Scale
Carbon uses a 2px base with a scale: 2, 4, 8, 12, 16, 24, 32, 40, 48px
(Bootstrap uses 4px base: 4, 8, 16, 24, 48px - use Bootstrap's $spacer variable)

---

### Structure Context
# Project Structure

## Directory Layout
```
modules/theme/
├── scss/                    # SCSS source files
│   ├── _variables.scss      # Bootstrap variable overrides (PRIMARY customization point)
│   ├── _variables-dark.scss # Dark mode variables (not in scope currently)
│   ├── _functions.scss      # Sass functions
│   ├── _mixins.scss         # Mixin imports
│   ├── _maps.scss           # Sass maps (can extend here)
│   ├── _utilities.scss      # Utility configuration (can extend here)
│   ├── _root.scss           # CSS custom properties
│   ├── _reboot.scss         # Base element styles
│   ├── _type.scss           # Typography
│   ├── _[component].scss    # Individual component styles
│   ├── forms/               # Form-related partials
│   ├── helpers/             # Helper classes
│   ├── mixins/              # Individual mixins
│   ├── utilities/           # Utility API
│   ├── vendor/              # Third-party (RFS)
│   └── bootstrap.scss       # Main entry point
├── js/src/                  # JavaScript source
├── dist/                    # Compiled output
├── site/                    # Documentation site
└── build/                   # Build scripts
```

## Customization Strategy

### CRITICAL RULE: No Direct Bootstrap File Modifications

**All customizations MUST be done through variable overrides, NOT by editing Bootstrap's source files.**

This ensures:
- Seamless merging of Bootstrap upstream updates
- Clear separation between Bootstrap core and our customizations
- Predictable behavior when Bootstrap releases new versions

### How to Customize (Bootstrap's Recommended Approach)

#### Method 1: Variable Overrides (Primary Method)
Set variables BEFORE they're used by Bootstrap. Variables use `!default`, so setting them first takes precedence.

```scss
// In a custom variables file loaded BEFORE Bootstrap's _variables.scss
$primary: #0f62fe;  // Carbon Blue 60
$body-color: #161616;  // Carbon text primary

// Then Bootstrap's _variables.scss will NOT override these
```

#### Method 2: Map Manipulation (For Complex Changes)
Use Sass map functions to extend or modify Bootstrap's maps AFTER importing variables but BEFORE importing components.

```scss
// After @import "variables";
// Before component imports

$theme-colors: map-merge(
  $theme-colors,
  (
    "custom-color": #custom-value
  )
);
```

#### Method 3: Utility API Extension
Extend utilities through the `$utilities` map:

```scss
$utilities: map-merge(
  $utilities,
  (
    "custom-utility": (
      property: custom-property,
      values: (...)
    )
  )
);
```

### What NOT to Do
- DO NOT edit `_buttons.scss`, `_forms.scss`, or other component files directly
- DO NOT remove `!default` flags from variables
- DO NOT copy-paste and modify Bootstrap component code
- DO NOT add custom CSS that duplicates Bootstrap functionality

### Where to Make Changes
1. **`scss/_variables.scss`**: Override color, typography, spacing, and component variables
2. **`scss/_maps.scss`**: Extend Sass maps if needed
3. **`scss/_utilities.scss`**: Extend utility classes if needed
4. **Custom partial file**: For truly custom styles that don't exist in Bootstrap (create sparingly)

### Variable Naming Convention
Bootstrap uses: `$component-state-property-size`
Examples:
- `$primary`, `$secondary`, `$success`, `$danger`, etc. (theme colors)
- `$body-bg`, `$body-color` (body defaults)
- `$font-family-sans-serif`, `$font-family-monospace` (typography)
- `$btn-padding-y`, `$btn-padding-x`, `$btn-font-size` (button sizing)
- `$border-radius`, `$border-color` (borders)
- `$spacer` (spacing base unit)

### Component Priority Order
Customize in this order (basic to complex):

**Phase 1 - Foundation (Variables Only)**
1. Colors (`$primary`, `$secondary`, `$body-color`, `$body-bg`, theme colors map)
2. Typography (`$font-family-sans-serif`, `$font-family-monospace`, `$font-size-base`, `$line-height-base`)
3. Spacing (`$spacer`, `$spacers` map)
4. Borders & Shadows (`$border-radius`, `$border-color`, `$box-shadow`)

**Phase 2 - Basic Components (Variables Only)**
5. Buttons (`$btn-*` variables)
6. Forms (`$input-*`, `$form-*` variables)
7. Tables (`$table-*` variables)
8. Alerts (`$alert-*` variables)
9. Badges (`$badge-*` variables)

**Phase 3 - Navigation (Variables Only)**
10. Nav (`$nav-*` variables)
11. Navbar (`$navbar-*` variables)
12. Breadcrumb (`$breadcrumb-*` variables)
13. Pagination (`$pagination-*` variables)

**Phase 4 - Content Components (Variables Only)**
14. Cards (`$card-*` variables)
15. List groups (`$list-group-*` variables)
16. Accordion (`$accordion-*` variables)

**Phase 5 - Overlays & Advanced (Variables Only)**
17. Modal (`$modal-*` variables)
18. Dropdown (`$dropdown-*` variables)
19. Tooltip (`$tooltip-*` variables)
20. Popover (`$popover-*` variables)
21. Toast (`$toast-*` variables)

## Using Bootstrap's Utilities

**Maximize use of Bootstrap's built-in utilities** in both SCSS and HTML:

### In SCSS (via mixins and functions)
```scss
// Use Bootstrap's color functions
color: shade-color($primary, 20%);
background: tint-color($primary, 80%);

// Use Bootstrap's mixins
@include media-breakpoint-up(md) { ... }
@include button-variant($primary, $primary);
```

### In HTML (via utility classes)
Prefer utility classes over custom CSS:
```html
<div class="d-flex justify-content-between align-items-center p-3 bg-light rounded">
```

## Coding Standards

### SCSS
- NEVER modify Bootstrap source files directly
- Override variables BEFORE Bootstrap imports them
- Use Bootstrap's variables, mixins, and functions extensively
- Keep Carbon reference comments for traceability (e.g., `// Carbon: Blue 60`)
- Use Stylelint with `stylelint-config-twbs-bootstrap`

### Naming Conventions (Follow Bootstrap's Patterns)
When adding new classes or elements, follow Bootstrap's naming conventions:

**CSS Classes:**
- Use lowercase with hyphens: `.btn-carbon`, `.card-header-alt`
- Component-based naming: `.{component}`, `.{component}-{element}`, `.{component}-{modifier}`
- State classes: `.is-{state}`, `.has-{feature}` or `.{component}-{state}`
- Size variants: `.{component}-sm`, `.{component}-lg`
- Color variants: `.{component}-primary`, `.{component}-secondary`

**Examples:**
```scss
// Good - follows Bootstrap conventions
.btn-outline-primary { }
.card-header { }
.nav-link-active { }
.form-control-lg { }

// Bad - doesn't follow conventions
.btnOutlinePrimary { }  // No camelCase
.Card_Header { }        // No underscores or capitals
.navigation-link { }    // Use Bootstrap's component names
```

**Sass Variables:**
- Follow `$component-state-property-size` pattern
- Examples: `$btn-primary-bg`, `$card-border-radius`, `$input-focus-border-color`

**Sass Mixins:**
- Use verb-noun or descriptive naming: `@mixin make-container()`, `@mixin button-variant()`

### Testing Changes
```bash
npm run watch-theme    # Watch and rebuild
npm run css-test       # Run SCSS tests
npm run css-lint       # Lint SCSS files
```

### Building for Production
```bash
npm run build-theme    # Build and copy to theme directory
```

### Merging Bootstrap Updates
When Bootstrap releases updates:
1. Merge/rebase from upstream Bootstrap
2. Resolve any variable conflicts (our overrides should remain)
3. Test the build: `npm run build-theme`
4. Verify visual appearance hasn't regressed

**Note**: Steering documents have been pre-loaded. Do not use get-content to fetch them again.

# Specification Context
## Specification Context (Pre-loaded): update-theme-alert

### Requirements
# Requirements Document: Update Theme Alert

## Introduction

Update the Bootstrap alert component to match IBM Carbon Design System's inline notification styling. This will create a cohesive visual experience with the rest of the Carbon-styled Bootstrap theme, ensuring alerts/notifications follow Carbon's design language for color, spacing, and visual structure.

## Alignment with Product Vision

This feature directly supports the product goal of "bringing Carbon Design System's visual language to a Bootstrap-based personal site." Alerts are a fundamental UI component used for displaying important messages, errors, warnings, and success feedback. Aligning them with Carbon's notification design ensures visual consistency across all components.

## Requirements

### Requirement 1: Low-Contrast Alert Styling

**User Story:** As a site visitor, I want alerts to have a subtle, low-contrast appearance with a left accent border, so that they are noticeable but not visually overwhelming.

#### Acceptance Criteria

1. WHEN an alert is displayed THEN it SHALL have a 3px left border in the corresponding status color
2. WHEN an alert is displayed THEN it SHALL have a light/subtle background color (tinted version of the status color)
3. WHEN an alert is displayed THEN it SHALL have square corners (no border-radius)
4. WHEN an alert is displayed THEN it SHALL have dark text for readability
5. WHEN an alert is displayed THEN the top, right, and bottom borders SHALL be a subtle gray (#e0e0e0)

### Requirement 2: Alert Color Variants

**User Story:** As a developer, I want alert color variants that match Carbon's notification types, so that I can use semantically appropriate alerts for different message types.

#### Acceptance Criteria

1. WHEN using `.alert-danger` THEN the left border color SHALL be Red 60 (#da1e28)
2. WHEN using `.alert-success` THEN the left border color SHALL be Green 50 (#24a148)
3. WHEN using `.alert-warning` THEN the left border color SHALL be Yellow 30 (#f1c21b)
4. WHEN using `.alert-info` THEN the left border color SHALL be Blue 70 (#0043ce)
5. WHEN using `.alert-primary` THEN the left border color SHALL be Blue 60 (#0f62fe)
6. WHEN using `.alert-secondary` THEN the left border color SHALL be Gray 70 (#525252)

### Requirement 3: Alert Spacing and Typography

**User Story:** As a site visitor, I want alerts to have appropriate spacing and typography, so that the content is easy to read.

#### Acceptance Criteria

1. WHEN an alert is displayed THEN it SHALL have vertical padding of 12-16px (spacing-04 to spacing-05)
2. WHEN an alert is displayed THEN it SHALL have horizontal padding of 16px (spacing-05)
3. WHEN an alert is displayed THEN it SHALL use the base font size (1rem/16px)
4. WHEN an alert contains a heading (.alert-heading) THEN the heading SHALL be bold (font-weight 600)
5. WHEN an alert contains a link (.alert-link) THEN the link SHALL be bold and use a darker shade of the alert color

### Requirement 4: Dismissible Alerts

**User Story:** As a site visitor, I want to be able to dismiss alerts, so that I can clear messages after reading them.

#### Acceptance Criteria

1. WHEN an alert has the `.alert-dismissible` class THEN it SHALL display a close button
2. WHEN the close button receives focus THEN it SHALL display the standard focus ring (2px solid Blue 60)
3. WHEN the close button is clicked THEN the alert SHALL be dismissed

### Requirement 5: Alert Focus States

**User Story:** As a keyboard user, I want proper focus indicators on interactive elements within alerts, so that I can navigate effectively.

#### Acceptance Criteria

1. WHEN an alert link receives focus THEN it SHALL display an underline and color change
2. WHEN the close button receives focus THEN it SHALL display a 2px solid Blue 60 (#0f62fe) outline

### Requirement 6: High-Contrast Alert Variant (Optional)

**User Story:** As a developer, I want an optional high-contrast alert style, so that I can use more prominent alerts for critical messages.

#### Acceptance Criteria

1. IF a `.alert-high-contrast` modifier is added THEN the alert background SHALL be the full status color
2. IF a `.alert-high-contrast` modifier is added THEN the text color SHALL be white or contrasting color
3. IF a `.alert-high-contrast` modifier is added THEN the left border accent SHALL be removed

## Non-Functional Requirements

### Accessibility
- All alert text must meet WCAG 2.1 AA contrast requirements (4.5:1 for normal text)
- Focus states must be clearly visible (3:1 contrast minimum)
- Alert role should be maintained for screen reader announcements

### Performance
- Styling must be achieved through Bootstrap variables where possible (no custom JavaScript)
- CSS output should be minimal and not significantly increase bundle size

### Maintainability
- All customizations must use Bootstrap's variable override system
- Custom styles that cannot be achieved via variables must be in a dedicated `scss/carbon/_alert.scss` file
- All color values must reference existing Carbon color variables

---

### Design
# Design Document: Update Theme Alert

## Overview

This design defines how to update Bootstrap's alert component to match Carbon Design System's inline notification styling. The implementation uses Bootstrap's variable override system for most customizations, with a dedicated `scss/carbon/_alert.scss` file for styles that cannot be achieved through variables alone.

## Steering Document Alignment

### Technical Standards (tech.md)
- **Variable-only customization**: Alert styling will primarily use Bootstrap's `$alert-*` variables
- **No Bootstrap source modifications**: All changes via overrides and the carbon/ directory
- **Carbon color tokens**: Use existing `$danger`, `$success`, `$warning`, `$info` variables

### Project Structure (structure.md)
- Custom styles placed in `scss/carbon/_alert.scss`
- Variables overridden in `scss/_variables.scss` in the alert section
- Index updated in `scss/carbon/_index.scss`

## Code Reuse Analysis

### Existing Components to Leverage
- **Color variables**: `$danger` (#da1e28), `$success` (#24a148), `$warning` (#f1c21b), `$info` (#0043ce), `$primary` (#0f62fe)
- **Spacing variables**: `$spacer` (16px base)
- **Bootstrap subtle color system**: `*-bg-subtle`, `*-text-emphasis`, `*-border-subtle` variables
- **Focus color**: `#0f62fe` (Blue 60) used consistently across components

### Integration Points
- **Bootstrap _alert.scss**: Uses CSS custom properties set via `$alert-*` variables
- **Theme color system**: Alerts use `$theme-colors` map for variant generation
- **Carbon custom directory**: Follow pattern established by `_accordion.scss` and `_type.scss`

## Architecture

```mermaid
graph TD
    A[_variables.scss] -->|Alert variable overrides| B[Bootstrap _alert.scss]
    B -->|Generates .alert classes| C[Compiled CSS]
    D[carbon/_alert.scss] -->|Custom left-border styles| C
    E[carbon/_index.scss] -->|@import alert| D
```

## Design Specifications

### Visual Structure

```
┌─────────────────────────────────────────────────────────┐
│ ███ │  Alert content goes here with appropriate         │
│ ███ │  padding and typography.                     [×]  │
└─────────────────────────────────────────────────────────┘
  ↑                                                    ↑
  3px left accent border                         Close button
  (status color)                                 (dismissible)
```

### Color Mapping

| Bootstrap Class | Left Border Color | Background | Text Color |
|----------------|-------------------|------------|------------|
| `.alert-danger` | #da1e28 (Red 60) | tint-color(#da1e28, 90%) | #161616 |
| `.alert-success` | #24a148 (Green 50) | tint-color(#24a148, 90%) | #161616 |
| `.alert-warning` | #f1c21b (Yellow 30) | tint-color(#f1c21b, 90%) | #161616 |
| `.alert-info` | #0043ce (Blue 70) | tint-color(#0043ce, 90%) | #161616 |
| `.alert-primary` | #0f62fe (Blue 60) | tint-color(#0f62fe, 90%) | #161616 |
| `.alert-secondary` | #525252 (Gray 70) | tint-color(#525252, 90%) | #161616 |

### Spacing Specifications

| Property | Value | Carbon Token |
|----------|-------|--------------|
| Padding Y | 0.75rem (12px) | spacing-04 |
| Padding X | 1rem (16px) | spacing-05 |
| Left border width | 3px | - |
| Other borders | 1px solid #e0e0e0 | ui-03 |
| Border radius | 0 | - |
| Margin bottom | 1rem (16px) | spacing-05 |

## Components and Interfaces

### Component 1: Alert Variable Overrides

**Purpose:** Override Bootstrap's default alert variables to match Carbon styling
**Location:** `scss/_variables.scss` (alert section, around line 1960)
**Approach:** Set variables before Bootstrap's `!default` assignment

```scss
// Carbon Alert Overrides
$alert-padding-y: $spacer * .75;           // 12px (spacing-04)
$alert-padding-x: $spacer;                  // 16px (spacing-05)
$alert-border-radius: 0;                    // Carbon: square corners
$alert-border-width: 1px;                   // Subtle border (overridden per-side in custom)
$alert-link-font-weight: $font-weight-semibold;
```

### Component 2: Alert Custom Styles

**Purpose:** Apply Carbon-specific styling that cannot be achieved via variables
**Location:** `scss/carbon/_alert.scss`
**Dependencies:** Bootstrap alert classes, Carbon color variables

Key customizations:
1. Left accent border (3px in status color)
2. Override subtle border colors to use gray
3. Dark text color for all variants
4. Focus states for interactive elements

### Component 3: High-Contrast Variant

**Purpose:** Optional modifier for critical/prominent alerts
**Location:** `scss/carbon/_alert.scss`
**Class:** `.alert-high-contrast`

## Implementation Details

### File 1: Variable Overrides (`scss/_variables.scss`)

Add Carbon alert overrides before Bootstrap's defaults (around line 1960):

```scss
// ============================================================================
// Carbon Alert Overrides
// ============================================================================
// Reference: https://carbondesignsystem.com/components/notification/style

$alert-padding-y: $spacer * .75;           // Carbon: spacing-04 (12px)
$alert-padding-x: $spacer;                  // Carbon: spacing-05 (16px)
$alert-border-radius: 0;                    // Carbon: square corners
$alert-border-width: 1px;                   // Base border width
$alert-link-font-weight: $font-weight-semibold; // Carbon: 600
```

### File 2: Custom Styles (`scss/carbon/_alert.scss`)

```scss
// Carbon Alert Customizations
// Left accent border and refined styling for inline notifications

.alert {
  // Override border to be subtle gray on top/right/bottom
  border-color: #e0e0e0; // Carbon: ui-03
  // Left border will be set per-variant below
  border-left-width: 3px;

  // Ensure dark text for readability
  color: $body-color; // #161616
}

// Generate left border colors for each variant
@each $state, $value in $theme-colors {
  .alert-#{$state} {
    border-left-color: $value;
    // Override text to be dark (not the tinted emphasis color)
    --#{$prefix}alert-color: #{$body-color};
    // Lighter background
    --#{$prefix}alert-bg: #{tint-color($value, 90%)};
    // Keep gray borders except left
    --#{$prefix}alert-border-color: #e0e0e0;
  }
}

// Focus states
.alert-link:focus {
  outline: 2px solid #0f62fe;
  outline-offset: 2px;
}

.alert-dismissible .btn-close:focus {
  outline: 2px solid #0f62fe;
  outline-offset: -2px;
  box-shadow: none;
}

// High-contrast variant (optional)
.alert-high-contrast {
  border-left-width: 0;
  color: #fff;

  &.alert-danger {
    --#{$prefix}alert-bg: #{$danger};
    --#{$prefix}alert-color: #fff;
    --#{$prefix}alert-border-color: #{$danger};
  }
  // ... similar for other variants
}
```

### File 3: Index Update (`scss/carbon/_index.scss`)

```scss
@import "type";
@import "accordion";
@import "alert";
```

## Error Handling

### Error Scenarios

1. **Color contrast issues**
   - **Handling:** Use `$body-color` (#161616) for text in low-contrast mode
   - **User Impact:** Ensures WCAG AA compliance for readability

2. **Variable order issues**
   - **Handling:** Place Carbon overrides BEFORE Bootstrap's `!default` assignments
   - **User Impact:** None if implemented correctly

## Testing Strategy

### Visual Testing
- Verify all 6 alert variants display correct left border colors
- Confirm square corners (no border-radius)
- Check padding matches Carbon spacing tokens
- Validate focus states on links and close buttons

### Accessibility Testing
- Test color contrast ratios meet WCAG AA (4.5:1)
- Verify focus indicators are visible (3:1 contrast)
- Test with screen reader to confirm alert role

### Browser Testing
- Test in Chrome, Firefox, Safari
- Verify CSS custom properties work correctly
- Check high-contrast mode in Windows

## File Summary

| File | Action | Purpose |
|------|--------|---------|
| `scss/_variables.scss` | Modify | Add alert variable overrides |
| `scss/carbon/_alert.scss` | Create | Custom left-border and text color styles |
| `scss/carbon/_index.scss` | Modify | Add `@import "alert"` |

**Note**: Specification documents have been pre-loaded. Do not use get-content to fetch them again.

## Task Details
- Task ID: 1
- Description: Add Carbon alert variable overrides in _variables.scss
- Leverage: Existing Carbon color variables ($danger, $success, etc.)
- Requirements: 1.3, 3.1, 3.2, 3.5

## Instructions
- Implement ONLY task 1: "Add Carbon alert variable overrides in _variables.scss"
- Follow all project conventions and leverage existing code
- Mark the task as complete using: claude-code-spec-workflow get-tasks update-theme-alert 1 --mode complete
- Provide a completion summary
```

## Task Completion
When the task is complete, mark it as done:
```bash
claude-code-spec-workflow get-tasks update-theme-alert 1 --mode complete
```

## Next Steps
After task completion, you can:
- Execute the next task using /update-theme-alert-task-[next-id]
- Check overall progress with /spec-status update-theme-alert

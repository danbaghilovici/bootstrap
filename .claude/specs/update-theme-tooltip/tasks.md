# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's tooltip component via variable overrides and minimal custom styles. The tooltip requires variable overrides for colors, dimensions, and padding, plus a small custom style file for box-shadow.

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_tooltip.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Atomic Task Requirements

Each task meets these criteria for optimal agent execution:
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify

## Tasks

- [ ] 1. Add tooltip variable overrides to `scss/_variables-carbon.scss`
  - File: `scss/_variables-carbon.scss`
  - Add Carbon Tooltip section after switch section
  - Define container variables: `$tooltip-font-size` (.875rem), `$tooltip-max-width` (288px), `$tooltip-color` ($white), `$tooltip-bg` ($gray-800), `$tooltip-border-radius` (2px), `$tooltip-opacity` (1)
  - Define padding variables: `$tooltip-padding-y` (.5rem), `$tooltip-padding-x` (1rem)
  - Define arrow variables: `$tooltip-arrow-width` (.5rem), `$tooltip-arrow-height` (.25rem)
  - Include stylelint disable/enable comments
  - _Requirements: 1.1, 1.2, 1.3, 1.4, 1.5, 2.1, 3.1, 3.2, 4.1, 4.2, 4.3_
  - _Leverage: scss/_variables-carbon.scss (switch section pattern)_

- [ ] 2. Create tooltip custom styles in `scss/carbon/_tooltip.scss`
  - File: `scss/carbon/_tooltip.scss` (new file)
  - Create new file with Carbon reference comment
  - Add box-shadow to `.tooltip-inner`: `0 2px 6px rgba(0, 0, 0, .3)`
  - _Requirements: 5.1_
  - _Leverage: scss/carbon/_switch.scss (custom styles pattern)_

- [ ] 3. Update `scss/carbon/_index.scss` to import tooltip
  - File: `scss/carbon/_index.scss`
  - Add `@import "tooltip";` after switch import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 4. Create demo page `demo/carbon-tooltip.html`
  - File: `demo/carbon-tooltip.html` (new file)
  - Follow structure from `demo/carbon-switch.html`
  - Include tooltip placements: top, bottom, left, right
  - Include long text tooltip example
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - Include Bootstrap tooltip JavaScript initialization script
  - _Leverage: demo/carbon-switch.html (demo page structure)_

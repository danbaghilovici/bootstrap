# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's switch component via variable overrides and custom styles. The switch requires both variable overrides (for colors and SVG handles) and custom styles (for fixed pixel dimensions).

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_switch.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Tasks

- [ ] 1. Add switch variable overrides to `scss/_variables-carbon.scss`
  - Add Carbon Switch/Toggle section after progress bar section
  - Define track dimensions: `$form-switch-width` (3rem), `$form-switch-border-radius` (.75rem)
  - Define handle colors (`$form-switch-color`, `$form-switch-focus-color`, `$form-switch-checked-color`) as `$white`
  - Define SVG background images for all states
  - _Requirements: 1.1, 1.2, 2.1, 2.2, 6.1, 6.2_
  - _Leverage: scss/_variables-carbon.scss (progress bar section pattern)_

- [ ] 2. Create switch custom styles in `scss/carbon/_switch.scss`
  - Create new file with Carbon reference comment
  - Add track overrides: fixed 48px × 24px dimensions, gray background (`$gray-500`), no border
  - Add handle sizing via `background-size: 1.125rem` (18px) and positioning
  - Add focus state: `box-shadow: none`, 2px solid `$primary` outline with 1px offset
  - Add checked state: green background (`$success`), handle position right
  - Add disabled state: light gray track (`$gray-300`), dimmed handle, `opacity: 1`
  - Add disabled label styling with muted text color
  - _Requirements: 1.3, 1.4, 1.5, 2.3, 2.4, 2.5, 3.1, 3.2, 3.3, 4.1, 4.2, 4.3, 4.4_
  - _Leverage: scss/carbon/_progress.scss (custom styles pattern)_

- [ ] 3. Add small variant styles to `scss/carbon/_switch.scss`
  - Add `.form-switch-sm` section for small variant
  - Track dimensions: 32px × 16px
  - Handle size: 10px via `background-size: .625rem`
  - Adjusted padding for smaller switch
  - _Requirements: 5.1, 5.2, 5.3, 5.4_

- [ ] 4. Update `scss/carbon/_index.scss` to import switch
  - Add `@import "switch";` after progress import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 5. Create demo page `demo/carbon-switch.html`
  - Follow structure from `demo/carbon-progress-bar.html`
  - Include: default OFF/ON states, with label, focus demo, small variant, disabled states
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - Add CSS classes reference table
  - _Leverage: demo/carbon-progress-bar.html (demo page structure)_

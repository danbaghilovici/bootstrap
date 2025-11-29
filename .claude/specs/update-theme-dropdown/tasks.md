# Implementation Tasks

## Task Overview

Implement Carbon Design System styling for Bootstrap's dropdown component via variable overrides and minimal custom styles. The dropdown requires variable overrides for menu container, items, hover/active/disabled states, dividers, headers, and dark variant. Custom styles are needed only for the focus outline state and header font-weight.

## Steering Document Compliance

- **tech.md**: Variable overrides in `_variables-carbon.scss`, custom styles in `scss/carbon/_dropdown.scss`
- **structure.md**: Follows established Carbon customization directories and patterns

## Atomic Task Requirements

Each task meets these criteria for optimal agent execution:
- **File Scope**: Touches 1-3 related files maximum
- **Time Boxing**: Completable in 15-30 minutes
- **Single Purpose**: One testable outcome per task
- **Specific Files**: Must specify exact files to create/modify

## Tasks

- [ ] 1. Add dropdown variable overrides to `scss/_variables-carbon.scss`
  - File: `scss/_variables-carbon.scss`
  - Add Carbon Dropdown section after toast section
  - Define menu container variables: `$dropdown-min-width` (10rem), `$dropdown-padding-x` (0), `$dropdown-padding-y` (0.5rem), `$dropdown-font-size` (0.875rem), `$dropdown-color` ($body-color), `$dropdown-bg` ($body-bg), `$dropdown-border-color` ($gray-200), `$dropdown-border-radius` (0), `$dropdown-border-width` (1px), `$dropdown-box-shadow` (0 2px 6px rgba(0, 0, 0, .3))
  - Define divider variables: `$dropdown-divider-bg` ($gray-200), `$dropdown-divider-margin-y` (0.5rem)
  - Define item variables: `$dropdown-item-padding-y` (0.5rem), `$dropdown-item-padding-x` (1rem), `$dropdown-link-color` ($body-color), `$dropdown-link-hover-color` ($body-color), `$dropdown-link-hover-bg` ($gray-200), `$dropdown-link-active-color` ($white), `$dropdown-link-active-bg` ($primary), `$dropdown-link-disabled-color` ($gray-300)
  - Define header variables: `$dropdown-header-color` ($gray-700), `$dropdown-header-padding-y` (0.5rem), `$dropdown-header-padding-x` (1rem)
  - Define dark variant variables: `$dropdown-dark-color`, `$dropdown-dark-bg`, `$dropdown-dark-border-color`, `$dropdown-dark-link-*`, `$dropdown-dark-header-color`
  - Include stylelint disable/enable comments
  - _Requirements: 1.1-1.5, 2.1-2.3, 3.1-3.2, 4.1-4.2, 5.1-5.3, 7.1-7.2, 8.1-8.3_
  - _Leverage: scss/_variables-carbon.scss (toast section pattern)_

- [ ] 2. Create dropdown custom styles in `scss/carbon/_dropdown.scss`
  - File: `scss/carbon/_dropdown.scss` (new file)
  - Create new file with Carbon reference comment
  - Add `.dropdown-item:focus` styles: `outline: 2px solid $primary`, `outline-offset: -2px`, `box-shadow: none`
  - Add `.dropdown-header` styles: `font-size: .75rem`, `font-weight: 600`
  - _Requirements: 6.1-6.2, 8.1-8.3_
  - _Leverage: scss/carbon/_form.scss (focus outline pattern)_

- [ ] 3. Update `scss/carbon/_index.scss` to import dropdown
  - File: `scss/carbon/_index.scss`
  - Add `@import "dropdown";` after toast import
  - _Leverage: scss/carbon/_index.scss (existing import pattern)_

- [ ] 4. Create demo page `demo/carbon-dropdown.html`
  - File: `demo/carbon-dropdown.html` (new file)
  - Follow structure from `demo/carbon-toast.html`
  - Include: basic dropdown menu with items
  - Include: dropdown with header and divider
  - Include: dropdown with disabled items
  - Include: dropdown with active item
  - Include: dark dropdown variant (`.dropdown-menu-dark`)
  - Include: split button dropdown
  - Include: dropup, dropend, dropstart variations
  - Add HTML structure reference section
  - Add Carbon design specifications table
  - Include Bootstrap dropdown JavaScript initialization
  - _Leverage: demo/carbon-toast.html (demo page structure)_

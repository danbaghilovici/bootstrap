# Tasks: Update Theme Pagination

## Task 1: Add Pagination Variable Overrides

**File:** `scss/_variables-carbon.scss`

**Action:** Add pagination section after Breadcrumb Overrides section (after line 472)

**Changes:**
1. Add section header comment for Carbon Pagination Overrides
2. Add typography variable (`$pagination-font-size`)
3. Add sizing variables for default, sm, and lg variants
4. Add color variables for default, hover, focus, active, and disabled states
5. Add shape variables (border-radius)
6. Add section footer comment

**Verification:**
- Run `npm run css-lint` - should pass
- Run `npm run css` - should compile without errors

---

## Task 2: Create Pagination Custom Styles

**File:** `scss/carbon/_pagination.scss` (new file)

**Action:** Create file with focus outline styles

**Content:**
```scss
// Carbon Pagination Customizations
// Focus state outline (cannot be done via variables)

.page-link {
  &:focus {
    outline: 2px solid $primary;    // Carbon: Blue 60 focus outline
    outline-offset: -2px;           // Carbon: inset outline style
  }
}
```

**Verification:**
- File created at correct location
- Follows existing Carbon partial patterns

---

## Task 3: Import Pagination Partial

**File:** `scss/carbon/_index.scss`

**Action:** Add import for pagination partial

**Changes:**
- Add `@import "pagination";` after breadcrumb import

**Verification:**
- Run `npm run css` - should compile without errors

---

## Task 4: Create Demo Page

**File:** `demo/carbon-pagination.html` (new file)

**Action:** Create demo page showing all pagination variants and states

**Content sections:**
1. Default pagination
2. Small pagination (pagination-sm)
3. Large pagination (pagination-lg)
4. Pagination with disabled items
5. Pagination with active state
6. Focus state demonstration (tab through)

**Verification:**
- Open in browser
- Verify all states display correctly
- Verify Carbon styling matches design spec

---

## Task 5: Build and Verify

**Action:** Run full build and verify output

**Commands:**
```bash
npm run css-lint
npm run css
npm run build-theme
```

**Verification:**
- All commands complete without errors
- Output CSS contains pagination overrides
- Demo page displays correctly with final CSS

---

## Execution Order

1. Task 1 (variables) - Foundation for all other changes
2. Task 2 (custom styles) - Focus outline styles
3. Task 3 (import) - Connect custom styles to build
4. Task 4 (demo) - Visual verification
5. Task 5 (build) - Final verification

## Rollback Plan

If issues occur:
1. Remove pagination section from `_variables-carbon.scss`
2. Delete `scss/carbon/_pagination.scss`
3. Remove import from `scss/carbon/_index.scss`
4. Delete `demo/carbon-pagination.html`
5. Run `npm run css` to verify clean state

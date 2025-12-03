# SCSS Guide

## Architecture Overview
The SCSS layer is organized for production builds: variables and utilities feed base styles, layout primitives, and component styles. Each component uses BEM naming and consumes shared design tokens so the compiled CSS can be copied into other systems without refactoring.

## Directory Layout
```scss
src/scss/
|- main.scss              // Entry point imported by layouts
|- base/
|  |- _fonts.scss         // Font declarations and @font-face rules
|  |- _globals.scss       // Global element defaults
|  |- _normalize.scss     // Normalize baseline
|  |- _typography.scss    // Typography scale
|- layout/
|  |- _container.scss     // Container widths and spacing (NEVER nest containers!)
|  |- _section.scss       // Section wrappers
|- components/
|  |- _achievements.scss
|  |- _buttons.scss
|  |- _clients.scss
|  |- _hero.scss
|  |- _hero-v2.scss
|  |- _testimonial.scss
|- utils/
|  |- _variables.scss     // Design tokens and mixins
```

## Container Rules
**CRITICAL:** Containers must NEVER be nested inside other containers of any type. Each container variant (`.container`, `.container--nav`, `.container-fluid`, `.container-sec-header`) is a standalone layout element with its own padding and max-width. Use separate sibling containers instead of nesting them.

## Import Order
`main.scss` must load utilities first, then base, layout, and finally components:
```scss
// UTILS
@use "./utils/variables" as *;

// BASE
@use "./base/fonts";
@use "./base/normalize";
@use "./base/typography";
@use "./base/globals";

// LAYOUT
@use "./layout/container";
@use "./layout/section";

// COMPONENTS
@use "components/buttons";
@use "components/achievements";
@use "components/clients";
@use "components/hero";
@use "components/hero-v2";
@use "components/testimonial";
```
Maintain this sequence so variables and mixins are available before they are used.

## Component Styling Rules
- Every component stylesheet imports variables: `@use "../utils/variables" as *;`
- Scope selectors to the component block (`.hero`, `.testimonial`, etc.).
- Use BEM naming with double underscores for elements and double hyphens for modifiers.
- Keep responsive rules mobile-first with `@media (min-width: $breakpoint)` queries from `_variables.scss`.
- Do NOT add `background-color` to component stylesheets. Use the `page-sec--bg-white` or `page-sec--bg-gray` modifiers in the component markup instead.
- Add the file to `main.scss` immediately after creation to ensure it is bundled.

## Tokens and Utilities
- Brand colors, spacing, breakpoints, and z-index scales live in `_variables.scss`.
- Typography rules (font stacks, weights, heading/body scales) live in `_typography.scss`.
- Update tokens first, then adjust component styles that consume them.

## Typography Design System
The project includes a comprehensive typography system with 11 type scales (Display 2xl through Text xs), each with 4 font weights (Regular 400, Medium 500, Semibold 600, Bold 700).

### Type Scales
- **Display 2xl**: 72px / 90px line-height / -2% letter-spacing
- **Display xl**: 60px / 72px line-height / -2% letter-spacing
- **Display lg**: 48px / 60px line-height / -2% letter-spacing
- **Display md**: 36px / 44px line-height / -2% letter-spacing
- **Display sm**: 30px / 38px line-height
- **Display xs**: 24px / 32px line-height
- **Text xl**: 20px / 30px line-height
- **Text lg**: 18px / 28px line-height
- **Text md**: 16px / 24px line-height
- **Text sm**: 14px / 20px line-height
- **Text xs**: 12px / 18px line-height

### Usage
Use mixins in component styles:
```scss
.hero__title {
  @include display-xl-semibold;
  color: $color-black;
}
```

Or apply utility classes directly in markup:
```html
<h1 class="display-2xl-semibold">Heading</h1>
<p class="text-lg-regular">Body text</p>
```

### Responsive Typography
HTML heading elements (h1-h6) automatically scale up on larger screens using responsive mixins. For example, `<h1>` uses `display-xl-semibold` on mobile and `display-2xl-semibold` on desktop (768px+).

### Color Utilities
Combine typography classes with color utilities:
```html
<p class="text-xl-medium text-grey">Muted text</p>
```

Available color classes: `.text-primary`, `.text-secondary`, `.text-grey`, `.text-light-grey`, `.text-dark-grey`, `.text-info`, `.text-success`, `.text-warning`, `.text-error`

### Typography Implementation Scope
When implementing or updating Typography from Figma, **ONLY modify these 3 files**:
- `src/scss/base/_fonts.scss` - Font imports and @font-face declarations
- `src/scss/base/_typography.scss` - Typography mixins, utility classes, and HTML element defaults
- `src/scss/utils/_variables.scss` - Typography design tokens (sizes, line-heights, letter-spacing, weights)

**CRITICAL: Do NOT create any of the following:**
- Documentation/showcase pages (e.g., `/typography` route in `src/pages/`)
- Example components (e.g., `TypographyExampleCard.astro`)
- Separate documentation markdown files (e.g., `TYPOGRAPHY.md`, `TYPOGRAPHY-QUICK-REFERENCE.md`)
- Any routes outside of `src/pages/prod/` (this project only ships production pages)

**Why:** This project follows a production-first approach. All pages must be in `src/pages/prod/` and serve actual production content. Design system documentation pages are considered development/demo content and violate the project's core principle: "No dev or example components; only files that ship to production belong in the repository."

## Workflow for New Production Styles
1. Define or update the shared design system tokens in `_variables.scss`, `_typography.scss`, and related base/layout files before styling components.
2. Create `_component-name.scss` in `src/scss/components/`.
3. Import variables at the top of the file.
4. Write base styles, responsive adjustments, and state modifiers that reference the shared tokens.
5. Import the file in the components block of `main.scss`.
6. Validate in the browser and run `npm run build` to confirm the compiled CSS succeeds.

## Quality Checklist
- Two-space indentation, no trailing whitespace.
- Avoid unused selectors or deeply nested rules (max three levels).
- Provide brief comments only when explaining non-obvious logic.
- Confirm color contrast and focus states meet WCAG guidance.
- Remove unused files when the related component is deleted.




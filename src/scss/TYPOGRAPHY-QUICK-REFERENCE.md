# Typography Quick Reference

## Available Type Scales

| Class/Mixin | Size | Line Height | Weight Options |
|-------------|------|-------------|----------------|
| `display-2xl-*` | 72px | 90px | regular, medium, semibold, bold |
| `display-xl-*` | 60px | 72px | regular, medium, semibold, bold |
| `display-lg-*` | 48px | 60px | regular, medium, semibold, bold |
| `display-md-*` | 36px | 44px | regular, medium, semibold, bold |
| `display-sm-*` | 30px | 38px | regular, medium, semibold, bold |
| `display-xs-*` | 24px | 32px | regular, medium, semibold, bold |
| `text-xl-*` | 20px | 30px | regular, medium, semibold, bold |
| `text-lg-*` | 18px | 28px | regular, medium, semibold, bold |
| `text-md-*` | 16px | 24px | regular, medium, semibold, bold |
| `text-sm-*` | 14px | 20px | regular, medium, semibold, bold |
| `text-xs-*` | 12px | 18px | regular, medium, semibold, bold |

## Usage Examples

### In HTML (Utility Classes)
```html
<h1 class="display-2xl-semibold">Page Title</h1>
<h2 class="display-lg-semibold">Section Heading</h2>
<p class="text-lg-regular">Body paragraph</p>
<span class="text-sm-medium text-grey">Caption text</span>
```

### In SCSS (Mixins)
```scss
@use "../utils/variables" as *;

.hero {
  &__title {
    @include display-2xl-bold;
    color: $color-black;
  }
  
  &__subtitle {
    @include text-xl-regular;
    color: $color-grey;
  }
}
```

### Responsive Typography
```scss
.page-title {
  @include display-md-semibold; // Mobile: 36px
  
  @media (min-width: $md) {
    @include display-xl-semibold; // Desktop: 60px
  }
}
```

## Color Utilities

Combine with color classes:
```html
<p class="text-lg-regular text-primary">Green text</p>
<p class="text-md-medium text-grey">Grey text</p>
<span class="text-sm-regular text-error">Error message</span>
```

Available: `.text-primary`, `.text-secondary`, `.text-grey`, `.text-light-grey`, `.text-dark-grey`, `.text-info`, `.text-success`, `.text-warning`, `.text-error`

## Recommended Pairings

### Hero Section
- Title: `display-2xl-bold` or `display-xl-semibold`
- Subtitle: `text-xl-regular` or `text-lg-regular`

### Card Components
- Title: `display-sm-semibold` or `display-xs-semibold`
- Body: `text-md-regular`
- Metadata: `text-sm-regular`

### Articles
- Headline: `display-xl-semibold`
- Section Heading: `display-md-semibold`
- Body: `text-lg-regular` or `text-md-regular`
- Captions: `text-sm-regular`

### Buttons
- Primary: `text-md-semibold` or `text-lg-semibold`
- Secondary: `text-sm-medium`

## Design Tokens

Located in `src/scss/utils/_variables.scss`:

```scss
// Font weights
$font-regular: 400;
$font-medium: 500;
$font-semibold: 600;
$font-bold: 700;

// Sizes (examples)
$display-2xl-size: 4.5rem;
$text-lg-size: 1.125rem;
```

## Breakpoints

```scss
$sm: 576px;
$md: 768px;  // Desktop starts here
$lg: 992px;
$xl: 1200px;
$xxl: 1400px;
```

## View Live Examples

Navigate to `/typography` to see all 44 typographic styles in action.

## Full Documentation

See [TYPOGRAPHY.md](../../TYPOGRAPHY.md) for complete documentation, best practices, and detailed examples.

# Typography Design System

This project uses a comprehensive, production-ready typography system based on the Inter font family. The system includes 11 type scales with 4 font weights each, providing a total of 44 typographic styles.

## Table of Contents
- [Font Family](#font-family)
- [Type Scales](#type-scales)
- [Font Weights](#font-weights)
- [Usage](#usage)
- [Responsive Behavior](#responsive-behavior)
- [Best Practices](#best-practices)

## Font Family

The primary typeface is **Inter**, a highly readable sans-serif font optimized for user interfaces.

```scss
$font-primary: 'Inter', -apple-system, Roboto, Helvetica, sans-serif;
```

### Font Loading
Fonts are loaded from Google Fonts with optimal fallbacks:
- Primary: Inter (weights 400, 500, 600, 700)
- Fallback: -apple-system, Roboto, Helvetica, sans-serif

## Type Scales

### Display Scales (Large Headings)

| Scale | Font Size | Line Height | Letter Spacing | Use Case |
|-------|-----------|-------------|----------------|----------|
| **Display 2xl** | 72px / 4.5rem | 90px / 5.625rem | -2% | Hero headlines, marketing |
| **Display xl** | 60px / 3.75rem | 72px / 4.5rem | -2% | Page titles, major headings |
| **Display lg** | 48px / 3rem | 60px / 3.75rem | -2% | Section headings |
| **Display md** | 36px / 2.25rem | 44px / 2.75rem | -2% | Subsection headings |
| **Display sm** | 30px / 1.875rem | 38px / 2.375rem | 0 | Card titles |
| **Display xs** | 24px / 1.5rem | 32px / 2rem | 0 | Small headings |

### Text Scales (Body Copy)

| Scale | Font Size | Line Height | Use Case |
|-------|-----------|-------------|----------|
| **Text xl** | 20px / 1.25rem | 30px / 1.875rem | Large body text, introductions |
| **Text lg** | 18px / 1.125rem | 28px / 1.75rem | Default body text |
| **Text md** | 16px / 1rem | 24px / 1.5rem | Standard body text |
| **Text sm** | 14px / 0.875rem | 20px / 1.25rem | Small body text, captions |
| **Text xs** | 12px / 0.75rem | 18px / 1.125rem | Fine print, labels |

## Font Weights

Each type scale is available in 4 weights:

| Weight | Value | Usage |
|--------|-------|-------|
| **Regular** | 400 | Default body text, regular headings |
| **Medium** | 500 | Emphasized text, subheadings |
| **Semibold** | 600 | Headings, important UI elements |
| **Bold** | 700 | Strong emphasis, CTAs |

## Usage

### 1. Using SCSS Mixins (Recommended for Components)

```scss
@use "../scss/utils/variables" as *;

.hero__title {
  @include display-2xl-semibold;
  color: $color-black;
}

.hero__description {
  @include text-xl-regular;
  color: $color-grey;
}

.card__title {
  @include display-sm-semibold;
}

.card__body {
  @include text-md-regular;
}
```

**Benefits:**
- Better maintainability
- Easier to update globally
- Semantic component styling
- Smaller compiled CSS (when used sparingly)

### 2. Using Utility Classes (Quick Prototyping)

```html
<!-- Hero Section -->
<h1 class="display-2xl-semibold">Welcome to Our Platform</h1>
<p class="text-xl-regular text-grey">Build amazing products faster</p>

<!-- Card Component -->
<div class="card">
  <h3 class="display-sm-semibold">Card Title</h3>
  <p class="text-md-regular">Card description text goes here.</p>
  <span class="text-sm-regular text-light-grey">Published 2 days ago</span>
</div>

<!-- Button -->
<button class="text-md-semibold">Get Started</button>
```

**Benefits:**
- Rapid prototyping
- Consistent typography without custom CSS
- Easy to scan in HTML

### 3. HTML Element Defaults

Standard HTML elements have default responsive styles:

```html
<h1>Automatically uses display-xl-semibold (mobile) → display-2xl-semibold (desktop)</h1>
<h2>Automatically uses display-lg-semibold (mobile) → display-xl-semibold (desktop)</h2>
<h3>Automatically uses display-md-semibold (mobile) → display-lg-semibold (desktop)</h3>
<h4>Automatically uses display-sm-semibold (mobile) → display-md-semibold (desktop)</h4>
<h5>Automatically uses display-xs-semibold (mobile) → display-sm-semibold (desktop)</h5>
<h6>Automatically uses text-xl-semibold (mobile) → display-xs-semibold (desktop)</h6>
<p>Automatically uses text-md-regular (mobile) → text-lg-regular (desktop)</p>
```

## Responsive Behavior

The typography system is mobile-first and fully responsive:

### Breakpoints
```scss
$sm: 576px;  // Small tablets
$md: 768px;  // Tablets (Desktop starts here)
$lg: 992px;  // Desktops
$xl: 1200px; // Large desktops
$xxl: 1400px; // Extra large screens
```

### Example: Responsive Heading

```scss
.page-title {
  @include display-md-semibold; // Mobile (36px)
  
  @media (min-width: $md) {
    @include display-xl-semibold; // Desktop (60px)
  }
}
```

### Fluid Typography (Optional)

For ultra-smooth scaling between breakpoints:

```scss
.hero__title {
  font-size: clamp(2.25rem, 5vw, 4.5rem); // 36px → 72px
  line-height: 1.25;
}
```

## Color Utilities

Combine typography with color utilities:

```html
<h2 class="display-lg-semibold text-primary">Green Heading</h2>
<p class="text-lg-regular text-grey">Grey body text</p>
<span class="text-sm-medium text-error">Error message</span>
```

### Available Color Classes

| Class | Color | Usage |
|-------|-------|-------|
| `.text-primary` | Brand green (#4CAF4F) | Primary brand elements |
| `.text-secondary` | Dark grey (#263238) | Secondary headings |
| `.text-grey` | Medium grey (#717171) | Body text |
| `.text-light-grey` | Light grey (#89939E) | Muted text |
| `.text-dark-grey` | Dark grey (#4D4D4D) | Emphasis |
| `.text-info` | Blue (#2194F3) | Information |
| `.text-success` | Green (#2E7D31) | Success states |
| `.text-warning` | Yellow (#FBC02D) | Warnings |
| `.text-error` | Red (#E53835) | Errors |

## Best Practices

### ✅ Do

1. **Use semantic scales**
   ```html
   <h1 class="display-2xl-semibold">Main Page Title</h1>
   <h2 class="display-lg-semibold">Section Heading</h2>
   <p class="text-lg-regular">Body paragraph</p>
   ```

2. **Combine with color utilities**
   ```html
   <p class="text-md-regular text-grey">Muted description</p>
   ```

3. **Use mixins in component SCSS**
   ```scss
   .card__title {
     @include display-sm-semibold;
     margin-bottom: 0.5rem;
   }
   ```

4. **Think mobile-first**
   ```scss
   .title {
     @include display-sm-semibold; // Mobile
     
     @media (min-width: $md) {
       @include display-lg-semibold; // Desktop
     }
   }
   ```

### ❌ Don't

1. **Don't override font-size directly** (breaks the design system)
   ```scss
   // ❌ Bad
   .title {
     font-size: 42px;
   }
   
   // ✅ Good
   .title {
     @include display-lg-semibold;
   }
   ```

2. **Don't mix too many weights in close proximity**
   ```html
   <!-- ❌ Too many weights -->
   <h2 class="display-lg-bold">Title</h2>
   <h3 class="display-md-medium">Subtitle</h3>
   <h4 class="display-sm-regular">Detail</h4>
   
   <!-- ✅ Better -->
   <h2 class="display-lg-semibold">Title</h2>
   <h3 class="display-md-regular">Subtitle</h3>
   ```

3. **Don't use Display scales for body text**
   ```html
   <!-- ❌ Bad -->
   <p class="display-sm-regular">This is a paragraph...</p>
   
   <!-- ✅ Good -->
   <p class="text-lg-regular">This is a paragraph...</p>
   ```

4. **Don't nest similar sizes**
   ```html
   <!-- ❌ Bad hierarchy -->
   <h1 class="display-xl-semibold">Main Title</h1>
   <h2 class="display-lg-semibold">Should be more distinct</h2>
   
   <!-- ✅ Better -->
   <h1 class="display-2xl-semibold">Main Title</h1>
   <h2 class="display-md-semibold">Clear hierarchy</h2>
   ```

## Viewing the Design System

Navigate to `/typography` to see the complete typography system showcase, which displays all 44 typographic styles exactly as they appear in the Figma design.

## Design Tokens Reference

All typography tokens are defined in `src/scss/utils/_variables.scss`:

```scss
// Font Family
$font-primary: 'Inter', -apple-system, Roboto, Helvetica, sans-serif;

// Font Weights
$font-regular: 400;
$font-medium: 500;
$font-semibold: 600;
$font-bold: 700;

// Display 2xl
$display-2xl-size: 4.5rem;
$display-2xl-line-height: 5.625rem;
$display-2xl-letter-spacing: -0.02em;

// ... (all other scales)
```

## Examples

### Landing Page Hero
```html
<section class="hero">
  <h1 class="display-2xl-bold text-primary">
    Build Something Amazing
  </h1>
  <p class="text-xl-regular text-grey">
    The fastest way to create beautiful, responsive websites.
  </p>
  <button class="text-lg-semibold">
    Get Started Free
  </button>
</section>
```

### Article Content
```html
<article>
  <h1 class="display-xl-semibold">Article Title</h1>
  <p class="text-sm-regular text-light-grey">Published on March 15, 2024</p>
  
  <p class="text-lg-regular">
    This is the introduction paragraph with larger text for better readability.
  </p>
  
  <h2 class="display-md-semibold">Section Heading</h2>
  <p class="text-md-regular">
    Regular body text for the main content of the article.
  </p>
</article>
```

### Pricing Card
```html
<div class="pricing-card">
  <h3 class="display-sm-semibold">Professional</h3>
  <p class="text-md-regular text-grey">For growing teams</p>
  
  <div class="price">
    <span class="display-2xl-bold text-primary">$49</span>
    <span class="text-lg-regular text-grey">/month</span>
  </div>
  
  <ul>
    <li class="text-md-regular">Unlimited projects</li>
    <li class="text-md-regular">24/7 support</li>
    <li class="text-md-regular">Advanced analytics</li>
  </ul>
  
  <button class="text-md-semibold">Choose Plan</button>
</div>
```

## Contributing

When adding new components or updating existing ones:

1. Always use the defined type scales (never arbitrary sizes)
2. Choose weights that create clear visual hierarchy
3. Test typography on mobile, tablet, and desktop viewports
4. Ensure sufficient color contrast (WCAG AA minimum)
5. Document any custom typography patterns in component docs

---

**Questions?** Check the design system documentation page at `/typography` or review `src/scss/base/_typography.scss` for implementation details.

# Skill: Figma to Pixel-Perfect Code (WordPress & HTML)

## Purpose
To convert Figma design files (via view links and screenshots) into pixel-perfect, responsive WordPress/Elementor or HTML/CSS implementations.

## When to Use
- Converting Figma website designs to WordPress sites
- Building pixel-perfect Elementor pages from Figma
- Creating static HTML/CSS pages from Figma designs
- Ensuring design fidelity between Figma and live site

## Procedure

### 1. Figma Design Interpretation
First, analyze the Figma design thoroughly:

**Key Metrics to Extract**:
- **Typography**: Font family, font size, font weight, line height, letter spacing, text color
- **Colors**: HEX/RGB/HSL values for backgrounds, text, borders, accents
- **Spacing**: Padding, margin, gap between elements (use Figma's measure tool)
- **Layout**: Container width, column structure, responsive breakpoints
- **Components**: Buttons, forms, cards, navigation (identify reusable components)
- **Assets**: Images, icons, SVGs (export from Figma in appropriate sizes)

**How to Extract from Figma**:
- Use **Inspect** tab in Figma to get exact CSS values
- Export assets at 1x, 2x, and 3x for responsiveness
- Note auto-layout properties for responsive behavior
- Document all design tokens (colors, fonts, spacing) first

---

### 2. HTML/CSS Implementation (Static Pages)
Build semantic, responsive HTML/CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pixel-Perfect Design</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* Design Tokens First! */
    :root {
      --color-primary: #2563eb;
      --color-secondary: #1e40af;
      --color-text: #1f2937;
      --color-light: #f3f4f6;
      --font-primary: 'Inter', sans-serif;
      --spacing-xs: 0.5rem;
      --spacing-sm: 1rem;
      --spacing-md: 1.5rem;
      --spacing-lg: 2rem;
      --spacing-xl: 3rem;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-primary);
      color: var(--color-text);
      line-height: 1.6;
    }

    /* Container Width (Match Figma) */
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 var(--spacing-md);
    }

    /* Example Component: Hero Section */
    .hero {
      padding: var(--spacing-xl) 0;
      background-color: var(--color-light);
    }

    .hero-content {
      display: flex;
      gap: var(--spacing-lg);
      align-items: center;
    }

    .hero-text h1 {
      font-size: 3.5rem;
      font-weight: 700;
      line-height: 1.1;
      margin-bottom: var(--spacing-md);
    }

    .btn {
      display: inline-flex;
      padding: var(--spacing-sm) var(--spacing-lg);
      background-color: var(--color-primary);
      color: white;
      text-decoration: none;
      border-radius: 8px;
      font-weight: 600;
      transition: background-color 0.2s ease;
    }

    .btn:hover {
      background-color: var(--color-secondary);
    }

    /* Responsive Adjustments */
    @media (max-width: 768px) {
      .hero-content {
        flex-direction: column;
        text-align: center;
      }

      .hero-text h1 {
        font-size: 2.5rem;
      }
    }
  </style>
</head>
<body>
  <section class="hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-text">
          <h1>Welcome to Our Site</h1>
          <p>Building pixel-perfect websites from Figma designs</p>
          <a href="#" class="btn">Get Started</a>
        </div>
        <div class="hero-image">
          <img src="images/hero.png" alt="Hero Image" width="600" height="400">
        </div>
      </div>
    </div>
  </section>
</body>
</html>
```

**CSS Best Practices**:
- Use design tokens (CSS variables) for consistency
- Use Flexbox/Grid for layouts
- Use relative units (rem, em, %) for responsiveness
- Add `width` and `height` attributes to images to prevent layout shifts
- Use modern CSS (e.g., `gap` instead of margin hacks)

---

### 3. WordPress/Elementor Implementation
Convert Figma designs to Elementor pages:

#### Step 1: Set Up Global Styles in Elementor
1. Go to **Elementor → Site Settings**
2. Set **Global Colors** (match Figma's color palette)
3. Set **Global Fonts** (match Figma's typography)
4. Configure **Theme Builder** for headers/footers

#### Step 2: Build Page Structure
1. Create a new page and edit with Elementor
2. Use **Sections** and **Columns** to match Figma's layout
3. Set section/column padding/margin exactly from Figma
4. Use **Container** widget (Elementor 3.0+) for modern layouts

#### Step 3: Add Elements
- **Text Editor**: For content, match font size/weight/line height
- **Image**: Add images with exact dimensions from Figma
- **Button**: Customize to match Figma's button style
- **Icon**: Use Elementor icons or import custom SVGs
- **Form**: Use Elementor Forms (or Gravity Forms) and style to match Figma

#### Step 4: Reusable Components with ACF (Optional)
For dynamic content, use **Advanced Custom Fields**:
1. Create a Field Group matching your design
2. Build a custom template (in your child theme)
3. Use ACF functions to output fields

#### Example: Elementor Workflow for Hero Section
```php
<!-- In your child theme's functions.php, add custom CSS or use Elementor's Custom CSS -->
```

1. Add a Section with background color from Figma
2. Add 2-column container (50% / 50% on desktop, stack on mobile)
3. Left column: Heading, Text Editor, Button
4. Right column: Image
5. Set exact padding/margin for all elements to match Figma
6. Use Elementor's **Advanced** tab for custom CSS classes if needed

---

### 4. Pixel-Perfect Verification
Always verify your implementation:

**Checklist**:
- ✅ Spacing matches exactly (padding, margin, gaps)
- ✅ Colors are accurate (use color picker to verify)
- ✅ Typography matches (font, size, weight, line height)
- ✅ Images are properly sized and optimized
- ✅ Responsive breakpoints match Figma's design
- ✅ All interactive elements (buttons, links) work
- ✅ Page loads quickly (optimize images, minify CSS/JS)
- ✅ Accessibility best practices are followed (alt text, semantic HTML)

**Tools for Verification**:
- Browser DevTools (Inspect Element) to measure spacing
- Color picker extensions to verify colors
- Responsive Design Mode in DevTools to test all breakpoints
- Lighthouse to check performance/accessibility

---

## Constraints & Tips
1. **Start with Design Tokens**: Define colors, fonts, and spacing first
2. **Use Semantic HTML**: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
3. **Responsive First**: Build mobile-first and scale up
4. **Reuse Components**: Create reusable blocks/sections in Elementor
5. **Export Assets Properly**: Use WebP/AVIF for images, SVG for icons
6. **Test on Real Devices**: Don't just rely on DevTools responsive mode
7. **Match Figma Breakpoints**: Use the exact responsive breakpoints from Figma

---

## Expected Output
A pixel-perfect, responsive website that exactly matches the Figma design in WordPress/Elementor or HTML/CSS!

---

## Iterative Workflow Reference
For tasks involving screenshots or iterative design adjustments, use the **Screenshot-Based Design Workflow** skill.

---

## Continuous Learning & Skill Improvement
**Crucial Note**: For every design, animation, or workflow task:
1. Document lessons learned after completion
2. Update relevant skills with new knowledge as an "Extras" or "Crucial Learnings" section
3. Apply improved approaches to all future similar tasks

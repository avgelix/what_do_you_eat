# GitHub Copilot Instructions - What Do You Eat

This document provides guidelines for GitHub Copilot and other AI assistants working on the "What Do You Eat" project.

## Project Overview

A data storytelling website exploring conscious eating in a globalized world, analyzing how "identical" foods differ across five countries representing five continents. The project combines personal narrative with data visualization to reveal hidden differences in food ingredients and additives.

## Tech Stack

### Core Technologies
- **HTML5**: Semantic markup with accessibility in mind
- **CSS3**: Custom styling, responsive design, no frameworks
- **Vanilla JavaScript**: Pure ES6+, no jQuery or frameworks required
- **Observable Framework**: Data visualizations via embeds only

### Data & Assets
- **Data Format**: JSON (cleaned dataset in `/data` directory)
- **Images**: SVG preferred for illustrations, optimized PNG/WebP for photos
- **Fonts**: 
  - **Self-hosted fonts preferred** for privacy and performance
  - **Fallback strategy**: serif fonts (Georgia, Times) for body, sans-serif (Helvetica, Arial) for UI
  - **Font loading**: Use `font-display: swap` to prevent invisible text
  - **Format**: WOFF2 for modern browsers, WOFF for fallback
  - Consider using font subsetting to reduce file size

### Deployment
- **Static Site**: No build process, pure client-side
- **Hosting**: GitHub Pages or Vercel
- **Version Control**: Git with conventional commits

### Browser Support
- Modern browsers (last 2 versions)
- Progressive enhancement approach
- Graceful degradation for older browsers

## Development Guidelines

### Code Style

#### HTML
- Use semantic HTML5 elements (`<article>`, `<section>`, `<nav>`, `<figure>`, etc.)
- Include ARIA labels where semantic meaning isn't clear
- All images must have descriptive `alt` attributes
- Use `<button>` for actions, `<a>` for navigation
- Maintain proper heading hierarchy (h1 → h2 → h3, no skipping)

```html
<!-- Good: Centered content with proper semantics -->
<article class="story-section" role="region" aria-label="Country comparison">
  <h2>Ingredient Differences Across Countries</h2>
  <p>
    Why? Because tens of millions of people are curious about 
    <a href="#" class="highlight">how ingredients differ</a>.
  </p>
  <p>
    In 2021, I moved from Italy to the United States and noticed 
    my health <span class="highlight">changed dramatically</span> despite 
    eating the <em>same</em> foods...
  </p>
  <figure class="visualization">
    <img src="chart.svg" alt="Bar chart showing Italy has average 8 ingredients per product while USA has 15">
    <figcaption>Average ingredient count by country</figcaption>
  </figure>
</article>

<!-- Avoid: Non-semantic, no centering, poor typography -->
<div class="section">
  <span class="title">Ingredient Differences</span>
  <img src="chart.svg">
</div>
```

#### CSS
- Mobile-first responsive design
- Use CSS custom properties (variables) for colors, spacing, typography
- BEM naming convention for classes: `.block__element--modifier`
- Avoid `!important` unless absolutely necessary
- Include focus states for all interactive elements
- Use `rem` for font sizes, `em` for spacing within components

**Color Palette** (inspired by reference design):
```css
:root {
  /* Colors */
  --color-bg-primary: #fef6e4;        /* Warm cream background */
  --color-text-primary: #2b1a1a;      /* Dark brown/maroon for body text */
  --color-heading: #3d1a3d;           /* Deep purple for headings */
  --color-accent: #f4b942;            /* Gold/yellow for highlights */
  --color-link: #3d1a3d;              /* Links match headings */
  --color-highlight-bg: #f4e06d;      /* Yellow highlight background */
  
  /* Typography */
  --font-heading: 'Publico', 'Freight', Georgia, serif;  /* Bold serif for headlines */
  --font-body: Georgia, 'Times New Roman', serif;         /* Serif for readability */
  --font-accent: 'Atlas Grotesk', 'Helvetica Neue', sans-serif; /* Sans for UI elements */
  
  --font-size-base: 1.125rem;         /* 18px base for readability */
  --font-size-large: 1.5rem;          /* 24px */
  --font-size-heading: 2.5rem;        /* 40px */
  --font-size-display: 4rem;          /* 64px for large headlines */
  
  --line-height-body: 1.6;
  --line-height-heading: 1.2;
  
  /* Spacing */
  --spacing-base: 1rem;
  --spacing-section: 4rem;            /* Between major sections */
  --spacing-paragraph: 1.5rem;        /* Between paragraphs */
  
  /* Layout */
  --content-max-width: 680px;         /* Optimal reading width */
  --page-margin: 2rem;
}

/* Example usage */
.story-section {
  max-width: var(--content-max-width);
  margin: var(--spacing-section) auto;
  padding: 0 var(--page-margin);
}

.story-section h2 {
  font-family: var(--font-heading);
  font-size: var(--font-size-heading);
  color: var(--color-heading);
  font-weight: 700;
  line-height: var(--line-height-heading);
  margin-bottom: var(--spacing-paragraph);
}

.story-section p {
  font-family: var(--font-body);
  font-size: var(--font-size-base);
  color: var(--color-text-primary);
  line-height: var(--line-height-body);
}

/* Highlighted text (like yellow marker) */
.highlight {
  background: linear-gradient(180deg, transparent 50%, var(--color-highlight-bg) 50%);
  padding: 0 0.2em;
}

/* Interactive elements */
.comparison-tool__button {
  font-family: var(--font-accent);
  font-size: 1rem;
  padding: calc(var(--spacing-base) * 0.5) var(--spacing-base);
  background: var(--color-accent);
  color: var(--color-heading);
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 600;
}

.comparison-tool__button:focus {
  outline: 2px solid var(--color-heading);
  outline-offset: 2px;
}
```

#### JavaScript
- Use ES6+ features (const/let, arrow functions, template literals, destructuring)
- Prefer functional programming patterns
- Avoid global variables; use modules or IIFE
- Add comments for complex logic
- Handle errors gracefully with user-friendly messages
- No external libraries unless absolutely necessary

```javascript
// Good
const loadProductData = async (country) => {
  try {
    const response = await fetch(`/data/${country}.json`);
    if (!response.ok) throw new Error('Data load failed');
    return await response.json();
  } catch (error) {
    console.error('Error loading data:', error);
    displayErrorMessage('Unable to load product data. Please try again.');
    return null;
  }
};

// Avoid
var data;
function getData(c) {
  $.get('/data/' + c + '.json', function(d) {
    data = d;
  });
}
```

### Accessibility Requirements (WCAG 2.1 AA)

**Critical accessibility requirements:**

1. **Keyboard Navigation**
   - All interactive elements must be keyboard accessible
   - Logical tab order
   - Visible focus indicators
   - Skip-to-content link at top of page

2. **Screen Readers**
   - Descriptive alt text for all images and visualizations
   - ARIA labels for complex interactive elements
   - Live regions for dynamic content updates (`aria-live="polite"`)
   - Proper heading structure

3. **Visual Design**
   - Minimum contrast ratio 4.5:1 for normal text, 3:1 for large text
   - Text resizable up to 200% without loss of functionality
   - No information conveyed by color alone
   - No flashing content (seizure risk)

4. **Observable Embeds**
   - Each embedded visualization must have:
     - Descriptive title/heading
     - Text alternative explaining key insights
     - Link to data table or CSV download
   - Example:
   ```html
   <section aria-labelledby="additive-chart">
     <h3 id="additive-chart">Additive Usage by Country</h3>
     <div class="observable-embed">
       <!-- Observable embed code -->
     </div>
     <p class="visualization-alt">
       This chart shows that the United States averages 7.2 additives per product,
       while Italy averages 3.1 additives per product. Full data available in
       <a href="/data/additives.csv">downloadable CSV format</a>.
     </p>
   </section>
   ```

### File Organization

```
what_do_you_eat/
├── .github/
│   └── copilot-instructions.md    # This file
├── index.html                      # Main story page
├── styles/
│   ├── main.css                    # Global styles & CSS variables
│   ├── typography.css              # Font and text styles
│   ├── layout.css                  # Grid and positioning
│   └── components.css              # Reusable component styles
├── scripts/
│   ├── main.js                     # App initialization
│   ├── data-loader.js              # Data fetching and caching
│   ├── comparison-tool.js          # Product comparison functionality
│   └── search.js                   # Search and filter logic
├── data/
│   ├── products.json               # Main dataset
│   └── categories.json             # Food category metadata
├── assets/
│   ├── fonts/                      # Self-hosted web fonts (WOFF2/WOFF)
│   ├── images/                     # Photos and illustrations
│   └── icons/                      # UI icons (SVG)
├── README.md                       # Project documentation
├── METHODOLOGY.md                  # Data process documentation
└── LICENSE                         # MIT License
```

### Data Handling

- **Never modify the source data** in `/data/products.json`
- For client-side filtering/manipulation, work with copies
- Validate data structure before processing
- Handle missing or null values gracefully
- Cache data after first load to reduce network requests

```javascript
// Good
let cachedData = null;

const getProductData = async () => {
  if (cachedData) return cachedData;
  
  const response = await fetch('/data/products.json');
  const data = await response.json();
  
  // Validate structure
  if (!Array.isArray(data) || data.length === 0) {
    throw new Error('Invalid data structure');
  }
  
  cachedData = data;
  return data;
};
```

## Software Development Life Cycle (SDLC)

Follow this iterative development process:

### 1. Planning
- Review requirements in GitHub Issues
- Break down features into small, testable units
- Identify dependencies and potential blockers
- Consider accessibility implications upfront

### 2. Design
- Sketch UI/UX before coding
- Ensure mobile-responsive from the start
- Validate color contrast and font sizes
- Plan keyboard navigation flow

### 3. Implementation
- Write semantic HTML first
- Add CSS styling (mobile-first)
- Implement JavaScript functionality
- Test incrementally (don't wait until the end)

### 4. Testing
- **Manual Testing**:
  - Test in multiple browsers (Chrome, Firefox, Safari, Edge)
  - Test on mobile devices (real devices preferred)
  - Test with keyboard only (no mouse)
  - Test with screen reader (NVDA, JAWS, VoiceOver)
  
- **Automated Testing**:
  - Validate HTML: [W3C Validator](https://validator.w3.org/)
  - Check accessibility: Browser DevTools, axe DevTools
  - Test contrast: WebAIM Contrast Checker

### 5. Deployment
- Commit with conventional commit message
- Push to GitHub
- Verify automatic deployment (GitHub Pages/Vercel)
- Test production site

### 6. Maintenance
- Monitor for issues
- Update dependencies if needed
- Refine based on user feedback

## Conventional Commits

Use [Conventional Commits](https://www.conventionalcommits.org/) specification for all commit messages.

### Format
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Types
- **feat**: New feature for the user
- **fix**: Bug fix for the user
- **docs**: Documentation changes
- **style**: Code style changes (formatting, missing semicolons, etc.)
- **refactor**: Code refactoring (no functional changes)
- **perf**: Performance improvements
- **test**: Adding or updating tests
- **build**: Changes to build system or dependencies
- **ci**: CI/CD configuration changes
- **chore**: Other changes (maintenance, cleanup)

### Scopes (for this project)
- **data**: Data-related changes
- **viz**: Observable visualizations
- **ui**: User interface components
- **a11y**: Accessibility improvements
- **search**: Search and filter functionality
- **comparison**: Comparison tool
- **nav**: Navigation components
- **styles**: CSS styling

### Examples

```bash
# Adding a new feature
feat(comparison): add side-by-side country comparison tool

# Fixing a bug
fix(search): correct filter logic for multi-word queries

# Improving accessibility
fix(a11y): add ARIA labels to visualization controls

Improves screen reader support for chart interactions.
Refs #12

# Documentation
docs: update README with deployment instructions

# Style/formatting
style(css): format stylesheets with consistent indentation

# Refactoring
refactor(data-loader): simplify async data fetching logic

# Performance
perf(viz): lazy-load Observable embeds on scroll

Reduces initial page load time by 40%.

# Breaking change
feat(data)!: change JSON structure for better querying

BREAKING CHANGE: Product data structure now uses nested objects
for additives. Update data-loader.js accordingly.
```

### Commit Message Best Practices

1. **Use imperative mood**: "add feature" not "added feature"
2. **Be specific**: "fix search filter" not "fix bug"
3. **Keep first line under 72 characters**
4. **Add body for complex changes**: Explain why, not what
5. **Reference issues**: Use `Refs #123` or `Closes #123`
6. **Breaking changes**: Add `!` after type/scope and `BREAKING CHANGE:` in footer

## Visual Design Principles

### Layout
- **Centered Content**: All narrative content centered with max-width of 680px
- **Generous Whitespace**: Use ample vertical spacing between sections (4rem minimum)
- **No sidebars**: Full-width storytelling, no distracting side elements
- **Scroll-driven narrative**: Content reveals naturally as user scrolls
- **Responsive breakpoints**: Adjust padding and font sizes for mobile (<768px)

### Typography Hierarchy
1. **Display Headlines** (4rem+): Large, bold statements, can incorporate illustrations
2. **Section Headlines** (2.5rem): Bold serif, dark purple, introduce major sections
3. **Subsection Headers** (1.5rem): Slightly smaller, maintain hierarchy
4. **Body Text** (1.125rem/18px): Comfortable reading size, serif, dark brown
5. **Captions/Small Text** (0.875rem): Secondary information

### Text Styling
- **Bold**: Use sparingly for emphasis within sentences
- **Italic**: For terms, proper nouns, or subtle emphasis
- **Highlighted text**: Yellow marker-style background for links or key terms
- **Links**: Underlined or highlighted, maintain readability

### Color Usage
- **Background**: Warm cream (#fef6e4), never pure white
- **Text**: Dark brown/maroon for body, deep purple for headings
- **Accents**: Yellow/gold for interactive elements and highlights
- **Illustrations**: Can use additional colors (pinks, purples) for visual interest
- **Contrast**: Always maintain WCAG AA standards (4.5:1 minimum)

### Visual Elements
- **Custom Illustrations**: Hand-drawn or artistic style preferred over stock photos
- **Circular Frames**: Use for profile images or featured items
- **Inline Graphics**: Integrate illustrations with text (e.g., letters made from food images)
- **Data Visualizations**: Clean, minimal design with accent colors
- **Loading States**: Friendly messages, not generic spinners

### Spacing Scale
```css
/* Consistent spacing rhythm */
--space-xs: 0.5rem;   /* 8px - tight spacing */
--space-sm: 1rem;     /* 16px - related elements */
--space-md: 1.5rem;   /* 24px - paragraphs */
--space-lg: 2.5rem;   /* 40px - subsections */
--space-xl: 4rem;     /* 64px - major sections */
--space-xxl: 6rem;    /* 96px - chapter breaks */
```

## Content Guidelines

### Narrative Voice
- **Personal but not self-indulgent**: Brief intro, then focus on data
- **Accessible language**: Explain technical terms without being condescending
- **Factual, not alarmist**: Present data objectively, let readers draw conclusions
- **Empowering tone**: Focus on awareness and action, not fear

### Data Visualization Principles
- Show data clearly without distortion
- Include context (scales, units, time periods)
- Use color purposefully (not just decoration)
- Provide multiple ways to access information (visual + text + data download)
- Tell a story with each visualization

### Writing Style
- Short paragraphs (2-4 sentences)
- Active voice preferred
- Vary sentence length for rhythm
- Use transition words for flow
- Proofread for clarity and conciseness

## Observable Embed Guidelines

### Integration Pattern

```html
<!-- Container with fallback -->
<div class="observable-container" role="region" aria-labelledby="viz-title">
  <h3 id="viz-title">Ingredient Complexity by Category</h3>
  
  <!-- Observable embed -->
  <div id="observablehq-viz-12345">
    <p>Loading visualization...</p>
  </div>
  <script type="module">
    import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@5/dist/runtime.js";
    import notebook from "https://api.observablehq.com/@username/notebook.js?v=3";
    
    const runtime = new Runtime();
    const main = runtime.module(notebook, name => {
      if (name === "chart") {
        return new Inspector(document.querySelector("#observablehq-viz-12345"));
      }
    });
  </script>
  
  <!-- Text alternative -->
  <details class="visualization-details">
    <summary>View data summary</summary>
    <p>Key findings: ...</p>
    <a href="/data/export.csv" download>Download full dataset (CSV)</a>
  </details>
</div>
```

### Best Practices
- Keep Observable notebooks modular (one concept per notebook)
- Document notebook parameters in Observable
- Test embeds in production environment (CDN can behave differently)
- Provide loading states
- Handle errors gracefully (network failures, browser compatibility)

## Git Workflow

### Branch Strategy
```bash
main          # Production-ready code
├── feature/* # New features (feature/comparison-tool)
├── fix/*     # Bug fixes (fix/search-filter)
└── docs/*    # Documentation (docs/update-readme)
```

### Development Flow

1. **Create feature branch**:
   ```bash
   git checkout -b feature/ingredient-search
   ```

2. **Make atomic commits**:
   ```bash
   # Stage specific changes
   git add scripts/search.js styles/search.css
   
   # Commit with conventional message
   git commit -m "feat(search): implement ingredient search functionality"
   ```

3. **Push and create PR**:
   ```bash
   git push origin feature/ingredient-search
   # Create pull request on GitHub
   ```

4. **After review and merge**:
   ```bash
   git checkout main
   git pull origin main
   git branch -d feature/ingredient-search
   ```

### Commit Checklist
Before committing, ensure:
- [ ] Code follows style guidelines
- [ ] Accessibility requirements met
- [ ] Manual testing completed
- [ ] No console errors or warnings
- [ ] Commit message follows conventional format
- [ ] Related issue referenced (if applicable)

## License Awareness

This project uses **dual licensing**:

### When Writing Code
- Code (HTML/CSS/JS) is **MIT Licensed**
- Include MIT license header in new JavaScript files:
  ```javascript
  /**
   * What Do You Eat - [Component Name]
   * Copyright (c) 2025 avgelix
   * Licensed under MIT License
   */
  ```

### When Writing Content
- Documentation and narrative content is **CC BY 4.0**
- Any reused content must be properly attributed
- Open Food Facts data must maintain attribution and ODbL compliance

## Common Pitfalls to Avoid

1. **Don't use external dependencies unnecessarily**: Stick to vanilla JS
2. **Don't skip accessibility**: It's not optional, build it in from the start
3. **Don't use generic commit messages**: "fix stuff" or "updates" are not helpful
4. **Don't make huge commits**: Break work into logical, reviewable chunks
5. **Don't ignore mobile**: Test mobile view constantly
6. **Don't hardcode values**: Use CSS variables and data-driven approaches
7. **Don't forget alt text**: Every image, chart, and diagram needs description
8. **Don't block the main thread**: Use async/await for data operations

## AI Assistant Guidelines

When working with this project, AI assistants should:

1. **Always provide functional commit messages** in conventional commits format when changes are made
2. **Follow SDLC with Conventional Commits**: Use semantic commit messages (feat:, fix:, docs:, style:, refactor:, test:, chore:)
3. **Commit often**: Make small, atomic commits after each logical change to maintain clear project history
4. **Prioritize accessibility** in all suggestions
5. **Maintain the established code style** and design patterns
6. **Ask clarifying questions** before making architectural decisions
7. **Suggest conventional commit messages** whenever user asks to commit or mentions committing

## Performance Considerations

- Lazy-load Observable embeds (only load when scrolling into view)
- Optimize images (compress, use appropriate formats)
- Minimize DOM manipulation (batch updates)
- Debounce search/filter inputs
- Cache API responses
- Minify assets for production (manual process before deployment)

## Questions or Updates?

If these instructions need clarification or updates:
1. Open an issue on GitHub
2. Suggest changes via pull request
3. Document decisions made during development

---

**Remember**: This project aims to make complex food data accessible and actionable. Every code decision should serve that goal while maintaining the highest standards of accessibility and web performance.

*Last updated: December 2025*

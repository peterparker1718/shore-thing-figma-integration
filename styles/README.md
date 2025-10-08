# Styles

This directory contains the design system's styles, design tokens, and global styling configuration for the Shore Thing application.

## Structure

```
styles/
├── tokens/           # Design tokens (colors, typography, spacing, etc.)
│   ├── colors.json
│   ├── typography.json
│   ├── spacing.json
│   ├── shadows.json
│   └── breakpoints.json
├── themes/           # Theme configurations (light, dark, etc.)
│   ├── light.css
│   ├── dark.css
│   └── theme.config.ts
├── global/           # Global styles and resets
│   ├── reset.css
│   ├── typography.css
│   └── utilities.css
├── mixins/           # Reusable style mixins and functions
└── variables.css    # CSS custom properties
```

## Design Tokens

Design tokens are the atomic units of our design system. They represent design decisions as data and ensure consistency across all platforms.

### Token Categories

#### Colors
- **Primary**: Brand colors for primary actions and key UI elements
- **Secondary**: Supporting colors for secondary actions and accents
- **Neutral**: Grayscale palette for text, backgrounds, and borders
- **Semantic**: Colors with specific meaning (success, warning, error, info)
- **Surfaces**: Background colors for different surface levels

#### Typography
- **Font Families**: Primary and secondary typeface definitions
- **Font Sizes**: Scale from small to display sizes
- **Font Weights**: Available weight variations
- **Line Heights**: Optimal line heights for different text sizes
- **Letter Spacing**: Tracking values for improved readability

#### Spacing
- **Base Unit**: 4px or 8px grid system
- **Scale**: Consistent spacing values (xs, sm, md, lg, xl, etc.)
- **Layout Spacing**: Margins and padding for layouts
- **Component Spacing**: Internal spacing for components

#### Shadows
- **Elevation Levels**: Shadow definitions for different z-axis levels
- **Focus States**: Shadows for keyboard focus indicators
- **Hover Effects**: Subtle shadows for interactive elements

#### Breakpoints
- **Mobile**: 320px - 767px
- **Tablet**: 768px - 1023px
- **Desktop**: 1024px - 1439px
- **Wide**: 1440px+

## Usage

### Importing Design Tokens

```typescript
import { colors, typography, spacing } from '@/styles/tokens';

// Use in JavaScript/TypeScript
const primaryColor = colors.primary[500];
const headingFont = typography.fontFamily.primary;
const spacing = spacing.md;
```

### Using CSS Variables

```css
/* Use CSS custom properties in your styles */
.component {
  color: var(--color-primary-500);
  font-family: var(--font-family-primary);
  padding: var(--spacing-md);
  box-shadow: var(--shadow-md);
}
```

### Theme Support

```typescript
import { ThemeProvider } from '@/styles/themes';

function App() {
  const [theme, setTheme] = useState('light');
  
  return (
    <ThemeProvider theme={theme}>
      <YourApp />
    </ThemeProvider>
  );
}
```

## Design Token Workflow

### 1. Extraction from Figma

Tokens are automatically extracted from Figma using the Figma API:

```bash
# Run the token extraction script
npm run extract-tokens
```

This script:
- Connects to the Figma API
- Extracts color styles, text styles, and effects
- Transforms them into design tokens
- Generates JSON files in the `tokens/` directory

### 2. Transformation

Tokens are transformed into multiple formats:

```bash
# Generate CSS variables, TypeScript types, and more
npm run transform-tokens
```

Outputs:
- `variables.css` - CSS custom properties
- `tokens.ts` - TypeScript constants and types
- `tokens.json` - Raw token data for tools

### 3. Validation

Tokens are validated against design system rules:

```bash
# Validate token consistency and accessibility
npm run validate-tokens
```

Validation checks:
- Color contrast ratios (WCAG AA/AAA compliance)
- Font size hierarchy
- Spacing scale consistency
- Token naming conventions

## Theming

The design system supports multiple themes:

### Light Theme (Default)
Optimized for daytime use with high contrast and vibrant colors.

### Dark Theme
Reduced brightness for low-light environments while maintaining accessibility.

### High Contrast Theme
Enhanced contrast for users with visual impairments (WCAG AAA compliance).

### Creating Custom Themes

```typescript
import { createTheme } from '@/styles/themes';

const customTheme = createTheme({
  colors: {
    primary: '#0066CC',
    secondary: '#FF6B35',
    // ... more color overrides
  },
  typography: {
    fontFamily: {
      primary: 'Inter, sans-serif',
    },
  },
});
```

## Responsive Design

All styles follow a mobile-first approach:

```css
/* Mobile first (default) */
.component {
  padding: var(--spacing-sm);
}

/* Tablet and up */
@media (min-width: 768px) {
  .component {
    padding: var(--spacing-md);
  }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .component {
    padding: var(--spacing-lg);
  }
}
```

## Accessibility

All design tokens are validated for accessibility:

- **Color Contrast**: Minimum 4.5:1 for normal text, 3:1 for large text
- **Focus Indicators**: Visible focus states for keyboard navigation
- **Touch Targets**: Minimum 44x44px for interactive elements
- **Motion**: Respects `prefers-reduced-motion` preference

## Best Practices

1. **Always use design tokens** instead of hard-coded values
2. **Never override token values** in component styles
3. **Request new tokens** if needed values don't exist
4. **Test theme switching** for all components
5. **Validate accessibility** when using color tokens
6. **Document custom mixins** and utility functions
7. **Keep global styles minimal** - prefer component-scoped styles

## Maintenance

### Updating Tokens from Figma

```bash
# Pull latest design changes from Figma
npm run sync-tokens

# Review changes
git diff styles/tokens/

# Test updated tokens
npm run test:tokens

# Commit changes
git commit -m "Update design tokens from Figma"
```

### Version Control

Token changes are versioned and documented:

- Major version: Breaking changes to token structure
- Minor version: New tokens added
- Patch version: Token value adjustments

## Resources

- [Design Tokens Specification](https://design-tokens.github.io/community-group/format/)
- [CSS Custom Properties Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- [WCAG Color Contrast Guidelines](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [Figma Design File](https://figma.com) (Access required)

## Contributing

For guidelines on contributing to the styles system, see [Contributing Guidelines](../documentation/CONTRIBUTING.md).

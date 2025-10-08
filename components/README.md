# Components

This directory contains the React components that mirror the Figma design system for the Shore Thing application.

## Structure

Components are organized by type and complexity:

```
components/
├── atoms/           # Basic building blocks (buttons, inputs, icons)
├── molecules/       # Simple component combinations
├── organisms/       # Complex UI sections
├── templates/       # Page-level layouts
└── pages/           # Full page implementations
```

## Component Guidelines

### Naming Conventions
- Use PascalCase for component names (e.g., `Button.tsx`, `NavBar.tsx`)
- Keep names descriptive and consistent with Figma layer names
- Use `.tsx` extension for TypeScript React components

### Component Structure

Each component should follow this structure:

```typescript
import React from 'react';
import styles from './ComponentName.module.css';

interface ComponentNameProps {
  // Props definition
}

export const ComponentName: React.FC<ComponentNameProps> = (props) => {
  // Component implementation
};
```

### Documentation

- Every component must include JSDoc comments
- Props should be clearly documented with types
- Include usage examples in Storybook
- Add visual regression tests for critical components

## Development Workflow

1. **Design Review**: Ensure Figma design is finalized
2. **Component Creation**: Build component matching design specs
3. **Testing**: Add unit tests and visual tests
4. **Documentation**: Create Storybook stories
5. **Review**: Submit PR for team review

## Figma Integration

Components are automatically synced with Figma designs:

- Component props map to Figma variants
- Styles use design tokens from the `styles/` directory
- Auto-generated component documentation from Figma descriptions

## Testing

All components must include:

- Unit tests (Jest + React Testing Library)
- Visual regression tests (Chromatic)
- Accessibility tests (jest-axe)

## Contributing

Refer to the main repository [Contributing Guidelines](../documentation/CONTRIBUTING.md) for detailed contribution instructions.

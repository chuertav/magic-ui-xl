# Contributing to Magic UI XL

First off, thank you for considering contributing to Magic UI XL! 🎉

## Ways to Contribute

### 🐛 Report Bugs
- Open an issue describing the bug
- Include steps to reproduce
- Share expected vs actual behavior

### 💡 Suggest Features
- Open an issue with the `enhancement` label
- Describe the component or template you'd like to see
- Include examples or mockups if possible

### 🔧 Submit Code
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-component`)
3. Make your changes
4. Test your changes
5. Commit (`git commit -m 'Add amazing component'`)
6. Push (`git push origin feature/amazing-component`)
7. Open a Pull Request

## Code Style

### Component Structure
```markdown
## Component Name

Brief description.

\`\`\`tsx
// TypeScript implementation with props interface
\`\`\`

**Usage:**
\`\`\`tsx
// Example usage
\`\`\`

**Required CSS:** (if any)
\`\`\`css
@keyframes animation-name { ... }
\`\`\`
```

### Guidelines
- Include TypeScript interfaces for all props
- Add artifact-ready versions for Claude.ai demos
- Document required dependencies
- Include usage examples
- Support dark mode

## Adding New Components

1. Choose the appropriate file in `references/`
2. Follow the existing component structure
3. Include both full and artifact-ready versions
4. Update `SKILL.md` catalog if needed

## Adding New Templates

1. Create a new file in `templates/`
2. Include section-by-section breakdown
3. Add complete artifact-ready version
4. Document all components used

## Questions?

Feel free to open an issue with the `question` label!

---

Thank you for helping make Magic UI XL better! ❤️

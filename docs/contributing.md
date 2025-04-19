# Contributing to NextScript

We love your input! We want to make contributing to NextScript as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code
- Submitting a fix
- Proposing new features
- Becoming a maintainer

## Development Process

We use GitHub to host code, to track issues and feature requests, as well as accept pull requests.

### Pull Request Process

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Git Commit Messages

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line to 72 characters or less
* Reference issues and pull requests liberally after the first line

Example:
```
feat(ui): add drag and drop support for components

- Implement drag and drop interface
- Add drop zone highlighting
- Include unit tests for drag events

Fixes #123
```

### Code Style Guidelines

#### TypeScript
- Use TypeScript for all new code
- Follow the existing code style
- Include type definitions
- Write unit tests

```typescript
// Good
interface UserProps {
  name: string;
  age: number;
}

const User: React.FC<UserProps> = ({ name, age }) => {
  return (
    <div>
      <h1>{name}</h1>
      <p>Age: {age}</p>
    </div>
  );
};

// Bad
const User = (props) => {
  return (
    <div>
      <h1>{props.name}</h1>
      <p>Age: {props.age}</p>
    </div>
  );
};
```

#### React Components
- Use functional components with hooks
- Props should be typed
- Use composition over inheritance
- Follow React best practices

### Documentation Guidelines

- Update README.md with details of changes to the interface
- Update API documentation for endpoint changes
- Include code examples where applicable
- Write clear commit messages

## Testing

### Running Tests
```bash
# Run all tests
npm test

# Run specific test file
npm test -- src/components/MyComponent.test.tsx

# Run tests in watch mode
npm test -- --watch
```

### Writing Tests
```typescript
import { render, fireEvent } from '@testing-library/react';
import { MyComponent } from './MyComponent';

describe('MyComponent', () => {
  it('should render correctly', () => {
    const { getByText } = render(<MyComponent />);
    expect(getByText('Hello')).toBeInTheDocument();
  });

  it('should handle click events', () => {
    const onClick = jest.fn();
    const { getByRole } = render(<MyComponent onClick={onClick} />);
    fireEvent.click(getByRole('button'));
    expect(onClick).toHaveBeenCalled();
  });
});
```

## Bug Reports

### Bug Report Template
```markdown
**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Environment:**
 - OS: [e.g. iOS]
 - Browser [e.g. chrome, safari]
 - Version [e.g. 22]
```

## Feature Requests

### Feature Request Template
```markdown
**Is your feature request related to a problem? Please describe.**
A clear and concise description of what the problem is.

**Describe the solution you'd like**
A clear and concise description of what you want to happen.

**Describe alternatives you've considered**
A clear and concise description of any alternative solutions or features.

**Additional context**
Add any other context or screenshots about the feature request here.
```

## Community

### Code of Conduct

#### Our Pledge
We pledge to make participation in our project and our community a harassment-free experience for everyone.

#### Our Standards
- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

### Getting Help

- Join our [Discord server](https://discord.gg/nextscript)
- Check out the [documentation](./README.md)
- Ask questions in [GitHub Discussions](https://github.com/yourusername/nextscript/discussions)

## License

By contributing, you agree that your contributions will be licensed under its MIT License.

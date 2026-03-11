# AGENTS.md - Agentic Coding Guidelines

This file provides guidelines for agentic coding agents operating in this repository.

## Project Overview

This is a new project. Before starting work, check if there's existing code to understand:
- The tech stack (framework, language, key libraries)
- Project structure and conventions
- Any existing configuration files (tsconfig.json, eslint.config.js, etc.)

---

## Build / Lint / Test Commands

### Common Commands

| Command | Description |
|---------|-------------|
| `npm run build` | Build the project |
| `npm run dev` | Start development server |
| `npm run lint` | Run linter |
| `npm run typecheck` | Run TypeScript type checking |
| `npm test` | Run all tests |
| `npm test -- --watch` | Run tests in watch mode |

### Running a Single Test

```bash
# Jest
npm test -- --testPathPattern="filename.spec"

# Vitest
npm test filename.spec

# Mocha
npm test -- --grep "test name"

# Pytest (Python)
pytest -k "test_name"

# Go
go test -run TestName ./...

# Rust
cargo test test_name
```

### Running Tests with Coverage

```bash
npm test -- --coverage
```

---

## Code Style Guidelines

### General Principles

- Keep functions small and focused (single responsibility)
- Write self-documenting code; add comments only for complex logic
- Use meaningful variable and function names
- Prefer explicit over implicit
- Handle errors explicitly; never swallow errors silently

### TypeScript / JavaScript

#### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables, functions | camelCase | `getUserData`, `isActive` |
| Classes, interfaces, types | PascalCase | `UserService`, `ApiResponse` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_BASE_URL` |
| Files (components) | PascalCase | `UserProfile.tsx` |
| Files (utilities, hooks) | camelCase | `formatDate.ts`, `useAuth.ts` |
| Boolean variables | is/has/can/should prefix | `isLoggedIn`, `hasPermission` |

#### Imports

```typescript
// Order: external → internal → relative
import React from 'react';
import { useState, useEffect } from 'react';
import { api } from '@/lib/api';
import { UserCard } from '@/components/UserCard';
import { formatDate } from '../utils/date';

// Named imports preferred over default
import { Button, Input } from '@/components/ui';
```

#### Type Definitions

- Always use explicit types for function parameters and return values
- Use interfaces for objects, type aliases for unions/intersections
- Avoid `any`; use `unknown` when type is truly unknown
- Use optional chaining (`?.`) and nullish coalescing (`??`)

```typescript
// Good
function getUser(id: string): Promise<User | null> {
  // ...
}

// Avoid
function getUser(id: any): any {
  // ...
}
```

#### React / Component Guidelines

- Use functional components with hooks
- Extract custom hooks for reusable stateful logic
- Keep components small (under 200 lines)
- Co-locate tests with components
- Use TypeScript for props

```typescript
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  return (
    <button className={variant} onClick={onClick}>
      {label}
    </button>
  );
}
```

### Error Handling

- Use try/catch for async operations
- Always handle promises with `.catch()` or `await` in try/catch
- Log errors with appropriate context
- Return meaningful error messages to users

```typescript
// Good
try {
  const data = await fetchUser(id);
  return data;
} catch (error) {
  logger.error('Failed to fetch user', { userId: id, error });
  return null;
}

// Avoid
const data = await fetchUser(id).catch(() => null);
```

### API / Backend Conventions

- Validate all input data
- Use appropriate HTTP status codes
- Return consistent response structures
- Log request/response for debugging
- Use transactions for multi-step operations

---

## Testing Guidelines

### Test Structure (AAA Pattern)

```typescript
describe('UserService', () => {
  describe('getUserById', () => {
    it('should return user when user exists', async () => {
      // Arrange
      const userId = '123';
      const mockUser = { id: '123', name: 'John' };

      // Act
      const result = await userService.getUserById(userId);

      // Assert
      expect(result).toEqual(mockUser);
    });
  });
});
```

### Testing Best Practices

- Test behavior, not implementation
- Use descriptive test names
- Mock external dependencies
- Test edge cases and error scenarios
- Aim for meaningful coverage of critical paths

---

## Git Conventions

- Use conventional commits: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`
- Keep commits atomic and focused
- Write descriptive PR titles and descriptions
- Never commit secrets or credentials
- Run lint/typecheck before committing

---

## File Organization

```
src/
├── components/      # Reusable UI components
├── features/        # Feature-specific code
├── hooks/           # Custom React hooks
├── lib/             # Library configurations
├── services/        # API/services
├── types/           # TypeScript types
├── utils/           # Utility functions
└── tests/           # Test utilities/fixtures
```

---

## Key Priorities

1. **Type Safety**: Use TypeScript, avoid `any`
2. **Error Handling**: Never silently fail
3. **Testing**: Write tests for new features
4. **Code Review**: Be thorough in reviews
5. **Documentation**: Document complex logic

---

## When in Doubt

- Follow the existing code style in the project
- Ask the user for clarification
- Check the README for project-specific instructions
- Look at similar files for patterns and conventions

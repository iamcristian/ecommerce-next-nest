# Contributing Guidelines

## Git Workflow

This project follows **Git Flow** for branch management and development.

### Branch Structure

```
main           (production-ready code)
  └─ develop   (integration branch for features)
       ├─ feature/user-authentication
       ├─ feature/product-catalog
       └─ feature/shopping-cart
```

### Branch Naming Conventions

- **Feature branches**: `feature/short-description`
  - Example: `feature/user-login`, `feature/payment-integration`
- **Bugfix branches**: `bugfix/issue-description`
  - Example: `bugfix/login-error`, `bugfix/cart-calculation`
- **Hotfix branches**: `hotfix/critical-issue`
  - Example: `hotfix/security-patch`
- **Release branches**: `release/v1.0.0`

### Development Workflow

#### 1. Starting New Feature

```bash
# Make sure develop is up to date
git checkout develop
git pull origin develop

# Create feature branch
git checkout -b feature/my-new-feature

# Work on your feature...
```

#### 2. Committing Changes

Follow **Conventional Commits** specification:

```bash
# Format: <type>(<scope>): <subject>
git commit -m "feat(auth): add user login endpoint"
git commit -m "fix(cart): correct total price calculation"
git commit -m "docs(readme): update installation steps"
```

**Commit Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependencies

#### 3. Before Pushing

Run quality checks:

```bash
# Backend
cd server
pnpm lint
pnpm test

# Frontend
cd ../client
pnpm lint
```

#### 4. Push and Create Pull Request

```bash
# Push your branch
git push -u origin feature/my-new-feature

# Go to GitHub and create Pull Request to 'develop'
```

#### 5. Merge to Develop

After PR approval:
- Squash and merge (preferred for clean history)
- Delete feature branch after merge

#### 6. Release to Production

```bash
# From develop, create release branch
git checkout develop
git pull origin develop
git checkout -b release/v1.0.0

# Make final adjustments, update version numbers
# Run full test suite

# Merge to main
git checkout main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main --tags

# Merge back to develop
git checkout develop
git merge release/v1.0.0
git push origin develop

# Delete release branch
git branch -d release/v1.0.0
```

### Code Review Guidelines

- All code must be reviewed before merging
- PRs should be focused and not too large
- Include tests for new features
- Update documentation when needed
- Ensure CI/CD passes

### Testing Requirements

- **Unit tests**: Required for new functions/methods
- **E2E tests**: Required for critical user flows
- **Coverage**: Aim for >80% code coverage

### Pull Request Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] E2E tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No new warnings
```

### Emergency Hotfixes

For critical production bugs:

```bash
# Create hotfix from main
git checkout main
git checkout -b hotfix/critical-bug

# Fix the issue
git commit -m "hotfix: fix critical security vulnerability"

# Merge to main
git checkout main
git merge hotfix/critical-bug
git tag -a v1.0.1 -m "Hotfix version 1.0.1"
git push origin main --tags

# Merge to develop
git checkout develop
git merge hotfix/critical-bug
git push origin develop
```

## Questions?

Open an issue or contact the team lead.

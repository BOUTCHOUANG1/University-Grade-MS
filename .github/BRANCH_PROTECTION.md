# Branch Protection Rules Configuration

This document outlines the recommended branch protection rules for the University Grade Management System repository.

## Recommended Branch Protection Rules for `main` Branch

### Required Settings

1. **Require a pull request before merging**
   - ✅ Enable "Require a pull request before merging"
   - ✅ Require approvals: **1** (minimum)
   - ✅ Dismiss stale PR approvals when new commits are pushed
   - ✅ Require review from code owners (CODEOWNERS file)

2. **Require status checks to pass before merging**
   - ✅ Enable "Require status checks to pass before merging"
   - ✅ Require branches to be up to date before merging
   - Add the following required status checks:
     - `build` (Maven build)
     - `test` (Unit tests)
     - `security-scan` (if implemented)

3. **Require linear history**
   - ✅ Enable "Require linear history"
   - This prevents merge commits and enforces a clean, linear Git history
   - Contributors must rebase their feature branches before merging

4. **Additional Security Settings**
   - ✅ Restrict pushes that create files larger than 100 MB
   - ✅ Require signed commits (recommended for enhanced security)
   - ✅ Lock branch (only allow force-pushes from admins)

### Implementation Steps

1. **Navigate to Repository Settings**
   ```
   Repository → Settings → Branches
   ```

2. **Add Branch Protection Rule**
   - Branch name pattern: `main`
   - Apply the settings listed above

3. **Configure Required Status Checks**
   - Add CI workflow names that must pass
   - Ensure workflows are running on PRs

## CI/CD Integration

The branch protection should work with these GitHub Actions workflows:

### Required Workflows (to be implemented)

```yaml
# .github/workflows/ci.yml
name: CI
on:
  pull_request:
    branches: [ main ]
  push:
    branches: [ main ]

jobs:
  build:
    name: Build and Test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 21
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'
      - name: Build with Maven
        run: ./mvnw clean compile
      - name: Run tests
        run: ./mvnw test
```

## Enforcement

With these rules in place:

- ✅ Direct pushes to `main` are blocked
- ✅ All changes must go through pull requests
- ✅ Code owner approval is required (@BOUTCHOUANG1)
- ✅ CI builds must pass before merging
- ✅ Branch must be up-to-date with main
- ✅ Linear history is maintained (no merge commits)

## Benefits

1. **Code Quality**: All changes are reviewed before merging
2. **Stability**: CI tests must pass, reducing broken builds
3. **Security**: Code owners review sensitive changes
4. **Clean History**: Linear history makes debugging easier
5. **Collaboration**: Encourages proper Git workflow

## Repository Owner Action Required

To implement these rules, the repository owner (@BOUTCHOUANG1) should:

1. Go to repository Settings → Branches
2. Click "Add rule" for the `main` branch
3. Configure the settings as outlined above
4. Set up CI workflows for automated testing
5. Consider implementing additional status checks as the project grows

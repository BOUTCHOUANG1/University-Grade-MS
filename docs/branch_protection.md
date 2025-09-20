# Branch Protection Rules

This document outlines the recommended branch protection rules for the `main` branch to ensure code quality and maintain a stable codebase.

## Recommended Settings for Main Branch

### 1. Require Pull Request Before Merging
- **Setting**: Enable "Require a pull request before merging"
- **Purpose**: Ensures all changes go through code review process
- **Configuration**:
  - Require approvals: At least 1 reviewer
  - Dismiss stale reviews when new commits are pushed
  - Require review from code owners (when CODEOWNERS file is present)

### 2. Require Status Checks to Pass
- **Setting**: Enable "Require status checks to pass before merging"
- **Purpose**: Ensures CI/CD pipeline passes before code is merged
- **Required Status Checks**:
  - CI Build (Maven compilation)
  - Unit Tests
  - Integration Tests (if available)
  - Security Scans (if configured)
  - Code Quality Checks (SonarQube, if configured)

### 3. Dismiss Stale Pull Request Approvals
- **Setting**: Enable "Dismiss stale pull request approvals when new commits are pushed"
- **Purpose**: Ensures reviewers see the latest changes before final approval
- **Benefit**: Prevents approved PRs from being merged with subsequent unreviewed changes

### 4. Enforce Linear History
- **Setting**: Enable "Require linear history"
- **Purpose**: Maintains a clean, linear git history without merge commits
- **Configuration**:
  - Only allow squash merging or rebase merging
  - Disable merge commits
  - This creates a cleaner project history and easier debugging

## Additional Recommendations

### 5. Require Branches to be Up to Date
- **Setting**: Enable "Require branches to be up to date before merging"
- **Purpose**: Ensures the PR includes the latest changes from main
- **Benefit**: Reduces conflicts and ensures tests run against the latest codebase

### 6. Restrict Pushes to Matching Branches
- **Setting**: Enable "Restrict pushes that create files that match a pattern"
- **Purpose**: Prevents direct pushes to main branch
- **Pattern**: Restrict all pushes to require pull requests

### 7. Allow Force Pushes (Administrators Only)
- **Setting**: Enable "Allow force pushes" for administrators only
- **Purpose**: Gives administrators ability to fix critical issues if needed
- **Caution**: Use sparingly and communicate with team

## Implementation Steps

1. Navigate to Repository Settings → Branches
2. Click "Add rule" or edit existing rule for `main` branch
3. Configure the following settings:
   - ☑ Require a pull request before merging
     - ☑ Require approvals (1)
     - ☑ Dismiss stale pull request approvals when new commits are pushed
     - ☑ Require review from code owners
   - ☑ Require status checks to pass before merging
     - ☑ Require branches to be up to date before merging
     - Add required status checks: CI, Tests, etc.
   - ☑ Require linear history
   - ☑ Include administrators (apply rules to admins too)
4. Save the protection rule

## Benefits

- **Code Quality**: All code is reviewed before merging
- **Stability**: Tests must pass before changes are accepted
- **History**: Clean linear history makes debugging easier
- **Security**: Code owners review ensures proper oversight
- **Collaboration**: Encourages proper development workflow

## Notes

- These settings should be configured after setting up CI/CD pipelines
- Adjust the number of required reviewers based on team size
- Consider adding specific status checks as your CI/CD pipeline matures
- Regularly review and update protection rules as the project evolves
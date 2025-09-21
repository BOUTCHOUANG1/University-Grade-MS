# GitHub Templates and Configuration

This directory contains GitHub templates and configuration files for the University Grade Management System repository.

## 📁 Contents

### Pull Request Template
- **`pull_request_template.md`** - Standard template for all pull requests with required checklist items including tests, documentation, security review, and database migrations.

### Issue Templates
- **`ISSUE_TEMPLATE/bug_report.yml`** - Structured template for bug reports with severity levels, environment details, and reproduction steps
- **`ISSUE_TEMPLATE/feature_request.yml`** - Comprehensive template for feature requests with problem statements, acceptance criteria, and technical considerations
- **`ISSUE_TEMPLATE/chore.yml`** - Template for maintenance tasks, refactoring, infrastructure work, and documentation updates
- **`ISSUE_TEMPLATE/config.yml`** - Configuration for issue templates with links to documentation and security reporting

### Code Review
- **`CODEOWNERS`** - Defines code ownership with @BOUTCHOUANG1 as the default reviewer for all files

### Repository Configuration
- **`REPOSITORY_CONFIGURATION.md`** - Comprehensive guide for setting up:
  - Branch protection rules for main branch
  - Recommended GitHub labels for triage (Type, Area, Priority, Size)
  - GitHub Project board integration
  - Security scanning setup
  - CLI commands for label creation

## 🚀 Features

### Pull Request Template Includes:
- ✅ Summary section for change description
- ✅ Comprehensive checklist covering tests, docs, security, and DB migrations
- ✅ Validation steps for reviewers
- ✅ Automatic issue linking with `Closes #ISSUE_ID`

### Issue Templates Support:
- 🐛 **Bug Reports**: Severity levels, affected areas, reproduction steps
- 🚀 **Feature Requests**: Problem statements, proposed solutions, acceptance criteria
- 🔧 **Chores**: Infrastructure tasks, refactoring, documentation updates

### Automatic Project Integration:
- All issue templates automatically link to the "Backend Roadmap" project board
- Issues are assigned to @BOUTCHOUANG1 by default
- Proper labeling for effective triage

## 🔧 Implementation

### Branch Protection (Recommended)
1. Require pull request reviews before merging
2. Require status checks (CI build/test) to pass
3. Dismiss stale approvals on new commits
4. Enforce linear history (no merge commits)

### Labels for Effective Triage
- **Type**: bug, feature, chore, docs, test
- **Area**: auth, db, grades, infra, ci, reports
- **Priority**: P0 (critical), P1 (high), P2 (medium), P3 (low)
- **Size**: S (small), M (medium), L (large)

See `REPOSITORY_CONFIGURATION.md` for detailed setup instructions and CLI commands.

## 📋 Usage

1. **Creating Issues**: Choose from Bug Report, Feature Request, or Chore templates
2. **Opening PRs**: Fill out the pull request template checklist
3. **Code Review**: All changes require approval from code owners
4. **Project Tracking**: Issues automatically appear in the Backend Roadmap board

## 🔒 Security

- Private security vulnerability reporting configured
- Code owners review required for all changes
- Branch protection prevents direct pushes to main
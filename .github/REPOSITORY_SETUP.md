# GitHub Repository Configuration Guide

This document provides recommendations for configuring GitHub repository settings to ensure code quality and proper workflow management.

## Branch Protection Rules for 'main'

To protect the main branch and ensure code quality, configure the following branch protection rules:

### Required Settings:
1. **Require a pull request before merging**
   - Require approvals: 1
   - Dismiss stale pull request approvals when new commits are pushed
   - Require review from code owners

2. **Require status checks to pass before merging**
   - Require branches to be up to date before merging
   - Status checks to require:
     - `CI Build` (when CI is set up)
     - `Tests` (when CI is set up)
     - `Security Scan` (when security scanning is configured)

3. **Require linear history**
   - Enforce a linear history by preventing merge commits
   - This keeps the commit history clean and easier to follow

4. **Additional Protections**
   - Restrict pushes that create files larger than 100MB
   - Require signed commits (recommended for security)
   - Do not allow bypassing the above settings (even for administrators)

### How to Configure:
1. Go to Repository Settings
2. Navigate to "Branches" section
3. Click "Add rule" for the main branch
4. Configure the settings as listed above

## Recommended Labels for Triage

### Type Labels:
- `Type: bug` - Bug reports and fixes
- `Type: feature` - New features and enhancements
- `Type: chore` - Maintenance, refactoring, and infrastructure tasks
- `Type: docs` - Documentation updates
- `Type: test` - Test-related changes

### Area Labels:
- `Area: auth` - Authentication and authorization
- `Area: db` - Database and data persistence
- `Area: grades` - Grade management functionality
- `Area: infra` - Infrastructure and deployment
- `Area: ci` - Continuous Integration and workflows
- `Area: reports` - Reporting functionality

### Priority Labels:
- `Priority: P0` - Critical issues requiring immediate attention
- `Priority: P1` - High priority issues
- `Priority: P2` - Medium priority issues
- `Priority: P3` - Low priority issues

### Size Labels:
- `Size: S` - Small tasks (1-2 days)
- `Size: M` - Medium tasks (3-5 days)
- `Size: L` - Large tasks (1+ weeks)

### Status Labels:
- `triage` - Needs initial review and classification
- `ready` - Ready for development
- `in-progress` - Currently being worked on
- `blocked` - Cannot proceed due to dependencies
- `needs-review` - Awaiting code review

### How to Create Labels:
1. Go to Repository Issues tab
2. Click on "Labels"
3. Create each label with appropriate color coding:
   - Type: Blue shades
   - Area: Green shades
   - Priority: Red/Orange/Yellow shades
   - Size: Purple shades
   - Status: Gray shades

## GitHub Project Board Integration

### Linking to 'Backend Roadmap' Project Board:

1. **Automatic Issue Assignment:**
   - Issues created from templates will automatically include the `triage` label
   - Set up automation rules in the project board to move issues with `triage` label to the "Triage" column
   - Configure rules to move issues to "Todo" when `ready` label is added
   - Move to "In Progress" when `in-progress` label is added

2. **Project Board Columns:**
   - **Triage** - New issues awaiting classification
   - **Backlog** - Prioritized but not yet scheduled
   - **Todo** - Ready for development
   - **In Progress** - Currently being worked on
   - **Review** - Awaiting code review
   - **Done** - Completed work

3. **Automation Rules:**
   - Auto-move issues when labels change
   - Auto-move PRs when they're opened/reviewed/merged
   - Auto-close issues when linked PRs are merged

### Setting up Automation:
1. Go to your GitHub Project Board
2. Click on "Automate" for each column
3. Set up the automation rules based on labels and PR status
4. Test the automation with a sample issue

## Getting Started Checklist:

- [ ] Configure branch protection rules for main branch
- [ ] Create all recommended labels
- [ ] Set up GitHub Project Board with automation
- [ ] Test issue templates by creating sample issues
- [ ] Test PR template by creating a sample PR
- [ ] Verify CODEOWNERS is working by checking review assignments
- [ ] Document any project-specific variations in README.md
# Repository Labels Configuration

This file defines the standard labels used for issue and pull request triage in the University Grade Management System.

## Type Labels
- **type: bug** 🐛 - Something isn't working
- **type: feature** ✨ - New feature or enhancement
- **type: chore** 🔧 - Maintenance, refactoring, or infrastructure
- **type: docs** 📚 - Documentation only changes
- **type: test** 🧪 - Adding missing tests or correcting existing tests

## Area Labels
- **area: auth** 🔐 - Authentication and authorization
- **area: db** 🗄️ - Database and data management
- **area: grades** 📊 - Grades and academic records
- **area: infra** 🏗️ - Infrastructure and deployment
- **area: ci** ⚙️ - Continuous integration and automation
- **area: reports** 📈 - Reports and analytics

## Priority Labels
- **P0** 🚨 - Critical (immediate attention required)
- **P1** 🔥 - High (should be addressed soon)
- **P2** ⚡ - Medium (normal priority)
- **P3** 🌱 - Low (when time permits)

## Size Labels
- **size: S** - Small change (< 1 day)
- **size: M** - Medium change (1-3 days)
- **size: L** - Large change (> 3 days)

## Status Labels
- **status: in-progress** 🚧 - Currently being worked on
- **status: blocked** 🚫 - Blocked by external dependency
- **status: needs-review** 👀 - Ready for code review
- **status: needs-testing** 🧪 - Needs manual testing

## Special Labels
- **good first issue** 👶 - Good for newcomers
- **help wanted** 🙋 - Extra attention is needed
- **duplicate** 📋 - This issue or pull request already exists
- **invalid** ❌ - This doesn't seem right
- **wontfix** ⛔ - This will not be worked on

## GitHub Project Integration

When using issue templates, issues are automatically:
1. Added to the "Backend Roadmap" project (project ID: 2)
2. Assigned appropriate labels based on the template
3. Prioritized according to the selections made

## Label Creation Script

Repository admins can use the GitHub CLI to create these labels:

```bash
# Type labels
gh label create "type: bug" --color "d73a4a" --description "Something isn't working"
gh label create "type: feature" --color "0075ca" --description "New feature or enhancement"
gh label create "type: chore" --color "fef2c0" --description "Maintenance, refactoring, or infrastructure"
gh label create "type: docs" --color "0052cc" --description "Documentation only changes"
gh label create "type: test" --color "1d76db" --description "Adding missing tests or correcting existing tests"

# Area labels
gh label create "area: auth" --color "5319e7" --description "Authentication and authorization"
gh label create "area: db" --color "006b75" --description "Database and data management"
gh label create "area: grades" --color "0e8a16" --description "Grades and academic records"
gh label create "area: infra" --color "8b5cf6" --description "Infrastructure and deployment"
gh label create "area: ci" --color "f97316" --description "Continuous integration and automation"
gh label create "area: reports" --color "84cc16" --description "Reports and analytics"

# Priority labels
gh label create "P0" --color "b60205" --description "Critical (immediate attention required)"
gh label create "P1" --color "d93f0b" --description "High (should be addressed soon)"
gh label create "P2" --color "fbca04" --description "Medium (normal priority)"
gh label create "P3" --color "0e8a16" --description "Low (when time permits)"

# Size labels
gh label create "size: S" --color "c2e0c6" --description "Small change (< 1 day)"
gh label create "size: M" --color "bfd4f2" --description "Medium change (1-3 days)"
gh label create "size: L" --color "f9d0c4" --description "Large change (> 3 days)"
```

## Usage Guidelines

### For Issues
- Always assign a **type** label
- Assign an **area** label when applicable
- Set **priority** based on business impact
- Estimate **size** for planning purposes

### For Pull Requests
- Inherit labels from linked issues when possible
- Add **status** labels to track progress
- Use **needs-review** when ready for review

### For Project Management
- Use priority labels for sprint planning
- Size labels help with capacity planning
- Area labels help assign to subject matter experts
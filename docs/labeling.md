# Repository Labels

This document outlines the suggested labeling system for organizing and categorizing issues and pull requests in the University Grade Management System repository.

## Label Categories

### Type Labels
Labels that indicate the type of work or issue:

- **`bug`** (🐛 #d73a4a) - Something isn't working correctly
- **`feature`** (✨ #a2eeef) - New feature or enhancement request
- **`chore`** (🔧 #fef2c0) - Infrastructure, refactoring, or maintenance tasks
- **`docs`** (📚 #0075ca) - Documentation improvements or additions
- **`test`** (🧪 #fbca04) - Testing improvements, new tests, or test fixes

### Area Labels
Labels that indicate which part of the system is affected:

- **`auth`** (🔐 #c5def5) - Authentication and authorization features
- **`db`** (🗄️ #e99695) - Database-related changes or issues
- **`grades`** (📊 #bfd4f2) - Grade management functionality
- **`infra`** (🏗️ #d4c5f9) - Infrastructure, deployment, or DevOps
- **`ci`** (⚙️ #ededed) - Continuous Integration and build processes
- **`reports`** (📈 #bfe5bf) - Reporting and analytics features

### Priority Labels
Labels that indicate the urgency or importance:

- **`P0`** (🚨 #b60205) - Critical priority - immediate attention required
- **`P1`** (⚡ #d93f0b) - High priority - should be addressed soon
- **`P2`** (📋 #fbca04) - Medium priority - normal development cycle
- **`P3`** (💡 #0e8a16) - Low priority - nice to have, future consideration

### Size Labels
Labels that indicate the estimated effort or complexity:

- **`S`** (🔹 #c2e0c6) - Small - Can be completed in 1-2 days
- **`M`** (🔸 #fef2c0) - Medium - Requires 3-5 days of work
- **`L`** (🔶 #f9d0c4) - Large - Significant effort, 1-2 weeks

## Additional Utility Labels

### Status Labels
- **`good first issue`** (👋 #7057ff) - Good for newcomers to the project
- **`help wanted`** (🙋 #008672) - Extra attention is needed from community
- **`wontfix`** (❌ #ffffff) - This will not be worked on
- **`duplicate`** (👥 #cfd3d7) - This issue or pull request already exists
- **`invalid`** (❓ #e4e669) - This doesn't seem right or is not reproducible

### Special Labels
- **`breaking change`** (💥 #b60205) - Changes that break backward compatibility
- **`security`** (🔒 #b60205) - Security-related issues or improvements
- **`performance`** (⚡ #0e8a16) - Performance improvements or issues
- **`dependency`** (📦 #ededed) - Dependency updates or related issues

## Usage Guidelines

### Combining Labels
Issues and PRs should typically have:
1. **One type label** (bug, feature, chore, docs, test)
2. **One or more area labels** (auth, db, grades, etc.)
3. **One priority label** (P0, P1, P2, P3)
4. **One size label** (S, M, L) - especially useful for planning

### Examples
- `bug` + `auth` + `P1` + `M` = Medium-sized, high-priority authentication bug
- `feature` + `grades` + `reports` + `P2` + `L` = Large, medium-priority feature affecting grades and reports
- `chore` + `infra` + `ci` + `P3` + `S` = Small, low-priority infrastructure maintenance task

### Label Management
- Repository maintainers should apply labels when issues/PRs are created
- Use consistent color coding for related label groups
- Review and update labels periodically as the project evolves
- Contributors can suggest label changes in comments

## Creating Labels in GitHub

### Via Web Interface
1. Go to repository → Issues → Labels
2. Click "New label"
3. Enter name, description, and color
4. Click "Create label"

### Bulk Creation Script
For creating all labels at once, you can use the GitHub CLI:

```bash
# Type labels
gh label create "bug" --description "Something isn't working correctly" --color "d73a4a"
gh label create "feature" --description "New feature or enhancement request" --color "a2eeef"
gh label create "chore" --description "Infrastructure, refactoring, or maintenance tasks" --color "fef2c0"
gh label create "docs" --description "Documentation improvements or additions" --color "0075ca"
gh label create "test" --description "Testing improvements, new tests, or test fixes" --color "fbca04"

# Area labels
gh label create "auth" --description "Authentication and authorization features" --color "c5def5"
gh label create "db" --description "Database-related changes or issues" --color "e99695"
gh label create "grades" --description "Grade management functionality" --color "bfd4f2"
gh label create "infra" --description "Infrastructure, deployment, or DevOps" --color "d4c5f9"
gh label create "ci" --description "Continuous Integration and build processes" --color "ededed"
gh label create "reports" --description "Reporting and analytics features" --color "bfe5bf"

# Priority labels
gh label create "P0" --description "Critical priority - immediate attention required" --color "b60205"
gh label create "P1" --description "High priority - should be addressed soon" --color "d93f0b"
gh label create "P2" --description "Medium priority - normal development cycle" --color "fbca04"
gh label create "P3" --description "Low priority - nice to have, future consideration" --color "0e8a16"

# Size labels
gh label create "S" --description "Small - Can be completed in 1-2 days" --color "c2e0c6"
gh label create "M" --description "Medium - Requires 3-5 days of work" --color "fef2c0"
gh label create "L" --description "Large - Significant effort, 1-2 weeks" --color "f9d0c4"
```

## Best Practices

1. **Be Consistent**: Always use the same labeling conventions
2. **Be Descriptive**: Label descriptions should be clear and helpful
3. **Regular Maintenance**: Review and clean up labels periodically
4. **Team Agreement**: Ensure all team members understand the labeling system
5. **Automation**: Consider using GitHub Actions to automatically apply labels based on file changes or keywords

This labeling system will help organize issues and pull requests, making it easier to prioritize work, track progress, and maintain the project effectively.
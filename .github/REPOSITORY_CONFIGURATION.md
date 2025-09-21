# GitHub Repository Configuration

This document outlines the recommended GitHub repository configuration for the University Grade Management System.

## Branch Protection Rules for `main`

To configure branch protection rules for the `main` branch, go to:
**Settings → Branches → Add rule** and configure the following:

### Recommended Settings:

1. **Branch name pattern**: `main`

2. **Protect matching branches**:
   - [x] **Require a pull request before merging**
     - [x] Require approvals: 1
     - [x] Dismiss stale pull request approvals when new commits are pushed
     - [x] Require review from code owners
   
   - [x] **Require status checks to pass before merging**
     - [x] Require branches to be up to date before merging
     - Status checks to require:
       - `build` (CI build)
       - `test` (CI tests)
       - `security-scan` (if implemented)
   
   - [x] **Require conversation resolution before merging**
   
   - [x] **Require linear history** (no merge commits)
   
   - [x] **Restrict pushes that create files larger than 100MB**

3. **Rules applied to administrators**:
   - [ ] Include administrators (allow admins to bypass rules for emergency fixes)

## Recommended GitHub Labels

### Type Labels
- `type:bug` - Bug reports and fixes (color: #d73a4a)
- `type:feature` - New features and enhancements (color: #0075ca)
- `type:chore` - Maintenance, refactoring, infrastructure (color: #7057ff)
- `type:docs` - Documentation updates (color: #0052cc)
- `type:test` - Testing improvements (color: #1a7f37)
- `type:security` - Security-related issues (color: #b60205)

### Area Labels
- `area:auth` - Authentication and authorization (color: #fef2c0)
- `area:db` - Database and data management (color: #fef2c0)
- `area:grades` - Grade management functionality (color: #fef2c0)
- `area:infra` - Infrastructure and DevOps (color: #fef2c0)
- `area:ci` - Continuous Integration (color: #fef2c0)
- `area:reports` - Reporting and analytics (color: #fef2c0)
- `area:ui` - User interface (color: #fef2c0)
- `area:api` - API and backend (color: #fef2c0)

### Priority Labels
- `priority:P0` - Critical/Urgent (color: #b60205)
- `priority:P1` - High priority (color: #d93f0b)
- `priority:P2` - Medium priority (color: #fbca04)
- `priority:P3` - Low priority (color: #0e8a16)

### Size Labels
- `size:S` - Small effort (1-2 days) (color: #c2e0c6)
- `size:M` - Medium effort (3-5 days) (color: #fef2c0)
- `size:L` - Large effort (1+ weeks) (color: #f9d0c4)

### Status Labels
- `status:triage` - Needs initial review (color: #ededed)
- `status:blocked` - Blocked by dependencies (color: #d93f0b)
- `status:in-progress` - Currently being worked on (color: #0075ca)
- `status:ready-for-review` - Ready for code review (color: #0e8a16)
- `status:waiting-for-feedback` - Waiting for feedback (color: #fbca04)

## GitHub Project Board Integration

### Backend Roadmap Project Board

To link issues created from templates to the "Backend Roadmap" project board:

1. **Create the Project Board** (if not exists):
   - Go to **Projects** tab
   - Create new project: "Backend Roadmap"
   - Choose "Table" or "Board" layout

2. **Configure Issue Templates**:
   - The issue templates already include `projects: ["BOUTCHOUANG1/1"]`
   - Update the project reference if your project has a different number
   - To find your project number: Go to Projects → Backend Roadmap → Settings → Note the URL (e.g., `/users/BOUTCHOUANG1/projects/1`)

3. **Automation Rules** (recommended):
   - **Auto-add to project**: All new issues automatically added
   - **Auto-move cards**:
     - When issue is assigned → Move to "In Progress"
     - When PR is opened → Move to "In Review"
     - When issue is closed → Move to "Done"

4. **Board Columns** (suggested):
   - 📥 **Triage** - New issues needing review
   - 📋 **Backlog** - Approved and prioritized issues
   - 🏗️ **In Progress** - Currently being worked on
   - 👀 **In Review** - Pull requests under review
   - ✅ **Done** - Completed issues

## Additional Recommendations

### Security Scanning
- Enable **Dependabot** for dependency updates
- Enable **CodeQL** for code scanning
- Enable **Secret scanning** for credential detection

### Required Status Checks
Configure these CI checks in your workflow (`.github/workflows/`):
- Build verification
- Unit tests
- Integration tests
- Code quality checks (SonarQube, CodeClimate)
- Security scans

### Merge Settings
- **Allow merge commits**: ❌ (Disabled for linear history)
- **Allow squash merging**: ✅ (Recommended)
- **Allow rebase merging**: ✅ (Alternative to squash)
- **Automatically delete head branches**: ✅ (Clean up merged branches)

## Implementation Commands

To create these labels programmatically using GitHub CLI:

```bash
# Type labels
gh label create "type:bug" --color d73a4a --description "Bug reports and fixes"
gh label create "type:feature" --color 0075ca --description "New features and enhancements"
gh label create "type:chore" --color 7057ff --description "Maintenance, refactoring, infrastructure"
gh label create "type:docs" --color 0052cc --description "Documentation updates"
gh label create "type:test" --color 1a7f37 --description "Testing improvements"

# Area labels
gh label create "area:auth" --color fef2c0 --description "Authentication and authorization"
gh label create "area:db" --color fef2c0 --description "Database and data management"
gh label create "area:grades" --color fef2c0 --description "Grade management functionality"
gh label create "area:infra" --color fef2c0 --description "Infrastructure and DevOps"
gh label create "area:ci" --color fef2c0 --description "Continuous Integration"

# Priority labels
gh label create "priority:P0" --color b60205 --description "Critical/Urgent"
gh label create "priority:P1" --color d93f0b --description "High priority"
gh label create "priority:P2" --color fbca04 --description "Medium priority"
gh label create "priority:P3" --color 0e8a16 --description "Low priority"

# Size labels
gh label create "size:S" --color c2e0c6 --description "Small effort (1-2 days)"
gh label create "size:M" --color fef2c0 --description "Medium effort (3-5 days)"
gh label create "size:L" --color f9d0c4 --description "Large effort (1+ weeks)"

# Status labels
gh label create "status:triage" --color ededed --description "Needs initial review"
gh label create "status:blocked" --color d93f0b --description "Blocked by dependencies"
gh label create "status:in-progress" --color 0075ca --description "Currently being worked on"
```
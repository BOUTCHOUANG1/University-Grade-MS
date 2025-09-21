# GitHub Project Integration Guide

This document explains how to integrate the issue templates and labels with the "Backend Roadmap" GitHub Project board.

## Project Setup

### Project Board: "Backend Roadmap"
- **Project ID**: 2 (referenced in issue templates)
- **Type**: Project (Beta) - Modern GitHub Projects
- **Visibility**: Repository-scoped

## Automatic Integration

The issue templates are configured to automatically:
1. Add new issues to the "Backend Roadmap" project
2. Apply appropriate labels based on template selections
3. Set initial priority levels

### Template Integration

Each issue template includes:
```yaml
projects: ["BOUTCHOUANG1/2"]
```

This automatically adds issues created from templates to the project board.

## Project Board Configuration

### Recommended Views

1. **Kanban Board View**
   - Columns: Backlog → In Progress → In Review → Done
   - Group by: Status
   - Filter: All open issues

2. **Priority View**
   - Group by: Priority (P0, P1, P2, P3)
   - Sort by: Created date (newest first)

3. **Area View**
   - Group by: Area labels
   - Useful for assigning work to specialists

4. **Sprint Planning View**
   - Filter by: Milestone or iteration
   - Group by: Size (S, M, L)

### Custom Fields

Add these custom fields to enhance project management:

1. **Status** (Single Select)
   - Backlog
   - In Progress  
   - In Review
   - Testing
   - Done

2. **Sprint** (Text)
   - Current sprint identifier

3. **Assignee** (People)
   - Team member responsible

4. **Effort** (Number)
   - Story points or time estimate

## Automation Rules

### Recommended GitHub Actions Automation

Create `.github/workflows/project-automation.yml`:

```yaml
name: Project Automation
on:
  issues:
    types: [opened, closed, reopened]
  pull_request:
    types: [opened, closed, merged]

jobs:
  auto-assign:
    runs-on: ubuntu-latest
    steps:
      - name: Add issue to project
        uses: actions/add-to-project@v0.4.0
        with:
          project-url: https://github.com/users/BOUTCHOUANG1/projects/2
          github-token: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Set status to "In Progress" when assigned
        if: github.event.action == 'assigned'
        uses: actions/github-script@v6
        with:
          script: |
            // Update project item status
            console.log('Setting status to In Progress')
```

### Manual Workflow

If automatic integration doesn't work initially:

1. **New Issue Created**
   - Automatically added to "Backend Roadmap" project
   - Placed in "Backlog" column
   - Labels applied based on template

2. **Issue Assignment**
   - Move to "In Progress" when assigned
   - Update custom fields as needed

3. **Pull Request Created**
   - Link to related issue
   - Move issue to "In Review" status

4. **Issue Completion**
   - Move to "Done" when PR is merged
   - Close related issue

## Benefits

### For Repository Owner (@BOUTCHOUANG1)
- **Centralized View**: All work visible in one place
- **Priority Management**: Easy to see what needs attention
- **Progress Tracking**: Visual status of all items
- **Planning**: Size estimates help with capacity planning

### For Contributors
- **Clear Process**: Templates guide proper issue creation
- **Visibility**: Can see project roadmap and priorities
- **Organization**: Easy to find related work by area/type

## Setup Instructions

### For Repository Owner

1. **Create Project Board**
   ```
   GitHub → Your Profile → Projects → New Project
   Name: "Backend Roadmap"
   Description: "University GMS development roadmap"
   ```

2. **Configure Views**
   - Add the recommended views listed above
   - Set up custom fields for better tracking

3. **Test Integration**
   - Create a test issue using one of the templates
   - Verify it appears in the project board
   - Confirm labels are applied correctly

4. **Train Team**
   - Share this documentation with contributors
   - Explain the workflow and expectations

### Workflow Example

1. **Bug Report Submission**
   ```
   User creates bug report → 
   Auto-added to project → 
   Triaged by owner → 
   Assigned priority → 
   Developer picks up → 
   Status: In Progress → 
   PR created → 
   Status: In Review → 
   PR merged → 
   Status: Done
   ```

## Troubleshooting

### Common Issues

1. **Issues not auto-adding to project**
   - Check project ID in templates
   - Verify repository permissions
   - Ensure project exists and is accessible

2. **Labels not being applied**
   - Verify labels exist in repository
   - Check template YAML syntax
   - Create missing labels using the script in LABELS.md

3. **Project access issues**
   - Ensure project visibility settings
   - Check repository member permissions

### Manual Fixes

If automation fails:
1. Manually add issues to project board
2. Apply labels according to LABELS.md
3. Set appropriate status and priority
4. Update custom fields as needed

## Future Enhancements

Potential improvements to consider:
- Automated milestone assignment
- Time tracking integration
- Slack/Teams notifications
- Custom dashboards and reporting
- Integration with external tools (Jira, etc.)
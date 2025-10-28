# Git Best Practices for VBUC Benchmark Project

## Branch Strategy

### Main Branches
- `main` - Production-ready code, stable releases
- `develop` - Integration branch for ongoing development

### Feature Branches
- `experiment/[experiment-id]-[short-description]` - For individual experiments
- `feature/[feature-name]` - For new features or significant improvements
- `bugfix/[issue-description]` - For bug fixes
- `optimization/[optimization-area]` - For performance improvements

### Example Branch Names
```
experiment/E001-initial-migration-analysis
experiment/E002-performance-optimization
feature/unit-testing-framework
bugfix/database-connection-issue
optimization/ui-response-time
```

## Commit Message Convention

### Format
```
[TYPE] Brief description (50 chars max)

More detailed explanation (if needed):
- Specific change 1
- Specific change 2
- Specific change 3

Relates to: #[issue-number]
Experiment: [experiment-id]
```

### Types
- `[EXPERIMENT]` - Changes related to experiments
- `[FEATURE]` - New features or functionality
- `[BUGFIX]` - Bug fixes
- `[OPTIMIZATION]` - Performance improvements
- `[REFACTOR]` - Code refactoring without functionality change
- `[DOCS]` - Documentation updates
- `[TEST]` - Test additions or modifications
- `[CONFIG]` - Configuration changes

### Examples
```
[EXPERIMENT] Add initial migration analysis for forms

Analyzed VBUC migration output for all forms:
- Documented compilation errors in frmMain
- Identified UI layout issues in frmCustomers
- Added baseline performance measurements

Experiment: E001
```

```
[BUGFIX] Fix database connection timeout issue

- Increased connection timeout from 30s to 60s
- Added retry logic for transient failures
- Improved error logging for debugging

Relates to: #123
```

```
[OPTIMIZATION] Improve form loading performance

- Implemented lazy loading for product grid
- Reduced memory allocation in customer search
- Optimized database queries for order lookup

Performance improvement: 40% faster form loading
Experiment: E003
```

## Workflow

### Starting a New Experiment
1. Create branch from `develop`
```bash
git checkout develop
git pull origin develop
git checkout -b experiment/E001-initial-migration-analysis
```

2. Make your changes and commit regularly
```bash
git add .
git commit -m "[EXPERIMENT] Document form migration issues"
```

3. Push branch and create pull request
```bash
git push origin experiment/E001-initial-migration-analysis
```

### Daily Development Workflow
1. Start with updated develop branch
2. Create feature/experiment branch
3. Make small, focused commits
4. Write descriptive commit messages
5. Push regularly to backup work
6. Create pull request when ready

### Before Committing
- [ ] Code compiles without errors
- [ ] Tests pass (when available)
- [ ] Documentation updated
- [ ] Experiment notes updated
- [ ] Performance impact documented (if applicable)

## File Organization Tips

### What to Commit
- Source code changes
- Documentation updates
- Configuration files
- Test files
- Experiment results (markdown files)
- Performance data (CSV, JSON)

### What NOT to Commit
- Build outputs (`bin/`, `obj/`)
- User-specific files (`.suo`, `.user`)
- Temporary files
- Large binary files
- Personal IDE settings
- Sensitive data (passwords, keys)

### .gitignore Essentials
The project should include these in `.gitignore`:
```
# Build results
[Dd]ebug/
[Dd]ebugPublic/
[Rr]elease/
[Rr]eleases/
x64/
x86/
bld/
[Bb]in/
[Oo]bj/

# Visual Studio files
.vs/
*.suo
*.user
*.sln.docstates

# Temporary files
*.tmp
*.temp
*.log
```

## Tagging Strategy

### Version Tags
```bash
# Major milestones
git tag -a v1.0.0 -m "Initial VBUC migration complete"
git tag -a v1.1.0 -m "First optimization cycle complete"

# Experiment completion
git tag -a exp-E001 -m "Initial migration analysis complete"
git tag -a exp-E002 -m "Performance optimization experiment complete"
```

### Push Tags
```bash
git push origin --tags
```

## Collaboration Guidelines

### Pull Request Process
1. Create descriptive PR title and description
2. Link to related experiment documentation
3. Include performance impact if applicable
4. Request review from team members
5. Update documentation before merging

### Code Review Checklist
- [ ] Code follows project standards
- [ ] Experiments are properly documented
- [ ] Performance impact is documented
- [ ] Tests pass (when available)
- [ ] No sensitive data exposed
- [ ] Documentation is updated

## Recovery and Backup

### Important Commands
```bash
# View commit history
git log --oneline --graph

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Create backup branch
git checkout -b backup/experiment-E001

# Recover deleted file
git checkout HEAD -- path/to/file
```

### Regular Backups
- Push branches regularly
- Tag important milestones
- Keep experiment documentation current
- Back up performance data externally

---
**Last Updated**: 2025-10-28
# REDAXO Documentation Repository

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Repository Overview

This is the official documentation repository for REDAXO CMS, a German PHP-based content management system. The repository contains exclusively Markdown documentation files and supporting image assets. All documentation is written in German.

**Live Documentation:** <https://redaxo.org/doku/main>

## Working Effectively

### Repository Structure
- **Root directory:** Contains 76 Markdown files covering all aspects of REDAXO CMS
- **assets/ directory:** Contains 65 PNG screenshot images for documentation
- **.github/ISSUE_TEMPLATE/:** Issue templates for documentation contributions
- **No build system:** This is a pure documentation repository with no compilation step

### Essential Commands
- Navigate to repository root: `cd /home/runner/work/docs/docs`
- Check repository status: `git --no-pager status`
- View repository structure: `ls -la` (shows all markdown files and assets directory)
- Count documentation files: `find . -name "*.md" | wc -l` (should return 76+)
- Count image assets: `ls assets/ | wc -l` (should return 65)
- Search across documentation: `grep -r "search-term" . --include="*.md"`

### Git Workflow
- Check current branch: `git branch -a`
- View recent changes: `git --no-pager log --oneline -5`
- Check for uncommitted changes: `git --no-pager status --porcelain`
- View differences: `git --no-pager diff`

## Validation

### Content Validation
Always validate documentation changes using these steps:

1. **Markdown Syntax Check:**
   - Verify files can be read: `head -5 filename.md`
   - Check for basic syntax issues by viewing content

2. **Image Link Validation:**
   - Find image references: `grep -r "\.png" . --include="*.md" | head -5`
   - Verify referenced images exist: `ls -la assets/image-name.png`
   - Note: Some files may have double extensions (.png.png) - this is intentional

3. **Cross-Reference Validation:**
   - Check internal links work within the documentation structure
   - Find internal markdown links: `grep -r '\[.*\](.*\.md)' . --include="*.md"`
   - Verify table of contents in dokumentation.md is updated when adding new files

4. **Style Guide Compliance:**
   - Follow German writing conventions
   - Use consistent terminology: "REDAXO", "AddOn", "PlugIn"
   - Include table of contents with anchor links for each new document
   - Use proper heading hierarchy (H1 for title, H2-H6 for sections)

### Content Search and Navigation
- Search for specific topics: `grep -r "installation\|backup\|addon" . --include="*.md" | wc -l` (returns ~310)
- Find references to external links: `grep -r "http" . --include="*.md" | wc -l` (returns ~110)
- Locate code examples: `grep -r '```' . --include="*.md" | wc -l` (returns ~930)
- Find internal markdown links: `grep -r '\[.*\](.*\.md)' . --include="*.md"`

## Common Tasks

### Repository Statistics
```bash
cd /home/runner/work/docs/docs
find . -name "*.md" | wc -l    # Count markdown files (76)
ls assets/ | wc -l             # Count images (65)
grep -r "REDAXO" . --include="*.md" | wc -l  # REDAXO mentions (390+)
```

### Key Documentation Files
- **dokumentation.md:** Master table of contents and index
- **README.md:** Contribution guidelines and formatting rules
- **installation.md:** REDAXO installation documentation
- **zusammenarbeit.md:** Collaboration and contribution process
- **einstieg.md:** Getting started guide

### Frequently Referenced Commands
```bash
# Repository overview
ls -la

# File content preview
head -10 filename.md

# Search for documentation topics
grep -r "keyword" . --include="*.md"

# Check git status
git --no-pager status

# View directory structure
find . -type d
```

### Sample Repository Output
```
ls -la /home/runner/work/docs/docs
total 756
drwxr-xr-x 5 runner docker  4096 .
drwxr-xr-x 3 runner docker  4096 ..
drwxr-xr-x 7 runner docker  4096 .git
drwxr-xr-x 3 runner docker  4096 .github
-rw-r--r-- 1 runner docker   380 LICENSE
-rw-r--r-- 1 runner docker  3145 README.md
[...75+ markdown files...]
drwxr-xr-x 2 runner docker  4096 assets
```

## Important Notes

### What Works
- ✅ Reading and editing Markdown files
- ✅ Git operations (status, diff, commit, push)
- ✅ File and content searching
- ✅ Image asset management

### What Does NOT Exist
- ❌ Build process (no package.json, Makefile, etc.)
- ❌ Test suite (no automated testing)
- ❌ CI/CD workflows (no GitHub Actions)
- ❌ Linting tools (no markdownlint or similar)
- ❌ Application runtime (pure documentation)

### Contribution Guidelines
Follow the style guide in README.md:
- Use German language consistently
- Include table of contents with anchor links
- Follow established naming conventions
- Place images in assets/ directory with v5.x.x prefix
- Update dokumentation.md index when adding new content
- Avoid direct address forms (Du/Sie), use "Du" if necessary
- Use consistent terminology: REDAXO, AddOn, PlugIn

### Time Expectations
- File reading/editing: Immediate
- Content searching: 1-5 seconds depending on scope
- Git operations: 1-3 seconds
- Repository exploration: Immediate (no build required)

Always validate that documentation changes follow the established format and include proper navigation elements before submitting pull requests.
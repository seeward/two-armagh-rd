# Release Process

This document describes how to create a release for the 2 Armagh 3D Property Viewer project.

## Overview

This project is a static web application deployed to Cloudflare Pages. Releases are created using Git tags and GitHub Releases.

## Prerequisites

- Write access to the repository
- Git installed locally
- GitHub CLI (`gh`) installed (optional, but recommended)

## Release Steps

### 1. Prepare for Release

Before creating a release, ensure:
- All changes for the release are committed and pushed to the main branch
- The application works correctly locally
- Any testing has been completed

### 2. Create a Git Tag

Releases are versioned using [Semantic Versioning](https://semver.org/):
- **MAJOR** version for incompatible changes
- **MINOR** version for new features (backwards-compatible)
- **PATCH** version for bug fixes (backwards-compatible)

Create and push a tag:

```bash
# Example: creating version 1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

### 3. Create a GitHub Release

#### Option A: Using GitHub CLI (Recommended)

```bash
# Create a release from the tag
gh release create v1.0.0 \
  --title "Version 1.0.0" \
  --notes "Description of changes in this release"
```

#### Option B: Using GitHub Web Interface

1. Go to the repository on GitHub
2. Click on "Releases" in the right sidebar
3. Click "Draft a new release"
4. Select the tag you created (e.g., `v1.0.0`)
5. Set the release title (e.g., "Version 1.0.0")
6. Add release notes describing the changes
7. Click "Publish release"

### 4. Deployment

The application is configured for Cloudflare Pages deployment (see `wrangler.json`). 

- **Automatic deployment**: If Cloudflare Pages is connected to this repository, pushes to the main branch and new tags will trigger automatic deployments
- **Manual deployment**: Use Wrangler CLI if needed:
  ```bash
  npx wrangler pages deploy .
  ```

## Release Notes Template

When creating release notes, include:

```markdown
## What's Changed

### Features
- New feature 1
- New feature 2

### Bug Fixes
- Fixed issue 1
- Fixed issue 2

### Improvements
- Improvement 1
- Improvement 2

### Dependencies
- Updated dependency X to version Y

## Assets

The application includes:
- `index.html` - Main application file
- `1.glb` - 3D model file
- `bg.exr` - Background environment texture
```

## Example: Creating Your First Release

```bash
# 1. Make sure you're on the main branch with latest changes
git checkout main
git pull origin main

# 2. Create a tag for version 1.0.0
git tag -a v1.0.0 -m "Initial release - 3D Property Viewer"

# 3. Push the tag
git push origin v1.0.0

# 4. Create the GitHub release
gh release create v1.0.0 \
  --title "Initial Release - v1.0.0" \
  --notes "🎉 First release of the 2 Armagh 3D Property Viewer

Features:
- Interactive 3D property viewing
- Waypoint navigation system
- Mobile-friendly controls
- macOS-style dock interface
- Hamburger menu with waypoint list
- EXR background support"
```

## Hotfix Releases

For urgent bug fixes:

```bash
# Create a patch version
git tag -a v1.0.1 -m "Hotfix: Fixed critical issue"
git push origin v1.0.1
gh release create v1.0.1 --title "Hotfix v1.0.1" --notes "Fixed critical issue X"
```

## Version History

To view all releases:

```bash
# List all tags
git tag -l

# View tag details
git show v1.0.0

# List GitHub releases
gh release list
```

## Best Practices

1. **Always tag from main branch** - Ensure releases are from stable code
2. **Write clear release notes** - Help users understand what changed
3. **Test before releasing** - Verify the application works locally
4. **Follow semantic versioning** - Makes version numbers meaningful
5. **Keep a changelog** - Consider maintaining a CHANGELOG.md file
6. **Tag signed commits** (optional) - For additional security:
   ```bash
   git tag -s v1.0.0 -m "Signed release v1.0.0"
   ```

## Troubleshooting

### Deleting a Tag (if needed)

```bash
# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin :refs/tags/v1.0.0

# Delete GitHub release (if created)
gh release delete v1.0.0
```

### Fixing a Release

If you need to update a release:

```bash
# Edit the release notes
gh release edit v1.0.0 --notes "Updated release notes"
```

## Additional Resources

- [GitHub Releases Documentation](https://docs.github.com/en/repositories/releasing-projects-on-github)
- [Semantic Versioning](https://semver.org/)
- [Cloudflare Pages Documentation](https://developers.cloudflare.com/pages/)
- [Wrangler CLI Documentation](https://developers.cloudflare.com/workers/wrangler/)

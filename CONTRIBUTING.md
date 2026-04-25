# Contributing to Pocket ID Community App Store

Thank you for interest in contributing! This guide explains how to add apps or improve existing ones.

## Before You Start

- Read our [README.md](README.md)
- Check [existing apps](Apps/) to avoid duplicates
- Understand [ZimaOS/CasaOS manifest format](https://www.zimaspace.com/docs/zimaos/Build-Apps)
- Test thoroughly on your own system first

## Adding a New Application

### Step 1: Prepare Application Files

Create folder: `Apps/{app-name}/`

Required files:
```
Apps/{app-name}/
├── docker-compose.yml       # ZimaOS/CasaOS manifest
├── icon.png or icon.svg     # Application icon (128x128+)
├── screenshot-1.png         # Main interface (required)
├── screenshot-2.png         # Additional features (optional)
└── README.md                # App-specific documentation (optional)
```

### Step 2: Create docker-compose.yml

Follow ZimaOS/CasaOS format with x-casaos metadata:

```yaml
name: app-name
services:
  app-service:
    image: registry/image:version
    restart: unless-stopped
    ports:
      - target: 8080
        published: $WebUI_PORT
    volumes:
      - type: bind
        source: /DATA/AppData/$AppID/data
        target: /app/data
    x-casaos:
      envs: []
      ports: []
      volumes: []

x-casaos:
  architectures:
    - amd64
    - arm64
  main: app-service
  category: Category
  description:
    en_us: "Short description of the app"
  title:
    en_us: "App Name"
  icon: https://url-to-icon
  port_map: "8080"
```

### Step 3: Create Icon

Requirements:
- **Size**: 128x128 pixels minimum
- **Format**: PNG or SVG
- **Style**: Professional, recognizable
- **Background**: Works on light/dark backgrounds
- **File**: `icon.png` or `icon.svg`

### Step 4: Capture Screenshots

See [Pocket ID SCREENSHOTS.md](Apps/pocket-id/SCREENSHOTS.md) for detailed instructions:

```
Apps/{app-name}/
├── screenshot-1.png   (Required - main interface)
├── screenshot-2.png   (Optional - additional features)
└── screenshot-3.png   (Optional - more features)
```

**Requirements**:
- Size: 1024x768 or similar aspect ratio
- Format: PNG (lossless)
- Quality: Clear, readable text
- Content: Show actual application interface

### Step 5: Write Documentation (Optional)

Create `Apps/{app-name}/README.md` with:
- What the app does
- Setup instructions
- Configuration options
- Troubleshooting
- Links to official resources

## Improving Existing Applications

### Fix Bugs in Manifest

Edit `Apps/{app-name}/docker-compose.yml`:
1. Test changes on your system
2. Verify ZimaOS/CasaOS compatibility
3. Commit with clear message
4. Create PR explaining fix

### Update to New Version

When app releases new version:
1. Update image tag in docker-compose.yml
2. Test with new version
3. Update screenshot if UI changed
4. Create PR with changelog reference

### Improve Documentation

Update `README.md`:
1. Fix typos or unclear sections
2. Add new tips or troubleshooting
3. Update links if needed
4. Improve examples

## Testing Requirements

Before submitting PR, test on actual ZimaOS/CasaOS:

- [ ] Application installs successfully
- [ ] Web UI is accessible
- [ ] All features work as expected
- [ ] Data persists after container restart
- [ ] Works with auto-assigned ports
- [ ] No sensitive data exposed
- [ ] Performance is acceptable
- [ ] Error messages are clear

## Manifest Validation

Validate docker-compose.yml:

```bash
docker-compose -f Apps/{app-name}/docker-compose.yml config
```

Check for:
- ✓ Valid YAML syntax
- ✓ No undefined variables
- ✓ x-casaos section present
- ✓ All required fields in x-casaos
- ✓ Specific image tags (no :latest)
- ✓ Proper port mapping

## Pull Request Process

### 1. Fork Repository
```bash
gh repo fork dn1ghtm/pocketid-appstore --clone
cd pocketid-appstore
```

### 2. Create Feature Branch
```bash
git checkout -b add/app-name
# or
git checkout -b fix/app-name-issue
```

### 3. Add Your Files
```bash
# For new app:
mkdir -p Apps/{app-name}
# Add files...

# For existing app:
# Edit files...
```

### 4. Commit Changes
```bash
git add Apps/{app-name}/
git commit -m "Add {app-name} application"
# or
git commit -m "Fix: {description of fix for app}"
```

### 5. Push and Create PR
```bash
git push origin add/app-name
gh pr create --fill
```

### 6. PR Description

Include:
```markdown
## Description
Brief description of app or changes

## Testing
- [x] Tested on ZimaOS/CasaOS
- [x] All features verified
- [x] Data persists correctly
- [x] Screenshots captured

## Manifest
- [x] Valid YAML
- [x] All x-casaos fields present
- [x] No hardcoded absolute paths
- [x] Specific image versions

## Links
- Official repo: [link]
- Docker Hub: [link]
- Docs: [link]
```

## App Store Standards

### Code Quality
- Docker images from official/trusted sources
- Specific version tags (never :latest)
- Health checks where possible
- Proper volume mounting
- Security best practices

### Documentation
- Clear setup instructions
- Configuration options explained
- Troubleshooting section
- Links to official resources
- Multi-language support (en_us minimum)

### User Experience
- Reasonable defaults
- Auto-assigned ports work
- Data persistence works
- Fast startup time
- Clear error messages

### Security
- No hardcoded secrets
- Environment variables for config
- Secure defaults
- Health checks enabled
- Updates encouraged

## Rejected Submissions

PRs may be rejected if:
- ❌ Uses :latest image tags
- ❌ No testing evidence provided
- ❌ Missing required files
- ❌ Security vulnerabilities
- ❌ Hardcoded paths/credentials
- ❌ Duplicate application
- ❌ Poor quality screenshots
- ❌ Incomplete documentation

## Questions?

### Documentation
- ZimaOS Build Guide: https://www.zimaspace.com/docs/zimaos/Build-Apps
- CasaOS Format: https://github.com/IceWhaleTech/CasaOS-AppStore
- Docker Compose: https://docs.docker.com/compose/

### Community
- GitHub Issues: Ask questions in issues
- Discussions: Feature requests and ideas
- Examples: Check existing apps

## Code of Conduct

- Be respectful and constructive
- Test before submitting
- Provide clear descriptions
- Accept feedback gracefully
- Help others learn

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in commit history
- Recognized for quality work

## License

By contributing, you agree that your contributions are licensed under the same license as this repository.

---

**Last Updated**: 2026-04-25  
**Questions?** Open an issue on GitHub  
**Ready to contribute?** Follow the steps above!

# Pocket ID Marketplace - Project Structure

Complete overview of the ZimaOS/CasaOS marketplace for Pocket ID.

## Directory Structure

```
pocketid-zimaos/
├── docker-compose.yml          # Main marketplace manifest (70 lines)
├── icon.svg                     # Application icon (128x128 SVG)
├── .env.example                 # Environment variables template
├── README.md                     # Main documentation and guide
├── QUICKSTART.md                # 5-minute quick start guide
├── CONTRIBUTING.md              # Marketplace submission guide
├── SCREENSHOTS.md               # Screenshot capture instructions
└── PROJECT_STRUCTURE.md         # This file
```

## File Descriptions

### 1. **docker-compose.yml** (Core Manifest)
- **Purpose**: ZimaOS/CasaOS marketplace definition
- **Contains**:
  - Service definition for Pocket ID
  - Image: `ghcr.io/pocket-id/pocket-id:v2`
  - Port mapping: 1411
  - Volume configuration: `/app/data`
  - x-casaos metadata (title, description, icons, etc.)
  - Environment variables (PUID, PGID, TZ)
  - Health checks
  - Multi-architecture support (amd64, arm64)

**Key Features**:
- Auto port assignment via `$WebUI_PORT`
- Proper volume binding for persistence
- Health check configured
- Multi-language support (en_us)
- Links to official documentation

### 2. **icon.svg** (Visual Asset)
- **Purpose**: Application icon for marketplace display
- **Specifications**:
  - 128x128px minimum
  - SVG format (scalable)
  - Passkey design (represents authentication)
  - Blue and green color scheme
  - Badge indicating security/verification

**Usage**:
- Displayed in ZimaOS/CasaOS app store
- Replace with official Pocket ID logo if available
- Can be converted to PNG (256x256 recommended)

### 3. **.env.example** (Configuration Template)
- **Purpose**: Example environment variables
- **Variables**:
  - `PUID` / `PGID` - Container user/group IDs
  - `TZ` - System timezone
  - `WebUI_PORT` - Web interface port
  - Optional: `DATABASE_URL` - PostgreSQL support
  - Optional: `JWT_SECRET` - Custom JWT secret
  - Optional: `CORS_ALLOWED_ORIGINS` - CORS configuration
  - Optional: `DEBUG` - Debug logging

**Usage**:
- Copy to `.env` for custom configuration
- Most defaults work out-of-the-box
- For PostgreSQL, update `DATABASE_URL`

### 4. **README.md** (Main Documentation)
- **Purpose**: Comprehensive setup and usage guide
- **Sections**:
  - What is Pocket ID?
  - Installation instructions
  - Basic and advanced configuration
  - First access and setup
  - Using as OIDC provider
  - Persistence and storage
  - Requirements and specs
  - Troubleshooting guide
  - Links to official resources

**Audience**: End users installing on ZimaOS/CasaOS

### 5. **QUICKSTART.md** (Fast Setup)
- **Purpose**: 5-minute deployment guide
- **Covers**:
  - Step-by-step installation via UI
  - Initial account setup
  - Passkey configuration
  - OIDC application setup
  - Common troubleshooting
  - Backup and recovery
  - Performance tips
  - Security notes

**Audience**: Users who want fast deployment

### 6. **CONTRIBUTING.md** (Marketplace Guide)
- **Purpose**: Instructions for marketplace submission
- **Includes**:
  - Submission checklist
  - Testing requirements
  - Asset requirements (icons, screenshots)
  - Manifest validation
  - Submission process for ZimaOS/CasaOS
  - PR description template
  - Multi-language support guide
  - Version update procedures
  - Troubleshooting submissions

**Audience**: Developers submitting to app stores

### 7. **SCREENSHOTS.md** (Visual Content Guide)
- **Purpose**: How to capture and prepare screenshots
- **Contains**:
  - Screenshot requirements and sizes
  - Step-by-step capture instructions
  - Tools and resources
  - Content guidelines (do's/don'ts)
  - Recommended screenshot sequence
  - File optimization tips
  - Preparation checklist

**Audience**: Marketplace contributors

### 8. **PROJECT_STRUCTURE.md** (This File)
- **Purpose**: Overview of all project files
- **Contains**: This complete structure documentation

## Marketplace Submission Workflow

### Prerequisites
1. ✅ docker-compose.yml - Valid YAML with x-casaos metadata
2. ✅ icon.svg - 128x128 or larger, clear design
3. ⚠️ screenshot-1.png - Not yet created (required)
4. ⚠️ screenshot-2.png - Not yet created (optional)
5. ✅ README.md - Comprehensive documentation
6. ✅ .env.example - Environment variables

### Steps to Submit

#### 1. Create Screenshots
```bash
# Deployment instance needed
1. Deploy Pocket ID on ZimaOS/CasaOS
2. Create test admin account
3. Configure passkey
4. Capture main interface (screenshot-1.png)
5. Capture settings/features (screenshot-2.png)
# See: SCREENSHOTS.md for detailed instructions
```

#### 2. Test Deployment
- ✅ Deploy on own ZimaOS/CasaOS instance
- ✅ Verify all functionality works
- ✅ Test data persistence
- ✅ Test with different ports
- ✅ Test on both amd64 and arm64 (if possible)

#### 3. Prepare Submission Package
```
Apps/pocket-id/
├── docker-compose.yml
├── icon.svg
├── screenshot-1.png
├── screenshot-2.png (optional)
└── README.md (optional)
```

#### 4. Fork and Submit
- Fork official marketplace repo
- Create folder: `Apps/pocket-id/`
- Copy files as shown above
- Create Pull Request with evidence

#### 5. Marketplace Options

**ZimaOS AppStore**:
- Repo: https://github.com/arvindmeena/ZimaOS-AppStore
- Process: Fork → Add files → PR

**CasaOS AppStore**:
- Repo: https://github.com/IceWhaleTech/CasaOS-AppStore
- Process: Fork → Add files → PR

## Configuration Reference

### Environment Variables
```env
# Required/Common
PUID=1000               # Container UID
PGID=1000               # Container GID
TZ=UTC                  # Timezone
WebUI_PORT=1411         # Web port

# Optional
DATABASE_URL=           # PostgreSQL URL
JWT_SECRET=             # JWT signing secret
CORS_ALLOWED_ORIGINS=   # CORS origins
DEBUG=false             # Debug logging
```

### Ports
- **Default**: 1411 (Pocket ID web interface)
- **ZimaOS/CasaOS**: Auto-assigned to available port

### Volumes
- **Data**: `/app/data` (mounted to `/DATA/AppData/$AppID/data`)
- **Content**: SQLite database, configuration files, credentials

### Supported Architectures
- ✅ amd64 (Intel/AMD x64)
- ✅ arm64 (ARM 64-bit, Raspberry Pi 4+)
- ❌ arm/v7 (32-bit ARM - not supported)

## Technical Specifications

### System Requirements
- **CPU**: Minimal (100m recommended)
- **Memory**: 256MB minimum, 512MB recommended
- **Storage**: 100MB+ for data volume
- **Network**: Port 1411 configurable

### Docker Configuration
- **Image**: `ghcr.io/pocket-id/pocket-id:v2` (latest v2)
- **Restart**: `unless-stopped` (auto-restart on failure)
- **Health Check**: 30-second intervals, 10-second startup grace
- **User**: Configurable via PUID/PGID

### Features
- ✅ Passkey/WebAuthn authentication
- ✅ OIDC protocol support
- ✅ SQLite (default) or PostgreSQL
- ✅ Multi-user support
- ✅ Account management UI
- ✅ OIDC application configuration
- ✅ Secure token generation
- ✅ Health check endpoints

## Documentation Map

```
├── README.md (start here)
│   ├── What is Pocket ID?
│   ├── Installation guide
│   ├── Configuration options
│   └── Troubleshooting
├── QUICKSTART.md (5-min setup)
│   ├── Step-by-step UI install
│   ├── Initial setup
│   └── First login
├── CONTRIBUTING.md (marketplace)
│   ├── Submission checklist
│   ├── Testing requirements
│   ├── PR template
│   └── Version updates
└── SCREENSHOTS.md (visual assets)
    ├── How to capture
    ├── Tools and resources
    └── Preparation checklist
```

## Checklist for Release

- [x] docker-compose.yml created and validated
- [x] x-casaos metadata configured
- [x] icon.svg created
- [x] .env.example with all options
- [x] README.md comprehensive documentation
- [x] QUICKSTART.md for fast deployment
- [x] CONTRIBUTING.md with submission guide
- [x] SCREENSHOTS.md with capture instructions
- [ ] screenshot-1.png (needs deployment)
- [ ] screenshot-2.png (optional, needs deployment)
- [ ] Test deployment on ZimaOS/CasaOS
- [ ] Verify all functionality works
- [ ] Submit to marketplaces

## Quick Commands

```bash
# Validate docker-compose syntax
docker-compose config

# Test locally
docker-compose up -d

# View logs
docker-compose logs -f

# Stop container
docker-compose down

# Check image
docker pull ghcr.io/pocket-id/pocket-id:v2
```

## External Links

**Official Resources**:
- Website: https://pocket-id.org
- GitHub: https://github.com/pocket-id/pocket-id
- Docker: https://hub.docker.com/r/11notes/pocket-id
- Docs: https://pocket-id.org/docs

**Marketplaces**:
- ZimaOS: https://github.com/arvindmeena/ZimaOS-AppStore
- CasaOS: https://github.com/IceWhaleTech/CasaOS-AppStore

**Standards**:
- OIDC: https://openid.net/connect/
- WebAuthn: https://webauthn.io/
- Docker Compose: https://docs.docker.com/compose/

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-04-25 | Initial release - complete marketplace manifest |

## Next Steps

1. **Create Screenshots**
   - Deploy instance
   - Capture interface
   - See SCREENSHOTS.md

2. **Test Thoroughly**
   - ZimaOS/CasaOS deployment
   - Verify functionality
   - Test persistence

3. **Submit to Marketplace**
   - Choose marketplace (ZimaOS or CasaOS)
   - Follow CONTRIBUTING.md
   - Create Pull Request

4. **Maintenance**
   - Monitor Pocket ID releases
   - Update image version when needed
   - Keep documentation current

---

**Created**: 2026-04-25  
**Project**: Pocket ID ZimaOS/CasaOS Marketplace  
**Status**: Ready for screenshot and testing phase

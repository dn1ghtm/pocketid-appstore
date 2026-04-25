# Pocket ID Community App Store

Community-maintained app store for ZimaOS and CasaOS with pre-configured Pocket ID application.

## About

This is a specialized app store containing the [Pocket ID](https://pocket-id.org) application - a self-hosted, open-source OIDC provider for passkey-based authentication.

**Ready to use**: Just add this app store to your ZimaOS/CasaOS and install Pocket ID in one click.

## Quick Start

### Add to ZimaOS/CasaOS

1. Open ZimaOS/CasaOS dashboard
2. Go to **App Store** → **Settings** or **Manage App Stores**
3. Click **Add App Store**
4. Enter URL:
   ```
   https://raw.githubusercontent.com/dn1ghtm/pocketid-appstore/main/Apps/pocket-id/docker-compose.yml
   ```
   OR for full store metadata:
   ```
   https://github.com/dn1ghtm/pocketid-appstore
   ```
5. Click **Add**
6. Find "Pocket ID" in app store
7. Click **Install**

### Manual Installation

If your ZimaOS/CasaOS supports direct docker-compose import:

```yaml
# Copy the content from:
# Apps/pocket-id/docker-compose.yml
```

## What's Included

### Apps
- **Pocket ID** (v2 latest)
  - Self-hosted OIDC provider
  - Passkey authentication
  - Multi-user support
  - SQLite (default) + PostgreSQL option

## Documentation

- **[Pocket ID Setup](Apps/pocket-id/README.md)** - Complete setup and configuration guide
- **[Quick Start](Apps/pocket-id/QUICKSTART.md)** - 5-minute deployment guide
- **[Screenshots](Apps/pocket-id/SCREENSHOTS.md)** - How to capture marketplace assets
- **[Contributing](CONTRIBUTING.md)** - How to contribute to this app store

## Directory Structure

```
.
├── Apps/
│   └── pocket-id/
│       ├── docker-compose.yml    # Marketplace manifest
│       ├── icon.svg              # Application icon
│       ├── .env.example          # Configuration template
│       ├── README.md             # Setup guide
│       ├── QUICKSTART.md         # Fast deployment
│       ├── SCREENSHOTS.md        # Asset capture guide
│       └── CONTRIBUTING.md       # Submission guide
├── README.md                      # This file
├── CONTRIBUTING.md               # App store contribution guide
└── LICENSE                        # License information
```

## Features

✅ **Pre-configured** - Pocket ID ready to install  
✅ **Multi-architecture** - Works on amd64 and arm64  
✅ **Documentation** - Complete setup and integration guides  
✅ **Community-maintained** - Open to contributions  
✅ **Open source** - Full transparency  

## Installation Requirements

- ZimaOS or CasaOS installed
- 256MB+ available RAM
- 100MB+ storage for data
- Network access

## First Access

After installation:

1. Open Pocket ID web interface (port auto-assigned)
2. Create admin account
3. Set up your first passkey
4. Configure OIDC applications (optional)
5. Start using for authentication

## Configuration

All settings customizable via environment variables. See:
- **[Apps/pocket-id/.env.example](Apps/pocket-id/.env.example)** - All available options
- **[Apps/pocket-id/QUICKSTART.md](Apps/pocket-id/QUICKSTART.md)** - Configuration walkthrough

## Integrations

Use Pocket ID as OIDC provider for:
- Web applications
- Self-hosted services
- Any OIDC-compatible app

See [setup guide](Apps/pocket-id/QUICKSTART.md) for integration examples.

## Support

### Documentation
- **Official Pocket ID**: https://pocket-id.org
- **GitHub**: https://github.com/pocket-id/pocket-id
- **Docker Hub**: https://hub.docker.com/r/11notes/pocket-id

### This App Store
- **Issues**: GitHub issues for this repository
- **Contributing**: See [CONTRIBUTING.md](CONTRIBUTING.md)

## Contributing

Want to add more apps or improve Pocket ID configuration?

See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to add new applications
- How to suggest improvements
- How to report issues
- Code of conduct

## License

- **App Store**: [See LICENSE file](LICENSE)
- **Pocket ID**: Open source (see https://github.com/pocket-id/pocket-id)

## Roadmap

Potential future additions:
- [ ] Additional OIDC providers
- [ ] Authentication middleware apps
- [ ] Identity management tools
- [ ] Security-focused applications

## Community

- GitHub: https://github.com/dn1ghtm/pocketid-appstore
- Pocket ID: https://github.com/pocket-id/pocket-id
- Issues: Report bugs and suggest features

## Disclaimer

This is a community-maintained app store. While we strive for quality and security:
- Test thoroughly before production use
- Report security issues responsibly
- Keep applications updated
- Back up important data

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-04-25 | Initial release with Pocket ID |

---

**Last Updated**: 2026-04-25  
**Repository**: https://github.com/dn1ghtm/pocketid-appstore  
**Maintainer**: Community

Need help? Check the [Pocket ID documentation](Apps/pocket-id/README.md) or [Contributing guide](CONTRIBUTING.md).

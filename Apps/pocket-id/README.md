# Pocket ID - ZimaOS/CasaOS Application

Self-hosted, open-source OIDC provider for passkey-based authentication.

## What is Pocket ID?

Pocket ID is a simple and easy-to-use OIDC (OpenID Connect) provider that enables password-free authentication using passkeys. It serves as a privacy-first alternative to external authentication services, giving you complete control over your identity management infrastructure.

**Key Features:**
- Passkey/WebAuthn authentication (no passwords needed)
- OpenID Connect (OIDC) protocol support
- Self-hosted and privacy-centric
- Multi-account support with multiple passkeys per user
- SQLite (default) or PostgreSQL database
- Multi-user support
- Secure token generation
- Health checks enabled

## Quick Start

1. **Install**: Add this app store to ZimaOS/CasaOS
2. **Deploy**: Click "Install" for Pocket ID
3. **Access**: Open web interface at assigned port
4. **Setup**: Create admin account and add passkey
5. **Use**: Configure OIDC applications

See [QUICKSTART.md](QUICKSTART.md) for detailed steps.

## System Requirements

- **CPU**: Minimal (100m recommended)
- **Memory**: 256MB minimum, 512MB recommended
- **Storage**: 100MB+ for data volume
- **Network**: Port 1411 (configurable)

## Installation

### Via ZimaOS/CasaOS App Store
1. Open ZimaOS/CasaOS dashboard
2. Go to **App Store**
3. Search for "Pocket ID"
4. Click **Install**
5. Wait for deployment (1-2 minutes)

### Manual Configuration
Edit `.env.example` before deployment:
```env
PUID=1000               # Container user ID
PGID=1000               # Container group ID
TZ=UTC                  # System timezone
WebUI_PORT=1411         # Web interface port (auto-assigned)
```

For PostgreSQL:
```env
DATABASE_URL=postgresql://user:pass@host:5432/pocket_id
```

See `.env.example` for all options.

## First Access

1. Open web interface (port shown in app details)
2. **Create Admin Account**:
   - Email: admin@example.com (or any email)
   - Password: Strong password
3. **Add Passkey**:
   - Click "Add Passkey"
   - Follow browser prompts
   - Confirm passkey creation
4. **Done**: You're now authenticated!

## Using as OIDC Provider

### Configure OIDC Application

1. Go to **Settings** → **OIDC Applications**
2. Click **Create Application**
3. Fill in details:
   - Name: Your application name
   - Redirect URI: `https://yourapp.com/auth/callback`
4. Copy **Client ID** and **Client Secret**

### OIDC Endpoints

Your application uses:
```
Authorization:  http://pocket-id-host:port/oauth/authorize
Token:          http://pocket-id-host:port/oauth/token
UserInfo:       http://pocket-id-host:port/oauth/userinfo
```

### Example Integration (Node.js)

```javascript
const passport = require('passport');
const OpenIDConnectStrategy = require('passport-openidconnect').Strategy;

passport.use('oidc', new OpenIDConnectStrategy({
  issuer: 'http://pocket-id:1411',
  authorizationURL: 'http://pocket-id:1411/oauth/authorize',
  tokenURL: 'http://pocket-id:1411/oauth/token',
  userInfoURL: 'http://pocket-id:1411/oauth/userinfo',
  clientID: 'your-client-id',
  clientSecret: 'your-client-secret',
  callbackURL: 'http://localhost:3000/auth/callback'
}, (issuer, sub, profile, done) => {
  return done(null, profile);
}));
```

## Configuration

### Environment Variables

| Variable | Default | Purpose |
|----------|---------|---------|
| PUID | 1000 | User ID for container |
| PGID | 1000 | Group ID for container |
| TZ | UTC | System timezone |
| WebUI_PORT | 1411 | Web interface port |
| DATABASE_URL | (empty) | PostgreSQL connection (optional) |
| JWT_SECRET | (auto) | JWT signing secret (optional) |
| CORS_ALLOWED_ORIGINS | * | CORS origins (optional) |
| DEBUG | false | Enable debug logging (optional) |

### Data Persistence

Data stored in `/app/data` (persistent volume):
- SQLite database (if using default)
- Configuration files
- User credentials
- Passkey data

Data persists across container restarts.

## Troubleshooting

### Container Won't Start
**Solution**: Check app logs in dashboard
- Verify disk space available
- Check configuration syntax
- Restart container

### Can't Access Web Interface
**Solution**: Verify network connectivity
- Check assigned port in app details
- Confirm "Running" status
- Try accessing via IP: `http://<zimaos-ip>:<port>`

### Forgot Password
**Solution**: Backup and reset
1. Stop Pocket ID app
2. Access data volume: `/DATA/AppData/<AppID>/data/`
3. Backup `pocket_id.db` (SQLite)
4. Restart app to recreate
5. Create new admin account

### Data Lost After Restart
**Check**: Data should persist
- Verify volume mounted correctly
- Check `/DATA/AppData/<AppID>/data` exists
- If lost, restore from backup

### Performance Issues
**Solutions**:
- Allocate more RAM (512MB+)
- Use PostgreSQL for large installations
- Check disk I/O
- Enable connection pooling (PostgreSQL)

## Backup and Recovery

### Backup Data
```bash
# Copy data directory to safe location
/DATA/AppData/<AppID>/data/
```

### Restore Data
1. Stop Pocket ID app
2. Delete current data directory
3. Copy backup directory back
4. Restart Pocket ID app

## Advanced Setup

### Using PostgreSQL

Instead of SQLite (default):

```env
DATABASE_URL=postgresql://user:password@postgres-host:5432/pocket_id
```

**Benefits**:
- Better performance under load
- Horizontal scaling support
- Advanced backup options
- Suitable for >1000 users

### Custom JWT Secret

Set custom secret for token signing:

```env
JWT_SECRET=your-very-long-random-secret-key-here
```

### Enable Debug Logging

```env
DEBUG=true
```

See logs in app container output.

## Security Considerations

✅ **Best Practices**:
- Use strong admin password
- Enable HTTPS in reverse proxy
- Keep regular backups
- Update Pocket ID regularly
- Monitor access logs
- Use complex Client Secrets
- Restrict CORS origins
- Run with minimal privileges (PUID/PGID)

⚠️ **Important**:
- Pocket ID password recovery requires database access
- Always backup sensitive data
- Test on non-production first
- Review OIDC integrations for security

## Performance Tips

- **Increase Memory**: If slow, allocate 512MB+ RAM
- **Database**: PostgreSQL faster than SQLite for many users
- **Network**: Use wired connection for stability
- **Load**: ~100-1000 users per instance with SQLite

## Updating

### To Latest Version

1. Go to App Store
2. Find Pocket ID
3. Click "Update" button
4. Wait for update (1-2 minutes)
5. Data is preserved automatically

### Check Version

Access admin panel:
- Go to Settings
- Look for version information
- Or check docker logs

## Support

### Official Resources
- **Website**: https://pocket-id.org
- **GitHub**: https://github.com/pocket-id/pocket-id
- **Docker Hub**: https://hub.docker.com/r/11notes/pocket-id
- **Documentation**: https://pocket-id.org/docs

### Community
- GitHub Issues: https://github.com/pocket-id/pocket-id/issues
- Discussions: https://github.com/pocket-id/pocket-id/discussions

### This App Store
- Issues: GitHub repository
- Improvements: Suggest via PR

## Additional Documentation

- **[QUICKSTART.md](QUICKSTART.md)** - 5-minute setup guide
- **[SCREENSHOTS.md](SCREENSHOTS.md)** - Asset capture instructions
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Marketplace submission
- **[PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)** - Technical details
- **[MANIFEST.md](MANIFEST.md)** - Release checklist

## License

Pocket ID is open-source. See https://github.com/pocket-id/pocket-id for license details.

This app store entry is MIT licensed. See [../../LICENSE](../../LICENSE).

---

**Version**: 2.0 (latest)  
**Last Updated**: 2026-04-25  
**Repository**: https://github.com/dn1ghtm/pocketid-appstore

Ready to deploy? Start with [QUICKSTART.md](QUICKSTART.md).

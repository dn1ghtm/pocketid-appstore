# Pocket ID - Quick Start Guide

Deploy Pocket ID on ZimaOS/CasaOS in 5 minutes.

## Prerequisites

- ZimaOS or CasaOS installed
- Network access to your ZimaOS/CasaOS device
- ~256MB available storage

## Installation (ZimaOS/CasaOS UI)

### Step 1: Add to App Store
1. Open ZimaOS/CasaOS dashboard
2. Go to **App Store** or **AppStore**
3. Search for "Pocket ID" or "pocket-id"
4. Click **Install**

### Step 2: Configure (Optional)
- Most settings work with defaults
- Port is auto-assigned
- Click **Install** to proceed

### Step 3: Wait for Deployment
- Container downloads (~50MB)
- Service starts
- Status shows "Running"
- Takes 1-2 minutes

### Step 4: Access Pocket ID
1. Find Pocket ID in your apps
2. Click the **Open** button
3. Or visit: `http://<your-zimaos-ip>:<assigned-port>`

### Step 5: Initial Setup
1. **Create Admin Account**
   - Enter email (can be fake: admin@localhost)
   - Set a strong password
   - Click "Create Account"

2. **Set Up Passkey**
   - Click "Add Passkey"
   - Follow browser prompts
   - Confirm passkey creation
   - You're now authenticated!

3. **Configure (Optional)**
   - Go to Settings → OIDC Applications
   - Create applications for your services
   - Note Client ID and Secret
   - Share endpoints with your apps

## Common Ports

ZimaOS/CasaOS auto-assigns ports. Check dashboard for actual port.

Example:
- Pocket ID: `http://192.168.1.100:8080` (or assigned port)

## Access from Other Devices

If accessing from different machine:
```
http://<zimaos-ip>:<assigned-port>

Examples:
http://192.168.1.50:8080
http://zimaos.local:8080
http://nas.example.com:8080
```

## First Time Login

After creating admin account:

1. **Email**: admin@localhost (or your email)
2. **Password**: Your chosen password
3. **Add Passkey**: Follow browser prompts
4. **Verify**: Login with passkey

## Integrating with Applications

### For Web Apps Using OIDC

Your application needs:
- **Client ID**: From Pocket ID admin panel
- **Client Secret**: From Pocket ID admin panel
- **Authorization Endpoint**: `http://your-zimaos:port/oauth/authorize`
- **Token Endpoint**: `http://your-zimaos:port/oauth/token`
- **UserInfo Endpoint**: `http://your-zimaos:port/oauth/userinfo`

### Example (Node.js):
```javascript
const passport = require('passport');
const OpenIDConnectStrategy = require('passport-openidconnect').Strategy;

passport.use('oidc', new OpenIDConnectStrategy({
  issuer: 'http://192.168.1.50:8080',
  authorizationURL: 'http://192.168.1.50:8080/oauth/authorize',
  tokenURL: 'http://192.168.1.50:8080/oauth/token',
  userInfoURL: 'http://192.168.1.50:8080/oauth/userinfo',
  clientID: 'your-client-id',
  clientSecret: 'your-client-secret',
  callbackURL: 'http://localhost:3000/auth/callback'
}, (issuer, sub, profile, done) => {
  return done(null, profile);
}));
```

## Troubleshooting

### Container Won't Start
**Solution**: Check logs in ZimaOS/CasaOS dashboard
- Look for errors in container details
- Verify disk space available
- Restart container

### Can't Access Web Interface
**Solution**: Verify network connectivity
```bash
# From another device
ping <zimaos-ip>
curl http://<zimaos-ip>:<port>
```

Check dashboard:
- Confirm port number
- Verify "Running" status
- Look for network errors

### Forgot Password
**Solution**: Reset via container
1. Stop Pocket ID in dashboard
2. Access container terminal (if available)
3. Or redeploy (data persists):
   - Stop app
   - Backup data volume
   - Reinstall
   - Restore backup

### Data Lost After Restart
**Check**: Data should persist
- Stop app
- Restart app
- Data should remain

If lost:
- Verify volume mounted in docker-compose
- Check `/DATA/AppData/<app-id>/data` exists
- Restore from backup if available

## Updating Pocket ID

When new version released:

1. Go to App Store
2. Find Pocket ID
3. Click "Update" button
4. Wait for update (1-2 minutes)
5. Access as normal

Your data is preserved automatically.

## Backup and Recovery

### Backup Data
Access ZimaOS/CasaOS storage:
```
/DATA/AppData/<AppID>/data/
```

Copy this directory to safe location.

### Restore Data
1. Stop Pocket ID
2. Delete current data directory
3. Copy backup data back
4. Restart Pocket ID

## Advanced Configuration

### Using PostgreSQL

Edit environment before install:
```env
DATABASE_URL=postgresql://user:password@postgres-host:5432/pocket_id
```

### Enable Debug Logging
```env
DEBUG=true
```

### Custom JWT Secret
```env
JWT_SECRET=your-very-long-random-secret-key
```

## Performance Tips

- **Increase Memory**: If slow, allocate 512MB+ RAM
- **Database**: PostgreSQL faster than SQLite for many users
- **Network**: Use wired connection for stability
- **Load**: ~100-1000 users per instance with SQLite

## Security Notes

⚠️ **Best Practices**:
- Use strong admin password
- Enable HTTPS in reverse proxy
- Keep backups of `/app/data`
- Regularly update Pocket ID
- Monitor access logs
- Use complex Client Secrets

## Next Steps

1. ✅ Installed Pocket ID
2. ✅ Created admin account
3. ✅ Added passkey
4. Next: Create OIDC applications
5. Next: Configure your services
6. Next: Test authentication flow

## Resources

- **Docs**: https://pocket-id.org/docs
- **GitHub**: https://github.com/pocket-id/pocket-id
- **OIDC Spec**: https://openid.net/connect/
- **Configuration**: [README.md](README.md)

## Support

Having issues?
1. Check Pocket ID logs in dashboard
2. Review [README.md](README.md) troubleshooting
3. Check GitHub: https://github.com/pocket-id/pocket-id/issues
4. See official docs: https://pocket-id.org/docs

---

**Version**: 1.0  
**Last Updated**: 2026-04-25  
**Pocket ID Version**: v2 (latest)

Need help? Check the [contributing guide](CONTRIBUTING.md) or official [documentation](https://pocket-id.org/docs).

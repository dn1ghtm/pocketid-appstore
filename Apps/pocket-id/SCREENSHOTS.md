# Screenshot Guide for Pocket ID Marketplace

This guide explains how to capture and prepare screenshots for marketplace submission.

## Screenshot Requirements

### Required: screenshot-1.png
- **Purpose**: Show main feature/interface
- **Size**: 1024x768px minimum (16:9 aspect ratio preferred)
- **Content**: 
  - Pocket ID login or dashboard page
  - Clear, readable interface
  - Show application branding/title
  - Demonstrate core functionality

### Recommended: screenshot-2.png, screenshot-3.png
- **Purpose**: Show additional features
- **Size**: Same as screenshot-1
- **Content options**:
  - Account settings page
  - Passkey management interface
  - OIDC configuration panel
  - User interface examples

## Steps to Create Screenshots

### 1. Set Up Test Instance

```bash
# Deploy on your ZimaOS/CasaOS
# Access the assigned port (e.g., http://localhost:8080)
```

### 2. Create Test Account
- Access Pocket ID web interface
- Create test account with email
- Set up a passkey for authentication
- Log in successfully

### 3. Capture Screenshots

#### Windows
1. Press `Win + Shift + S` (Snip & Sketch)
2. Select area or window to capture
3. Save as PNG

#### Linux
1. Use `gnome-screenshot`:
   ```bash
   gnome-screenshot -w -f screenshot-1.png
   ```
2. Or use `scrot`:
   ```bash
   scrot screenshot-1.png
   ```

#### macOS
1. Press `Cmd + Shift + 4`
2. Select area
3. Click to save

#### Cross-Platform
- **Firefox DevTools**: Tools → Browser Tools → Take Screenshot
- **Chrome DevTools**: Ctrl+Shift+P → "Capture full page screenshot"

### 4. Optimize for Web

```bash
# Use ImageMagick to optimize
convert screenshot-1.png -resize 1024x768 -quality 85 screenshot-1-opt.png

# Or use online tools
# https://tinypng.com (for PNG optimization)
```

## Recommended Screenshot Sequence

### Screenshot 1: Login/Dashboard
**What to show:**
- Main Pocket ID interface
- Authentication options
- Clean, professional appearance
- No sensitive data visible

**Best to capture:**
- After logging in successfully
- Dashboard or home page
- User profile area visible
- All UI elements clear

**File**: `screenshot-1.png`

### Screenshot 2: Passkey Management (Optional)
**What to show:**
- Account settings page
- List of configured passkeys
- Add/manage passkey UI
- User-friendly interface

**File**: `screenshot-2.png`

### Screenshot 3: OIDC Configuration (Optional)
**What to show:**
- OIDC application management
- Configuration interface
- Integration setup flow
- Admin panel features

**File**: `screenshot-3.png`

## Screenshot Content Rules

### Do's
✓ Show the actual web interface  
✓ Include title bar/navigation  
✓ Demonstrate key features  
✓ Use good lighting/clarity  
✓ Show representative UI  
✓ Clean, organized layout  

### Don'ts
✗ Don't show sensitive information  
✗ Don't include real email addresses  
✗ Don't show real passwords or tokens  
✗ Don't use blurry images  
✗ Don't include personal data  
✗ Don't crop too tightly  

## Preparation Checklist

Before submitting:

- [ ] Screenshots are 1024x768 or similar aspect ratio
- [ ] All PNG files (lossless format)
- [ ] File size < 500KB each
- [ ] Text is readable (font size > 12px effective)
- [ ] No sensitive data visible
- [ ] Interface looks clean and professional
- [ ] No error messages shown
- [ ] Consistent styling across screenshots

## File Names

Follow this naming convention:
```
screenshot-1.png    # Main feature/dashboard
screenshot-2.png    # Secondary feature
screenshot-3.png    # Additional feature
```

## Where to Place Files

Directory structure for submission:
```
Apps/pocket-id/
├── docker-compose.yml
├── icon.svg
├── screenshot-1.png
├── screenshot-2.png (optional)
└── screenshot-3.png (optional)
```

## Tools and Resources

### Free Image Tools
- **GIMP**: https://www.gimp.org/ (Full editor)
- **Krita**: https://krita.org/ (Painting/editing)
- **ImageMagick**: https://imagemagick.org/ (CLI resize/optimize)
- **TinyPNG**: https://tinypng.com (Online optimizer)

### Screen Capture Tools
- **ShareX** (Windows): https://getsharex.com/
- **Flameshot** (Linux): https://flameshot.org/
- **CleanShot** (macOS): https://cleanshot.com/
- **Greenshotshot** (Cross-platform): https://getgreenshot.org/

## Troubleshooting

**Screenshot too blurry**:
- Increase zoom/scale in browser
- Use native resolution capture
- Ensure window is fully rendered

**Text not readable**:
- Increase browser zoom (120-150%)
- Capture at higher resolution first
- Resize down afterward

**File size too large**:
```bash
# Use ImageMagick
convert large.png -quality 85 small.png

# Or pngquant
pngquant 256 large.png
```

## Examples

Good screenshot shows:
- Clear, readable Pocket ID interface
- User logged in
- Dashboard or settings visible
- Professional appearance
- No errors or warnings
- Good contrast and legibility

Poor screenshot shows:
- Blurry or hard to read
- System UI overlapping
- Contains sensitive data
- Resolution too small
- Error messages or warnings

## Submission Checklist

- [x] Screenshots captured at proper resolution
- [x] All files in PNG format
- [x] Filenames follow convention (screenshot-1.png, etc.)
- [x] Placed in Apps/pocket-id/ directory
- [x] File sizes optimized (< 500KB each)
- [x] No sensitive data visible
- [x] Clear and professional appearance

---

**Last Updated**: 2026-04-25

For more information, see:
- Main README: [README.md](README.md)
- Contributing Guide: [CONTRIBUTING.md](CONTRIBUTING.md)

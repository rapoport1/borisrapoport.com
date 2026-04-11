# Implementation Guide - Clean Nebula Hero Design

## Step-by-Step Implementation

### Step 1: Obtain the Eskimo Nebula Image
```bash
# Create images directory if it doesn't exist
mkdir -p boris-website/static/images/

# Download the image from NASA (replace with actual URL)
# Option 1: High-res from NASA
wget -O boris-website/static/images/eskimo-nebula-full.jpg \
  "https://www.nasa.gov/sites/default/files/[ACTUAL_IMAGE_PATH]"

# Option 2: Manual download
# Go to NASA/ESA site, download, and place in static/images/
```

### Step 2: Optimize the Image
```bash
# Navigate to images directory
cd boris-website/static/images/

# Optimize with ImageMagick
convert eskimo-nebula-full.jpg \
  -resize 1920x1920 \
  -quality 85 \
  -strip \
  eskimo-nebula.jpg

# Create mobile version
convert eskimo-nebula-full.jpg \
  -resize 1080x1080 \
  -quality 80 \
  -strip \
  eskimo-nebula-mobile.jpg
```

### Step 3: Backup Current Files
```bash
# Backup existing index.html
cp boris-website/themes/quantum-ascent/layouts/index.html \
   boris-website/themes/quantum-ascent/layouts/index-backup.html

# Backup existing CSS
cp boris-website/themes/quantum-ascent/static/css/quantum-ascent.css \
   boris-website/themes/quantum-ascent/static/css/quantum-ascent-backup.css
```

### Step 4: Apply New HTML Template
```bash
# Replace the index.html with new design
cp boris-website/themes/quantum-ascent/layouts/index-new.html \
   boris-website/themes/quantum-ascent/layouts/index.html
```

### Step 5: Add New CSS
```bash
# The hero-nebula.css file has been created
# Now add import to main CSS file

# Add this line to the top of quantum-ascent.css:
echo '@import url("hero-nebula.css");' | \
  cat - boris-website/themes/quantum-ascent/static/css/quantum-ascent.css > temp && \
  mv temp boris-website/themes/quantum-ascent/static/css/quantum-ascent.css
```

### Step 6: Update Hugo Configuration (if needed)
```toml
# In config.toml or hugo.toml, ensure these are set:
[params]
  # Add custom CSS file reference
  customCSS = ["css/hero-nebula.css"]
```

### Step 7: Remove Old Hero Styles (Clean-up)
Edit `quantum-ascent.css` and remove or comment out:
- `.hero` section styles (lines ~300-400)
- `.hero-content` styles
- `.hero-accent` and `.mountain-silhouette` styles
- Old `.hero-title`, `.hero-subtitle`, `.hero-tagline` styles

### Step 8: Test Locally
```bash
# Navigate to site root
cd boris-website/

# Start Hugo server
hugo server -D

# Open browser to http://localhost:1313
```

### Step 9: Responsive Testing
Test on multiple viewports:
- Desktop: 1920x1080, 1440x900
- Tablet: 768x1024 (iPad)
- Mobile: 375x812 (iPhone X)

### Step 10: Build for Production
```bash
# Build the site
hugo --minify

# Check the output in docs/ folder
ls -la docs/
```

### Step 11: Performance Check
```bash
# Check final image sizes
du -h docs/images/eskimo-nebula*

# Ensure total page weight < 1MB
du -sh docs/index.html docs/css/* docs/images/eskimo-nebula.jpg
```

### Step 12: Deploy
```bash
# If using Git
git add .
git commit -m "Redesign: Clean hero with Eskimo Nebula focal point"
git push origin main

# If using GitHub Pages, ensure docs/ is built
```

## Rollback Procedure (if needed)

```bash
# Restore original files
cp boris-website/themes/quantum-ascent/layouts/index-backup.html \
   boris-website/themes/quantum-ascent/layouts/index.html

cp boris-website/themes/quantum-ascent/static/css/quantum-ascent-backup.css \
   boris-website/themes/quantum-ascent/static/css/quantum-ascent.css

# Remove new CSS file
rm boris-website/themes/quantum-ascent/static/css/hero-nebula.css

# Rebuild
hugo --minify
```

## Final Checklist

- [ ] Eskimo Nebula image obtained (NASA/ESA source)
- [ ] Image optimized for web (< 500KB)
- [ ] Mobile version created (< 250KB)
- [ ] Old files backed up
- [ ] New HTML applied
- [ ] New CSS integrated
- [ ] Old hero styles removed/disabled
- [ ] Local testing complete
- [ ] Responsive testing complete
- [ ] Performance acceptable (< 1MB total)
- [ ] Production build successful
- [ ] Deployed to hosting

## Notes

- The mountain SVG has been completely removed
- Text has been reduced by ~70%
- Focus is now on the nebula image
- Glassmorphic effects enhance but don't dominate
- Clean, minimal, sophisticated design achieved
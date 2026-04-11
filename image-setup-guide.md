# Eskimo Nebula Image Setup Guide

## Image Requirements

### Primary Image: Eskimo Nebula (NGC 2392)
- **Source**: NASA/ESA Hubble Space Telescope
- **Recommended Resolution**: 1920x1920px minimum (square aspect ratio preferred)
- **File Format**: JPEG (optimized for web, 85-90% quality)
- **File Name**: `eskimo-nebula.jpg`
- **Location**: `/static/images/eskimo-nebula.jpg`

### Where to Get the Image

1. **NASA Image Gallery** (Public Domain):
   - Visit: https://www.nasa.gov/image-feature/goddard/2020/hubble-views-the-final-frontier
   - Search for "NGC 2392" or "Eskimo Nebula"
   - Download the highest resolution available

2. **ESA/Hubble Site**:
   - Visit: https://esahubble.org/images/
   - Search for "NGC 2392"
   - Choose the golden/orange toned version

3. **Direct Links** (if available):
   ```bash
   # Example download command (replace URL with actual NASA/ESA link)
   wget -O eskimo-nebula-full.jpg "NASA_IMAGE_URL_HERE"
   ```

### Image Optimization

```bash
# Using ImageMagick to optimize for web
convert eskimo-nebula-full.jpg \
  -resize 1920x1920 \
  -quality 85 \
  -strip \
  eskimo-nebula.jpg

# Alternative: Using cwebp for WebP format (better compression)
cwebp -q 85 eskimo-nebula-full.jpg -o eskimo-nebula.webp
```

### Fallback Options

If you can't find the Eskimo Nebula with golden/orange tones, consider these alternatives:

1. **Helix Nebula** (NGC 7293) - Similar circular structure with warm tones
2. **Ring Nebula** (M57) - Already used in nav, but larger version could work
3. **Cat's Eye Nebula** (NGC 6543) - Circular with golden hues

### File Structure

```
boris-website/
├── static/
│   └── images/
│       ├── eskimo-nebula.jpg      (main hero image)
│       ├── eskimo-nebula.webp     (optional WebP version)
│       └── eskimo-nebula-mobile.jpg (optional mobile optimized)
```

### Performance Considerations

- **Desktop**: 1920x1920px @ 85% quality ≈ 300-500KB
- **Mobile**: 1080x1080px @ 80% quality ≈ 150-250KB
- Use `loading="eager"` for hero image (already in code)
- Consider `<picture>` element for responsive images

### Color Profile Notes

The Eskimo Nebula typically shows:
- Golden/orange outer shell
- Blue-green inner regions
- Perfect complement to the Quantum Ascent color palette
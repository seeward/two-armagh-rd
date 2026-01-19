# 2 Armagh - 3D Property Viewer

An interactive 3D property viewer built with Three.js, featuring waypoint navigation and a modern UI.

## Features

- 📐 **Interactive 3D Viewing** - Navigate a detailed 3D model with smooth controls
- 🎯 **Waypoint Navigation** - Jump between predefined viewpoints with keyboard shortcuts (1-9)
- 📱 **Mobile-Friendly** - Touch controls for mobile and tablet devices
- 🎨 **Modern UI** - macOS-style dock and hamburger menu interface
- 🌅 **HDR Background** - EXR environment map support for realistic lighting
- ⚡ **Fast Loading** - Progress indicator and optimized asset loading

## Quick Start

### Running Locally

Since this is a static web application using ES modules, you need to serve it via a local web server (not `file://` protocol):

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (http-server)
npx http-server -p 8000

# Using PHP
php -S localhost:8000
```

Then open your browser to `http://localhost:8000`

### Files

- `index.html` - Main application (standalone, includes all HTML, CSS, and JavaScript)
- `1.glb` - 3D model file (GLTF binary format)
- `bg.exr` - Background environment texture (HDR)
- `wrangler.json` - Cloudflare Pages configuration

## Usage

### Controls

- **Mouse Drag** - Look around
- **Scroll/Pinch** - Zoom in/out  
- **Right-Click Drag** - Pan the view
- **Keys 1-9** - Jump to waypoints 1-9
- **Hamburger Menu** - Access all waypoints

### Waypoints

Waypoints are defined as named objects in the 3D model file:
- Name format: `WP_001`, `WP_002`, etc.
- Each waypoint represents a camera position and orientation
- Can be accessed via the sidebar menu, dock, or keyboard shortcuts

### Customization

You can customize the application by editing `index.html`:

- `DEFAULT_GLB_URL` - Path to your 3D model file
- `WAYPOINT_PREFIX` - Prefix for waypoint object names (default: `WP_`)
- `FADE_MS` - Transition fade duration in milliseconds
- `LOOK_AHEAD` - Distance (in meters) to place the camera target in front of waypoints

You can also load a different model via URL parameter:
```
http://localhost:8000/?glb=path/to/your-model.glb
```

## Deployment

This project is configured for Cloudflare Pages deployment.

### Cloudflare Pages

The `wrangler.json` file configures the project for Cloudflare Pages:
- Project name: `two-armagh-rd`
- Build output: current directory (`.`)

To deploy:

1. Connect your GitHub repository to Cloudflare Pages
2. Cloudflare will automatically deploy on push to main branch
3. Or manually deploy using Wrangler CLI:
   ```bash
   npx wrangler pages deploy .
   ```

### Other Hosting Options

Since this is a static site, you can host it anywhere:
- GitHub Pages
- Netlify
- Vercel
- AWS S3 + CloudFront
- Any static hosting service

## Creating a Release

See [RELEASE.md](RELEASE.md) for detailed instructions on creating releases for this project.

Quick version:
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
gh release create v1.0.0 --title "Version 1.0.0" --notes "Description of changes"
```

## Requirements

- Modern web browser with WebGL support
- ES6 module support
- Three.js (loaded from CDN)

## Technology Stack

- **Three.js** - 3D rendering engine
- **OrbitControls** - Camera controls
- **GLTFLoader** - 3D model loading
- **EXRLoader** - HDR environment loading
- **Vanilla JavaScript** - No build process required

## Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers with WebGL support

## Development

The entire application is contained in a single `index.html` file for simplicity. This makes it easy to:
- Deploy anywhere
- Customize without a build process
- Share as a single file

### File Structure

```
.
├── index.html      # Main application (all-in-one)
├── 1.glb          # 3D model
├── bg.exr         # Background texture
├── wrangler.json  # Cloudflare config
├── README.md      # This file
└── RELEASE.md     # Release process documentation
```

## Troubleshooting

### Model doesn't load
- Make sure you're running via a local web server (not `file://`)
- Check browser console for errors
- Verify the GLB file path is correct

### Waypoints not appearing
- Check that your 3D model contains objects named with the prefix `WP_` (e.g., `WP_001`, `WP_002`)
- The objects should be empties or low-poly helpers in your 3D software
- Verify object names in your 3D modeling software before export

### EXR background not loading
- Ensure `bg.exr` file is in the same directory as `index.html`
- The application will fall back to a solid color background if EXR fails to load

## License

See repository license file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

# Atelier 3D Configurator — Asset Setup Guide

Place this file alongside `configurator.html`. The folder structure should be:

```
project/
├── configurator.html
├── model.glb
├── SETUP.md              ← this file
└── assets/
    ├── fonts/
    │   ├── manifest.json
    │   ├── MyFont-Regular.ttf
    │   ├── MyFont-Bold.ttf
    │   └── StreetFont.otf
    └── images/
        ├── manifest.json
        ├── star.png
        ├── crown.png
        ├── flame.svg
        └── logo.png
```

---

## fonts/manifest.json

Each entry tells the configurator how to load and display the font in the selector dropdown.

```json
[
  {
    "name":     "My Brand Font",
    "file":     "MyFont-Regular.ttf",
    "weight":   400,
    "italic":   false,
    "category": "Brand"
  },
  {
    "name":     "My Brand Bold",
    "file":     "MyFont-Bold.ttf",
    "weight":   700,
    "italic":   false,
    "category": "Brand"
  },
  {
    "name":     "Street Style",
    "file":     "StreetFont.otf",
    "weight":   400,
    "italic":   false,
    "category": "Street"
  }
]
```

**Fields:**
| Field | Required | Description |
|-------|----------|-------------|
| `name` | ✅ | Display name shown in dropdown |
| `file` | ✅ | Filename inside `assets/fonts/` |
| `weight` | optional | CSS font-weight (100–900). Default: 400 |
| `italic` | optional | `true` / `false`. Default: false |
| `category` | optional | Groups fonts under a header in the dropdown |

**Supported formats:** `.ttf` `.otf` `.woff` `.woff2`

If `manifest.json` is missing, the configurator falls back to Google-hosted fonts (Bebas Neue, Anton, Russo One, etc.).

---

## images/manifest.json

Each entry tells the configurator which images to show in the Assets tab and how to label/group them.

```json
[
  {
    "file":     "star.png",
    "label":    "Star",
    "category": "Shapes"
  },
  {
    "file":     "crown.png",
    "label":    "Crown",
    "category": "Fashion"
  },
  {
    "file":     "flame.svg",
    "label":    "Flame",
    "category": "Street"
  },
  {
    "file":     "logo.png",
    "label":    "Brand Logo",
    "category": "Brand"
  }
]
```

**Fields:**
| Field | Required | Description |
|-------|----------|-------------|
| `file` | ✅ | Filename inside `assets/images/` |
| `label` | optional | Display name shown on hover / in layers |
| `category` | optional | Groups assets under a header in the grid |

**Supported formats:** `.png` `.jpg` `.jpeg` `.svg` `.webp` `.gif`

If `manifest.json` is missing, the configurator tries a list of common filenames automatically. Built-in SVG shapes (star, triangle, circle, diamond, etc.) are always shown regardless.

---

## Running the project

Always use a local server — browsers block local file loading over `file://`.

```bash
# Python (simplest)
python -m http.server 8000
# then open: http://localhost:8000/configurator.html

# Node
npx serve .

# VS Code: install Live Server extension → right-click → Open with Live Server
```

### Flutter WebView
Load: `https://yourhost.com/configurator.html?uid=USER_UID&email=user@email.com&name=John`

Or call from Dart after page load:
```dart
webViewController.runJavaScript(
  'window.receiveFlutterUser(\'${jsonEncode({"uid": user.uid, "email": user.email, "displayName": user.displayName})}\')'
);
```

Add `?debug=1` to the URL to see the Flutter bridge log overlay on screen.

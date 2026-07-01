# arfari 🌐

A polished, lightweight web browser designed specifically for Arch Linux "rice" setups aiming to perfectly replicate the macOS desktop experience. It blends native performance with a Cupertino-inspired user interface.

## ⚠️ Compatibility Note

* **XFCE is NOT supported.** 
* This browser relies on modern compositor effects (like advanced blur and window management) found in GNOME, KDE Plasma, or Wayland-based window managers (e.g., Hyprland). It will not render correctly on XFCE.

## 🚀 Installation

Follow these steps to clone, build, and run arfari on your system:

```bash
# 1. Navigate to the project directory
cd /path/to/arfari

# 2. Install dependencies
npm install

# 3. Start the application
npm start
```

## ✨ Key Features

* **macOS-Native UI:** Translucent sidebars, header bars, and window controls that match your Apple-themed Arch desktop.
* **Smart Tab Management:** Safari-style tab grouping and clean navigation layouts.
* **Apple-esque Gestures:** Smooth touchpad gestures for navigating back, forward, and viewing tab overviews.
* **Minimal Resource Footprint:** Built to respect Arch Linux's minimalism, keeping RAM usage low and extending battery life.

## 🤝 Contribution

Contributions are welcome! If you want to help develop arfari:

* Open an issue to report bugs or suggest features.
* Submit pull requests with your improvements.
* Recommended setup: Use **Cursor** editor for the best development experience with this codebase.
# arfari 🌐

A polished, lightweight web browser designed specifically for Arch Linux "rice" setups aiming to perfectly replicate the macOS desktop experience. It blends native performance with a Cupertino-inspired user interface.

## ⚠️ Compatibility Note

* **XFCE is NOT supported.** 
* This browser relies on modern compositor effects (like advanced blur and window management) found in GNOME, KDE Plasma, or Wayland-based window managers (e.g., Hyprland). It will not render correctly on XFCE.

## 🚀 Installation

Follow these steps to clone, build, and run arfari on your system:

```bash
# 1. Navigate to the project directory
cd /path/to/arfari

# 2. Install dependencies
npm install

# 3. Start the application
npm start
```

## ✨ Key Features

* **macOS-Native UI:** Translucent sidebars, header bars, and window controls that match your Apple-themed Arch desktop.
* **Smart Tab Management:** Safari-style tab grouping and clean navigation layouts.
* **Apple-esque Gestures:** Smooth touchpad gestures for navigating back, forward, and viewing tab overviews.
* **Minimal Resource Footprint:** Built to respect Arch Linux's minimalism, keeping RAM usage low and extending battery life.

## 🤝 Contribution

Contributions are welcome! If you want to help develop arfari:

* Open an issue to report bugs or suggest features.
* Submit pull requests with your improvements.
* Recommended setup: Use **Cursor** editor for the best development experience with this codebase.
# arfari 🌐

A polished, lightweight web browser designed specifically for Arch Linux "rice" setups aiming to perfectly replicate the macOS desktop experience. It blends native performance with a Cupertino-inspired user interface.

## ⚠️ Compatibility Note

* **XFCE is NOT supported.** 
* This browser relies on modern compositor effects (like advanced blur and window management) found in GNOME, KDE Plasma, or Wayland-based window managers (e.g., Hyprland). It will not render correctly on XFCE.

## 🚀 Installation

Follow these steps to clone, build, and run arfari on your system:

```bash
# 1. Navigate to the project directory
cd /path/to/arfari

# 2. Install dependencies
npm install

# 3. Start the application
npm start
```

## ✨ Key Features

* **macOS-Native UI:** Translucent sidebars, header bars, and window controls that match your Apple-themed Arch desktop.
* **Smart Tab Management:** Safari-style tab grouping and clean navigation layouts.
* **Apple-esque Gestures:** Smooth touchpad gestures for navigating back, forward, and viewing tab overviews.
* **Minimal Resource Footprint:** Built to respect Arch Linux's minimalism, keeping RAM usage low and extending battery life.

## 🤝 Contribution

Contributions are welcome! If you want to help develop arfari:

* Open an issue to report bugs or suggest features.
* Submit pull requests with your improvements.
* Recommended setup: Use **Cursor** editor for the best development experience with this codebase.
# Arfari

**Arfari** is a Chromium-based browser for Arch Linux with a Safari-inspired interface, built-in ad blocking, and a high-quality liquid glass UI that stays fast.

![Arfari logo](assets/icon.svg)

## Features

- **Safari-like design** — Unified toolbar, centered pill URL bar, compact tab strip, and traffic-light window controls
- **Liquid glass chrome** — Frosted `backdrop-filter` panels with GPU compositing; falls back to solid chrome when blur is unavailable or disabled
- **Built-in ad blocker** — Powered by [@ghostery/adblocker-electron](https://github.com/ghostery/adblocker) with EasyList + EasyPrivacy
- **Performance-first** — BrowserView per tab (not iframes), single blur layer per panel, no nested glass effects
- **Arch Linux ready** — PKGBUILD, `.desktop` entry, and system icon theme integration

## Quick start (development)

```bash
git clone https://github.com/hansith7/arfari.git
cd arfari
npm install
npm start
```

## Build for Linux

```bash
npm run build
npm run pack:linux
```

Output appears in `release/` as AppImage and `.deb`.

## Install on Arch Linux

```bash
cd packaging/archlinux
makepkg -si
```

Then launch **Arfari** from your application menu or run:

```bash
arfari
```

### Dependencies

The PKGBUILD expects `electron33` from the Arch repos. If your Electron package version differs, update the launcher script in `packaging/archlinux/arfari.sh`.

## Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+T` | New tab |
| `Ctrl+W` | Close tab |
| `Ctrl+L` | Focus address bar |

## XFCE on Arch Linux

Arfari auto-detects XFCE and uses **solid chrome** instead of transparent windows — this avoids the black-window glitch when the xfwm4 compositor is disabled.

For liquid glass on XFCE, enable the compositor:

**Settings → Window Manager Tweaks → Compositor → Enable display compositing**

Then remove the XFCE solid override (optional, advanced):

```bash
ARFARI_FORCE_GLASS=1 arfari
```

## New tab page

New tabs open with a **centered search bar** on the start page — Safari-style. Type a query or URL, or pick a shortcut. The tab strip stays centered in the chrome above.

## Performance tuning

Liquid glass uses `backdrop-filter: blur(24px)` on the chrome only — never on the web content area. To disable glass for maximum performance on low-end hardware:

```javascript
localStorage.setItem('arfari-no-glass', '1')
```

Reload the browser. To re-enable:

```javascript
localStorage.removeItem('arfari-no-glass')
```

## Architecture

```
┌─────────────────────────────────────┐
│  Title bar + window controls        │
├─────────────────────────────────────┤
│  Tab bar (glass panel)              │
├─────────────────────────────────────┤
│  Toolbar: nav · URL bar · shield    │
├─────────────────────────────────────┤
│  BrowserView (Chromium web content) │
│  Ad blocker hooks into session      │
└─────────────────────────────────────┘
```

- **Electron main process** — Window management, tabs, BrowserViews, ad blocker session hooks
- **Renderer process** — Safari-style chrome UI (HTML/CSS/TS)
- **BrowserView** — Native Chromium rendering per tab for best performance

## License

MIT

# Terminal Support and Troubleshooting

Reflect runs as a full-screen TUI powered by Bubble Tea. This covers terminal compatibility and common fixes.

---

## Quick Fixes

### Truecolor (24-bit colors)

```bash
# Add to ~/.zshrc or ~/.bashrc
export COLORTERM=truecolor
```

Inside __TRELAY_PROTECT__, add to `~/.__TRELAY_PROTECT__.conf`:

```__TRELAY_PROTECT__
set -g default-terminal "__TRELAY_PROTECT__-256color"
set -as terminal-features ",*:RGB"
```

---

## Terminal Detection

Reflect detects these terminals:

- Apple Terminal
- iTerm2
- Ghostty
- Kitty
- WezTerm
- VS Code / Cursor / Windsurf / Zed terminals
- Alacritty
- GNOME Terminal (VTE)
- Windows Terminal

Run `/terminal-setup` for diagnostics.

---

## Common Problems

### Colors Look Wrong

**Cause**: Terminal not configured for truecolor.

**Fix**: Set `COLORTERM=truecolor` and configure __TRELAY_PROTECT__ for RGB.

### Clipboard Not Working

**Cause**: Terminal doesn't support OSC 52.

**Fix**:
- iTerm2: Enable "Applications in terminal may access clipboard"
- Ghostty: Add `clipboard-provider = "work-area"` to config
- __TRELAY_PROTECT__: Add `set -g set-clipboard on`

### Fullscreen Not Activating

**Cause**: Zellij, __TRELAY_PROTECT__ control mode, or config.

**Fix**: Set in `~/.reflect/settings.json`:

```json
{ "terminal": { "alt_screen": "always" } }
```

### Shift+Enter Not Working in VS Code

**Cause**: xterm.js partial Kitty protocol support.

**Fix**: Use **Alt+Enter** for newlines.

---

## __TRELAY_PROTECT__ Configuration

Recommended settings in `~/.__TRELAY_PROTECT__.conf`:

```__TRELAY_PROTECT__
set -g default-terminal "__TRELAY_PROTECT__-256color"
set -as terminal-features ",*:RGB"
set -g set-clipboard on
set -g allow-passthrough on
```

---

## WezTerm Configuration

Add to `~/.config/wezterm/wezterm.lua`:

```lua
config.enable_kitty_keyboard = true
```

---

## SSH Considerations

Over SSH:
- OSC 52 clipboard may not work (Apple Terminal limitation)
- Use terminal-native paste (`Shift+Insert` or `Shift+Middle Click`)
- Run `/terminal-setup` to verify detection

---

## Multiplexers

### Zellij

Zellij intercepts many Ctrl/Alt keys. Use:
- **Unlock-First mode** (recommended)
- Press `Ctrl+O` then `C` to enter configuration
- Select "Unlock-First (non-colliding)"

### __TRELAY_PROTECT__

Add to config:
```__TRELAY_PROTECT__
set -g allow-passthrough on
set -g set-clipboard on
```

---

## Diagnostics

Run in Reflect:

```
/terminal-setup
```

Shows:
- Terminal detection
- Color level
- Available themes
- Clipboard routes
- Fix recommendations

---

## Where to Go Next

| Document | What You Will Learn |
|----------|-------------------|
| [Permissions](22-permissions-and-safety.md) | Safety controls |
| [Dashboard](23-dashboard.md) | HUD and monitoring |

---

© 2026 GrayCode AI. All rights reserved.
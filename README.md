# AesTerm

> **AesTerm** (Asterisk `*` + Terminal) is a local-first, keyboard-driven All-in-One Terminal Workstation. Built on Tauri v2 and Rust, it bridges the gap between CLI execution, modal code editing, graphical extensions, and live web previews in a single window.

Rather than running heavy, background-bloated AI tools by default, AesTerm aims itself around developer velocity, ultra-low latency (<100ms startup), and a sub-50MB idle memory footprint. It treats AI as a quiet, opt-in subsystem—providing intelligent assistance strictly when invoked, while functioning as a hyper-fast terminal IDE when idle.

---

### ✨ Core Pillars

* **Spatial tmux Multiplexer:** Split panes horizontally or vertically, swap layouts, and manage workspaces using a low-latency native Finite State Machine (FSM) key interceptor (`Ctrl+Space` prefix engine).
* **Native Modal Editing (Vim Core):** Launch floating or split editor buffers directly inside your active workspace (`Ctrl+Space e` or `:e filename`). Supports standard Vim modes (`NORMAL`, `INSERT`, `VISUAL`), motions (`hjkl`, `ciw`, `d$`), Ex commands (`:wq`), and LSP auto-completion.
* **VS Code-Style Plugin Ecosystem:** Extend your workspace with third-party JavaScript plugins running in a sandboxed runtime (`window.WorkspaceAPI`). Add custom sidebar panels, status bar widgets, or terminal macros.
* **Live Webview Viewports:** Render hot-reloading web applications (`localhost:5173`) right next to your compiler logs in a native split pane.
* **Opt-In Agentic Co-Pilot:** Asynchronously monitors `stderr`/`stdout` streams to offer non-intrusive error remediation (`Ctrl+Space Shift+E`) and natural-language-to-CLI generation (`Ctrl+Space Space`) strictly on demand.
* **Multi-Theme Engine:** Seamlessly switch between curated palettes (Catppuccin, Tokyo Night, Gruvbox, One Dark, and custom JSON themes) unified across terminal matrices, editor buffers, and UI chrome.

---

### 🛠️ Tech Stack

* **Desktop Shell:** Tauri v2 (Rust-backed native window manager)
* **Backend Engine:** Rust (Edition 2024) + `portable-pty` + `notify` file watcher
* **Frontend UI:** React 18 + Tailwind CSS + Lucide Icons
* **Terminal Subsystem:** `@xterm/xterm` with `@xterm/addon-webgl` (GPU-accelerated 60 FPS cell rendering)
* **Modal Code Editor:** Monaco Editor + `monaco-vim` + Native LSP Bridge
* **Plugin Sandbox:** Webview JS Bridge (`window.WorkspaceAPI`)

---

### ⌨️ Keybindings Cheatsheet

AesTerm uses `Ctrl+Space` as its default prefix sequence (customizable in `~/.config/aesterm/config.json`).

#### Workspace & Pane Management (tmux engine)

| Keybinding | Action |
| --- | --- |
| `Ctrl+Space "` | Split active pane horizontally |
| `Ctrl+Space %` | Split active pane vertically |
| `Ctrl+Space h / j / k / l` | Move focus to left / down / up / right pane |
| `Ctrl+Space x` | Close active pane |
| `Ctrl+Space z` | Toggle active pane zoom / fullscreen |
| `Ctrl+Space s` | Save current workspace layout session |

#### Editor & Workspace Tools (VS Code / Vim layer)

| Keybinding | Action |
| --- | --- |
| `Ctrl+Space e` | Toggle inline Vim editor overlay for active directory |
| `Ctrl+Space b` | Toggle file explorer & Git status drawer |
| `Ctrl+Space p` | Toggle Live Webview Preview (`localhost:5173`) |

#### Opt-In Agent Subsystem

| Keybinding | Action |
| --- | --- |
| `Ctrl+Space Space` | Open Natural Language CLI command prompt |
| `Ctrl+Space Shift+E` | Send active pane stderr error trace to AI for fix |

---

### 📁 Directory Architecture

AesTerm isolates its configurations to keep your projects and system clean:

```yaml
# Global Configuration & Plugins
~/.config/aesterm/
├── config.json         # Global user preferences, keybinds, and default shell
├── themes/             # Custom color schemes (.json palettes)
│   └── catppuccin-mocha.json
└── plugins/            # Installed community extensions
    └── git-lens-lite/
        ├── manifest.json
        └── index.js

# Project-Scoped Local State
your-code-project/
└── .aesterm/           # Local workspace directory (add to .gitignore)
    ├── session.json    # Saved pane layouts, split ratios, active CWDs
    └── workspace.json  # Project-specific task macros & overrides

```

# Khayyam PDF Editor

A free, privacy-first PDF editor with no subscriptions and no cloud uploads.  
Available for **macOS** (native Swift/SwiftUI) and **Windows** (Python/PyQt6).

> Named after Omar Khayyam (1048–1131) — Persian mathematician, astronomer, and poet.

---

## Features

- **Annotate** — Highlight, underline, and strikethrough text
- **Draw** — Freehand ink, rectangles, ovals, and lines (Shift to constrain)
- **Comment** — Sticky notes and typewriter text
- **Edit** — Replace existing text blocks in-place
- **Insert** — Place images anywhere on the page
- **Organize** — Merge multiple PDFs, split by page range or intervals
- **Navigate** — Thumbnail sidebar, outline/bookmarks, full-text search
- **Save** — Incremental or full save; drag-and-drop to open

---

## macOS Edition

Built with Swift, SwiftUI, PDFKit, and MuPDF. Requires macOS 13 or later.

### Build from source

**Prerequisites**

- Xcode 15+
- MuPDF library (path configured via `Config/LocalPaths.xcconfig`)

**Setup**

```bash
git clone https://github.com/your-username/khayyam-pdf-editor-MacOs.git
cd khayyam-pdf-editor-MacOs
cp Config/LocalPaths.xcconfig.template Config/LocalPaths.xcconfig
# Edit Config/LocalPaths.xcconfig and set MUPDF_PATH to your MuPDF install
open khayyam.xcodeproj   # or use xcodebuild
```

---

## Windows Edition

Built with Python 3.10+, PyQt6, and PyMuPDF. Runs on Windows 10/11 (64-bit).

### Quick start (run from source)

```powershell
cd Windows
pip install -r requirements.txt
python main.py
```

### Build a standalone installer

**Prerequisites — install once**

```powershell
pip install pyinstaller Pillow
# Download and install Inno Setup 6 from: https://jrsoftware.org/isdl.php
```

**Build**

```powershell
cd Windows
.\build.bat
```

This produces:
- `dist\Khayyam PDF Editor\Khayyam PDF Editor.exe` — portable app bundle
- `installer\Khayyam-PDF-Editor-Setup-1.0.0.exe` — full Windows installer

Or run the steps manually in PowerShell:

```powershell
python make_icon.py                              # generate icon.ico from Mac PNGs
python -m PyInstaller khayyam.spec --noconfirm  # bundle the app
& "C:\Program Files (x86)\Inno Setup 6\ISCC.exe" installer.iss  # compile installer
```

### Windows file structure

```
Windows/
├── main.py              # Entry point
├── requirements.txt     # Python dependencies
├── khayyam.spec         # PyInstaller spec (one-folder bundle)
├── installer.iss        # Inno Setup script → produces .exe installer
├── build.bat            # Full build pipeline (icon → PyInstaller → Inno Setup)
├── make_icon.py         # Converts Mac PNG icons → Windows icon.ico
├── icon.ico             # Pre-generated Windows icon
└── src/
    ├── models.py        # AnnotationTool enum, data types
    ├── pdf_viewer.py    # Core rendering + annotation widget (QGraphicsView + PyMuPDF)
    ├── pdf_document.py  # Merge / split operations
    ├── toolbar.py       # Annotation toolbar (grouped tool buttons)
    ├── sidebar.py       # Thumbnails, outline, search panel
    ├── main_window.py   # Main window, menus, nav toolbar
    └── dialogs.py       # Merge, Split, AddText, StickyNote, GoToPage dialogs
```

### Windows keyboard shortcuts

| Action | Shortcut |
|--------|----------|
| Open PDF | Ctrl+O |
| Save | Ctrl+S |
| Save As | Ctrl+Shift+S |
| Zoom In | Ctrl+= |
| Zoom Out | Ctrl+- |
| Fit page | Ctrl+0 |
| Previous page | Ctrl+Left |
| Next page | Ctrl+Right |
| Delete annotation | Delete |
| Cancel / Escape | Esc |
| Constrain shape to square | Hold Shift while dragging |
| Constrain line to 45° | Hold Shift while dragging |
| Zoom with scroll wheel | Ctrl+Scroll |

---

## Privacy

All processing happens locally on your device. No files are uploaded, no analytics are collected, no account is required.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

## Website

[oxinstudio.com/khayyam-pdf-editor](https://oxinstudio.com/khayyam-pdf-editor/)

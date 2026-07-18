# Bug Reports / CPOchat — Matrix View

**🌐 Language / 語言：English (current) · [中文](README.md)**

An **offline, single-file** HTML bug tracker. Just open [`bug-tracker-v4.html`](bug-tracker-v4.html) and start using it — no installation, no backend, no internet connection required. All data stays in your own browser.

Core idea: every bug spans the **Test → Dev → Production** environments, laid out as a matrix (table) so you can see each environment's fix progress and validation status at a glance.

---

## ✨ Features

### 🧩 Three-environment matrix view
- One row per bug, split horizontally into **Test / Dev / Production** columns.
- Each environment has its own:
  - **Bug Fix ETA** (free-text, e.g. `2026-05-30 · Next deployment`)
  - **Pass toggle** (mark that environment as validated)
  - **Screenshots**, split into *Bug Evidence* and *Validation / Pass Evidence*
- The left "Bug" column is **resizable** — drag the divider, double-click to reset to default width.

### 💾 IndexedDB storage
- Data lives in the browser's **IndexedDB** (far larger than localStorage's ~5MB cap — hundreds of MB including screenshots).
- On first launch, any data from the old localStorage build is **migrated automatically, once**.
- A warning appears as data approaches ~50MB; export a backup periodically.

### 📸 Screenshot handling
- **Upload** files, or **paste** straight from the clipboard with **Ctrl+V** into the paste box.
- Images are **auto-compressed** (longest side scaled to 1600px, re-encoded as JPEG), shrinking size dramatically while staying readable.
- Click a thumbnail to open the **lightbox**: zoom in/out, scroll-wheel zoom, drag to pan; keyboard shortcuts `+` / `-` / `0`, `Esc` to close.

### ✏️ Inline editing
- Click **Description / Solution / ETA / Notes** directly on the card to edit in place.
- `Enter` saves, `Esc` cancels (use `Shift+Enter` for a newline in multi-line fields).
- **Notes** are a multi-item bulleted list — add, edit, and delete each entry individually.

### 🔍 Filtering & sorting
- Keyword search (covers ID, title, description, solution, notes, Jira, owner, and ETA).
- **Bug ID** multi-select and **Owner** multi-select filters, each with an in-panel live search.
- Status filter: **Not Started** (0 environments passed) / **In Progress** (some passed) / **Ready to Archive ✓** (all three passed).
- Sort by Bug ID (A–Z / Z–A, natural numeric ordering).

### 📦 Archive
- Once all three environments pass, a bug is marked **Ready to Archive** and can be tucked away.
- Archive individually, browse the archive, move back to active, or delete all archived items at once.

### 📝 Change history
- Every bug keeps a **timestamped change history** (creation, status changes, ETA edits, screenshot additions/removals, archiving, etc.).

### 🎫 Other
- **Jira Ticket / URL** field (a URL becomes a clickable link).
- **Owner** field with auto-suggestions from existing names.
- **Light / dark theme** toggle (defaults to light, remembers your choice).
- The header, toolbar, and summary bar are all **sticky** and stay visible while scrolling.

### 📤 Export / Import
- **Export**: save all data to a JSON file as a backup.
- **Import**: load a JSON file; if data already exists, you're asked whether to merge (duplicate IDs are reassigned fresh IDs).

---

## 🚀 Usage

Just open it in a browser:

```
open bug-tracker-v4.html      # macOS
```

Or drag `bug-tracker-v4.html` into any browser tab.

> ⚠️ **Data is stored in the IndexedDB of whichever browser opened the file.**
> Switching browsers, switching computers, or clearing browser data will not sync your data automatically.
> To move or back up your data, use **⬆ Export / ⬇ Import** in the top-right corner.

---

## 🔒 Privacy

Runs entirely locally — no server, no tracking, no external requests. Your bug data and screenshots never leave your browser.

---

## 🛠 Tech

- A single `.html` file, plain HTML / CSS / JavaScript, **zero dependencies**.
- Storage: IndexedDB (data) + localStorage (small UI preferences such as theme, sort, column width, expanded state).

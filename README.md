# nox
A minimal, local-first note system that lives entirely in the browser. No accounts. No sync. No server. Just type and it’s saved.

**Website**: [nox.directory](https://nox.directory)

---

## What is nox?

nox is a radically simple web-based note-taking tool built for **privacy, permanence, and precision**.

It turns any URL into a self-contained notebook entry, saved entirely inside your own browser — optionally encrypted with a password, accessible only from the same device.

---

## Core Principles

- **No accounts** – no signups, no tracking, no backends  
- **Local-first** – your data never leaves your browser  
- **Ephemeral by design** – nothing is stored in a database or synced to the cloud  
- **Private by default** – optional password encryption keeps your data safe even from your future self  
- **Ultra-minimal** – just you and your text  
- **Offline-compatible** – works even if you're not connected  
- **Portable** – built as a single HTML file  

---

## How It Works

nox stores note data using your browser’s built-in `localStorage`.

- Each unique URL path (e.g. `/my-notes`, `/journal`, `/work/plan-a`) creates a different note
- The full state of the note (including encryption) is saved locally on that browser
- You can optionally enter a password to encrypt your note using **AES-GCM with PBKDF2** key derivation
- The encrypted content is also stored in `localStorage`, but can only be unlocked with your password

---

## How to Use It

1. **Go to any URL** on your nox site:  
   `nox.directory/grocery-list`  
   `nox.directory/ideas`  
   `nox.directory/2024-vision`  

2. **Start typing** — your changes are saved automatically.

3. **Want privacy?** Add a password and it will encrypt the content. You'll need the same password to unlock that note in the future.

4. **Clear note?** Hit `Forget`.

---

## Encryption Details

- Encryption is client-side only using Web Crypto API
- AES-GCM symmetric encryption
- Passwords never leave your machine
- A static salt is used for key derivation (can be improved later with dynamic salts per-note)
- You must remember your password. There’s no recovery.

---

## Tricks & Architecture

### 1. Single-Page Architecture via 404 Routing

To use custom URLs like `/note/journal`, we use GitHub Pages' 404 fallback trick.

- We set `index.html` as the 404 page in GitHub Pages
- Any non-existent route is redirected to `index.html`, and the JavaScript reads the URL path to generate a `note-id`
- Each path becomes a unique key in `localStorage`

This enables “permalink notes” while hosting everything in a static site.

### 2. Tiny UI with Large Writing Surface

- The writing experience is optimized for space: most of the screen is the text
- Footer and controls are tucked away smartly
- Works beautifully on mobile and desktop

### 3. Persistent Dark/Light Theme

- Toggle dark/light mode
- Theme preference is saved in localStorage and remembered on reload

---

## Use Cases

- Private journals
- Scratchpad for writing
- Quick, local todo lists
- Project planning
- Daily logs or coding notes
- Encrypted thoughts or secrets
- Custom wiki with zero setup

---

## Potential Roadmap

This project is intentionally minimal, but future ideas could include:

- [ ] Support for downloadable `.txt` or `.md` export
- [ ] Drag-and-drop file attachment (stored locally via blobs)
- [ ] Tagging or folder-like navigation (in-memory)
- [ ] Remote sync via opt-in storage providers (e.g., WebDAV or Dropbox — but still optional)
- [ ] Markdown rendering toggle
- [ ] IndexedDB support for larger notes
- [ ] Per-note theme or font
- [ ] URL shortening / shareable note links (client-side only)

---

## Design Philosophy

nox isn’t trying to be Notion. Or Evernote. Or Google Docs.

It’s for those who want something **instant**, **private**, and **local**.  
It’s about creating a space where:

- The interface disappears  
- The system never owns your content  
- And writing is the primary action, not an afterthought  

---

## Challenges + Limitations

- **No sync** – your note stays on the same browser/device
- **No versioning** – autosave overwrites immediately (may be extended with snapshots)
- **Password recovery is impossible** – if you forget, it’s gone (by design)
- **Not secure against local device compromise**
- **localStorage is limited (~5MB)** — don't store massive notes or files

---

## Install Locally

You can self-host nox anywhere (GitHub Pages, Netlify, Vercel, etc).

To run it locally:

```bash
git clone https://github.com/yourusername/nox
cd nox
# drop the index.html in your browser or serve it:
python3 -m http.server
```

If you want per-URL routing locally, use a static server that rewrites all paths to `index.html`.

---

## Hosting on GitHub Pages

1. Drop `index.html` in your repo root
2. Enable GitHub Pages (branch = `main`, folder = `/`)
3. Go to Settings → Pages → Set `404.html` to the same file as `index.html`
4. Done. Now `yoursite.github.io/whatever/path` will always load the app

---

## License
See: github.com/korzewarrior/license

---

## Author

Made by korze,  
Built with intention, minimalism, and a typewriter’s soul.

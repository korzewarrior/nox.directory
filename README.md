# nox

A local-first note-taking tool that runs entirely in the browser. Each URL path becomes a separate note stored in localStorage. Optional AES-GCM encryption.

No accounts, no server, no sync. Single HTML file.

[nox.directory](https://nox.directory)

## Usage

Visit any path to create a note:

```
nox.directory/grocery-list
nox.directory/journal
nox.directory/work/plan-a
```

Notes autosave as you type. Add a password to encrypt. Hit Forget to clear.

## Self-host

```bash
git clone https://github.com/korzewarrior/nox.directory
python3 -m http.server
```

Your server needs to rewrite all paths to `index.html` for URL routing to work.

## License

See [github.com/korzewarrior/license](https://github.com/korzewarrior/license)

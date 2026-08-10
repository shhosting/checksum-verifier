# Checksum Verifier

A small, dependency-free browser tool for verifying a file's checksum against
an expected SHA-256, SHA-1, SHA-384, or SHA-512 hash.

**Live:** https://shhosting.net/checksum-verifier

## Why

Most "online checksum verifier" tools ask you to upload the file to a server.
That defeats the point of verifying a download you don't yet trust. This tool
never uploads anything — hashing happens entirely client-side via the
browser's native [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/digest).
Open DevTools → Network tab and confirm nothing leaves the browser.

## Features

- Drag-and-drop or file picker
- SHA-256, SHA-1, SHA-384, SHA-512
- Flags SHA-1 as weak/deprecated for integrity verification
- For very large files (where in-browser hashing risks running out of memory),
  falls back to showing the equivalent native command for Windows
  (`certutil`), macOS (`shasum`), and Linux (`sha256sum` / etc.), pre-filled
  with the correct filename and algorithm flag
- No build step, no dependencies, no analytics — a single static HTML file

## Running locally

There's nothing to build. Open `index.html` in a browser, or serve the
directory with any static file server:

```bash
python3 -m http.server 8000
```

## Contributing / review

This was written quickly for personal use using several different AI agents 
and hasn't had independent review — that's exactly what I'm looking for. 
If you spot anything questionable in the hashing logic, the large-file 
fallback, or general code quality, please open an issue or PR. 
Particularly interested in:

- Correctness of the Web Crypto usage
- Edge cases in file handling (empty files, 0-byte drops, etc.)
- Anything that looks like it could leak data despite the "nothing uploaded"
  claim above

## License

MIT — see [LICENSE](./LICENSE). Use it, fork it, embed it, whatever.

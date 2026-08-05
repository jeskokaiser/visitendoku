# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is

`visitendoku.html` is the entire product: a single, self-contained static HTML file
(vanilla HTML/CSS/JS, no build step, no framework, no backend, no database). It is a
German ward-round documentation ("Visitendokumentation") generator for general surgery.
`README.md` and `LICENSE` are the only other files. There is no `package.json`,
lockfile, dependency manifest, or CI config — so there are no dependencies to install
and nothing to build.

### Running it for development

Serve the repo root over `http://localhost` rather than opening via `file://`. The app's
"copy to clipboard" feature relies on the async Clipboard API, which browsers only enable
in a secure context (`localhost` counts). A static file server is all that is needed:

```bash
python3 -m http.server 8080   # then open http://localhost:8080/visitendoku.html
```

There is no lint/test/build tooling in this repo (no linters, no test runner, no
bundler). "Running the app" is the only workflow. Editing content means editing the
`BAUSTEINE` data structure inline in the `<script>` block of `visitendoku.html`; changes
take effect on a browser reload (no hot-reload/watcher — refresh manually).

### Gotchas

- Patienteneingaben werden absichtlich nicht gespeichert (kein `localStorage`, keine
  Cookies, kein Netzwerk). Visite-Zustand lebt nur im Speicher und ist nach Reload weg.
  Baustein-Katalog-Änderungen über die UI müssen explizit mit „HTML speichern" als
  Datei auf dem PC abgelegt werden — sonst sind auch sie nach Reload weg.
- Because unsaved input triggers a browser `beforeunload` prompt, automated navigation
  away from a filled-in form may surface a "Leave site?" confirmation.

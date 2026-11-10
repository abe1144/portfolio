# Lesson 0: Setup

## Why

A React app is not something the browser runs as-is. You write JSX and modern
JS split across many files; a **build tool** (Vite) turns that into plain
HTML/CSS/JS the browser understands. While you work, Vite also runs a **dev
server** that rebuilds and refreshes the page the moment you save.

Flask comparison: in Flask, Python on the server builds the HTML for every
request. Here, the server's only job is to hand over files once. After that,
React runs **in the browser** and builds the page there.

## Mental model

```
 Python world                     JavaScript world
 ------------                     ----------------
 python (interpreter)        <->  node  (runs JS outside a browser)
 pip / uv                    <->  npm   (installs packages)
 requirements.txt / pyproject <-> package.json      (what you depend on)
 uv.lock                     <->  package-lock.json (exact versions, commit it)
 .venv/                      <->  node_modules/     (installed code, never commit)
 flask run                   <->  npm run dev       (local dev server)
```

What happens on `npm run dev`:

```
 your files (src/*.jsx) --> Vite dev server --> browser at localhost:5173
        ^                                              |
        +------ you save a file: page updates (HMR) ---+
```

What happens on `npm run build`:

```
 src/ + index.html --> Vite --> dist/  (plain static files: this is what goes to S3 later)
```

## Project anatomy (after scaffolding)

| File / folder       | What it is                                                                     |
| ------------------- | ------------------------------------------------------------------------------ |
| `index.html`        | The one HTML page. It has an empty `<div id="root">` and loads `src/main.jsx`. |
| `src/main.jsx`      | Entry point. Finds `#root` and tells React to render `<App />` into it.        |
| `src/App.jsx`       | Your first component.                                                          |
| `public/`           | Files copied as-is (favicon, resume PDF, images).                              |
| `package.json`      | Project name, scripts (`dev`, `build`, `lint`), dependencies.                  |
| `package-lock.json` | Exact resolved versions. Commit it.                                            |
| `node_modules/`     | Installed packages. Never commit. Rebuild with `npm install`.                  |
| `vite.config.js`    | Vite settings (plugins).                                                       |
| `eslint.config.js`  | Lint rules.                                                                    |

## Steps (Abraham types these)

1. Scaffold Vite + React (JavaScript) into this folder.
2. `npm install`, then `npm run dev`; open the page; edit `App.jsx`, watch it update.
3. Tour the files above; trace `index.html` -> `main.jsx` -> `App.jsx`.
4. Replace the demo with a "hello" page.
5. Check `.gitignore` covers `node_modules`, `dist`, `.env*`.
6. Add Prettier; make `npm run lint` pass.
7. First commit.

## Acceptance criteria

- [ ] `npm run dev` shows a page that says hello (your words), no demo logo/counter.
- [ ] `npm run build` succeeds and creates `dist/`.
- [ ] `npm run lint` passes with no errors.
- [ ] `.gitignore` includes `node_modules`, `dist`, and `.env*` (while keeping `.env.example` allowed).
- [ ] `git status` before the commit shows no `node_modules/` or `dist/`.
- [ ] First commit made with a clear message.

## Explain-back questions

1. What is the difference between `node_modules/` and `package-lock.json`, and which one goes in git?
2. Trace what happens from opening `localhost:5173` to seeing "hello" on screen.
3. What does `npm run build` produce, and why is that different from what `npm run dev` serves?

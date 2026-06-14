# CLAUDE.md — Twitch Live + Firebase TTS Interactive Page

## Project Overview
Static web page for GitHub Pages. Embeds a Twitch live stream with offline GIF fallback, accepts audience text input and pushes to Firebase Realtime Database for a local Python TTS program.

## Standard Document Paths

| Document | Path | Purpose |
|----------|------|---------|
| Requirements | [docs/requirements.md](docs/requirements.md) | Functional & non-functional requirements |
| Technical Spec | [docs/tech-spec.md](docs/tech-spec.md) | Architecture, SDKs, data flow |
| Design Spec | [docs/design-spec.md](docs/design-spec.md) | Color palette, typography, UI patterns |
| Execution Plan | [docs/execution-plan.md](docs/execution-plan.md) | Step-by-step phases with acceptance criteria |

## Working Conventions

1. **Development logs**: After each coding session, write a log to `devlogs/YYYY-MM-DD.md` recording what was completed and what remains to-do.
2. **Phase by phase**: Follow [docs/execution-plan.md](docs/execution-plan.md). Do not jump ahead — complete and verify each phase before starting the next.
3. **All visible text in English**: No Chinese in the rendered page.
4. **User-provided values**: Twitch channel name, image paths, Firebase config are clearly commented with `[USER: ...]` markers in `index.html`.
5. **Single file architecture**: `index.html` contains all HTML, CSS (in `<style>`), and JS (in `<script>`). No build tools, no separate files.
6. **Assets**: All user-provided media files go in `assets/`. The directory already exists with placeholder notes.
7. **Verification**: After each phase, verify by opening `index.html` in a browser or via `python3 -m http.server 8080`.

## Key Technical Choices
- Twitch: JS SDK (Embed API) with `ONLINE`/`OFFLINE` events
- Firebase: Modular CDN SDK, Realtime Database at `messages/`
- Parent domain: Always `window.location.hostname` (dynamic)
- UI: Terminal/noise-art fusion, background `#303030`, monospace fonts

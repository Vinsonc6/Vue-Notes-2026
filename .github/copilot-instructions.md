<!--
Guidance file for AI coding agents working on this repository.
Keep this short and action-focused. Mention only discoverable patterns and concrete commands.
-->

# Copilot instructions for Vue-Notes-2026

Be concise. Make minimally invasive changes. When in doubt, prefer a small, working PR that preserves existing behavior.

Key facts
- Project type: Vue 3 app scaffolded for Vite (see `vite.config.js`). Entry: `src/main.js` mounts `App.vue`.
- Router: `src/router/index.js` — routes use file imports from `src/views/`. The base route maps to `src/views/CookieClicker.vue`.
- Module alias: `@` -> `src/` (configured in `vite.config.js` and `jsconfig.json`) — use `@/components/...` and `@/views/...` imports.
- Package scripts (run from `app/`): `npm run dev` (hot dev), `npm run build`, `npm run preview`, `npm run lint`, `npm run format` — see `package.json`.

Coding conventions and patterns (observable)
- All components use the Composition API and `<script setup>` format (e.g. `AnimalCard.vue`, `CookieClicker.vue`). Follow the same style.
- Styles are scoped by default (`<style scoped>`) and sometimes use `lang="scss"` — preserve scoping unless a global rule is being added.
- Props: components declare props with `defineProps` (see `AnimalCard.vue`); prefer typed prop checks where simple (Object, String, Number).
- State: `ref` and `reactive` are used (examples: `CookieClicker.vue`, `UserCreate.vue`, `ViewLists.vue`). Prefer these primitives for local component state.
- Events: parent components attach event listeners directly to child components (e.g. `<AnimalCard @click="addToCart(...)" />`). Note: this relies on the child root element receiving DOM events.

Common pitfalls to check before committing
- Router import typo: `src/router/index.js` currently imports `ViewLists` with a trailing slash: `@/views/ViewLists.vue/` — fix to `@/views/ViewLists.vue` if touching routing.
- Public assets live in `public/` and are referenced with absolute paths like `/cookie.png` (see `CookieClicker.vue`).
- Node engine requirement: package.json sets Node to `^20.19.0 || >=22.12.0`. Ensure CI/dev environment satisfies this.
- Linting uses two tools: `oxlint` and `eslint` (scripts: `lint:oxlint`, `lint:eslint`). Use the `npm run lint` umbrella script.

Build / dev workflow (explicit commands)
- Install: `npm install` (run from `app/`).
- Start dev server: `npm run dev` — Vite hot reload + `vite-plugin-vue-devtools` loaded.
- Build production: `npm run build` and to locally preview: `npm run preview`.
- Lint & format: `npm run lint` and `npm run format`.

When making changes
- Keep changes small and focused. Prefer editing a single component or view per PR.
- Preserve `<script setup>` and `ref`/`reactive` usage. Convert Options API only if you update all related files consistently.
- Use the `@` alias for imports. Avoid relative deep paths like `../../../` when `@/` is available.

Files to inspect for context before edits
- `package.json` — scripts, deps, Node engine
- `vite.config.js`, `jsconfig.json` — alias & plugins
- `src/main.js`, `src/App.vue` — app mounting and layout
- `src/router/index.js` — route definitions and common typo
- `src/views/*` and `src/components/*` — component patterns (props, events, scoped styles)

If you change config or build files
- Run the local build/dev to verify: `npm run dev` then visit the app.
- Run `npm run build` and `npm run preview` to sanity-check production output.

No existing agent guidance files were found in the repo. If you add or merge content from a human-written `AGENT.md` or similar, keep only concrete, discoverable commands and patterns.

If anything above is ambiguous, ask for a short clarifying question and prefer a safe, incremental edit.

Examples (copyable snippets)
- Use alias imports:
  - import AnimalCard from '@/components/AnimalCard.vue'
- Define props in `<script setup>`:
  - const props = defineProps({ animal: { type: Object, required: true } })

Thank you — request feedback if any items are unclear or missing.

# Copilot instructions

Project context Copilot should apply to every session in this repository.

## Stack

- Framework: Astro (static output).
- Language: JavaScript inside Astro components, with TypeScript syntax where Astro explicitly supports it.
- Styling: plain CSS in `src/layouts/Base.astro`.
- Package scripts: use `npm run dev`, `npm run build`, and `npm run preview`.

## Conventions

- Keep components small and focused.
- Prefer semantic HTML and accessible markup.
- Use two-space indentation, semicolons, and descriptive variable and function names.
- Keep implementation logic in small functions and avoid unnecessary dependencies or abstractions.
- Preserve strict TypeScript settings. Do not use `any` or unsafe casts; type DOM elements before using element-specific properties.
- Validate bookmark URLs before saving them. Accept only valid HTTP(S) URLs, and preserve the original URL entered by the user.
- Generate every bookmark slug in the form `mona-` followed by four short, URL-safe characters, for example `mona-7fk2`.
- Keep slugs unique within the saved bookmark list. Prefer a counter or hash-based generator rather than random or opaque identifiers.
- Do not close, or add closing keywords for, the exercise walkthrough issue (issue #1) in any pull request.
- When opening a pull request for app work, link only the specific app work-item issue being implemented.

## Bookmark persistence

- Persist saved bookmarks with `localStorage` under the stable key `mona-bookmarks`.
- Store each bookmark as a JSON object containing at least `url` and `slug` fields.
- Read and parse stored data defensively: malformed or unavailable browser storage must not break the page.
- Write the complete bookmark list after a bookmark is added or cleared.
- Render from the persisted list on page load, and keep the in-memory list as the source for normal page interactions.
- Never persist or transmit bookmark data to a server.

## Browser and hydration boundaries

- Put browser-only behavior, including `localStorage`, `document`, DOM events, URL validation, slug generation, and the Clipboard API, in the client-side `<script>` block of `src/components/Bookmarks.astro`.
- Do not access browser APIs in Astro frontmatter, component module code, or layout markup that runs during the static build.
- Guard browser behavior for the client lifecycle; use no build-time assumptions about `window`, `localStorage`, or `navigator`.
- Build the static markup in Astro, then enhance it only in the client-side script.

## Quality and pull request workflow

- Make changes small and focused, follow existing markup and class names, and avoid unrelated cleanup.
- Run `npm run build` after code changes and address any build or type errors.
- Check the relevant UI behavior in the browser, including adding, rendering, copying, clearing, and reloading bookmarks.
- In a pull request description, summarize the app behavior changed and link the relevant app work-item issue.
- Never link or close issue #1 as the implementation work item; its GitHub Actions workflows manage it automatically.

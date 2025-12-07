<!-- Copilot instructions for AI coding agents working on the magic-portfolio repo -->
# Magic Portfolio — AI Assistant Instructions

This file captures the minimal, actionable knowledge an AI coding agent needs to be immediately productive in this repository.

## Quick Context
- **Framework:** Next.js (app-router) — code lives in `src/app/` and uses server/client components and `generateMetadata()` exports (see `src/app/about/page.tsx`).
- **UI library:** `@once-ui-system/core` is imported across components (e.g. `src/app/about/page.tsx`).
- **MDX content:** Blog and project pages use MDX files under `src/app/blog/posts/` and `src/app/work/projects/`.
- **Styling:** SCSS module files alongside components (e.g. `src/components/*.module.scss`).
- **API routes:** Under `src/app/api/` (e.g. `authenticate`, `check-auth`, `og/generate`, `rss`). Expect both `route.ts` and server-side React route components.

## Important Files & Directories (examples)
- `src/app/` — application entry points and pages (app-router). Inspect `page.tsx` files to understand routing and server/client boundaries.
- `src/components/` — shared UI components, SCSS modules, and small helpers like `RouteGuard.tsx` and `Providers.tsx`.
- `src/resources/` — central content and configuration used across pages (`baseURL`, `about`, `person`, `social`).
- `src/app/api/og/generate/route.tsx` — dynamic Open Graph generator; useful when modifying metadata or OG images.
- `public/` — static images and assets, including project images in `public/images/projects/`.
- `package.json` — scripts used by developers: `dev`, `build`, `start`, `export`, `lint`, plus `biome-write` formatting.

## Typical Developer Workflows (commands)
- Install dependencies: `npm install`.
- Run dev server: `npm run dev` (Next dev server; uses `next dev`).
- Build for production: `npm run build` (Next build).
- Export static site (project supports `next export`): `npm run export`.
- Start production server: `npm run start`.
- Lint: `npm run lint`.
- Format (project uses Biome): `npm run biome-write` → runs `npx @biomejs/biome format --write .`.

When making changes, prefer running `npm run dev` and visiting the matching route in the browser. Many pages use server-side code (async `generateMetadata()`), so confirm behavior both client and server-side when relevant.

## Code Patterns & Conventions (concrete)
- App Router & metadata: pages export async `generateMetadata()` and include `Schema` / `Meta.generate()` usages for SEO. See `src/app/about/page.tsx` for an example.
- Component imports: components import UI primitives from `@once-ui-system/core` (e.g., `Row`, `Column`, `Avatar`, `Media`). Follow existing prop patterns (layout props like `fillWidth`, `gap`, `paddingX`) rather than introducing raw CSS unless necessary.
- MDX usage: content authors add `.mdx` files under `src/app/blog/posts` and `src/app/work/projects`. Treat those as content-only; components render their output via MDX loader/renderer.
- Styling: use SCSS modules next to components and reference by `className={styles.foo}`. Avoid global CSS unless located in `src/resources/custom.css`.
- Images: For project/gallery images prefer `public/images/...` paths and use `Media` component wrappers that already implement sizing and radius props.

## API & Integration Notes
- OG generation and proxying are implemented under `src/app/api/og/*`. If you change metadata format, update both `generate` and `proxy` routes.
- Authentication endpoints live under `src/app/api/authenticate` and `check-auth`. These are small server-only routes – treat credentials or tokens carefully (no secrets in source).

## Tests & Static Checks
- There are no explicit unit tests in the repository. Rely on `npm run build` and `npm run lint` as verification steps.
- Formatting uses Biome; run `npm run biome-write` before opening PRs.

## How to Edit Safely (best practices specific to this repo)
- When changing layout or shared components, update `src/components/*` and keep SCSS module names stable to avoid breaking page layouts.
- When altering `resources` data (e.g., `about`, `person`, `social`), search for usages in `src/app/**` — these objects are referenced directly by pages.
- If you add routes under `src/app/api`, maintain consistent filenames: `route.ts` for server handlers and `route.tsx` only when returning React/JSX for dynamic images (OG generation uses `route.tsx`).

## When in doubt — files to inspect first
- `package.json` — confirm scripts and dependency versions.
- `src/app/layout.tsx` — global layout & Providers.
- `src/resources/index.ts` — shared constants and content.
- `src/components/Providers.tsx` and `RouteGuard.tsx` — app-level behaviors.

## Request for feedback
If any section is unclear or you'd like more detail (examples, code snippets, or additional file references), reply with what to expand and I will iterate.

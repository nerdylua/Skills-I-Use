---
name: vite-to-nextjs-port
description: Port Vite React apps to Next.js App Router projects. Use when migrating from Vite, copying TSX/CSS/components into a scaffolded Next app, moving root app code into app/page.tsx, configuring app/layout.tsx, or fixing Next build issues after a Vite migration.
---

# Vite To Next.js Port

## First Steps

1. Fetch or read the official Next.js guide: `https://nextjs.org/docs/app/guides/migrating/from-vite`.
2. Identify the Vite root (`index.html`, `src/main.tsx`, `src/App.tsx`, `src/index.css`, `src/components`) and the scaffolded Next root (`app/layout.tsx`, `app/page.tsx`, `app/globals.css`).
3. Use shell copy commands for the initial port when the user asks for a direct migration. Avoid over-inferring from code before copying.
4. Preserve the user's requested structure. If they say no `src` folder, put files directly under `app/` and `app/components/`.

## Copying Pattern

Use your shell to copy Vite components and global CSS into the Next app. A common mapping is `src/components` -> `app/components` and `src/index.css` -> `app/globals.css`.

Prefer moving the Vite `App.tsx` body into `app/page.tsx` rather than keeping an extra `app/App.tsx` unless the user wants that wrapper.

## App Router Wiring

`app/layout.tsx` is the App Router equivalent of Vite's `index.html`. Convert the HTML shell there:

- Keep `<html lang="en">` and `<body>{children}</body>`.
- Do not keep Vite's `<div id="root">` or `<script type="module" src="/src/main.tsx">`.
- Next already manages charset and viewport metadata.
- Move title/description into `export const metadata`.
- Remove create-next-app defaults, especially unused scaffold fonts/classes.

If the Vite app is interactive, make `app/page.tsx` a client component:

```tsx
"use client";

import { useState } from "react";
```

Any component using hooks, browser APIs, or DOM refs must be inside the client component tree or marked with `"use client"`.

## Fonts

Fonts are a common source of "looks slightly off" bugs.

Remove scaffolded fonts you did not use in Vite, and if the Vite app used Google CSS imports, prefer replacing them with `next/font/google`. If you use Tailwind, point its theme font variables at the Next font variables.

## Dependencies

Compare Vite `package.json` imports against Next `package.json`. Install runtime dependencies used by copied components.

Do not install Vite-only dependencies into the Next app unless still needed.

## Common Fixes

- Escape JSX text that Next lint rejects: `&apos;`, `&quot;`.
- Fix hook/state declaration order surfaced by React lint.
- Client-only libraries (animations, media, DOM APIs) should run only in client components. Initialize them in `useEffect` and clean up on unmount.
- Leave copied `<img>` tags initially if the goal is a faithful port. Treat `@next/next/no-img-element` as an optimization warning unless the user asks for Next Image conversion.

## Nested Repos (Optional)

When a scaffolded Next app lives inside a parent repo and Next infers the wrong root, set `turbopack.root` to the Next app directory in `next.config`. Verify the warning is gone by running a build.

## Validation Checklist

Run lint and build from the Next app root using the repo's package manager.

Expected for a no-`src` direct port:

- `app/page.tsx` contains the page/client root.
- `app/layout.tsx` owns the root HTML, metadata, and font variables.
- `app/globals.css` contains the copied global CSS adjusted for Next fonts.
- `app/components/` contains copied Vite components.
- `app/App.tsx` does not exist if the user asked to inline it into `page.tsx`.
- `src` does not exist in the Next app if the user asked for no `src` folder.

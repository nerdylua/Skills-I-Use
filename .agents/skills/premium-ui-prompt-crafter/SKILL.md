---
name: premium-ui-prompt-crafter
description: Generate long, technically exact prompts for one-shot premium hero sections and landing pages. Use when the user wants beautiful UI prompts, MotionSites-style hero or landing page prompting, UI requirement interviews, visual direction into Vite/Next.js prompts, video/background asset direction, or highly specified React/Tailwind UI generation prompts.
---

# Premium UI Prompt Crafter

Use this skill to turn a user's UI idea into a high-fidelity implementation prompt for Google AI Studio, Cursor, Lovable, Bolt, or another coding agent. The goal is not to implement the UI directly unless the user asks. The goal is to interrogate the brief, resolve ambiguity, then create a long, precise `design.md` prompt that can one-shot a premium hero or landing page.

## Core Principle

These prompts work because they replace vague taste words with concrete production instructions. Do not say only "beautiful, modern, aesthetic." Specify the stack, design system, section order, exact copy, typography, colors, media, layout geometry, animation timings, responsive behavior, interaction states, constraints, and acceptance criteria.

The final `design.md` must read like an implementation blueprint, not a moodboard. Include concrete code elements wherever they reduce ambiguity: representative React/HTML structure, Tailwind class strings, CSS variables, custom CSS utilities, keyframes, JS/TS animation logic, asset manifests, component props/data arrays, icon names, exact ARIA labels, and responsive class changes. The target generator should be able to build the page without inventing layout, typography, or design-system details.

Prefer one strong visual concept over many loose ideas. A premium result should usually have one video-led signature scene: fullscreen AI-generated video, ambient product footage, Spline/3D object with video backdrop, cinematic mockup, dashboard, glass card system, marquee, animated pipeline, or editorial typography.

## Workflow

1. Interview the user hard before generating the final prompt unless they already provided unusually complete detail.
2. Ask targeted follow-up batches until product, visual direction, copy, assets, stack, and constraints are mutually clear. If answers are vague, ask another sharper batch instead of rushing to assumptions.
3. Do not generate the prompt until the user has answered enough to make the result specific, or explicitly tells you to proceed with named assumptions.
4. Once requirements are clear, create or overwrite `design.md` with one complete implementation prompt. Do not stream the long prompt in chat.
5. Default to React + TypeScript + Vite + Tailwind CSS unless the user asks for Next.js. For production app routes, use Next.js App Router. For Google AI Studio/manual generation, Vite is usually the safest default.
6. Treat a video asset as the default highest-priority media choice for heroes and premium sections. Only decide "no video asset is required" in rare cases: when the user explicitly asks for no video, the target platform forbids it, performance constraints make it unsuitable, or a deliberately static/typographic concept is clearly stronger.
7. Include asset-generation direction when video, 3D, mockup, or image assets are needed. If no suitable hosted video already exists, create a separate AI video-generation prompt in chat, tell the user to generate it in their video tool, host the MP4/WebM, and paste that hosted URL into `design.md`. Do not include the AI video-generation prompt inside `design.md`.
8. Include "do not add" constraints to prevent the generator from inventing off-brand decorations.

## Requirement Interview

Ask about every category that affects fidelity:

- Product: name, category, audience, offer, desired conversion action.
- Output scope: hero only, single landing page, or multi-section landing page.
- Stack: Vite or Next.js, Tailwind version, animation library, icon library, UI kit allowed or forbidden.
- Visual world: mood, industry analogies, luxury level, dark/light, editorial/SaaS/cinematic/fintech/web3/agency/portfolio.
- Signature visual: default to video background/ambient video unless constrained; otherwise 3D object, dashboard mockup, product UI, image collage, shader, Spline scene, glass orb, animated illustration, or pure typography.
- Media assets: existing URLs, generated asset brief, fallback poster, video loop behavior, focal point, overlays, blend modes.
- Typography: display font, body font, accent font, weights, tracking, line-height, italic accent words. Instrument Sans is a beautiful hero/UI font and can quietly elevate a premium hero when the visual direction fits.
- Color system: exact hex/HSL tokens, allowed accent colors, forbidden colors.
- Design system implementation: CSS variables, Tailwind theme tokens, utility classes, component variants, border/shadow/glass/noise recipes, and exact icon names.
- Layout: viewport height, section order, max widths, grid columns, pinned/floating elements, card sizes, border radii, spacing rhythm, z-index layers, absolute offsets, and container padding.
- Navigation: logo, links, CTA, mobile menu behavior.
- Copy: headline, subheadline, badges, stats, buttons, cards, testimonials, nav labels.
- Code shape: component names, data arrays, representative JSX/HTML for complex sections, required CSS classes, JS hooks/effects, and file boundaries.
- Animation: page-load entrance, text reveal, scroll effects, marquee, hover states, video fade loops, reduced-motion expectations.
- Responsiveness: breakpoints, mobile substitutions, hidden elements, fluid typography.
- Technical constraints: no backend, no routing, no extra libraries, use local assets, no placeholder copy, no random gradients.

If the user is unsure, offer 3 opinionated directions and ask them to choose. Keep interviewing after they choose until the brief is implementation-ready.

## Prompt Anatomy

Generate the final prompt with these sections, adapting as needed:

1. **Opening Command**: one sentence naming the product, scope, stack, and intended aesthetic.
2. **Non-Negotiables**: exact reproduction goals, forbidden additions, output framework, no backend unless asked.
3. **Files To Create/Edit**: exact files, exported components, imported assets, and whether code lives in `App.tsx`, `app/page.tsx`, `globals.css`, `tailwind.config`, or component files.
4. **Dependencies & Setup**: packages, font imports, Tailwind theme extensions, global CSS reset/body styles.
5. **Design System Tokens**: colors as hex/HSL/CSS variables, typography scale, font stacks, radii, spacing rhythm, shadows, glass/noise/gradient utilities, and component variant recipes.
6. **Asset Manifest & Media Handling**: exact URLs or non-video generation briefs; video URL placeholder or final hosted URL; video attributes; object-fit, focal point, poster, overlay, blend mode, loop/fade behavior. If video is intentionally omitted, state the reason clearly.
7. **Data & Copy Constants**: arrays/objects for nav links, stats, cards, testimonials, feature rows, logos, and every visible copy string.
8. **Page/Section Structure**: ordered sections, component names, semantic HTML tags, z-index/layering model, and DOM hierarchy.
9. **Detailed Section Specs**: layout, copy, classes, inline styles, grid behavior, measurements, z-index, responsive changes, and representative JSX/HTML snippets for visually important parts.
10. **CSS & Tailwind Implementation**: exact class strings, CSS variables, custom utilities, pseudo-elements, keyframes, media queries, and when to use inline styles.
11. **Interactions & Animation**: exact delays, durations, easing curves, Framer Motion/GSAP logic, JS hooks/effects, hover/tap states, cleanup for listeners/rAF, and reduced-motion behavior.
12. **Responsive Rules**: mobile-first behavior, breakpoints, alternate layouts, mobile-specific copy/media decisions, and exact class substitutions.
13. **Accessibility & QA Notes**: ARIA labels, focus states, contrast requirements, image alt text, keyboard behavior, and performance constraints.
14. **Acceptance Criteria**: concise checklist describing what must be true when complete.

## Required Code-Level Detail

Every `design.md` must include enough code-level detail to prevent the generator from designing by guesswork:

- For critical visual or behavioral elements, do not merely describe the effect. Provide exact implementation blocks with file names, constants, component structure, CSS/keyframes, hooks/effects, cleanup logic, class names, and edge-case notes. "Representative" snippets are acceptable only for simple repeated layout, not for signature effects, scroll/video behavior, animation systems, navigation interactions, coded mockups, or the main hero composition.
- Show representative JSX/HTML for the navbar, hero, and any complex visual section. Do not write a full app unless needed, but include the actual tag hierarchy, key class names, data mapping pattern, and component names.
- Show CSS/Tailwind implementation for the design system: `:root` tokens, font imports, custom utility classes, keyframes, pseudo-elements, and any Tailwind config extensions that matter.
- Show JS/TS logic for nontrivial behavior: video crossfade, marquee arrays, scroll listeners, `requestAnimationFrame`, Framer Motion variants, GSAP timelines, mobile menu state, or pointer interactions.
- Show an asset manifest with variable names, hosted URLs/placeholders, expected dimensions, formats, fallback poster, focal point, alt text, and whether the asset is generated, provided, or coded in JSX/SVG.
- Specify exact typography at each breakpoint: font family, size or `clamp()`, weight, tracking, line-height, max-width, text balance/wrap behavior, and any highlighted words.
- Specify exact layout geometry: section min-height, container width, padding, grid/flex rules, card sizes, gap scale, absolute positions, border radius, z-index, and overflow behavior.
- Specify exact interaction states: hover, active, focus-visible, disabled, loading, reduced-motion, and mobile menu open/closed states.
- If a section is visually important but not shown as code, add a short reason and compensate with exact class strings, measurements, and copy.

## MotionSites-Style Patterns To Use

Use these patterns when they fit the brief:

- Fullscreen `video` background with `autoPlay muted loop playsInline object-cover`; specify focal point and whether overlays are allowed.
- Manual video crossfade when the loop edge matters: requestAnimationFrame fade in/out, fade out when `duration - currentTime <= 0.55`, reset on `ended`, no CSS transitions.
- Liquid glass utility with nearly transparent background, `backdrop-filter`, inset highlight, and a masked gradient-border `::before`.
- Large typography with negative tracking, tight line-height, and one italic/display accent word.
- Floating pill nav with desktop links and either a precise mobile sheet or explicit no-mobile-menu behavior.
- Bottom-left or bottom-aligned hero content over video for cinematic compositions.
- Dashboard/mockup built in code instead of screenshots when the product is SaaS or fintech.
- Marquees by rendering arrays twice and translating `0 -> -50%` with linear infinite CSS animation.
- Staggered entrances using exact delays: badge 0.1s, title 0.2s, subtitle 0.3s, CTAs 0.4s, mockup 0.5s, adjusted to the composition.
- Strong negative constraints: no purple/indigo, no random blobs, no dark overlay, no extra sections, no placeholder copy, no UI libraries.
- Coded mockup systems with explicit arrays and JSX fragments for cards, chart bars, terminal rows, workflow nodes, avatars, or product panels instead of asking for generic mockups.

## Asset Generation Guidance

When the design needs an image, 3D render, or mockup and the user has no asset, include a separate asset brief in `design.md`:

- Subject and setting: what appears in frame.
- Camera: lens feel, angle, motion, parallax, depth of field.
- Motion: subtle movement, loopability, or static treatment when relevant.
- Composition: safe areas for text, focal point, object position, empty space.
- Color grade: palette, contrast, grain, glow, exposure.
- Technical output: aspect ratio, minimum resolution, transparent/background requirements, and no text baked in unless required.

For AI video tools, default to providing a video-generation prompt for the hero or most visually important section. Do not put the video-generation prompt in `design.md`. Put it in the chat response after creating `design.md`, and instruct the user to generate a clean loop with no captions, no watermark, no fast cuts, no brand text, and enough negative space for UI copy, then host it and replace the video URL placeholder in `design.md`.

## Final Output Rules

- Write the generated implementation prompt to `design.md`; do not paste it into chat.
- In chat, respond with a short note that `design.md` was created and include the AI video-generation prompt plus instructions to host the video and update the URL in `design.md`, unless video was explicitly forbidden or intentionally omitted for a rare stated reason.
- Make the prompt long enough to remove ambiguity. It is acceptable for premium prompts to be 1500-5000 words.
- Do not include a markdown table in the final prompt unless the user explicitly wants one.
- Make copy strings explicit and final. Do not write "add compelling copy".
- Include exact code snippets for all implementation-critical design details: representative JSX/HTML structure, CSS variables/utilities, Tailwind config extensions, keyframes, SVG paths, data arrays, and JS/TS interaction logic. Use snippets to constrain the design system, not just fragile effects.
- For signature effects and hero-defining systems, write near copy-paste implementation instructions instead of summary prose. Include exact files, imports, constants, refs/state, effects, event listeners, cleanup, class names, animation timing, responsive branches, and failure/edge-case guards.
- When making assumptions, place them under "Assumptions baked into this prompt" inside `design.md`.

## Reference

For deeper rationale and reusable templates, read [reference.md](reference.md).

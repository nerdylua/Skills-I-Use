---
name: premium-ui-prompt-crafter
description: Generate long, technically exact prompts for one-shot premium hero sections and landing pages. Use when the user wants beautiful UI prompts, MotionSites-style hero or landing page prompting, UI requirement interviews, visual direction into Vite/Next.js prompts, video/background asset direction, or highly specified React/Tailwind UI generation prompts.
---

# Premium UI Prompt Crafter

Use this skill to turn a user's UI idea into a high-fidelity implementation prompt for Google AI Studio, Cursor, Lovable, Bolt, or another coding agent. The goal is not to implement the UI directly unless the user asks. The goal is to interrogate the brief, resolve ambiguity, then create a long, precise `design.md` prompt that can one-shot a premium hero or landing page.

## Core Principle

These prompts work because they replace vague taste words with concrete production instructions. Do not say only "beautiful, modern, aesthetic." Specify the stack, design system, section order, exact copy, typography, colors, media, layout geometry, animation timings, responsive behavior, interaction states, constraints, and acceptance criteria.

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
- Layout: viewport height, section order, max widths, grid columns, pinned/floating elements, card sizes, border radii, spacing rhythm.
- Navigation: logo, links, CTA, mobile menu behavior.
- Copy: headline, subheadline, badges, stats, buttons, cards, testimonials, nav labels.
- Animation: page-load entrance, text reveal, scroll effects, marquee, hover states, video fade loops, reduced-motion expectations.
- Responsiveness: breakpoints, mobile substitutions, hidden elements, fluid typography.
- Technical constraints: no backend, no routing, no extra libraries, use local assets, no placeholder copy, no random gradients.

If the user is unsure, offer 3 opinionated directions and ask them to choose. Keep interviewing after they choose until the brief is implementation-ready.

## Prompt Anatomy

Generate the final prompt with these sections, adapting as needed:

1. **Opening Command**: one sentence naming the product, scope, stack, and intended aesthetic.
2. **Non-Negotiables**: exact reproduction goals, forbidden additions, output framework, no backend unless asked.
3. **Dependencies & Setup**: packages, font imports, Tailwind theme extensions, global CSS.
4. **Design System**: colors, fonts, radii, shadows, glass/noise/gradient utilities, CSS variables.
5. **Assets & Media**: exact URLs or non-video generation briefs; video URL placeholder or final hosted URL; video attributes; object-fit, focal point, poster, overlay, blend mode, loop/fade behavior. If video is intentionally omitted, state the reason clearly.
6. **Page/Section Structure**: ordered sections and component names.
7. **Detailed Section Specs**: layout, copy, classes, inline styles, grid behavior, measurements, z-index, responsive changes.
8. **Interactions & Animation**: exact delays, durations, easing curves, keyframes, Framer Motion/GSAP logic, hover/tap states.
9. **Responsive Rules**: mobile-first behavior, breakpoints, alternate layouts.
10. **Implementation Notes**: reusable components, state logic, accessibility basics, cleanup for listeners/rAF.
11. **Acceptance Criteria**: concise checklist describing what must be true when complete.

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
- Include exact code snippets only for fragile effects: liquid glass CSS, video fade logic, keyframes, SVG paths, complex animation loops.
- When making assumptions, place them under "Assumptions baked into this prompt" inside `design.md`.

## Reference

For deeper rationale and reusable templates, read [reference.md](reference.md).

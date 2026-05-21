# Premium UI Prompt Reference

## What Made The Source Prompts Effective

The corpus succeeds because it combines art direction with implementation direction. It does not ask the model to invent a taste system. It supplies a complete visual operating system.

Recurring traits:

- Clear scope: hero only, two full-height sections, or named landing page sections.
- Stack pinned early: React, TypeScript, Vite/Next.js, Tailwind, animation library, icon package, forbidden libraries.
- Typography treated as a core asset: font source, weights, global application, display/body/accent roles, tracking and line-height.
- Colors are tokens, not adjectives: exact hex or HSL variables, semantic usage, forbidden colors.
- One signature visual: fullscreen video, Spline scene, shader stack, dashboard mockup, glass orb, animated pipeline, marquee gallery, or large editorial type.
- Media details are exact: URL, object-fit, focal point, scale, overlay/no-overlay, poster, playback attributes, crossfade logic.
- Layout is measurable: viewport height, max-widths, padding, grid columns, absolute positions, z-index, radius, card dimensions.
- Copy is complete: headline, subheadline, nav labels, CTA labels, stats, card text, testimonial text.
- Animation is mechanical: delays, durations, easing, keyframes, scroll ranges, hover/tap states, requestAnimationFrame logic.
- Responsive behavior is explicit: breakpoints, hidden desktop/mobile elements, alternate mobile menus, fluid typography.
- Negative constraints are frequent: no extra sections, no overlay, no purple, no placeholders, no UI library, no random blobs.

## Quality Bar

A generated prompt should allow a capable coding model to build the UI without asking design questions. If a detail affects visual identity, specify it. If a detail does not matter, constrain it with a default instead of leaving it open.

Good:
"Use a fixed fullscreen background video, object-cover, object-position center top, scale 1.08. Do not add a dark overlay; contrast comes from glass panels."

Weak:
"Use a nice cinematic background."

Good:
"Headline uses Instrument Serif italic, text-6xl md:text-8xl, line-height 0.9, tracking -0.05em. The words 'silent systems' use text-white/55."

Weak:
"Use elegant typography."

## Interview Defaults

If the user does not know what they want, use these defaults:

- Framework: Vite + React 18 + TypeScript + Tailwind CSS 3.
- Icons: lucide-react.
- Animation: Framer Motion for entrance/scroll; CSS for simple hover/keyframes; GSAP only for complex parallax/timelines.
- Visual style: cinematic premium, one accent color, restrained palette, no decorative clutter.
- Layout: full-viewport hero with floating pill nav, large headline, focused CTA, one signature visual.
- Fonts: Inter for UI/body, Instrument Serif for editorial accent, or a category-specific display font.
- Responsiveness: mobile-first, nav collapses below md, typography uses clamp or Tailwind responsive sizes.

## Prompt Template

```markdown
Build a [scope] for [product name], a [category] for [audience], using [stack]. The aesthetic is [visual world] with [signature visual]. Reproduce the following specification exactly.

## Non-Negotiables
- [Framework/output target]
- [No backend/routing unless needed]
- [Allowed/forbidden libraries]
- [Forbidden colors/decorations/placeholders]
- [Responsiveness requirement]

## Dependencies & Setup
- [packages]
- [font imports]
- [Tailwind config or CSS variables]
- [global body/root styles]

## Design System
- Background: [token]
- Foreground: [token]
- Accent: [token]
- Font roles: [display/body/accent]
- Radius/shadow/glass/noise utilities: [exact CSS if needed]

## Assets & Media
- Background video/image/Spline/shader: [exact URL or asset brief]
- Attributes: [autoPlay, loop, muted, playsInline]
- Positioning: [object-cover, focal point, scale]
- Overlay: [none or exact gradient/blur/noise]
- Asset generation brief if no URL exists: [subject, camera, loop, safe areas, color grade]

## Layout Structure
Render components in this order:
1. [Navbar]
2. [Hero]
3. [Optional section]

## Navbar
[Exact logo, links, buttons, layout, mobile behavior]

## Hero
[Exact section height, alignment, headline, subheadline, CTA, stats/mockups/cards, classes, spacing, z-index]

## Additional Sections
[Repeat with exact layouts and copy]

## Animations & Interactions
[Entrance timings, hover/tap, marquee, scroll, video fade, cleanup]

## Responsive Behavior
[Mobile/tablet/desktop rules]

## Acceptance Criteria
- [Visual signature is present]
- [No forbidden additions]
- [Responsive behavior works]
- [Animations and media behave as specified]
```

## Video Asset Brief Template

```markdown
Create a seamless looping background video for [brand/product].

Scene: [subject, environment, objects]
Composition: [text-safe empty area, focal point, depth]
Camera: [static/slow push/parallax/orbit], [lens feel], [movement speed]
Motion: [what moves], subtle and loopable, no fast cuts
Color grade: [palette, contrast, grain/glow]
Mood: [cinematic/luxury/calm/technical]
Restrictions: no text, no logos, no watermark, no people unless specified, no sudden flashes
Output: 1920x1080 MP4/WebM, 6-10 second seamless loop, suitable for `object-cover`, muted autoplay background
```

## Common High-Fidelity CSS Snippets

Liquid glass:

```css
.liquid-glass {
  background: rgba(255, 255, 255, 0.01);
  background-blend-mode: luminosity;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border: none;
  box-shadow: inset 0 1px 1px rgba(255, 255, 255, 0.1);
  position: relative;
  overflow: hidden;
}
.liquid-glass::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1.4px;
  background: linear-gradient(180deg,
    rgba(255,255,255,0.45) 0%, rgba(255,255,255,0.15) 20%,
    rgba(255,255,255,0) 40%, rgba(255,255,255,0) 60%,
    rgba(255,255,255,0.15) 80%, rgba(255,255,255,0.45) 100%);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

Manual video crossfade behavior:

- Start video opacity at 0.
- Use `requestAnimationFrame` to fade opacity to 1 on load.
- Watch `timeupdate`; when `duration - currentTime <= 0.55`, fade to 0.
- Disable native `loop`; on `ended`, set opacity 0, wait 100ms, reset `currentTime = 0`, play, fade to 1.
- Cancel any active animation frame before starting a new fade.
- Resume from current opacity instead of snapping.

## Anti-Patterns

Avoid:

- Asking for "beautiful UI" without specifying what makes it beautiful.
- Multiple competing signature visuals.
- Generic placeholder copy.
- Unbounded library choices.
- Saying "responsive" without breakpoint behavior.
- Letting the generator invent colors, fonts, icons, or card content.
- Adding overlays to video when the prompt says raw video should provide depth.
- Using screenshots where the prompt asks for a coded dashboard or mockup.

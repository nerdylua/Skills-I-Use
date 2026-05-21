# Premium UI Prompt Reference

## What Made The Source Prompts Effective

The corpus succeeds because it combines art direction with implementation direction. It does not ask the model to invent a taste system. It supplies a complete visual operating system.

Recurring traits:

- Clear scope: hero only, two full-height sections, or named landing page sections.
- Stack pinned early: React, TypeScript, Vite/Next.js, Tailwind, animation library, icon package, forbidden libraries.
- File and component boundaries are explicit: which files to create, component names, data arrays, global CSS, and asset imports.
- Typography treated as a core asset: font source, weights, global application, display/body/accent roles, tracking and line-height.
- Colors are tokens, not adjectives: exact hex or HSL variables, semantic usage, forbidden colors.
- One signature visual, with video as the preferred default: fullscreen AI-generated video, ambient product footage, Spline scene with motion backdrop, shader stack, dashboard mockup, glass orb, animated pipeline, marquee gallery, or large editorial type.
- Media details are exact: URL, object-fit, focal point, scale, overlay/no-overlay, poster, playback attributes, crossfade logic.
- Layout is measurable: viewport height, max-widths, padding, grid columns, absolute positions, z-index, radius, card dimensions.
- Implementation details are visible: representative JSX/HTML, Tailwind class strings, CSS variables, custom utilities, keyframes, JS/TS hooks, and interaction state logic.
- Copy is complete: headline, subheadline, nav labels, CTA labels, stats, card text, testimonial text.
- Animation is mechanical: delays, durations, easing, keyframes, scroll ranges, hover/tap states, requestAnimationFrame logic.
- Responsive behavior is explicit: breakpoints, hidden desktop/mobile elements, alternate mobile menus, fluid typography.
- Negative constraints are frequent: no extra sections, no overlay, no purple, no placeholders, no UI library, no random blobs.

## Quality Bar

A generated prompt should allow a capable coding model to build the UI without asking design or implementation questions. If a detail affects visual identity, specify it. If a detail affects how the page is built, show it as code, class strings, variables, or data structures. If a detail does not matter, constrain it with a default instead of leaving it open.

Good:
"Use a fixed fullscreen background video, object-cover, object-position center top, scale 1.08. Do not add a dark overlay; contrast comes from glass panels."

Weak:
"Use a nice cinematic background."

Good:
"Headline uses Instrument Serif italic, text-6xl md:text-8xl, line-height 0.9, tracking -0.05em. The words 'silent systems' use text-white/55."

Weak:
"Use elegant typography."

Good:
"Create `const metrics = [{ label: 'Median deployment', value: '8m' }, ...]` and map it into three `.glass-card` stat tiles. Each tile is `min-h-[116px] rounded-[28px] border border-white/10 bg-white/[0.035] p-5 shadow-[0_24px_80px_rgba(0,0,0,0.28)]`."

Weak:
"Add some premium stat cards."

## Interview Defaults

If the user does not know what they want, interview first. Use these defaults only after asking targeted follow-ups or after the user explicitly asks you to proceed:

- Framework: Vite + React 18 + TypeScript + Tailwind CSS 3.
- Icons: lucide-react.
- Animation: Framer Motion for entrance/scroll; CSS for simple hover/keyframes; GSAP only for complex parallax/timelines.
- Visual style: cinematic premium, one accent color, restrained palette, no decorative clutter.
- Layout: full-viewport hero with floating pill nav, large headline, focused CTA, one signature visual.
- Fonts: Inter or Instrument Sans for UI/body, Instrument Serif for editorial accent, or a category-specific display font. Instrument Sans is especially strong for premium hero typography when you want clean, graceful, modern letterforms.
- Responsiveness: mobile-first, nav collapses below md, typography uses clamp or Tailwind responsive sizes.

## Prompt Template

Write the final implementation prompt to `design.md`, not to chat. Assume the hero or most important section should use an AI-generated video asset unless the user forbids video, the platform/performance constraints rule it out, or a static typographic concept is clearly stronger. Put only a hosted video URL placeholder in `design.md`; send the video-generation prompt separately in chat.

```markdown
Build a [scope] for [product name], a [category] for [audience], using [stack]. The aesthetic is [visual world] with [signature visual]. Reproduce the following specification exactly.

## Non-Negotiables
- [Framework/output target]
- [No backend/routing unless needed]
- [Allowed/forbidden libraries]
- [Forbidden colors/decorations/placeholders]
- [Responsiveness requirement]

## Files To Create/Edit
- [src/App.tsx or app/page.tsx: component structure]
- [src/index.css or app/globals.css: font imports, tokens, utilities, keyframes]
- [tailwind.config.* if needed: theme extension]
- [assets or public paths if needed]

## Dependencies & Setup
- [packages]
- [font imports]
- [Tailwind config or CSS variables]
- [global body/root styles]

## Design System Tokens
Define these exactly:
```css
:root {
  --background: [hex/hsl];
  --foreground: [hex/hsl];
  --muted: [hex/hsl];
  --accent: [hex/hsl];
  --radius-card: [value];
}
```
- Typography: [font family, import URL, weights, sizes/clamp, tracking, line-height]
- Components: [button, nav pill, card, badge, input, mockup panel variants]
- Utilities: [glass/noise/gradient/ring CSS classes, pseudo-elements, shadows]

## Asset Manifest & Media Handling
- Background video/image/Spline/shader: [exact hosted URL, non-video asset brief, or video URL placeholder]
- Attributes: [autoPlay, loop, muted, playsInline]
- Positioning: [object-cover, focal point, scale]
- Overlay: [none or exact gradient/blur/noise]
- Manifest:
```ts
const media = {
  heroVideo: "[HOSTED_VIDEO_URL]",
  heroPoster: "[POSTER_URL]",
  logoAlt: "[exact alt text]"
};
```
- Asset generation brief if no non-video URL exists: [subject, composition, safe areas, color grade]

## Data & Copy Constants
Use explicit arrays/objects for every repeated UI element:
```ts
const navItems = [
  { label: "[label]", href: "#[id]" }
];

const stats = [
  { value: "[value]", label: "[label]" }
];
```

## Layout Structure
Render components in this order:
1. [Navbar]
2. [Hero]
3. [Optional section]

## Navbar
[Exact logo, links, buttons, layout, mobile behavior, ARIA labels]

Representative structure:
```tsx
function Navbar() {
  return (
    <header className="[exact classes]">
      <nav className="[exact classes]" aria-label="Primary navigation">
        {/* exact logo/link/button hierarchy */}
      </nav>
    </header>
  );
}
```

## Hero
[Exact section height, alignment, headline, subheadline, CTA, stats/mockups/cards, classes, spacing, z-index]

Representative structure:
```tsx
function Hero() {
  return (
    <section className="[exact classes]">
      {/* video/media layer, overlay layer, content layer, mockup/card layer */}
    </section>
  );
}
```

## Additional Sections
[Repeat with exact layouts, copy, data arrays, class strings, and representative JSX for complex sections]

## CSS & Tailwind Implementation
Include exact CSS/Tailwind details:
```css
.glass-card {
  [properties]
}

@keyframes [name] {
  [steps]
}
```

## Animations & Interactions
[Entrance timings, hover/tap, marquee, scroll, video fade, cleanup]

For nontrivial logic, show JS/TS or animation variants:
```ts
const containerVariants = {
  hidden: { opacity: 0 },
  show: { opacity: 1, transition: { staggerChildren: [value] } }
};
```

## Responsive Behavior
[Mobile/tablet/desktop rules, exact breakpoint class substitutions, hidden/reordered elements]

## Accessibility & Performance
- [ARIA labels, alt text, focus-visible styles, contrast notes]
- [prefers-reduced-motion behavior]
- [image/video loading, poster, compression expectations]

## Acceptance Criteria
- [Visual signature is present]
- [No forbidden additions]
- [Responsive behavior works]
- [Animations and media behave as specified]
```

## Code Detail Checklist

Before writing `design.md`, confirm the prompt includes:

- Concrete file map and component names.
- Representative JSX/HTML for navbar, hero, and complex visual sections.
- Near copy-paste implementation blocks for signature effects, scroll/video behavior, animation systems, navigation interactions, coded mockups, and the main hero composition. Include file names, imports, constants, refs/state, effects, cleanup, class names, timings, responsive branches, and edge-case guards.
- Exact Tailwind class strings for key containers, text, cards, buttons, and media layers.
- CSS variables, custom utilities, pseudo-elements, and keyframes where relevant.
- JS/TS snippets for data arrays and nontrivial interactions.
- Asset manifest with URL placeholders, dimensions, formats, alt text, poster, focal point, and generation status.
- Typography specs for desktop, tablet, and mobile.
- Layout measurements: min-heights, max-widths, padding, gaps, card sizes, z-index, absolute offsets.
- Interaction states: hover, active, focus-visible, mobile menu open/closed, reduced motion.
- Negative constraints that prevent generic filler.

## Video Asset Brief Template

Use this in the chat response only, not inside `design.md`. Prefer including this for most hero or premium-section prompts. Tell the user to generate the video in their AI video tool, host the MP4/WebM, then replace the video URL placeholder in `design.md`.

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
- Writing a moodboard when the user needs an implementation prompt.
- Omitting JSX/HTML/CSS/JS details for visually important areas.
- Multiple competing signature visuals.
- Generic placeholder copy.
- Unbounded library choices.
- Saying "responsive" without breakpoint behavior.
- Letting the generator invent colors, fonts, icons, or card content.
- Adding overlays to video when the prompt says raw video should provide depth.
- Using screenshots where the prompt asks for a coded dashboard or mockup.

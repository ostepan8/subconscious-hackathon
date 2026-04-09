# subconscious-hackathon

Custom Slidev deck for the **Subconscious × ACM Hackathon** — _Agents on the Edge_.

The working deck lives in [`agents-on-the-edge/`](./agents-on-the-edge). See
[`agents-on-the-edge/DESIGN.md`](./agents-on-the-edge/DESIGN.md) for the full
design system (tokens, motion, component inventory, asset provenance, slide
map), and [`agents-on-the-edge/README.md`](./agents-on-the-edge/README.md) for
run instructions.

## Quick start

```bash
cd agents-on-the-edge
pnpm install
pnpm dev       # http://localhost:3030
pnpm build     # static site → dist/
```

## What's inside

- 15 custom slides authored in `slides.md`
- 14 hand-written Vue components (OrbitLogo, ReasoningTree, TokenStream, …)
- 6 custom Slidev layouts (cover, split, section, centered, default, end)
- Brand fonts (Manrope + Geist Mono) and HSL colors sourced directly from
  `subconscious-monorepo/apps/web`
- Real product imagery (logos, landing art, integration marks, backers)
  mirrored from the shipping site

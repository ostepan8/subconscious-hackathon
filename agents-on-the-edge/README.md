# Agents on the Edge

Custom Slidev deck for the **Subconscious × ACM Hackathon** (2026-04-09).

See [`DESIGN.md`](./DESIGN.md) for the full design system, asset provenance,
motion tokens, component inventory, and slide map.

## Quick start

```bash
pnpm install
pnpm dev        # http://localhost:3030
pnpm build      # static site → dist/
pnpm export     # pdf export
```

## Layout

```
agents-on-the-edge/
├── slides.md            # the deck itself (15 slides)
├── DESIGN.md            # design system + rationale
├── layouts/             # custom Slidev layouts
├── components/          # Vue components (OrbitLogo, TaskTree, …)
├── styles/              # tokens, fonts, reset, animations
├── snippets/            # python code samples
└── public/assets/       # brand + product imagery (mirrored from monorepo)
```

## Credits

- Logo, wordmark, product screenshots, and integration icons are pulled
  from `subconscious-monorepo/apps/web/public/` — the shipping
  subconscious.dev website — so the deck is visually 1:1 with the
  product.
- Content copy (slides, QR targets, schedule) matches
  `Agents on the Edge.pdf` verbatim.

# Ink Bloom

A photo card in one HTML file. Photos switch with an ink bloom that spreads from where you tap, the card's edges are feathered into the page, and deleting a photo feeds it through a desk shredder.

No build step and no dependencies: WebGL, Canvas 2D and plain CSS.

## Run it

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Photos load from [Lorem Picsum](https://picsum.photos), so the page needs a connection.

## What's inside

**Ink bloom.** The next photo grows out of the press point inside a fragment shader. Its edge is a circle pushed in and out by drifting fbm noise, a thin band around the edge refracts both photos like a lens, and a hairline white rim rides the edge until the bloom settles. Start a new bloom halfway through and the half-finished frame is captured into a framebuffer and becomes the outgoing photo, so nothing jumps.

**Feathered card.** The card is a rounded-box SDF. Toward its border the photo blurs progressively and pulls in the white outside the box, so dark photos fog at the edge and light ones barely change.

**Shredder delete.** Deleting the photo on screen raises a shredder under the card. The photo feeds down into its slot over three seconds and comes out underneath as 4px strips. Each strip is a Verlet rope: fed straight down out of the mouth, hanging under gravity, swaying with the others, curling a little at the tip. Tap the photo before it's all in and it comes back out. Once it's through, the strips fall loose, the machine slides away and the next photo blooms into the empty frame.

**Controls.** A liquid-glass panel sets the frame size, the photo's zoom and the orientation (portrait or landscape, which turns the whole card). Add your own photos with the panel or by dropping them anywhere on the page; they stay in the tab until you reload.

| Input | Does |
| --- | --- |
| Tap the photo | Next photo, blooming from the tap |
| Swipe left / right | Next / previous, blooming from that side |
| ← / → | Previous / next |
| Thumbnail | Jump to that photo |
| × on a thumbnail, Delete, Backspace | Delete |
| Tap during the shred | Keep the photo |

`prefers-reduced-motion` is respected throughout: no bloom spread, no machine motion, the same undo window.

## Credits

- The ink bloom transition is an independent re-implementation inspired by Lorenzo Cabral's [Ink Bloom](https://x.com/cabralorenzo/status/2114082220566860026) block for bencho.dev. No code from it is used.
- The feathered photo library with the blurring caption was inspired by [this post](https://x.com/premiumtantan/status/2099703062478918099) by @premiumtantan.
- The glass panel's rim shading is adapted from [glass-icon-reveal](https://github.com/zanwei/glass-icon-reveal) by Zanwei Guo, MIT licensed; its notice is in [LICENSE](LICENSE).
- Photos from [Lorem Picsum](https://picsum.photos), sourced from Unsplash.

## License

[MIT](LICENSE)

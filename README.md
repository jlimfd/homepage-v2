# FanDuel Homepage V2 — Interactive Prototype

An interactive, responsive HTML/CSS/JS prototype of the **Homepage V2 (improved conversion)** landing page, built from the Figma design.

- **Figma source:** [Homepage V2 for improved conversion (4 Geo Scenarios) — node 16081-12587](https://www.figma.com/design/trmN4kzd4yO27nitzhAlDm/Homepage-V2-for-improved-conversion--4-Geo-Scenarios-?node-id=16081-12587)
- **Stack:** plain HTML, CSS and vanilla JavaScript. No build step and no dependencies apart from the Inter font from Google Fonts.

## Running it locally

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then visit <http://localhost:8000>.

## Page sections

| # | Section | What it contains |
|---|---------|------------------|
| 1 | **Nav** | Sticky, frosted top bar with product links, Support and Log in. Collapses to a hamburger menu at ≤960px. |
| 2 | **Hero – Sportsbook** | "Where fans become champions" with the new-user offer card and a phone mockup. |
| 3 | **Hero – Casino** | "The thrills of Vegas in your pocket" with the casino offer and a phone mockup. |
| 4 | **Refer a Friend** | "Share the fun. Get rewarded." with Sportsbook, Casino and Predicts promo cards. |
| 5 | **Ways to play** | Geo-specific block (Pennsylvania) with product tabs and an availability map. |
| 6 | **Social proof** | "X million players. X billion won." stats, plus a scrolling App Store review carousel. |
| 7 | **Get to know FanDuel** | FAQ accordion and a "Play with a plan" responsible-gaming card. |
| 8 | **Footer** | App download QR codes, link columns, legal copy and payment / responsible-gaming logos. |

## Interactions & microanimations

Motion is kept subtle. It's used to add depth where it supports conversion, not as decoration.

- **Hero depth:** on desktop, moving the cursor over a hero card tilts the phone mockup in 3D and shifts the sparkles at different speeds (parallax). Behind each phone, a glow slowly pulses and the sparkles twinkle.
- **Offer card emphasis:** the "New user offer" box has a slowly rotating gradient border that draws the eye to the primary CTA.
- **Scroll reveals:** sections fade and slide up as they enter the viewport, staggered one after another, using `IntersectionObserver`.
- **Buttons:** they lift slightly on hover and press down on click. Primary buttons also get a soft coloured glow.
- **Nav:** link underlines slide in on hover. The bar gains a border and more opacity once you scroll.
- **Refer cards:** hovering lifts the card, zooms the image slightly and adds a blue shadow.
- **Ways-to-play tabs:** switching product cross-fades the map, re-tints it, staggers in the product list and updates the CTA label (for example "Join Casino").
- **Location pin:** drops in when the map scrolls into view, then pulses.
- **Reviews carousel:** loops endlessly and pauses on hover. The edges fade out.
- **FAQ accordion:** the answer opens with a smooth height animation and the chevron rotates. Only one answer is open at a time.
- **"Play with a plan" card:** a radial spotlight follows the cursor.
- **QR codes:** tilt and scale slightly on hover.
- **Back to top:** a floating button appears after scrolling past the hero.

Parallax and tilt only run on devices with a precise pointer (a mouse or trackpad). **All motion is turned off** when the user has `prefers-reduced-motion` enabled.

## Responsive behaviour

| Breakpoint | Changes |
|------------|---------|
| > 1100px | Full desktop layout matching the Figma frame (content max-width 1280px). |
| ≤ 1100px | Tighter nav spacing, and the footer links drop to 2 columns. |
| ≤ 960px | Hamburger nav. Hero cards, refer cards, Ways-to-play, FAQ and app downloads stack into a single column. Review cards get narrower. |
| ≤ 560px | Footer links drop to 1 column, and the QR codes get smaller. |

Tested at 375px (mobile) with no horizontal overflow.

## Project structure

```
.
├── index.html        # All markup, styles and scripts
├── assets/
│   ├── phone-sb.png        # Sportsbook phone mockup
│   ├── phone-casino.png    # Casino phone mockup
│   ├── refer-sb.png        # Refer-a-friend: Sportsbook
│   ├── refer-casino.png    # Refer-a-friend: Casino
│   ├── refer-predicts.png  # Refer-a-friend: Predicts
│   ├── map.png             # US availability map
│   ├── qr-sb.png           # Sportsbook app QR
│   ├── qr-casino.png       # Casino app QR
│   └── payments.png        # Payment & RG partner logos
└── README.md
```

Design tokens (colours, easing) are defined as CSS custom properties on `:root` at the top of `index.html`.

## Known limitations

- **Assets are cropped from a Figma render.** The Figma API couldn't return this frame's full node data, so the image assets were cropped from a high-resolution screenshot rather than exported individually. They may look slightly soft on high-DPI screens. Replace them with proper Figma exports when they're available.
- **The map is a single static image.** Switching product tabs only re-tints it. It doesn't reflect real per-product state availability.
- **The logo is a placeholder.** The FanDuel shield is a simplified inline SVG, not the official brand asset.
- **Placeholder copy:** the FAQ answers were written for the prototype and need real content. The "X million / X billion" stats are kept as placeholders from the design.
- **Geo scenarios:** only the Pennsylvania scenario is built. The other geo scenarios from the Figma file aren't implemented yet.
- **All links and CTAs are dummy `#` links.**

## Next steps

- Swap in exported Figma assets and the official logo.
- Build the remaining geo scenarios, switchable with a URL parameter such as `?state=NJ`.
- Replace the map with an interactive SVG that highlights states per product.
- Wire real CTA destinations and add analytics events for conversion tracking.

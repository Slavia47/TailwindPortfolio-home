# Architectural Integrity — Hero & Case Study Page

A hero-led landing page for an architecture studio, combining a large asymmetric headline section, a four-column stats bar, a featured case study, and supporting methodology/lab-archive panels. Uses a custom Tailwind theme with brand colors `tahiti` and `LiGr`.

## Preview

The layout includes:
- **Header** — logo, search icon, nav links (Home, Projects, Contact), and a CV_download button
- **Hero section** — large asymmetric two-column headline ("Architectural integrity & spatial logic.") paired with a description and two CTA buttons ("Explore portfolio" / "Our philosophy")
- **Stats bar** — four-column strip (Projects completed, Global awards, Technical certs, Design labs)
- **Case study spotlight** — large background-image card (The Monolith Pavilion) alongside a methodology panel (BIM Integration & Structural Analytics) with tag links
- **Lab Archive + CTA tiles** — a "Shadow Studies" preview tile and a black "Join the architectural dialogue" tile with a submit inquiry button
- **Footer** — currently empty

## Tech Stack

- **HTML5**
- **Tailwind CSS v4** — compiled via `output.css`, using a custom `@theme` block to define two brand colors:
  ```css
  @theme {
      --color-tahiti: #3ab7bf;
      --color-LiGr:  #C2C2C2;
  }
  ```
  This generates utility classes like `bg-tahiti`, `hover:bg-tahiti`, `bg-LiGr`, `text-LiGr`, etc.
- **Font Awesome** (via Kit CDN) for the header search icon

Note: unlike other pages in this project, this one does **not** load the Tailwind CDN script — it relies entirely on the compiled `output.css`, so a Tailwind build step is required for any class changes to take effect.

## File Structure

```
.
├── index.html          # Page markup
├── input.css             # Tailwind source file (contains @theme block)
├── output.css              # Compiled Tailwind stylesheet
└── Emblem.png                # Case study background + lab archive image
```

## Getting Started

This page requires a Tailwind build step (no CDN fallback is included):

1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd <repo-folder>
   ```
2. Install Tailwind and build `output.css` from your `input.css`:
   ```bash
   npm install tailwindcss @tailwindcss/cli
   npx @tailwindcss/cli -i ./input.css -o ./output.css --watch
   ```
3. Open `index.html` directly in a browser, or serve it locally:
   ```bash
   npx serve .
   ```

## Responsive Behavior

- No explicit `md:`/`lg:` responsive classes are used on this page — the hero grid, stats bar, and case study columns are all fixed-width (`grid-cols-[70%_30%]`, `grid-cols-4`, `w-[50%]`), so this page will likely need additional breakpoint classes to reflow cleanly on tablet/mobile screens

## Notes / TODO

- There's an extra, unmatched closing `</div>` right after the hero section (`grid grid-cols-[70%_30%]...`) — it closes once correctly, then again immediately after with nothing to close. Remove the stray extra `</div>`.
- Color usage is inconsistent: the header nav buttons use the custom `hover:bg-tahiti`, but the hero and case study buttons still use the default Tailwind `hover:bg-blue-700` — worth deciding whether all interactive elements should use the brand `tahiti` color for consistency
- The `CV_download` `<button>` has an `href="#"` attribute — buttons don't support `href` (only `<a>` does); this attribute currently has no effect and can be removed, or the button converted to a styled `<a>`
- `<footer></footer>` is currently empty — add copyright/social links to match the other pages in this project
- Stats bar numbers (`42+`, `12`, `08`, `03`) have no accompanying `text-4xl`-style sizing — check if they're intended to stand out more visually as key metrics
- Consider adding responsive grid classes (e.g. `grid-cols-1 md:grid-cols-[70%_30%]`) so the hero and stats sections stack on smaller screens

## License

This project is provided as-is for personal portfolio or educational use. Add a license of your choice (MIT, etc.) if distributing publicly.

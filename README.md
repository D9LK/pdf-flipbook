## Flipbook.js

Vanilla JS flipbook viewer for PDFs (powered by pdf.js). It supports a single-page cover, two-page spreads, and hover arrows. Drop it in via link/script tags and point it at a PDF URL.

### Features
- Cover mode on page 1 (centered single page)
- Two-page spreads after the cover
- Hover arrows for next/prev (hidden when unavailable)
- Click-to-navigate: click left/right page half for prev/next
- Fullscreen control (button + API)
- Responsive single-page mode on small screens (configurable breakpoint, overrideable)
- Auto-loads pdf.js from CDN if it’s not present
- No frameworks, just HTML/CSS/JS

### Quick start (CDN)
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.css">
<div id="flip" style="height:100dvh"></div>
<script src="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.js"></script>
<script>
  const fb = Flipbook.mount({
    target: '#flip',
    pdfUrl: 'https://example.com/path/to/file.pdf'
  });
</script>
```

### Quick start (local dist)
```html
<link rel="stylesheet" href="./dist/flipbook.css">
<div id="flip" style="height:100dvh"></div>
<script src="./dist/flipbook.js"></script>
<script>
  const fb = Flipbook.mount({ target: '#flip', pdfUrl: 'https://example.com/file.pdf' });
  window.fb = fb; // optional: for console testing
</script>
```

### Using your own pdf.js (optional)
Flipbook.js auto-loads pdf.js 3.10.x from a CDN when `window.pdfjsLib` is not present. If you prefer to pin/control pdf.js yourself:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.css">
<div id="flip" style="height:100dvh"></div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.10.111/pdf.min.js"></script>
<script>
  pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.10.111/pdf.worker.min.js';
</script>
<script src="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.js"></script>
<script>
  Flipbook.mount({ target: '#flip', pdfUrl: 'https://example.com/file.pdf' });
</script>
```

### API
```js
const fb = Flipbook.mount({ target, pdfUrl, single, breakpoint });
// target: HTMLElement or selector string
// pdfUrl: string (must be accessible with CORS if cross-origin)
// single: boolean (optional). If provided, forces initial single/double and enables override.
// breakpoint: number (optional, default 900). Below this width, single-page mode is enabled automatically unless overridden.

fb.next();  // go to next spread/page
fb.prev();  // go to previous spread/page
fb.render(); // re-render at current zoom/size (called automatically on resize)

// Single-page mode controls
fb.singleMode(true);      // force single-page
fb.singleMode(false);     // force double-page
fb.singleMode();          // return to auto (responsive) behavior
fb.setSingle(true);       // alias for singleMode(true)
fb.toggleSingle();        // toggle current single/double

// Fullscreen controls
fb.enterFullscreen();
fb.exitFullscreen();
fb.toggleFullscreen();
```

Notes:
- To load a different PDF, mount a new instance with another container or rebuild the existing container.
- The viewer auto-switches to cover mode on page 1 and to spreads afterwards.
- In single-page mode, the wrapper sizes to a single page and is larger on mobile by default.
- Click on the left/right half of the spread to navigate; nav arrows are hidden when disabled (first/last page).

### Layout & styling
- Set the height of your container (e.g., `style="height:100dvh"`). The book scales to fit.
- CSS classes are namespaced with `flipbook-`.
- The spine divider is hidden in cover mode.

### CDN
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.css">
<script src="https://cdn.jsdelivr.net/gh/D9LK/pdf-flipbook@v1.1.1/dist/flipbook.js"></script>
```

### Requirements & compatibility
- Modern browsers (ES6, CSS Grid)
- If your PDF is served from another origin, ensure it allows CORS

### License
MIT



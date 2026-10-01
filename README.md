# day-9
Responsive Design — Media Queries
**What responsive design means**

A responsive site adjusts its layout depending on the screen size it's viewed on — desktop, tablet, mobile — instead of breaking or looking cramped/stretched on smaller or larger screens.

**The viewport meta tag — required first step**

```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

Without this, mobile browsers render the page at desktop width and zoom out — media queries won't behave correctly. This goes in every project, always.

**Media queries — basic syntax**

```css
@media (max-width: 768px) {
  body {
    background-color: lightyellow;
  }
}
```

This block of CSS only applies when the screen width is 768px or less. Outside a media query, styles apply everywhere; inside one, styles apply only when the condition is true.

**`max-width` vs `min-width`**

```css
@media (max-width: 768px) {
  /* applies to screens 768px and SMALLER */
}

@media (min-width: 768px) {
  /* applies to screens 768px and LARGER */
}
```

- `max-width` — common in a **desktop-first** approach: write default styles for desktop, then override for smaller screens
- `min-width` — common in a **mobile-first** approach: write default styles for mobile, then override for larger screens

**Mobile-first vs desktop-first** 

```css
/* Mobile-first example */
.container {
  display: flex;
  flex-direction: column;   /* mobile default: stacked */
}

@media (min-width: 768px) {
  .container {
    flex-direction: row;    /* tablet/desktop: side by side */
  }
}
```

Mobile-first is generally considered better practice in real projects — you design for the most constrained screen first, then add complexity as space allows.

**Common breakpoints (rough guide, not fixed rules)**

```css
/* Mobile: default styles, no media query needed */

@media (min-width: 640px) {
  /* small tablets */
}

@media (min-width: 768px) {
  /* tablets */
}

@media (min-width: 1024px) {
  /* small laptops */
}

@media (min-width: 1280px) {
  /* desktops */
}
```

These numbers aren't magic — they're common conventions (also close to what Tailwind uses by default, which we'll get to in Week 6). Real breakpoints should be based on where *your* design actually breaks, not blindly copied numbers.

**A practical example — responsive grid**

```css
.gallery {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 768px) {
  .gallery {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .gallery {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

One column on mobile, two on tablets, three on desktop — progressive enhancement as space increases.

**Responsive typography**

```css
h1 {
  font-size: 1.8rem;
}

@media (min-width: 1024px) {
  h1 {
    font-size: 3rem;
  }
}
```

Headings especially need to shrink on small screens — a desktop-sized `h1` often overflows or looks oversized on mobile.

**Responsive images**

```css
img {
  max-width: 100%;
  height: auto;
}
```

This single rule (often placed globally) prevents images from overflowing their container on small screens — it's one of the most commonly forgotten fixes for broken mobile layouts.

**Combining conditions**

```css
@media (min-width: 768px) and (max-width: 1023px) {
  /* applies only to this specific range — e.g. tablet-only styles */
}
```

**Common mistakes**

- Forgetting the viewport meta tag — nothing else works right without it
- Mixing `min-width` and `max-width` inconsistently in the same project, causing overlapping/conflicting rules
- Hardcoding `px` widths on containers instead of using `max-width` + `width: 100%`, which breaks on smaller screens
- Testing only by shrinking the browser window and never checking on an actual device or dev-tools device emulator

**Small practice task**

Take yesterday's Grid page layout and make it responsive:

- Stack sidebar and main content into a single column below 768px
- Make the card gallery go from 1 column (mobile) → 2 columns (tablet) → 3 columns (desktop)
- Shrink the heading font size on mobile
- Add `max-width: 100%` to all images

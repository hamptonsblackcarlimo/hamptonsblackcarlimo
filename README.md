# Hamptons Black Car & Limo — deploying this

## Upload BOTH of these to your repo, side by side

```
your-repo/
├── index.html
└── assets/
    ├── hero.webp
    ├── hero-mobile.webp
    ├── logo.webp
    ├── experience.webp
    ├── fleet-sclass.webp
    ├── fleet-suv.webp
    └── fleet-sprinter.webp
```

If you upload `index.html` on its own, every image will show as broken. The
folder must be named exactly `assets` and sit next to `index.html`.

## Why the images moved out of the HTML

They were previously base64-encoded inside `index.html`, which made the file
6.5 MB. Nothing on the page could render until all 6.5 MB had downloaded,
and none of it could be cached between visits. Your logo alone was a 681 KB
PNG, embedded twice, displayed at 36 pixels.

| | Before | After |
|---|---|---|
| index.html | 6.5 MB | 90 KB |
| Images | inline, uncacheable | 472 KB, cached separately |
| Phone first load | ~6.5 MB | ~250 KB |

Phones get `hero-mobile.webp` (70 KB) instead of `hero.webp` (175 KB), and
everything below the fold is lazy-loaded.

## Deploying

Drag both items into your GitHub repo (or commit and push). Vercel will
redeploy automatically. No build step or configuration needed — it's still
a plain static site.

## Two things worth doing next

1. **The service card photos are hotlinked from Unsplash.** They load from
   `images.unsplash.com` at runtime, so they'll break if Unsplash changes
   those URLs. For a commercial site, download them and put them in
   `assets/` alongside the rest, and check the licence terms.

2. **"View Rides" has no backend.** It validates the form and produces a
   summary with call and email links. To take real bookings you'll need a
   form endpoint — Vercel Functions, Formspree, or your dispatch software's
   booking API.

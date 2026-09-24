# Editorial asset register

All photographs were sourced through the available image search using its Creative-Commons/Public-Domain filtered results, downloaded locally and checked visually. No generated people or copied Spectrum.Life images are used. Verify applicable source terms, attribution requirements and model-release permissions again before a commercial/public launch. Stock license information does not itself imply a subject endorses this ministry.

| Local asset | Role | Source |
| --- | --- | --- |
| `images/stage.jpg` | Hero, event atmosphere, fallbacks | PxHere: https://pxhere.com/en/photo/915242 |
| `images/worship.jpg` | Congregation, editorial worship, cinematic closing section | PxHere: https://pxhere.com/en/photo/1203167 |
| `images/singer.jpg` | Clearly labeled temporary vocalist portrait and music atmosphere | PxHere: https://pxhere.com/en/photo/1418450 |
| `images/gathering.jpg` | Live stage, editorial inset and invitation banner | PxHere: https://pxhere.com/en/photo/1086247 |

## Replacement instructions

1. Replace a local file at the same path to preserve layout, or change the relevant `photo()` filename in `js/app.js`.
2. Keep wide hero photographs at least 1600px wide, with enough negative space on the left for text. Warm light and dark tonal depth work best with the current overlays.
3. Supply an approved, high-resolution Deborah portrait for the arched about crop. The current crop uses `object-position:57% center`; tune this in `css/style.css` for the new portrait.
4. Update alt text and captions everywhere the replaced image appears. Only remove the **not Deborah** label after an authentic, authorized portrait is installed.
5. The current `singer.jpg` appears both in the about portrait and music area. Use separate filenames if different official images should be used in these positions.
6. Keep photography cohesive: restrained saturation, warm highlights, dark stage environments, genuine human moments. Avoid adding embedded type or fabricated release artwork.
7. Public event records support their own `image_url`. An empty/failed image falls back to the stage photograph; do not imply that the fallback was photographed at the actual event.

## Other assets

- Typeface: DM Sans from Google Fonts; Google hosts the font request.
- Favicon: original SVG typographic mark.
- Brand monogram and giving motif: original CSS/SVG, not copied from the reference.
- Platform names are plain-text placeholders, not official linked accounts or release claims.

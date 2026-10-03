# holapao
HolaPao — personal website for Paola Solórzano (cruise ship entertainer and content creator).
Live at https://holapao.com.mx via GitHub Pages, which deploys automatically from the `main` branch.

## Editing guide (for humans and bots)

Almost every content change happens in ONE place: the JSON block inside `index.html`,
in the `<script id="site-config" type="application/json">` tag near the top of the file.
It sits between these two HTML comments:

- `SITE CONFIGURATION — EDIT ONLY THIS SECTION`
- `END OF CONFIGURATION — Do not edit below this line`

The page renders entirely from that JSON. Edit the JSON, commit to `main`, and the site
updates within a minute or two. Do not touch anything below `END OF CONFIGURATION`
(CSS, JS, rendering logic) unless specifically asked.

### Rules
- Keep the JSON valid: balanced braces and brackets, commas between items, double quotes around keys and strings.
- `"show": false` hides an item and the layout adjusts automatically. Prefer hiding over deleting.
- Dates use `YYYY-MM-DD`. Assignments whose `endDate` is in the past hide automatically.

### Config sections
| Section | What it controls |
|---|---|
| `site` | `siteUrl`, `googleFormUrl` (contact form), `kofiUrl`, `amazonWishlistUrl` (empty string hides the button) |
| `social` | TikTok, Instagram, Facebook, LinkedIn profile URLs |
| `stats` | Hero numbers: `tiktokFollowers`, `videosPublished`, `languages` |
| `assignments` | Ship contracts. Fields: `show`, `shipName`, `cruiseLine`, `startDate`, `endDate` |
| `events` | Highlight and event cards. Fields: `show`, `tag`, `title`, `description`, `type` |
| `collaborations` | Brand partnership cards. Same fields as `events` |
| `reviews` | Testimonial cards. Fields: `show`, `quote`, `name`, `title`, `initials` |

### Card types (`events` and `collaborations`)
`type` is one of `image`, `instagram`, or `tiktok`. Each needs one extra field:
- `image` → add `"src": "images/filename.jpg"` (upload the file to `images/` first)
- `instagram` → add `"url": "https://www.instagram.com/p/..."` (post or reel link)
- `tiktok` → add `"videoId": "1234567890"` (the number at the end of the TikTok URL)

### Common changes
- Follower count grew → update `stats.tiktokFollowers` (e.g. `"75K+"`).
- New ship contract → add an object to `assignments`; old ones hide on their own via `endDate`.
- New event or brand deal → append an object to `events` or `collaborations` with the right `type`.
- Hide anything → set its `"show"` to `false`.
- Social handle changed → update `social` AND the matching URLs in the JSON-LD block in `<head>` (see below).

### SEO block in `<head>`
The `<head>` holds meta tags and a JSON-LD `schema.org` block that duplicate some config
facts (name, job title, employer, social URLs, description). When those facts change,
update both the site-config JSON and the `<head>` block so search results stay accurate.

### Images
New images go in `images/` and are referenced as `"images/filename.jpg"`. If the hero
photo ever changes, also update the preload `<link>` and the `og:image` / `twitter:image`
meta tags that point at `images/MainPic.jpg`.

### Do not touch
- `CNAME` (custom domain configuration)
- Anything below `END OF CONFIGURATION` in `index.html`

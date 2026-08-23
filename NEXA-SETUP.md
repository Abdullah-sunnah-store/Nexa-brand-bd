# NexaBrand BD — theme setup

A gift-store design built on Shopify's **Horizon** theme, for wallets, watches, rings,
sunglasses, beauty and gift sets. Everything in this repo is theme code — the parts that
live in your Shopify admin (collections, menus, pages, logo) are listed below.

The theme renders complete on day one: every custom section ships with bundled SVG
artwork, so the homepage looks finished before you upload a single product photo. Upload
real photos later and they take over automatically.

---

## 1. Push the theme

```bash
shopify theme push --unpublished --theme "NexaBrand BD"
```

Then preview it from **Online Store → Themes** before publishing.

---

## 2. Create these collections

The templates reference collections by handle. Create them under
**Products → Collections**; the handle is the last part of the URL.

| Handle | Used by |
|---|---|
| `wallets` | Homepage categories, 404, all-collections |
| `watches` | Homepage categories, 404, all-collections |
| `rings` | Homepage categories, 404, all-collections |
| `sunglasses` | Homepage categories, 404, all-collections |
| `beauty` | Homepage categories, beauty promo, 404 |
| `gift-sets` | Homepage categories, gift-set promo, cart upsell |
| `best-sellers` | Homepage "Best sellers", 404 |
| `new-arrivals` | Homepage "Just landed" |
| `for-him`, `for-her`, `couples`, `anniversary`, `birthday`, `eid` | Gift finder — recipient chips |
| `under-1000`, `under-2500`, `under-5000`, `premium` | Gift finder — budget chips |
| `skincare-sets` | Beauty promo secondary button |

Automated collections work well here — e.g. `under-2500` as *price is less than 2500*,
`best-sellers` sorted by best selling.

**Nothing breaks if a collection is missing.** Category tiles fall back to the bundled
illustration and link to `#`; product lists render empty. Create them as you go.

---

## 3. Create these menus

**Content → Menus.**

- **`main-menu`** — header nav and the footer "Shop" column:
  Shop All, Wallets, Watches, Rings, Sunglasses, Beauty, Gift Sets
- **`footer`** — footer "Help" column:
  About, Contact, FAQ, Shipping & Delivery, Returns, Privacy Policy, Terms

---

## 4. Create these pages

**Content → Pages.** For each, set **Theme template** in the sidebar.

| Page title | Handle | Template |
|---|---|---|
| About | `about` | `page.about` |
| Contact | `contact` | `page.contact` |
| Help & FAQ | `faq` | `page.faq` |

The About and FAQ templates already carry their own headline copy and sections — the page
body content you type in the admin appears in the middle of the page, so it is optional.

Every other page uses the default `page` template (hero + your content + promise bar).

---

## 5. Upload the logo

`assets/nexa-logo.svg` is the wordmark. Shopify's logo picker wants a raster file, so
export it to PNG first (about 520×120, transparent) and upload under
**Theme editor → Theme settings → Logo**. Set logo height to 40px desktop / 30px mobile.

While you are there, upload a favicon (a square crop of the diamond monogram works).

---

## 6. Replace the placeholder contact details

These appear in the footer, contact page and FAQ page. Search-and-replace, or edit in the
theme editor:

- `+880 1700-000000` — phone / WhatsApp
- `hello@nexabrandbd.com` — general email
- `corporate@nexabrandbd.com` — bulk enquiries
- `House 42, Road 11, Banani, Dhaka 1213` — pickup address
- Social URLs in **Footer → Brand group → Social links**

Also confirm the delivery numbers quoted throughout (৳2,000 free-delivery threshold,
৳60 / ৳120 charges, 24–48hr Dhaka, 2–4 day nationwide) match what you actually offer.

---

## What was built

### Brand system — `config/settings_data.json`

| | |
|---|---|
| Headings | Playfair Display (regular) |
| Body / UI | Inter |
| Ink | `#141210` |
| Gold | `#b4884b` |
| Cream | `#f7f2ea` |
| Sand border | `#e7dfd3` |
| Muted text | `#6c6259` |
| Buttons | Full pill (100 radius) |
| Cards | 12px radius, lift on hover |
| Sale badge | Gold, uppercase, top-left |

### Custom sections — `sections/nexa-*.liquid`

All ten are addable and fully editable in the theme editor, with presets.

| Section | What it does |
|---|---|
| `nexa-hero` | Headline, accent line, dual CTA, trust row, art panel with badge |
| `nexa-usp-bar` | Bordered 4-up promise strip |
| `nexa-categories` | 2–4 column category tiles; collection image → bundled art fallback |
| `nexa-split` | Image/content promo with icon bullet list, flippable |
| `nexa-gift-finder` | Recipient and budget chip panels, `Label \| /link` per line |
| `nexa-testimonials` | Review cards with star ratings and initial avatars |
| `nexa-stats` | Number strip |
| `nexa-faq` | Native `<details>` accordion, no JavaScript |
| `nexa-newsletter` | Dark CTA band wired to Shopify's customer form (tags `newsletter`) |
| `nexa-page-hero` | Inner-page banner; pulls title from page/collection/blog/article |

Supporting files: `snippets/nexa-icon.liquid` (19 line icons), `assets/nexa.css`
(loaded once via `snippets/stylesheets.liquid`).

### Artwork — `assets/nexa-*.svg`

Hand-drawn, on one gold/ink/cream palette: six category tiles (wallets, watches, rings,
sunglasses, beauty, gift sets), a hero flat lay, two promo scenes, and the logo.
Vector, so they stay sharp at any size and add almost nothing to page weight.

### Templates

| Template | Layout |
|---|---|
| `index` | Hero → promise bar → categories → best sellers → gift-set promo → new arrivals → gift finder → beauty promo → reviews → stats → FAQ → newsletter |
| `product` | Gallery + title/stars/price → variants → quantity + add to cart → inventory → trust strip → 4-row accordion (description, delivery, returns, authenticity) → SKU → info columns → recommendations → product FAQ |
| `collection` | Page hero with breadcrumbs → filtered grid (portrait cards, 24/page) → promise bar → newsletter |
| `list-collections` | Hero → category tiles → all collections grid → newsletter |
| `page` | Hero → content → promise bar |
| `page.about` | Hero → stats → story split → values → NexaBeauty split → content → reviews → newsletter |
| `page.contact` | Hero → contact cards → form → content → FAQ |
| `page.faq` | Hero → four grouped FAQ blocks → content → contact cards |
| `cart` | Cart → gift-set upsell → promise bar |
| `search` | Search header → portrait result grid → promise bar |
| `blog` / `article` | Serif headings → posts → promise bar → newsletter |
| `404` | Custom copy → category tiles → best sellers |
| `password` | Brand launch copy → email capture |

Header: rotating announcement bar (3 messages) on ink, logo left, centred menu,
scroll-up sticky, gold cart bubble.
Footer: ink, four columns (brand + socials + payment icons, Shop, Help, contact +
signup), policy row beneath.

---

## Verification

`shopify theme check` — **371 files, 0 offenses** (errors and warnings).
All JSON templates parse, and every section type, block type and setting id used in them
was cross-checked against the schemas in `sections/` and `blocks/`.
